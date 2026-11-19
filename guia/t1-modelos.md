---
titulo: 'Modelos: qué son y cuál usar'
bloque: Teoría
tiempo: 15 min (10 de lectura + 5 de prueba)
para: Todos
necesitas: nada
resultado: Entendés qué es un modelo, por qué "se olvida", qué es un token y qué modelo elegir para cada tarea.
---

Un modelo es el "motor" que está detrás de Claude, ChatGPT o Gemini. Si entendés 4 ideas sobre cómo funciona, vas a saber por qué a veces responde genial y a veces cualquier cosa.
Ejemplo: en Viajes TDH, si le pedís "armá un paquete a Bariloche" sin decirle nada más, te arma uno para cualquier agencia del mundo. Si le das tus precios, tus hoteles y cómo hablás, te arma el tuyo.

> **Datos:** verificado en la documentación oficial de Claude Code el 18/11/2026. Los nombres de modelos cambian varias veces por año: si leés esto en 2027, revisá `/model`.

> **Tip:** esta página tiene dos pruebas. La primera se hace en el chat de [claude.ai](https://claude.ai). La segunda, en **Claude Code** (Claude trabajando en tu compu): si todavía no lo instalaste, leé la página ahora y hacé esa prueba después de [Instalá Claude Code](#s2-claude-code).

## Las 4 ideas que explican todo

### 1. Predice la palabra siguiente
Un modelo leyó una biblioteca enorme y aprendió qué palabra suele venir después de otra. No "sabe" de tu negocio: completa texto con lo más probable.
**Analogía:** un empleado nuevo que leyó todos los libros del mundo pero nunca pisó tu local.

### 2. No tiene memoria entre chats
Cada chat empieza de cero. Lo que no está en la conversación (o en un archivo que le pasás) no existe para él.
**Analogía:** cada mañana llega un empleado distinto. Si no le dejás el manual en el escritorio, no sabe nada de ayer.

### 3. Solo ve su ventana de contexto
Todo lo que lee en esa conversación (tu pedido, los archivos, lo que respondió antes) entra en una "ventana" con límite. Se mide en **tokens**.

- **Token** = un pedacito de palabra. Una palabra larga, como "presupuestación", puede ser 3 o 4 tokens. Es lo que se paga y lo que se llena.
- Los modelos actuales de Claude tienen una ventana de **1 millón de tokens** en Claude Code (más de mil páginas de texto). Parece mucho, pero un chat largo con archivos pesados la llena.
- Cuando se llena, Claude Code **resume** la conversación para seguir (eso se llama compactar). En el resumen se pierden detalles.

**Analogía:** una mochila. Entra mucho, pero si la llenás de cosas que no sirven, lo importante queda abajo y no lo encuentra.

### 4. Más contexto bueno = mejor respuesta
Lo único que controlás es **lo que le das para leer**. Contexto bueno (tus precios, tus clientes, tu forma de hablar) = respuesta tuya. Contexto basura (un chat de 3 horas que mezcló cinco temas) = respuesta confundida y más cara.

## Por qué "se olvida" (y qué hacer)
| Te pasa | Por qué | Qué hacés |
|---|---|---|
| Al otro día no se acuerda de nada | No tiene memoria entre chats | Armá tu **cerebro**: una carpeta de archivos de texto que lee siempre. El principal se llama `CLAUDE.md` ([Tu cerebro](#p1-cerebro)) |
| En un chat largo empieza a contradecirse | La mochila se llenó y se resumió | Un chat por tarea. En Claude Code: `/context`, `/compact`, `/clear` ([Atajos](#t5-atajos)) |
| Inventa un precio o un dato | Completa con "lo más probable" cuando no tiene el dato | Dale el dato y pedile: "si no está en mis archivos, escribí PENDIENTE" |
| Responde genérico | No sabe nada de vos | Pasale el archivo: "leé `negocio/oferta-y-precios.md`" |

> **Tip:** pasale el archivo, no lo pegues entero. "Leé `ventas/preguntas-frecuentes.md`" gasta menos que copiar 10 páginas en el chat.

**Probalo** (en el chat de [claude.ai](https://claude.ai); reemplazá `[MI NEGOCIO]` por una línea que describa tu empresa):

```prompt
Antes de responder, decime qué sabés de mi negocio y qué no sabés. Después escribí un post para Instagram para [MI NEGOCIO]. Si te falta un dato, marcalo PENDIENTE en vez de inventarlo.
```

## Las familias de Claude: cuál usar
Claude viene en "tamaños". Más grande = piensa mejor, pero tarda más y consume más de tu plan.

| Modelo | Cómo pensarlo | Usalo para | Ejemplo del taller |
|---|---|---|---|
| **Opus 5.5** | El gerente que piensa | Lo difícil: planificar, escribir con criterio, armar un sistema, revisar | Armar el cerebro de Fondus, diseñar el agente que filtra consultas |
| **Sonnet 5.5** | El empleado senior | El día a día: casi todo lo demás. Es el más usado en bots y automatizaciones por la API | Responder consultas en un bot de Telegram, armar una planilla |
| **Haiku 5.5** | El pasante rápido | Tareas simples y repetidas: clasificar, resumir, ordenar | Clasificar 500 mensajes en "consulta / queja / venta" |
| **Fable 5.2** | El especialista para tareas largas | Trabajos muy largos y difíciles (según la doc: "las tareas más difíciles y largas") | Rara vez en una PyME. Probalo si Opus no alcanza |

- En los planes Pro, Max y Ultra, Claude Code usa **Opus 5.5** de forma predeterminada.
- En la **API** (la puerta para que un programa, como un bot o n8n, use Claude sin vos) elegís vos el modelo, y cada uno tiene su precio. Ver [Stack y costos](#r-stack-y-costos).

> **Ojo:** Fable 5.2 aparece en Claude Code (`/model fable`, versión 2.1.321 o posterior). No es el modelo predeterminado en ningún plan. Si no lo ves en tu lista, actualizá con `claude update`.

### Cambiar de modelo y de "esfuerzo"
- **`/model`**: abre la lista de modelos. Con flechas elegís, **Enter** lo deja como predeterminado, **s** lo usa solo en esta sesión. También directo: `/model sonnet`, `/model opus`, `/model haiku`.
- **`/effort`**: cuánto piensa antes de responder. Niveles: `low`, `medium`, `high`, `xhigh`, `max`. El predeterminado en los modelos 5.5 es `medium`. También directo: `/effort high`.
- Dentro de `/model`, las **flechas izquierda y derecha** mueven el esfuerzo.

| Si la tarea es… | Modelo | Esfuerzo |
|---|---|---|
| Ordenar archivos, renombrar, resumir | Sonnet o Haiku | `low` o `medium` |
| Escribir un guion, armar una planilla, un bot simple | Sonnet u Opus | `medium` |
| Diseñar un proceso, un agente, el cerebro de la empresa | Opus | `high` |
| Algo que salió mal dos veces | Opus | `xhigh` |

> **Costo:** más modelo y más esfuerzo = más uso de tu plan. Si te quedás sin uso a media tarde, bajá a Sonnet y `medium`. Mirá cuánto te queda con `/usage`.

**Probalo** (en Claude Code, cuando ya lo tengas instalado):

1. Escribí esto y apretá **Enter**:

```prompt
/model
```

2. Movete con las flechas **arriba** y **abajo**. Apretá **s** sobre **Sonnet** para usarlo solo en esta sesión.
3. Pegá este pedido:

```prompt
Explicame en 5 líneas qué hace mi negocio y a quién le vende, a partir de mi CLAUDE.md. Si no tenés CLAUDE.md, decímelo.
```

4. Repetí los pasos 1 a 3 eligiendo **Opus** y compará las dos respuestas.

**Tenés que ver:** dos respuestas distintas. Si todavía no armaste tu cerebro, las dos te van a decir que no tienen `CLAUDE.md`: es normal, lo armás en [Tu cerebro](#p1-cerebro).

## Otros modelos del mercado: para qué sirve cada uno
Claude es el modelo de **texto, código y razonamiento** del taller. Para imagen, video y voz se usan otros. Esto es lo que usamos en la agencia en noviembre de 2026:

| Para… | Modelos / herramientas | Dónde lo usás | Ejemplo |
|---|---|---|---|
| Texto, código, agentes | Claude (Anthropic) · también ChatGPT (OpenAI) y Gemini (Google) | [claude.ai](https://claude.ai), Claude Code | Responder consultas, armar una web |
| Imágenes y placas | GPT Image 2 · Nano Banana 2 / Pro (Google) | Higgsfield, Canva | Placa de una promo de Celve |
| Video generado | Seedance 2.0 · Kling 3.0 · Veo 3 (Google) | Higgsfield | Escena de un producto para un anuncio |
| Presentador / avatar que habla | HeyGen | HeyGen | Video de Manuel explicando un ejercicio, con su avatar |
| Voz (locución, clon de voz) | ElevenLabs | ElevenLabs, Vapi | Locución de un reel, agente que atiende llamadas |

Detalle de cuentas y precios: [Herramientas creativas](#s12-creativas) y [Stack y costos](#r-stack-y-costos).

> **Ojo:** las versiones de los modelos de imagen y video cambian casi todos los meses. Verificá en la herramienta cuál está disponible el día que lo uses.

## Los planes de Claude, en una línea
- **Free**: chat. **No** incluye Claude Code ni Cowork.
- **Pro** (USD 20/mes, USD 17/mes anual): todo lo del taller. Es el mínimo.
- **Max** (USD 100/mes) y **Ultra** (USD 200/mes): más uso. Max y Ultra incluyen créditos de API, que **no** sirven dentro de Claude Code ni de la app.

Precios de noviembre de 2026. Verificá en [claude.com/pricing](https://claude.com/pricing) y mirá el detalle en [Stack y costos](#r-stack-y-costos).

## Para seguir solo
- Hacé la prueba "sin cerebro / con cerebro": el mismo pedido en un chat vacío y en Claude Code parado en la carpeta de tu cerebro. Compará.
- Usá una semana Sonnet como predeterminado y subí a Opus solo para lo difícil. Mirá con `/usage` cuánto te rinde el plan.
- Leé [Las piezas](#t2-piezas): el modelo es el motor, pero lo que lo vuelve útil es todo lo que le ponés alrededor.
