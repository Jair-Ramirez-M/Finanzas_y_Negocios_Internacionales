# 02 · Ruta de aprendizaje (plan de 6 meses, gratis)

> Plan realista, en orden, con recursos **gratuitos y de primer nivel**. Dedica **1–1.5 h/día** o **8–10 h/semana**. Si vas más lento, no pasa nada: la constancia gana.
>
> Principio pedagógico: **aprende haciendo**. No veas 20 horas de video sin escribir código. Por cada hora de teoría, una hora de práctica.

---

## Mapa general

```
Mes 1: Python + datos (pandas)          ──┐
Mes 2: Estadística y probabilidad         │  CIMIENTOS
Mes 3: Visualización + primer modelo    ──┘
Mes 4: Machine learning (scikit-learn)  ──┐
Mes 5: Modelado de mercados + backtesting │  ESPECIALIZACIÓN
Mes 6: Polymarket en papel + calibración──┘
```

No necesitas terminar el Mes 1 para empezar a divertirte: desde la semana 1 ya manipularás datos reales.

---

## Mes 1 — Python y manejo de datos

**Meta:** poder cargar un CSV de partidos y calcular estadísticas básicas con pandas.

- 🟢 [Kaggle Learn · Python](https://www.kaggle.com/learn/python) — micro-curso gratis, 5 h.
- 🟢 [Kaggle Learn · Pandas](https://www.kaggle.com/learn/pandas) — gratis, 4 h. **Pandas es LA herramienta para tablas de datos.**
- 🟢 [Harvard CS50P · Python](https://cs50.harvard.edu/python/) — gratis, más profundo si quieres bases sólidas de programación.
- 📺 [Corey Schafer · Python (YouTube)](https://www.youtube.com/@coreyms) — tutoriales claros y gratis.

**Proyecto del mes:** descarga un CSV de [football-data.co.uk](https://www.football-data.co.uk/data.php) (gratis) y responde con pandas: ¿qué equipo metió más goles de local la temporada pasada? ¿Con qué frecuencia gana el local?

---

## Mes 2 — Estadística y probabilidad (el músculo del data scientist)

**Meta:** entender distribuciones, valor esperado, regresión y Bayes (lo de [`docs/01`](01-primeros-principios.md), ya con matemáticas).

- 🟢 [Khan Academy · Statistics and Probability](https://www.khanacademy.org/math/statistics-probability) — gratis, base sólida desde cero.
- 📺 [StatQuest with Josh Starmer](https://www.youtube.com/@statquest) — **el mejor canal gratuito** para entender estadística y ML "claramente explicado". Empieza por sus playlists de estadística.
- 📺 [3Blue1Brown](https://www.youtube.com/@3blue1brown) — intuición visual de probabilidad, Bayes y álgebra/ cálculo.
- 🟢 [Seeing Theory (Brown University)](https://seeing-theory.brown.edu/) — probabilidad **interactiva** en el navegador, gratis.

**Conceptos imprescindibles este mes:** media/varianza, distribución normal, **distribución de Poisson** (clave para goles), distribución binomial, regresión lineal y logística, teorema de Bayes.

**Proyecto del mes:** estima "a mano" con Poisson la probabilidad de que un equipo que promedia 1.4 goles marque exactamente 2 en un partido.

---

## Mes 3 — Visualización + tu primer modelo simple

**Meta:** graficar datos y construir un **modelo de regresión** que prediga algo.

- 🟢 [Kaggle Learn · Data Visualization](https://www.kaggle.com/learn/data-visualization) — gratis.
- 🟢 [Kaggle Learn · Intro to Machine Learning](https://www.kaggle.com/learn/intro-to-machine-learning) — gratis, 3 h. Tu primer modelo predictivo.
- 📖 Lectura ligera y motivadora: *The Signal and the Noise* de Nate Silver (sobre por qué unos pronósticos fallan y otros no). Opcional.

**Proyecto del mes:** una **regresión logística** que prediga si gana el local usando 2–3 variables (forma reciente, ventaja de local). Mide su acierto.

---

## Mes 4 — Machine Learning en serio (scikit-learn)

**Meta:** entrenar, validar y evaluar modelos correctamente (sin engañarte a ti mismo).

- 🟢 [Kaggle Learn · Intermediate Machine Learning](https://www.kaggle.com/learn/intermediate-machine-learning) — gratis.
- 🟢 [scikit-learn · User Guide oficial](https://scikit-learn.org/stable/user_guide.html) — documentación de referencia, gratis.
- 🟢 [fast.ai · Practical Deep Learning for Coders](https://course.fast.ai/) — gratis, enfoque "construye primero". Para cuando quieras ir más allá.
- 📖 (Opcional, ~USD 35, muy recomendado) *Hands-On Machine Learning* de Aurélien Géron — el mejor libro práctico. O lee gratis sus [notebooks en GitHub](https://github.com/ageron/handson-ml3).

**Conceptos clave:** train/test split, **validación cruzada**, overfitting, **calibración de probabilidades**, métricas (Brier, log loss, AUC). El error #1 del principiante es evaluar mal y creerse mejor de lo que es.

**Proyecto del mes:** modelo de Poisson o gradient boosting para 1X2 (local/empate/visitante) de una liga. Evalúa con log loss en datos que el modelo **no vio**.

---

## Mes 5 — Modelado de mercados de predicción + backtesting

**Meta:** convertir probabilidades en decisiones de trading y **probarlas contra el pasado** (backtesting).

- Lee a fondo [`docs/04-modelado-tablas-prediccion.md`](04-modelado-tablas-prediccion.md) de este repo (ejemplo completo con código).
- 🟢 [Pinnacle · Betting Resources](https://www.pinnacle.com/en/betting-resources) — artículos gratuitos y serios sobre valor esperado, Kelly, closing line value (CLV) y eficiencia de mercado. Pinnacle es la casa de apuestas más "afilada"; aprender de ellos es oro.
- 📄 [A Systematic Review of Machine Learning in Sports Betting (arXiv 2024)](https://arxiv.org/html/2410.21484v1) — panorama académico gratuito.

**Conceptos clave:** edge, **Closing Line Value (CLV)** como medida de si realmente tienes ventaja, **criterio de Kelly** para tamaño de apuesta, comisiones/spread, y el peligro del **backtest sobreajustado**.

**Proyecto del mes:** backtest honesto: con cuotas históricas, ¿tu modelo habría tenido ROI positivo apostando solo cuando hay edge > X%?

---

## Mes 6 — Polymarket en papel + calibración personal

**Meta:** operar **sin dinero real** (paper trading), llevar registro y medir tu calibración.

- Lee [`docs/05-polymarket-practica.md`](05-polymarket-practica.md) completo.
- 📖 *Superforecasting* de Philip Tetlock — **lectura obligada para geopolítica**. Cómo gente común vence a expertos pronosticando eventos mundiales. (~USD 12, o búscalo en tu biblioteca / resumen del [Good Judgment Project](https://goodjudgment.com/).)
- 🟢 [Good Judgment Open](https://www.gjopen.com/) — **gratis**: practica pronósticos de geopolítica reales y recibe tu Brier score. **El mejor gimnasio de calibración que existe.**
- 🟢 [Metaculus](https://www.metaculus.com/) — comunidad gratuita de pronóstico con historial y puntajes.

**Proyecto del mes:** durante 4 semanas registra en una hoja de cálculo cada pronóstico (tu probabilidad, el precio del mercado, el resultado). Calcula tu **Brier score**. ¿Estás calibrado? ¿Le ganas al mercado?

---

## Reglas de oro del aprendizaje

1. **Una hora de práctica por cada hora de teoría.** El conocimiento que no usas se evapora.
2. **Construye en público.** Sube tus notebooks a este repo / GitHub. Tu historial es tu currículum.
3. **No persigas lo "avanzado" antes de tiempo.** Deep learning y LLMs son geniales, pero una buena regresión logística bien calibrada le gana a una red neuronal mal evaluada.
4. **Mide todo.** Si no lo mides (Brier, log loss, ROI, CLV), te estás engañando.

➡️ Siguiente: instala las herramientas → [`docs/03-herramientas-stack.md`](03-herramientas-stack.md)
