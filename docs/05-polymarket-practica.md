# 05 · Polymarket en la práctica: cómo funciona, su API y cómo operar con criterio

> Aquí conectamos todo lo aprendido con la plataforma. Primero lo legal y lo estructural, luego la API (gratis), y al final la estrategia por tipo de mercado (deportes, futuros, geopolítica) y la gestión de riesgo.

---

## 1. ¿Qué es Polymarket exactamente?

Es un **mercado de predicción**: una bolsa donde se compran y venden contratos sobre si un evento ocurrirá. Cada contrato paga **$1 si el evento sucede** y **$0 si no**. El precio (entre $0 y $1) es la **probabilidad** que el mercado asigna al evento (ver [`docs/01`](01-primeros-principios.md)).

- Funciona sobre la blockchain **Polygon** y se liquida en **USDC** (un stablecoin = 1 dólar).
- Usa un **CLOB** (Central Limit Order Book): un libro de órdenes igual que una bolsa de valores, con compradores y vendedores poniendo precios.
- Ganas dinero de dos formas: (a) **aciertas** el evento y cobras $1 por contrato, o (b) **vendes antes** a un precio más alto del que compraste (trading).

---

## 2. Situación legal (verifícala SIEMPRE, cambia rápido)

- En **2022**, la CFTC multó a Polymarket (~USD 1.4 millones) por operar como mercado de derivados no registrado y **bloqueó a usuarios de EE. UU.**
- En **julio de 2025**, Polymarket compró **QCEX** (un exchange/clearinghouse con licencia CFTC) por ~USD 112 millones.
- El **25 de noviembre de 2025** la CFTC emitió una Orden de Designación enmendada, y el **3 de diciembre de 2025** lanzó **Polymarket US** (operado por QCX LLC), un **DCM regulado** para residentes de EE. UU.
- La **versión internacional** sigue **bloqueando IPs de EE. UU.**

👉 **Para ti:** revisa qué versión y qué mercados son legales **en tu país**. Las reglas sobre apuestas/derivados varían por jurisdicción. No uses VPN para evadir bloqueos: puede violar los términos y la ley local, y arriesgas tus fondos.

Fuentes: [Comunicado oficial (PR Newswire)](https://www.prnewswire.com/news-releases/polymarket-receives-cftc-approval-of-amended-order-of-designation-enabling-intermediated-us-market-access-302625833.html) · [Orden de la CFTC (PDF)](https://www.cftc.gov/media/12806/Polymarket%20US%20Amended%20Order%20of%20Designation/download) · [Polymarket – Wikipedia](https://en.wikipedia.org/wiki/Polymarket).

---

## 3. Las APIs de Polymarket (gratis para leer datos)

Polymarket ofrece APIs públicas y SDKs de código abierto. **Leer datos (precios, mercados, order books) es gratis y no requiere cuenta.** Operar con dinero sí requiere cuenta, fondos y firmar transacciones.

| API | Para qué sirve |
|-----|----------------|
| **Gamma API** | Metadatos de mercados: qué mercados existen, preguntas, categorías, fechas. |
| **CLOB API** | Precios, order books, y **colocar órdenes** (requiere autenticación con tu wallet). |
| **Data API / WebSocket** | Datos en tiempo real (precios que cambian al instante). |

**SDK oficial de Python:** [`py-clob-client`](https://github.com/Polymarket/py-clob-client) (y el nuevo [`py-clob-client-v2`](https://github.com/Polymarket/py-clob-client-v2), recomendado para proyectos nuevos: combina REST + WebSocket).

Documentación: [docs.polymarket.com](https://docs.polymarket.com/).

### Ejemplo: leer mercados (solo lectura, sin cuenta)

```python
import requests

# Gamma API: lista de mercados activos
r = requests.get(
    "https://gamma-api.polymarket.com/markets",
    params={"closed": "false", "limit": 5},
)
for m in r.json():
    print(m.get("question"), "→", m.get("outcomePrices"))
```

### Ejemplo: leer el precio/order book de un mercado con el SDK

```python
# pip install py-clob-client
from py_clob_client.client import ClobClient

# Solo lectura: no necesitas private key para ver precios públicos
client = ClobClient("https://clob.polymarket.com", chain_id=137)  # 137 = Polygon

# token_id lo obtienes de la Gamma API para el resultado que te interesa
# libro = client.get_order_book(token_id)
# precio = client.get_price(token_id, side="BUY")
# print(precio)
```

⚠️ Para **operar** necesitas: una wallet de Polygon, fondos en USDC, una API key derivada de tu firma (EIP-712), y las órdenes se firman con tu clave privada. **Nunca pongas tu clave privada en código que subas a GitHub.** Usa variables de entorno. Límite de ~60 órdenes/minuto por key.

---

## 4. Cómo leer un order book (lo esencial)

Un mercado de "Sí" muestra:
- **Bids** (compras): a qué precio la gente quiere comprar "Sí".
- **Asks** (ventas): a qué precio la gente quiere vender "Sí".
- **Spread**: la diferencia entre el mejor bid y el mejor ask. **Un spread amplio = mercado ilíquido = costoso de operar.**

Para que tu edge sobreviva, el spread debe ser **menor** que tu ventaja. Si tu edge es 4% pero el spread es 6%, **pierdes** aunque tu modelo acierte.

---

## 5. Estrategia por tipo de mercado

### 🏟️ Deportes (tu mejor punto de entrada)
- **Por qué empezar aquí:** datos abundantes, eventos repetidos (muchas operaciones → tu edge se manifiesta), modelos bien estudiados (Poisson, Elo, ML).
- **Método:** el flujo del [`docs/04`](04-modelado-tablas-prediccion.md). Tu rival de referencia son las cuotas de [Pinnacle](https://www.pinnacle.com/en/betting-resources) (la casa más eficiente). Si tu modelo no le gana a Pinnacle, busca nichos menos seguidos (ligas pequeñas, mercados secundarios).
- **Edge típico para principiantes:** disciplina y nichos ignorados, no batir el mercado principal de la NBA.

### 📈 Futuros / macro (intermedio)
- Mercados sobre precios, tasas, inflación, decisiones de bancos centrales.
- **Método:** análisis de **series temporales**, datos macro de [FRED](https://fred.stlouisfed.org/), entender el contexto económico. Más difícil de "modelar" puramente; mezcla datos y criterio.

### 🌍 Geopolítica (el más difícil, pero donde la multitud falla más)
- Eventos únicos: elecciones, conflictos, acuerdos. No hay "1000 repeticiones" → enfoque **bayesiano** y **superforecasting**.
- **Método (Tetlock / Good Judgment Project):**
  1. **Empieza por la base rate** (frecuencia histórica): ¿cuántas veces, históricamente, un gobierno en esta situación ha caído en 1 año?
  2. **Descompón la pregunta** en sub-preguntas más manejables.
  3. **Ajusta con la evidencia específica** (Bayes), poco a poco, sin sobre-reaccionar a titulares.
  4. **Piensa en probabilidades, no en historias.** Evita el sesgo de confirmación.
  5. **Promedia fuentes/puntos de vista** (la "sabiduría de las multitudes" interna).
- **Entrena gratis** tu calibración en [Good Judgment Open](https://www.gjopen.com/) y [Metaculus](https://www.metaculus.com/) antes de arriesgar dinero. Lee *Superforecasting* (Tetlock).

---

## 6. Gestión de riesgo (lo que separa a quien sobrevive de quien quiebra)

1. **Paper trading primero.** Registra predicciones sin dinero durante **meses**. Mide tu **Brier score**. Solo arriesga dinero si demuestras calibración y ventaja sobre el mercado.
2. **Bankroll separado.** Define un capital que puedas perder por completo. Nunca lo amplíes para "recuperar".
3. **Kelly fraccionado (¼).** Nunca apuestes grande en un solo evento. Ver [`docs/04`](04-modelado-tablas-prediccion.md).
4. **Diversifica operaciones.** Muchas apuestas pequeñas con edge > pocas grandes.
5. **Exige edge mínimo** (ej. > 4–5%) que cubra spread y comisiones.
6. **Lleva un diario.** Cada operación: tu probabilidad, el precio, el tamaño, el resultado, qué aprendiste. Tu diario es tu mejor maestro.
7. **Cuida tu psicología.** El tilt (operar enojado o eufórico) destruye cuentas. Si pierdes la calma, cierra el portátil.

---

## 7. Tu plan de "primeras 100 operaciones" (en papel)

1. Elige **un** deporte/liga con buenos datos.
2. Construye el modelo del [`docs/04`](04-modelado-tablas-prediccion.md).
3. Cada semana, genera tu tabla de predicciones y compárala con Polymarket (lee precios vía API).
4. Registra dónde **habrías** operado (edge > umbral) y el resultado real.
5. Tras ~100 operaciones, evalúa: ¿Brier mejor que el mercado? ¿ROI positivo? ¿CLV positivo?
6. Solo entonces considera dinero real, **pequeño**, con Kelly ¼.

> Si tus números en papel no son buenos, **no es momento de dinero real**. Es momento de mejorar el modelo. Esto es lo más importante de toda la guía.

➡️ Siguiente: fuentes confiables y presupuesto → [`docs/06-recursos-presupuesto.md`](06-recursos-presupuesto.md)
