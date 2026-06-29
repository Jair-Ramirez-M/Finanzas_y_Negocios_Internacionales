# 03 · Herramientas y stack (las "aplicaciones para hacer modelos")

> Dijiste que **desconoces las aplicaciones para hacer modelos**. Aquí están, explicadas desde cero, con cómo instalarlas y para qué sirve cada una. Todo es **gratis y de código abierto**.

---

## La idea: un modelo no es una "app", es código que escribes

No existe un botón mágico de "hacer modelo". Un modelo es un **programa** (normalmente en **Python**) que:

1. **Lee datos** (una tabla),
2. **Aprende patrones** de esos datos con una librería de estadística/ML,
3. **Produce probabilidades** para casos nuevos.

Tú escribes ese programa en un **cuaderno (notebook)**. Veamos las piezas.

---

## El stack mínimo (en orden de importancia)

| Herramienta | Qué es | Para qué la usas |
|-------------|--------|------------------|
| **Python** | Lenguaje de programación | El idioma de la ciencia de datos. Casi todo se hace aquí. |
| **Jupyter Notebook** | Cuaderno interactivo: escribes código y ves resultados/gráficos al instante | Donde construyes y exploras modelos, celda por celda. |
| **pandas** | Librería de tablas de datos | Cargar, limpiar y manipular tus datos (la "hoja de cálculo con esteroides"). |
| **NumPy** | Cálculo numérico rápido | La base matemática debajo de todo. |
| **Matplotlib / seaborn** | Gráficos | Visualizar datos y resultados. |
| **scikit-learn** | Machine learning clásico | Entrenar modelos: regresión, clasificación, calibración, métricas. **Tu caballo de batalla.** |
| **statsmodels** | Estadística clásica | Regresiones interpretables (ej. **Poisson** para goles), con p-valores y detalle estadístico. |
| **SciPy** | Matemáticas/estadística | Distribuciones (Poisson, normal), optimización (Kelly). |

Más adelante (opcional): **XGBoost / LightGBM** (modelos potentes para tablas), **PyTorch / fast.ai** (deep learning).

---

## Dos caminos para empezar HOY (elige uno)

### Opción A — Google Colab (recomendada para empezar, **0 instalación, 0 costo**)

[Google Colab](https://colab.research.google.com/) es Jupyter en la nube, gratis, con todo preinstalado y hasta **GPU gratuita**. Solo necesitas una cuenta de Google y un navegador.

1. Entra a [colab.research.google.com](https://colab.research.google.com/).
2. "Nuevo cuaderno".
3. Escribe en una celda y presiona ▶️:

```python
import pandas as pd
import numpy as np
print("¡Listo! pandas", pd.__version__)
```

Ventajas: nada que instalar, funciona en cualquier computadora, gratis. **Empieza aquí.**

### Opción B — Instalación local (cuando quieras tu propio entorno)

Instala **Miniconda** (gestor de Python y paquetes) desde [docs.conda.io](https://docs.conda.io/en/latest/miniconda.html). Luego, en la terminal:

```bash
# Crea un entorno aislado para este proyecto
conda create -n polymarket python=3.11 -y
conda activate polymarket

# Instala el stack de ciencia de datos
pip install pandas numpy scipy scikit-learn statsmodels matplotlib seaborn jupyter

# Lanza tu cuaderno
jupyter notebook
```

Editor recomendado (gratis): [VS Code](https://code.visualstudio.com/) con la extensión de Python y Jupyter.

---

## Tu primer programa de datos reales (cópialo y córrelo)

Este código descarga partidos reales de la Premier League (gratis, de football-data.co.uk) y calcula la ventaja de jugar en casa:

```python
import pandas as pd

# Datos reales y gratuitos: temporada de la Premier League
url = "https://www.football-data.co.uk/mmz4281/2324/E0.csv"
df = pd.read_csv(url)

# FTR = Full Time Result: H (gana local), D (empate), A (gana visitante)
conteo = df["FTR"].value_counts(normalize=True).round(3)
print("Frecuencia de resultados:")
print(conteo)
# Verás algo como: la ventaja de local es real (H suele ser ~45%)

# Promedio de goles del equipo local y visitante
print("\nGoles promedio local (FTHG):", round(df["FTHG"].mean(), 2))
print("Goles promedio visita (FTAG):", round(df["FTAG"].mean(), 2))
```

Si esto corre y ves números, **ya eres capaz de empezar a modelar**. El siguiente documento convierte estos datos en un modelo de predicción real.

---

## Control de versiones: Git y este repositorio

Guarda tu trabajo en **Git/GitHub** (ya estás en un repo). Beneficios:
- Historial de todo lo que haces (tu portafolio).
- Respaldo en la nube.
- Demuestra tus habilidades a empleadores.

Comandos mínimos:
```bash
git add .
git commit -m "Mi primer notebook de análisis de fútbol"
git push
```

📺 Si Git te confunde: [Git & GitHub para principiantes (freeCodeCamp, gratis)](https://www.youtube.com/results?search_query=git+github+freecodecamp).

---

## Fuentes de datos gratuitas que usarás

| Fuente | Qué tiene | Costo |
|--------|-----------|-------|
| [football-data.co.uk](https://www.football-data.co.uk/data.php) | Resultados y **cuotas históricas** de fútbol europeo | Gratis |
| [Kaggle Datasets](https://www.kaggle.com/datasets) | Miles de datasets de deportes, finanzas, etc. | Gratis |
| [API de Polymarket (Gamma + CLOB)](https://docs.polymarket.com/) | Mercados, precios y order books en vivo | Gratis (leer datos) |
| [Good Judgment Open](https://www.gjopen.com/) / [Metaculus](https://www.metaculus.com/) | Preguntas de geopolítica con resultados | Gratis |
| [FRED (Reserva Federal)](https://fred.stlouisfed.org/) | Datos macro/económicos para "futuros" | Gratis |

➡️ Siguiente: construir un modelo y una tabla de predicciones de verdad → [`docs/04-modelado-tablas-prediccion.md`](04-modelado-tablas-prediccion.md)
