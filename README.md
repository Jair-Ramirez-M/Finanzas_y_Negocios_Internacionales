# De cero a Data Scientist para Mercados de Predicción (Polymarket)

> Una ruta de aprendizaje **en español**, **desde primeros principios**, con **fuentes reales y confiables**, pensada para **máxima calidad al mínimo costo** (casi todo gratis).
>
> Objetivo final: tener el criterio y las herramientas para **modelar probabilidades** y **operar (trade) deportes, futuros y geopolítica en Polymarket** de forma disciplinada.

---

## ⚠️ Lee esto primero (honestidad ante todo)

1. **Esto es inversión/especulación con riesgo real de pérdida.** Ningún modelo garantiza ganancias. Empieza con dinero que puedas perder por completo, e idealmente practica primero **en papel** (sin dinero real) durante meses.
2. **Los mercados son razonablemente eficientes.** El precio de un mercado ya contiene mucha información. Ganar dinero significa encontrar y explotar pequeñas **ventajas (edge)** de forma consistente, no "adivinar el futuro".
3. **Ser data scientist es la habilidad de fondo; Polymarket es solo una aplicación.** Las mismas habilidades te sirven para empleo, finanzas, deportes, negocios internacionales, etc. Esto te protege: aprendes algo valioso aunque nunca operes.
4. **Legalidad:** desde diciembre de 2025 existe **Polymarket US** (regulado por la CFTC). La versión internacional bloquea IPs de EE. UU. Verifica siempre qué es legal en **tu país** antes de operar. Ver [`docs/05-polymarket-practica.md`](docs/05-polymarket-practica.md).

---

## ¿Cómo usar este repositorio?

Este repo **es tu curso**. Léelo en orden. Cada documento es una clase autocontenida con teoría desde primeros principios, ejemplos y enlaces a fuentes gratuitas y confiables.

| # | Documento | Qué aprenderás |
|---|-----------|----------------|
| 1 | [`docs/01-primeros-principios.md`](docs/01-primeros-principios.md) | Qué es realmente una probabilidad, una cuota, el valor esperado, el "edge", por qué un precio ES una probabilidad. La base mental de todo. |
| 2 | [`docs/02-ruta-aprendizaje.md`](docs/02-ruta-aprendizaje.md) | Plan de estudio mes a mes (6 meses) con recursos gratuitos: Python, estadística, machine learning. |
| 3 | [`docs/03-herramientas-stack.md`](docs/03-herramientas-stack.md) | Las herramientas con las que se hacen modelos: Python, pandas, scikit-learn, Jupyter/Colab. Instalación y primeros pasos. |
| 4 | [`docs/04-modelado-tablas-prediccion.md`](docs/04-modelado-tablas-prediccion.md) | Cómo se construye un modelo y una **tabla de predicciones** de verdad. Ejemplo completo con código (fútbol/Poisson), calibración y backtesting. |
| 5 | [`docs/05-polymarket-practica.md`](docs/05-polymarket-practica.md) | Cómo funciona Polymarket, su API, cómo leer un order book, deportes vs. geopolítica (superforecasting), gestión de riesgo (Kelly). |
| 6 | [`docs/06-recursos-presupuesto.md`](docs/06-recursos-presupuesto.md) | Lista curada de fuentes confiables + presupuesto realista (cómo gastar casi $0). |

---

## La idea en una sola imagen

```
        TUS DATOS              TU MODELO            TU PROBABILIDAD        EL MERCADO
   (resultados pasados,   (estadística / ML que   (ej: "el equipo A     (precio de Polymarket
    estadísticas, base  → aprende patrones de   → gana con 62% de   →  = probabilidad que
    rates, noticias)        esos datos)             probabilidad")        cree la multitud)
                                                          │                     │
                                                          └─────────┬───────────┘
                                                                    ▼
                                                    ¿Tu probabilidad difiere
                                                    del precio lo suficiente?
                                                          │
                                          SÍ (hay edge) ──┴── NO (no operes)
                                                  │
                                                  ▼
                                   Apuesta un tamaño prudente (Kelly fraccionado)
                                   y mide tus resultados a largo plazo.
```

Todo el curso consiste en aprender a hacer bien **cada caja** de ese diagrama.

---

## Filosofía de costo: calidad máxima, precio casi cero

- **Aprender:** 100% gratis es posible y es de los mejores materiales del mundo (fast.ai, Kaggle, StatQuest, MIT/Harvard abiertos, 3Blue1Brown).
- **Computar:** Google Colab da GPUs gratis; tu laptop basta para empezar.
- **Datos:** football-data.co.uk, Kaggle Datasets, APIs públicas — gratis.
- **Único gasto recomendable (opcional):** 1 o 2 libros (~USD 30–40 en total) y, si quieres, el capital pequeño con el que operarás. Detalle en [`docs/06-recursos-presupuesto.md`](docs/06-recursos-presupuesto.md).

---

## Primer paso concreto (hoy mismo)

1. Lee [`docs/01-primeros-principios.md`](docs/01-primeros-principios.md) (30–45 min).
2. Crea una cuenta gratis en [Kaggle](https://www.kaggle.com) y abre [Kaggle Learn → Python](https://www.kaggle.com/learn/python).
3. Mira el primer video de [StatQuest](https://www.youtube.com/@statquest) sobre "probability vs likelihood".

Bienvenido. Empecemos por los cimientos. 👉 [`docs/01-primeros-principios.md`](docs/01-primeros-principios.md)
