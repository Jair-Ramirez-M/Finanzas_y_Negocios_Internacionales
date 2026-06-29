# 04 · Cómo se construye un modelo y una tabla de predicciones (ejemplo completo)

> Aquí pasamos de la teoría al **código real**. Construiremos, paso a paso, un modelo de fútbol que produce una **tabla de predicciones** (probabilidades de cada resultado), lo **evaluaremos** honestamente y lo conectaremos con el **edge** y el **tamaño de apuesta**.
>
> Usaremos fútbol porque hay datos gratis y abundantes, pero la **estructura es idéntica** para cualquier mercado. Puedes correr todo esto en [Google Colab](https://colab.research.google.com/) sin instalar nada.

---

## Paso 0 — Qué es una "tabla de predicciones"

Es simplemente una tabla donde cada fila es un evento y las columnas son **tus probabilidades**:

| Partido | P(Local) | P(Empate) | P(Visita) | Precio mercado Local | Edge |
|---------|---------|-----------|-----------|----------------------|------|
| A vs B | 0.55 | 0.25 | 0.20 | 0.48 (48%) | +7% ✅ |
| C vs D | 0.30 | 0.30 | 0.40 | 0.42 | −12% ❌ |

El trabajo del modelo es **llenar las columnas P(...) bien calibradas**. El resto (edge, decisión) es aritmética.

---

## Paso 1 — La intuición del modelo de Poisson (desde primeros principios)

El número de goles que mete un equipo en un partido se parece mucho a una **distribución de Poisson**: una distribución para "cuántas veces ocurre algo raro en un intervalo" (goles en 90 minutos).

La Poisson tiene **un solo parámetro λ (lambda)** = goles esperados. Si conoces λ, sabes la probabilidad de 0, 1, 2, 3... goles:

```
P(k goles) = (λ^k × e^(−λ)) / k!
```

La idea del modelo:
1. Estimar la **fuerza de ataque** y **fuerza de defensa** de cada equipo a partir del historial.
2. Combinarlas (más la ventaja de local) para obtener λ_local y λ_visita de un partido.
3. Con esas dos λ, calcular la probabilidad de **cada marcador** (0-0, 1-0, 2-1...).
4. Sumar los marcadores para obtener **P(Local), P(Empate), P(Visita)**.

---

## Paso 2 — Cargar datos y ajustar el modelo (código completo)

```python
import pandas as pd
import numpy as np
import statsmodels.formula.api as smf

# 1) Datos reales y gratuitos (Premier League). Puedes apilar varias temporadas.
url = "https://www.football-data.co.uk/mmz4281/2324/E0.csv"
df = pd.read_csv(url)[["HomeTeam", "AwayTeam", "FTHG", "FTAG"]].dropna()

# 2) Reorganizamos: una fila por equipo-partido, marcando si jugó de local.
#    Esto permite estimar ataque/defensa con UNA sola regresión de Poisson.
local = df.rename(columns={
    "HomeTeam": "team", "AwayTeam": "opponent", "FTHG": "goals"
}).assign(home=1)[["team", "opponent", "goals", "home"]]

visita = df.rename(columns={
    "AwayTeam": "team", "HomeTeam": "opponent", "FTAG": "goals"
}).assign(home=0)[["team", "opponent", "goals", "home"]]

datos = pd.concat([local, visita])

# 3) Modelo de Poisson: los goles dependen del equipo (ataque),
#    del rival (su defensa) y de si juega en casa (ventaja de local).
modelo = smf.glm(
    formula="goals ~ home + C(team) + C(opponent)",
    data=datos,
    family=__import__("statsmodels").api.families.Poisson()
).fit()

print(modelo.summary().tables[0])  # resumen del ajuste
```

> Qué acaba de pasar: `statsmodels` aprendió un coeficiente de **ataque** por equipo, uno de **defensa** por equipo, y uno de **ventaja de local**. Con eso puede predecir los goles esperados de cualquier enfrentamiento.

---

## Paso 3 — Predecir un partido y construir la tabla de marcadores

```python
from scipy.stats import poisson

def predecir(local_team, away_team, modelo, max_goles=8):
    # Goles esperados (λ) para cada lado
    lam_local = modelo.predict(pd.DataFrame(
        {"team": [local_team], "opponent": [away_team], "home": [1]}))[0]
    lam_visita = modelo.predict(pd.DataFrame(
        {"team": [away_team], "opponent": [local_team], "home": [0]}))[0]

    # Probabilidad de cada cantidad de goles (0..max) para cada equipo
    p_local = [poisson.pmf(i, lam_local) for i in range(max_goles + 1)]
    p_visita = [poisson.pmf(i, lam_visita) for i in range(max_goles + 1)]

    # Matriz de probabilidad conjunta de cada marcador (asume independencia)
    matriz = np.outer(p_local, p_visita)

    # Sumamos las regiones de la matriz:
    p_gana_local = np.tril(matriz, -1).sum()   # local mete más
    p_empate     = np.trace(matriz)            # diagonal: mismo marcador
    p_gana_visita = np.triu(matriz, 1).sum()   # visita mete más

    return {
        "lambda_local": round(lam_local, 2),
        "lambda_visita": round(lam_visita, 2),
        "P(Local)": round(p_gana_local, 3),
        "P(Empate)": round(p_empate, 3),
        "P(Visita)": round(p_gana_visita, 3),
    }

print(predecir("Man City", "Burnley", modelo))
# Ejemplo de salida: {'P(Local)': 0.78, 'P(Empate)': 0.15, 'P(Visita)': 0.07, ...}
```

¡Felicidades! Eso es una **predicción probabilística** generada por un modelo. Repítela en bucle para todos los partidos de una jornada y tendrás tu **tabla de predicciones**.

---

## Paso 4 — Lo MÁS importante: evaluar sin engañarte

Un modelo solo vale si **predice bien datos que no vio**. Nunca evalúes con los mismos datos con los que entrenaste (eso es trampa y se llama *overfitting*).

### Métricas de calibración (las que de verdad importan)

```python
from sklearn.metrics import brier_score_loss, log_loss

# Supón que tienes, para muchos partidos pasados de PRUEBA:
#   y_real  = 1 si el local ganó, 0 si no
#   p_modelo = tu probabilidad de que el local ganara
# (las construyes prediciendo partidos que el modelo NO usó para entrenar)

# brier = brier_score_loss(y_real, p_modelo)   # más bajo = mejor (0 = perfecto)
# ll    = log_loss(y_real, p_modelo)           # más bajo = mejor
```

**Comparaciones de referencia (benchmarks):** tu modelo debe ganarle a:
1. **Predecir siempre la frecuencia base** (ej. local gana 45% siempre).
2. **El precio del mercado** (¡este es el rival difícil!). Si no le ganas al mercado en log loss sobre cientos de partidos, **no tienes edge**.

### Diagrama de calibración

Agrupa tus predicciones por nivel de confianza (todas las de "60-70%") y mira si ganaron ~65% de las veces. `sklearn.calibration.calibration_curve` lo hace. Si tu modelo dice 70% pero solo ocurre 55%, está **sobreconfiado** y debes calibrarlo (`CalibratedClassifierCV`).

---

## Paso 5 — De probabilidad a decisión: edge y valor esperado

```python
def edge(prob_modelo, precio_mercado):
    """Edge = tu probabilidad menos la del mercado.
    Positivo = el mercado infravalora el evento → posible compra."""
    return prob_modelo - precio_mercado

# Ejemplo: tu modelo da 0.55 de que gane el local; el mercado lo pone a 0.48
print(edge(0.55, 0.48))  # +0.07  → 7% de ventaja teórica
```

⚠️ **Margen de seguridad:** no operes con cualquier edge. Las comisiones, el spread (diferencia compra/venta) y el error de tu modelo se comen las ventajas pequeñas. Muchos traders exigen un **edge mínimo (ej. > 3–5%)** antes de actuar.

---

## Paso 6 — Cuánto apostar: el criterio de Kelly

El **criterio de Kelly** te dice qué **fracción de tu capital** apostar para maximizar el crecimiento a largo plazo sin arruinarte.

```python
def kelly(prob, precio):
    """Fracción del bankroll a apostar en un mercado tipo Polymarket
    donde pagas 'precio' y recibes $1 si aciertas.
    b = ganancia neta por unidad apostada = (1 - precio) / precio."""
    b = (1 - precio) / precio
    q = 1 - prob
    f = (b * prob - q) / b
    return max(f, 0)  # nunca negativo (si es <=0, no apuestes)

f = kelly(prob=0.55, precio=0.48)
print(f"Kelly completo: {f:.1%} del capital")
# Usa SIEMPRE Kelly fraccionado (1/4 o 1/2) para reducir varianza:
print(f"Kelly 1/4 (recomendado): {f*0.25:.1%} del capital")
```

**Regla práctica:** usa **¼ de Kelly**. Kelly completo es matemáticamente óptimo pero brutalmente volátil; si tu probabilidad está un poco mal (siempre lo está), te puede arruinar. Mejor crecer lento y sobrevivir.

---

## Paso 7 — Backtesting honesto (probar contra el pasado)

Antes de arriesgar un peso, simula tu estrategia sobre datos históricos **con cuotas reales** (football-data.co.uk las incluye):

1. Recorre partidos pasados **en orden cronológico**.
2. Para cada uno, entrena el modelo **solo con datos anteriores** a ese partido (¡nunca con el futuro!).
3. Calcula tu probabilidad, compárala con la cuota, decide si hay edge, aplica Kelly.
4. Acumula el resultado real.
5. Mide: **ROI**, número de apuestas, y **Closing Line Value (CLV)**.

**Trampas mortales del backtest (lee esto dos veces):**
- **Look-ahead bias:** usar información del futuro. El error #1.
- **Overfitting:** ajustar tanto el modelo al pasado que falla en el futuro. Si probaste 50 variantes y elegiste la mejor, esa "mejor" probablemente fue suerte.
- **Ignorar comisiones/spread/liquidez:** en papel todo gana; en la realidad pagas costos.
- **Pocas operaciones:** 20 apuestas no prueban nada. Necesitas cientos.

> **CLV (Closing Line Value)** es la mejor señal temprana de que tienes edge real: ¿conseguiste mejor precio del que tenía el mercado **al cierre**? Si tu precio promedio le gana al de cierre consistentemente, vas por buen camino, aunque la varianza aún no te haya pagado.

---

## Resumen del flujo completo

```
Datos → Modelo (Poisson/ML) → P(resultado) → Calibrar y EVALUAR (Brier/log loss)
   → Comparar con el mercado → Edge → ¿Edge > umbral? → Kelly fraccionado
   → Registrar y medir (ROI, CLV) → Mejorar y repetir
```

Domina este ciclo en **papel** y con **deportes** (datos abundantes) antes de tocar geopolítica o dinero real.

➡️ Siguiente: aplicar todo esto en Polymarket → [`docs/05-polymarket-practica.md`](05-polymarket-practica.md)
