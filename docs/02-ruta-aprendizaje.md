# 02 · Ruta de aprendizaje para DOMINAR el tema (12 meses, casi todo gratis)

> Versión 3. Novedades de esta versión:
> - **Carril de empleabilidad 💼** integrado en las Fases 1–2: SQL, un dashboard (Power BI) y un primer proyecto freelance hacia el mes 6–9. La meta sigue siendo **científico de datos**; el carril 💼 te hace contratable como **analista** por el camino (ver la nueva sección "Analista vs. científico").
> - **Multiplicadores de ingreso**: inglés y contexto de negocio.
>
> (De la versión 2 se conservan: Fase 0 en español, checkpoints por fase, horizonte honesto de 12 meses, sistema de retención y guía para usar la IA como tutor.)
>
> Dedicación: **1–1.5 h/día** (8–10 h/semana). Si un mes te toma dos, no pasa nada: los checkpoints mandan, no el calendario.

---

## Mapa general

```
FASE 0 (semanas 1–2)   Perder el miedo a programar        ── el peaje de entrada
FASE 1 (meses 1–3)     Cimientos: Python + estadística    ── COMPETENTE en datos
FASE 2 (meses 4–6)     Especialización: ML + mercados     ── COMPETENTE en predicción
FASE 3 (meses 7–12)    Dominio: Bayes, series temporales, ── DOMINIO real
                       paper trading sostenido, portafolio
```

**Regla de oro:** no avanzas de fase hasta pasar su checkpoint. Es mejor repetir un mes que construir sobre arena.

---

## Analista vs. científico de datos: tu meta no cambia, el camino gana un escalón

Tu meta es ser **científico de datos** (modelos, probabilidad, predicción — lo que esta ruta ya construye). Pero al mercado laboral casi nadie entra directo como científico: el rol de **analista de datos** es el escalón de entrada que **te paga mientras terminas** de construir el perfil de científico. La mayoría de científicos de datos fueron analistas primero.

| | Analista de datos | Científico de datos |
|---|-------------------|---------------------|
| Pregunta que responde | "¿Qué pasó y por qué?" | "¿Qué va a pasar y qué hacemos?" |
| Herramientas núcleo | **SQL**, Excel, dashboards (Power BI/Tableau), algo de Python | Python, estadística profunda, **machine learning**, modelos |
| Entrada realista al empleo | 6–12 meses de estudio | 18–24 meses (o creciendo internamente desde analista) |

La superposición es ~70% (datos, limpieza, estadística, comunicación). El científico añade la capa de modelado — justo lo que cubren las Fases 2 y 3. Por eso esta ruta forma **ambos perfiles a la vez**: el *carril de empleabilidad* (marcado con 💼 abajo) te hace contratable como analista hacia el mes ~9, y el resto de la ruta te convierte en científico hacia el mes ~24. No es un desvío: es el mismo camino con una puerta de ingreso antes.

---

## Cómo estudiar (léelo antes de empezar)

1. **1 hora de práctica por cada hora de teoría.** Ver videos sin escribir código = no aprender.
2. **Estudia en sesiones cortas y frecuentes** (45–60 min diarios) en vez de maratones de fin de semana. La memoria funciona así.
3. **Repasa con tarjetas ([Anki](https://apps.ankiweb.net/), gratis).** Cada concepto nuevo (¿qué es λ en Poisson? ¿fórmula del EV?) va a una tarjeta. 10 min de repaso diario evita reaprender todo cada mes.
4. **Lleva un diario de aprendizaje** (un archivo `diario.md` en este repo): 3 líneas al final de cada sesión — qué hice, qué no entendí, qué sigue. Releerlo los domingos consolida muchísimo.
5. **Construye en público:** sube cada notebook a este repo. En 12 meses tendrás un portafolio real.

### Cómo usarme a mí (Claude) como tutor — sin hacerte trampa

La IA puede acelerarte 3× o puede impedir que aprendas. La diferencia está en el orden:

- ✅ **Intenta primero tú** (aunque sea 10 minutos). Luego pídeme: *"esto intenté, esto esperaba, esto pasó — ¿qué no entiendo?"*
- ✅ Pídeme que **explique** código línea por línea, que te ponga **ejercicios**, que revise tu solución, que te traduzca errores.
- ✅ Pídeme **analogías** cuando un concepto no entre ("explícame la validación cruzada como si fuera cocina").
- ❌ No me pidas el código final para copiarlo sin leerlo. Lo sabrás porque en el checkpoint no podrás reproducirlo solo — y los checkpoints se hacen **sin ayuda**.

---

## FASE 0 (semanas 1–2) — Perder el miedo a programar

**Meta:** que escribir y correr código deje de intimidarte. Nada de modelos todavía: solo familiaridad.

**Recursos (en español, gratis):**
- 🟢 [Python para todos — es.py4e.com](https://es.py4e.com/) — el curso del Prof. Charles Severance (U. de Michigan) traducido al español, con [libro PDF gratis](http://do1.dr-chuck.com/pythonlearn/ES_es/pythonlearn.pdf). Diseñado para gente **sin** perfil técnico. Haz los capítulos 1–5.
- 📺 [freeCodeCamp en Español (YouTube)](https://www.youtube.com/@freecodecampespanol) — cursos completos de Python en español, gratis.
- 🟢 [Google Colab](https://colab.research.google.com/) — tu cuaderno de trabajo: cero instalación.

**Plan de las 2 semanas:**
- Días 1–3: variables, números, texto, `print()`. Escribe una calculadora de probabilidad implícita (`1/cuota`).
- Días 4–7: condicionales (`if`) y bucles (`for`). Escribe un programa que recorra una lista de cuotas y diga cuáles superan un umbral.
- Días 8–14: listas, diccionarios, funciones. Reescribe la calculadora como función `edge(prob_modelo, precio)`.

**Trabaja cada sesión conmigo:** dime qué intentas, pega tus errores, pídeme ejercicios. Para eso estoy.

### ✅ Checkpoint Fase 0 (sin ayuda, sin IA)
Escribes desde cero, en Colab, una función que reciba una probabilidad y un precio, calcule el valor esperado y devuelva `"operar"` o `"no operar"`. Si la escribes y corre: **pasaste**. Si no, repite la semana 2 — es normal y no dice nada malo de ti.

---

## FASE 1 (meses 1–3) — Cimientos

### Mes 1 — Python para datos (pandas)

**Meta:** cargar un CSV de partidos y responder preguntas con pandas.

- 🟢 [Kaggle Learn · Python](https://www.kaggle.com/learn/python) (repaso, ahora en inglés — ya tendrás la base para seguirlo) y [Kaggle Learn · Pandas](https://www.kaggle.com/learn/pandas).
- 🟢 [Python para todos](https://es.py4e.com/), capítulos de archivos y datos, si prefieres seguir en español.
- 📺 [Corey Schafer · Pandas (YouTube)](https://www.youtube.com/@coreyms) para profundizar.

**Proyecto:** con datos de [football-data.co.uk](https://www.football-data.co.uk/data.php): ¿qué equipo metió más goles de local? ¿con qué frecuencia gana el local? ¿qué pasa con esa frecuencia en ligas distintas?

### Mes 2 — Estadística y probabilidad (ya lo empezaste — bien)

**Meta:** dominar los conceptos del [`docs/01`](01-primeros-principios.md) con matemáticas.

- 🟢 [Khan Academy en español · Estadística y probabilidad](https://es.khanacademy.org/math/statistics-probability) — **sigue donde vas**, es la elección correcta.
- 📺 [StatQuest](https://www.youtube.com/@statquest) (inglés, activa subtítulos) — refuerzo visual.
- 📺 [3Blue1Brown](https://www.youtube.com/@3blue1brown) — Bayes y distribuciones con intuición visual.
- 🟢 [Seeing Theory (Brown)](https://seeing-theory.brown.edu/) — probabilidad interactiva.

**Imprescindibles:** media/varianza, normal, **Poisson**, binomial, regresión lineal y logística, Bayes.

**Proyecto (une los meses 1 y 2):** calcula con `scipy.stats.poisson` la probabilidad de que un equipo que promedia 1.4 goles marque 0, 1, 2, 3 goles, y compárala con las frecuencias reales del CSV. Ver que la teoría encaja con datos reales es un momento mágico.

### Mes 3 — Visualización + primer modelo + SQL 💼

- 🟢 [Kaggle Learn · Data Visualization](https://www.kaggle.com/learn/data-visualization).
- 🟢 [Kaggle Learn · Intro to Machine Learning](https://www.kaggle.com/learn/intro-to-machine-learning).
- 💼 [Kaggle Learn · Intro to SQL](https://www.kaggle.com/learn/intro-to-sql) (~4 h) y luego [Advanced SQL](https://www.kaggle.com/learn/advanced-sql). **SQL aparece en más del 80% de las vacantes de datos** — es la habilidad que más rápido te vuelve empleable, y es fácil: si ya piensas en pandas, SQL es lo mismo con otra sintaxis.
- 📖 Opcional y motivador: *The Signal and the Noise* (Nate Silver).

**Proyecto:** regresión logística que prediga si gana el local con 2–3 variables. Grafica sus probabilidades.

### ✅ Checkpoint Fase 1 (sin ayuda)
1. Cargas un CSV nuevo y produces una tabla resumen con pandas (agrupar, promediar, ordenar).
2. Explicas en voz alta, a otra persona, qué es una distribución de Poisson y por qué sirve para goles.
3. Entrenas una regresión logística y explicas qué significa su salida.
4. 💼 Escribes una consulta SQL con `JOIN` y `GROUP BY` sobre dos tablas y explicas qué devuelve.

---

## FASE 2 (meses 4–6) — Especialización en predicción y mercados

### Mes 4 — Machine learning en serio

**Meta:** entrenar, validar y **evaluar sin engañarte** (el error #1 del principiante).

- 🟢 [Kaggle Learn · Intermediate ML](https://www.kaggle.com/learn/intermediate-machine-learning).
- 🟢 [scikit-learn · User Guide](https://scikit-learn.org/stable/user_guide.html) — referencia oficial.
- 📖 Gratis y de nivel universitario: [*An Introduction to Statistical Learning* (ISLP, edición Python)](https://www.statlearning.com/) — PDF oficial gratuito. Lee los capítulos de clasificación y validación.
- 📖 Opcional (~USD 35): *Hands-On Machine Learning* (Géron), o sus [notebooks gratis](https://github.com/ageron/handson-ml3).

**Clave:** train/test split, validación cruzada, overfitting, **calibración**, Brier, log loss.

### Mes 5 — Modelado de mercados + backtesting

- Trabaja a fondo [`docs/04`](04-modelado-tablas-prediccion.md) de este repo: reproduce TODO el código tú mismo.
- 🟢 [Pinnacle · Betting Resources](https://www.pinnacle.com/en/betting-resources) — EV, Kelly, CLV, eficiencia.
- 📄 [Systematic Review of ML in Sports Betting (arXiv)](https://arxiv.org/html/2410.21484v1).

**Proyecto:** backtest honesto con cuotas históricas (cronológico, sin mirar el futuro, con costos).

### Mes 6 — Paper trading + calibración personal

- Lee [`docs/05`](05-polymarket-practica.md) completo.
- 🟢 [Good Judgment Open](https://www.gjopen.com/) — empieza a pronosticar geopolítica real con puntaje. **No lo dejarás en 12 meses.**
- 📖 *Superforecasting* (Tetlock) — obligada para geopolítica.

**Proyecto:** 4 semanas registrando cada pronóstico (tu probabilidad, precio del mercado, resultado) y calcula tu Brier.

### 💼 Carril de empleabilidad Fase 2 (meses 5–6, en paralelo)

- Descarga [Power BI Desktop](https://www.microsoft.com/es-es/power-platform/products/power-bi/desktop) (gratis) y construye **un dashboard financiero** con datos reales (ej. indicadores macro de [FRED](https://fred.stlouisfed.org/) o datos de tu liga). Súbelo al portafolio con capturas y explicación.
- Con Python + SQL + un dashboard publicado ya tienes el kit mínimo de analista. **Hito del mes 6–9:** consigue tu **primer proyecto freelance pequeño** (automatizar un reporte, un dashboard para una pyme) en [Workana](https://www.workana.com/) o [Upwork](https://www.upwork.com/). No es por el dinero: es la primera validación de mercado de tu habilidad, y una línea real en tu portafolio.
- Aprovecha tu carrera: proyectos con sabor a **finanzas/fintech** (el sector que mejor paga en LATAM) te diferencian de los mil portafolios genéricos de Titanic e iris.

### ✅ Checkpoint Fase 2 (sin ayuda)
1. Reconstruyes el modelo de Poisson del [`docs/04`](04-modelado-tablas-prediccion.md) desde cero en un notebook limpio.
2. Tu backtest reporta ROI, número de apuestas y log loss, y puedes defender por qué no tiene look-ahead bias.
3. Tienes ≥ 30 pronósticos registrados con tu Brier calculado.
4. 💼 Tienes un dashboard publicado en tu portafolio y has enviado al menos 5 propuestas freelance.

**Al pasar este checkpoint eres *competente*** (y contratable como analista de datos). Lo que sigue es la diferencia entre competente y dominio — es decir, el tramo de analista a **científico**.

---

## FASE 3 (meses 7–12) — Dominio

El dominio no es "más cursos": es **profundidad en tres frentes + volumen de práctica real**.

### Meses 7–8 — Estadística bayesiana en serio (geopolítica)

- 📺 [Statistical Rethinking — Richard McElreath (lecturas completas gratis en YouTube)](https://www.youtube.com/@rmcelreath) — el mejor curso bayesiano aplicado del mundo, gratis. Con [código y materiales en GitHub](https://github.com/rmcelreath/stat_rethinking_2024).
- Práctica continua en [Good Judgment Open](https://www.gjopen.com/) y [Metaculus](https://www.metaculus.com/): mínimo 3 preguntas activas siempre.

**Proyecto:** para una pregunta geopolítica real, documenta tu proceso completo: base rate → descomposición → actualizaciones bayesianas con cada noticia → comparación con el precio de Polymarket.

### Meses 9–10 — Series temporales (futuros/macro) + ML avanzado

- 🟢 [Kaggle Learn · Time Series](https://www.kaggle.com/learn/time-series).
- 📖 [*Forecasting: Principles and Practice* (Hyndman & Athanasopoulos)](https://otexts.com/fpp3/) — el libro de referencia mundial de pronóstico, **gratis online** (usa R; lee la teoría ahí y practica en Python con `statsmodels`).
- 🟢 XGBoost/LightGBM sobre tus datos de fútbol: ¿le ganan a tu Poisson en log loss? Documenta el experimento.
- Datos macro: [FRED](https://fred.stlouisfed.org/).

### Meses 11–12 — Volumen, portafolio y comunidad

1. **Completa tus primeras 100 operaciones en papel** (plan del [`docs/05`](05-polymarket-practica.md)) con diario, Brier, ROI y CLV.
2. **Portafolio público:** deja este repo impecable — 3 proyectos estrella (modelo deportivo con backtest, análisis bayesiano geopolítico, experimento de series temporales), cada uno con README claro. Esto también es tu currículum de data scientist.
3. **Comunidad:** participa en una [competencia de Kaggle](https://www.kaggle.com/competitions) (las "Playground" son ideales) y en los foros de Metaculus. Explicar tus modelos a otros es el examen final real.
4. **Decisión informada:** con tus números de 100 operaciones en papel, decide si pasas a dinero real pequeño (Kelly ¼) o si iteras el modelo otro trimestre.

### ✅ Checkpoint de DOMINIO (el examen final)
1. Tu Brier en Good Judgment Open está en la mitad superior de los pronosticadores.
2. Tu modelo deportivo le gana en log loss a la frecuencia base **y** te acercas al mercado de cierre (CLV ≥ 0 en promedio).
3. Puedes explicarle a un principiante, sin notas, todo el flujo: datos → modelo → calibración → edge → Kelly → medición.
4. Tienes 100+ operaciones en papel documentadas y sabes exactamente cuál es (o no es) tu ventaja.

Si cumples los 4: ya no estás aprendiendo el tema. **Lo dominas.** Lo que sigue es refinamiento infinito, como en cualquier disciplina seria.

---

## Multiplicadores de ingreso (en paralelo, poco tiempo al día)

Dos variables que no son "de datos" pero multiplican lo que ganarás con los mismos conocimientos:

1. **Inglés (20 min/día desde hoy).** Es la frontera entre el mercado local y el remoto internacional, donde los sueldos de datos se multiplican por 3–5×. Con B2 puedes aplicar a remoto. Gratis: [Duolingo](https://www.duolingo.com/) para el hábito + consumir StatQuest/Kaggle en inglés con subtítulos (aprendes datos e inglés a la vez).
2. **Contexto de negocio.** La IA está automatizando las tareas junior mecánicas; lo que los empleadores reportan que falta no es sintaxis sino criterio de negocio. Tu carrera (finanzas y negocios internacionales) es exactamente ese diferenciador — úsala eligiendo proyectos y vacantes de fintech/banca, no la escondas.

---

## Si solo recuerdas cinco cosas

1. Los **checkpoints** mandan, no el calendario.
2. **Práctica diaria corta** le gana a maratones. Anki + diario para no olvidar.
3. Usa la IA para **entender**, nunca para saltarte el entender.
4. **Competente** = 6 meses. **Dominio** = 12 con Fase 3 y volumen real de práctica.
5. Nada de dinero real hasta que tus números en papel lo justifiquen.

➡️ Siguiente: instala las herramientas → [`docs/03-herramientas-stack.md`](03-herramientas-stack.md)
