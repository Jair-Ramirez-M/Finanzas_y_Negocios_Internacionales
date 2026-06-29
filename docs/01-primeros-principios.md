# 01 · Primeros principios: probabilidad, precio y ventaja (edge)

> Antes de tocar una sola línea de código, necesitas la **estructura mental**. Si entiendes bien estas ideas, ya estás por delante del 90% de la gente que opera mercados de predicción. Tiempo de lectura: ~40 min. Releélo cuando quieras.

---

## 1. ¿Qué es una probabilidad? (la definición desde la base)

Una **probabilidad** es un número entre 0 y 1 que mide **cuánto crees que ocurrirá algo**, dada la información que tienes.

- 0 = imposible. 1 = seguro. 0.5 = total incertidumbre (moneda al aire).
- No es una propiedad mágica del universo: es una **medida de tu ignorancia**. Si supieras todo, no habría probabilidades, solo certezas.

**Frecuentista vs. Bayesiano (las dos formas de pensar la probabilidad):**

- **Frecuentista:** "probabilidad = frecuencia a largo plazo". Si una moneda sale cara 500 de 1000 veces, su probabilidad es ~0.5. Útil cuando puedes repetir el experimento muchas veces (deportes: miles de partidos).
- **Bayesiano:** "probabilidad = grado de creencia que actualizas con evidencia". Útil para eventos únicos (¿habrá un acuerdo de paz este año?), donde no hay "1000 repeticiones". La geopolítica vive aquí.

👉 Necesitarás **ambas**. Deportes ≈ frecuentista. Geopolítica ≈ bayesiana.

---

## 2. El teorema de Bayes: cómo actualizar creencias (el corazón de todo)

Es la regla matemática para **cambiar de opinión correctamente** cuando llega información nueva.

```
P(hipótesis | evidencia) = P(evidencia | hipótesis) × P(hipótesis)
                           ───────────────────────────────────────
                                        P(evidencia)
```

En lenguaje humano:

> Creencia nueva = Creencia previa × (qué tan bien la evidencia encaja con tu hipótesis)

**Ejemplo intuitivo:** crees que un equipo tiene 50% de ganar (creencia previa). Te enteras de que su mejor jugador está lesionado (evidencia). Bajas tu estimación a, digamos, 40%. Acabas de hacer Bayes "a ojo". Un modelo lo hace con números.

La idea clave del trader: **empieza con una base (prior) razonable y ajústala con cada dato nuevo, sin sobre-reaccionar.**

📺 Aprende esto visualmente con [3Blue1Brown – Bayes theorem](https://www.youtube.com/watch?v=HZGCoVF3YvM) y [StatQuest](https://www.youtube.com/@statquest).

---

## 3. Cuotas, precios y probabilidad implícita (son lo mismo)

Aquí está la conexión central que mucha gente nunca entiende:

> **El precio de un contrato en un mercado de predicción ES una probabilidad.**

En Polymarket, un mercado "¿Ganará X?" tiene acciones que pagan **$1 si ocurre** y **$0 si no**. Si esa acción cuesta **$0.62**, el mercado está diciendo:

> "Creemos que hay **62%** de probabilidad de que ocurra."

Conversión rápida entre formatos:

| Formato | Ejemplo | Probabilidad implícita |
|--------|---------|------------------------|
| Precio Polymarket | $0.62 | 62% |
| Cuota decimal (casas de apuestas) | 1.61 | 1 / 1.61 = 62% |
| Cuota americana | +61 | 100 / (161) ≈ 62% |

**Fórmula que debes memorizar:**
```
Probabilidad implícita = 1 / cuota_decimal
Precio (mercado de predicción) ≈ probabilidad
```

---

## 4. Valor esperado (EV): la única razón para hacer una operación

El **valor esperado** es el promedio de lo que ganarías si pudieras repetir la apuesta infinitas veces.

```
EV = (prob_de_ganar × ganancia_si_ganas) − (prob_de_perder × pérdida_si_pierdes)
```

**Ejemplo:** compras una acción "Sí" a **$0.50** (mercado dice 50%). Pero **tu modelo** dice que la probabilidad real es **60%**. Cada acción paga $1 si aciertas.

```
EV = (0.60 × $0.50 de ganancia) − (0.40 × $0.50 de pérdida)
   = $0.30 − $0.20
   = +$0.10 por cada $0.50 arriesgado  →  +20% de EV
```

Regla de oro:
> **Solo operas cuando TU probabilidad difiere del precio del mercado a tu favor. Eso, y solo eso, es "edge" (ventaja).**

Si tu modelo coincide con el mercado, **no hay nada que hacer**. La oportunidad nace de la **diferencia**.

---

## 5. ¿De dónde sale el edge? (y por qué es difícil)

El precio del mercado es la opinión combinada de mucha gente, parte de ella muy informada. Para ganarle necesitas una de estas ventajas:

1. **Mejor información** (datos que otros no procesan bien: estadísticas avanzadas, line-ups, clima).
2. **Mejor modelo** (procesas la misma información con menos error/sesgo).
3. **Mejor disciplina** (no reaccionas con emoción; explotas el pánico o euforia de otros).
4. **Velocidad** (reaccionas a una noticia antes de que el precio se ajuste).
5. **Nichos ignorados** (mercados pequeños, ligas menores, eventos raros con poca atención).

⚠️ Para un principiante, lo más realista es **(3) disciplina + (5) nichos**. Los grandes mercados líquidos (elección presidencial de EE.UU., Champions League) son los más eficientes y difíciles de batir.

---

## 6. Edge vs. varianza: por qué puedes tener razón y aun así perder (a corto plazo)

- **Edge** = tu ventaja matemática a largo plazo.
- **Varianza** = la suerte/aleatoriedad a corto plazo.

Aunque tengas 55% de probabilidad real, perderás el 45% de las veces. Con pocas operaciones, la **suerte domina**. Solo con **muchas** operaciones tu **edge** se impone (esto es la **Ley de los Grandes Números**).

Consecuencias prácticas:
- Necesitas **muchas operaciones pequeñas**, no pocas grandes.
- Necesitas **bankroll management** para no quebrar durante una mala racha (ver Kelly en [`docs/05`](docs/05-polymarket-practica.md)).
- **Mide tu desempeño con cientos de operaciones**, no con 5.

---

## 7. Calibración: la cualidad #1 de un buen pronosticador

Un pronosticador está **bien calibrado** si, de todas las veces que dice "70%", el evento ocurre ~70% de las veces.

> No te pagan por "tener razón". Te pagan por **poner el número correcto**.

Esto se **mide objetivamente** con dos métricas que usarás todo el tiempo:

- **Brier score** (error cuadrático): `(probabilidad − resultado)²`. Más bajo = mejor. Resultado es 1 (ocurrió) o 0 (no).
- **Log loss / puntaje logarítmico**: castiga fuerte la confianza equivocada. Más bajo = mejor.

Detalle y código en [`docs/04`](docs/04-modelado-tablas-prediccion.md). Por ahora quédate con: **tu meta no es adivinar, es estar calibrado.**

---

## 8. La diferencia entre deportes, futuros y geopolítica

| Dimensión | Deportes | Futuros (precios/macro) | Geopolítica |
|-----------|----------|-------------------------|-------------|
| Tipo de probabilidad | Frecuentista (muchos datos) | Mixto | Bayesiana (eventos únicos) |
| Fuente de edge | Modelos estadísticos sobre datos históricos | Análisis de series temporales, macro | Base rates + razonamiento estructurado (superforecasting) |
| Herramienta estrella | Regresión de Poisson, Elo, ML | Series temporales, factores | Tetlock / Brier, descomposición del problema |
| Dificultad de datos | Datos abundantes y limpios | Medio | Datos escasos, mucho criterio |

La buena noticia: las **habilidades base son las mismas** (probabilidad, EV, calibración, código). Cambia la "caja del modelo".

---

## Resumen para recordar

1. Probabilidad = grado de creencia (0 a 1).
2. Bayes = cómo actualizar esa creencia con evidencia.
3. Precio del mercado = probabilidad implícita.
4. Operas **solo** si tu probabilidad ≠ precio a tu favor → eso es **edge**.
5. Edge se gana a largo plazo; la varianza manda a corto plazo.
6. Tu objetivo es **calibración**, no "tener razón".
7. Mismos cimientos para deportes, futuros y geopolítica.

➡️ Siguiente: el plan de estudio mes a mes → [`docs/02-ruta-aprendizaje.md`](02-ruta-aprendizaje.md)
