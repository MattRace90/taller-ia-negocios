---
titulo: Tu bot de Telegram
bloque: Setup
tiempo: 15 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: nada
resultado: Un bot de Telegram creado, su token guardado en un lugar seguro y tu chat ID anotado.
---

Telegram es la forma más rápida de tener un asistente propio: crear un bot es gratis, lleva 5 minutos y no pide trámites ni aprobaciones de Meta.
Ejemplo: Denvet puede tener un bot donde el equipo escribe "¿cuántos turnos hay mañana?" y recibe la respuesta, o donde llega el reporte del lunes.
Hoy creás el bot y guardás sus datos. Lo conectás a Claude en [Asistente en Telegram](#p2-asistente-telegram) o en [Agente que responde](#p3-agente-preguntas).

## Antes de empezar
- [ ] Telegram instalado en el celular (o en la compu) y con tu cuenta.

> **Ojo:** si todavía no tenés Telegram, crear la cuenta pide tu número de celular y un código por SMS (a veces tarda unos minutos). Hacelo **antes** de este paso, con el celular en la mano. Si el código no llega, esperá y pedí que te lo reenvíe, o seguí en dupla con alguien de tu empresa.
- [ ] Un gestor de contraseñas para guardar el token (el de tu navegador, el de tu celular, 1Password, Bitwarden…).

> **Ojo:** el **token** del bot es una contraseña. Quien lo tenga controla tu bot: puede leer lo que le escriben y mandar mensajes en su nombre. No lo pegues en un chat con Claude, en el cerebro, en GitHub ni en una captura de pantalla. Va solo en tu gestor de contraseñas y en las credenciales de n8n o en los secretos de Cloudflare.

> **Costo:** los bots de Telegram son gratis. Lo único pago es mandar mensajes masivos a más de 30 por segundo, que no vas a necesitar.

## Paso 1 · Abrí @BotFather
@BotFather es el bot oficial de Telegram para crear bots.

1. En Telegram, buscá **@BotFather** (o abrí **[t.me/botfather](https://t.me/botfather)**).
2. Fijate que el usuario sea exactamente `@BotFather`. Hay imitaciones con nombres parecidos.
3. Tocá **Iniciar** (o **Start**).

**Tenés que ver:** un mensaje de BotFather con la lista de comandos.

## Paso 2 · Creá el bot
1. Escribí:

```text
/newbot
```

2. BotFather te pide el **nombre** del bot: es el que ve la gente y lo podés cambiar después. Ejemplo: `Asistente Denvet`.
3. Después te pide el **usuario** (username). Reglas:
   - De 5 a 32 caracteres.
   - Solo letras sin tilde, números y guion bajo.
   - **Tiene que terminar en `bot`**. Ejemplos: `denvet_asistente_bot`, `CelveReportesBot`.
   - **No se puede cambiar después.** Pensalo un segundo.
4. Si el usuario ya existe, BotFather te pide otro. Probá con otra variante.

**Tenés que ver:** un mensaje que confirma que el bot se creó, con el link `t.me/[TU_BOT]` y un **token** (una tira larga de números y letras con dos puntos en el medio).

## Paso 3 · Guardá el token
1. Copiá el token completo.
2. Guardalo en tu gestor de contraseñas como una entrada nueva: **Nombre:** `Telegram - [TU_BOT]`, **Contraseña:** el token.
3. Borrá el token de cualquier otro lado donde lo hayas pegado (notas, portapapeles de otra app).

> **Tip:** si el token se filtra o lo perdés, en @BotFather usá `/token` para generar uno nuevo. El viejo deja de funcionar.

**Tenés que ver:** la entrada guardada en tu gestor de contraseñas.

## Paso 4 · Escribile a tu bot
Un bot **no puede escribirte primero**. Tenés que iniciar vos la conversación.

1. Tocá el link `t.me/[TU_BOT]` que te dio BotFather.
2. Tocá **Iniciar** (o **Start**).

**Tenés que ver:** el chat con tu bot abierto. Todavía no responde: lo conectamos en [Asistente en Telegram](#p2-asistente-telegram).

## Paso 5 · Conseguí tu chat ID
El **chat ID** es el número que identifica tu chat. Lo vas a usar para que el bot te mande avisos a vos (y no a cualquiera).

**Camino rápido (bot de terceros):**
1. En Telegram, buscá **@userinfobot** y tocá **Iniciar**.
2. Te responde con tus datos. El número que aparece como **Id** es tu ID de usuario. En un chat privado con tu bot, tu chat ID es ese mismo número.

> **Ojo:** @userinfobot **no es oficial** de Telegram: es un bot de terceros que te muestra los datos de tu cuenta. Si preferís no usarlo, usá el camino oficial.

**Camino oficial (con la API de Telegram):**
1. Escribile cualquier cosa a **tu** bot (por ejemplo, "hola").
2. En tu navegador, abrí `https://api.telegram.org/bot[TU_TOKEN]/getUpdates`, reemplazando `[TU_TOKEN]` por tu token (sin espacios ni corchetes).
3. Buscá `"chat":{"id":` en el texto: el número que sigue es tu chat ID.
4. Cerrá la pestaña y no compartas esa dirección: tiene el token adentro. Si querés ser prolijo, borrala del historial del navegador. Si `getUpdates` no muestra nada, mandale otro mensaje al bot y recargá.

Anotá el chat ID en la misma entrada del gestor de contraseñas (en notas). No es secreto como el token, pero tampoco hace falta publicarlo.

**Tenés que ver:** un número de varios dígitos anotado como tu chat ID.

## Paso 6 · Si tu ruta tiene dos prácticas con Telegram, creá un segundo bot
Un bot manda sus mensajes a un solo sistema. Si tu ruta tiene [Asistente en Telegram](#p2-asistente-telegram) **y** [Agente que responde](#p3-agente-preguntas), necesitás **un bot para cada una**.

1. Repetí los Pasos 2 a 4 con otro nombre y otro usuario (por ejemplo, `denvet_gastos_bot` y `denvet_consultas_bot`).
2. Guardá el segundo token en otra entrada del gestor, con un nombre que diga para qué es.

Tu chat ID es el mismo para los dos bots.

**Tenés que ver:** dos entradas en tu gestor, una por bot, cada una con su token.

## Cómo sé que funcionó
- Tenés el link `t.me/[TU_BOT]`, el token guardado en tu gestor y tu chat ID anotado.
- Prueba opcional del token: abrí en tu navegador `https://api.telegram.org/bot[TU_TOKEN]/getMe` (reemplazando `[TU_TOKEN]`, sin espacios). Tiene que mostrar `"ok":true` y el usuario de tu bot. Después cerrá la pestaña y no compartas esa dirección: tiene el token adentro.

Y en Claude, sin pasarle ningún token:

```prompt
Creé un bot de Telegram para [TU NEGOCIO]. Proponeme 5 cosas útiles que podría hacer para mi equipo interno (no para clientes) y, para cada una, qué tendría que leer del cerebro de la empresa. Ordenalas de la más fácil a la más difícil.
```

**Tenés que ver:** una lista de ideas para elegir en la práctica.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| BotFather dice que el usuario no es válido | Revisá que termine en `bot`, que no tenga tildes, espacios ni guiones medios, y que tenga entre 5 y 32 caracteres. |
| BotFather dice que el usuario ya está en uso | Probá con otro: agregá tu ciudad o un número. |
| Perdiste el token | En @BotFather, `/token`, elegí tu bot y guardá el nuevo. |
| `getMe` devuelve `"ok":false` o "Unauthorized" | El token está mal copiado. Copialo de nuevo desde tu gestor. |
| No encontrás a @userinfobot | Usá el camino oficial con `getUpdates` (Paso 5). |
| `getUpdates` devuelve `"result":[]` (vacío) | Mandale un mensaje nuevo a tu bot y recargá. Si el bot ya está conectado a n8n o a Cloudflare, `getUpdates` no funciona: usá @userinfobot. |

## Para seguir solo
- En @BotFather podés cambiar la foto y la descripción del bot (comando `/mybots`).
- Creá un bot por función (uno para avisos internos, otro para clientes): es más fácil de controlar.
- Si lo agregás a un grupo, el chat ID del grupo es otro número distinto al tuyo.

## Fuentes
Consultadas el 18/11/2026.
- Crear bots con @BotFather (nombre, usuario, token, `/token`): https://core.telegram.org/bots/features
- Bot API (`getMe`, `getUpdates`, formato de las llamadas): https://core.telegram.org/bots/api
- Preguntas frecuentes y costos de bots: https://core.telegram.org/bots/faq
- @BotFather: https://t.me/botfather
- @userinfobot: bot de terceros, sin documentación oficial de Telegram.
