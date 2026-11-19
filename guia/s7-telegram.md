---
titulo: Tu bot de Telegram
bloque: Setup
tiempo: 15 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s2-claude-code
resultado: Un bot de Telegram creado, su token guardado en un lugar seguro (nunca en el chat) y tu chat ID anotado.
---

Telegram es la forma más rápida de tener un asistente propio: crear un bot es gratis, lleva 5 minutos y no pide aprobaciones de Meta.
Ejemplo: Denvet puede tener un bot donde el equipo escribe "¿cuántos turnos hay mañana?" y recibe la respuesta.
Hoy creás el bot y guardás sus datos. Lo conectás en [Asistente en Telegram](#p2-asistente-telegram) o en [Agente que responde](#p3-agente-preguntas).

## Antes de empezar
- [ ] Telegram instalado en el celular (o en la compu) con tu cuenta. Si no la tenés, creala **antes**: pide tu número y un código por SMS.
- [ ] Un gestor de contraseñas para guardar el token.
- [ ] La pestaña **Code** abierta en **Local** con tu carpeta `prueba-claude` ([Claude Code](#s2-claude-code)).

> **Ojo:** el **token** del bot es una contraseña: quien lo tenga controla tu bot. **Nunca** lo pegues en el chat con Claude, en el cerebro, en GitHub ni en una captura. Va en tu gestor, en un archivo `.env` de tu compu (Paso 3) y en las credenciales de n8n o los secretos de Cloudflare.

> **Costo:** los bots de Telegram son gratis.

## Paso 1 · Abrí @BotFather
1. En Telegram, buscá **@BotFather** (o abrí **[t.me/botfather](https://t.me/botfather)**). Fijate que sea exactamente `@BotFather`: hay imitaciones.
2. Tocá **Iniciar** (o **Start**).

**Tenés que ver:** un mensaje de BotFather con la lista de comandos.

## Paso 2 · Creá el bot
1. Escribí `/newbot`.
2. Poné el **nombre** (lo ve la gente, se puede cambiar). Ejemplo: `Asistente Denvet`.
3. Poné el **usuario**: de 5 a 32 caracteres, sin tildes ni espacios, **terminado en `bot`** (por ejemplo `denvet_asistente_bot`). **No se puede cambiar después.**

**Tenés que ver:** el mensaje de confirmación con el link `t.me/[TU_BOT]` y el **token** (una tira larga con dos puntos en el medio).

## Paso 3 · Guardá el token (sin pasarlo por el chat)
1. Copiá el token y guardalo en tu gestor: **Nombre** `Telegram - [TU_BOT]`, **Contraseña** el token.
2. En la pestaña Code, pegá:

```prompt
Creá en esta carpeta un archivo .env con la línea TELEGRAM_TOKEN= vacía, agregá .env al .gitignore y abrime el .env en el editor de texto de mi compu. No me pidas el token por el chat.
```

3. En el editor que se abre, pegá el token justo después del `=` (sin espacios), guardá (**Cmd+S** o **Ctrl+S**) y cerralo.
4. Escribile a Claude: `listo`.

**Tenés que ver:** el archivo `.env` guardado. El token nunca apareció en el chat.

## Paso 4 · Escribile a tu bot
Un bot **no puede escribirte primero**.

1. Tocá el link `t.me/[TU_BOT]` y tocá **Iniciar** (o **Start**).
2. Mandale "hola".

**Tenés que ver:** el chat con tu bot abierto. Todavía no responde: es normal.

## Paso 5 · Conseguí tu chat ID
El **chat ID** es el número de tu chat. Sirve para que el bot te avise solo a vos. Pedíselo a Claude:

```prompt
Leé TELEGRAM_TOKEN del archivo .env sin mostrármelo ni repetirlo. Usá la API oficial de Telegram para: 1) confirmar con getMe que el token funciona y decirme el usuario del bot, 2) buscar con getUpdates el chat ID del mensaje "hola" que le mandé. Decime solo el usuario del bot y el chat ID.
```

Anotá el chat ID en la misma entrada del gestor (en notas).

**Tenés que ver:** el usuario de tu bot y un número de varios dígitos (tu chat ID).

> **Tip:** si no querés que Claude lea el token, buscá **@userinfobot** en Telegram: te responde tu **Id**, que es tu chat ID en un chat privado. Ojo: ese bot no es oficial de Telegram.

## Paso 6 · Si tu ruta tiene dos prácticas con Telegram, creá un segundo bot
Si vas a hacer [Asistente en Telegram](#p2-asistente-telegram) **y** [Agente que responde](#p3-agente-preguntas), necesitás **un bot para cada una**. Repetí los Pasos 2 a 4 con otro usuario y guardá el segundo token en otra entrada del gestor (en el `.env`, como `TELEGRAM_TOKEN_2=`). Tu chat ID es el mismo.

**Tenés que ver:** dos entradas en tu gestor, una por bot.

## Cómo sé que funcionó
Tenés el link `t.me/[TU_BOT]`, el token en tu gestor y en el `.env`, Claude confirmó que el token funciona y tu chat ID está anotado.

```prompt
Creé un bot de Telegram para [TU NEGOCIO]. Proponeme 5 cosas útiles que podría hacer para mi equipo interno y, para cada una, qué tendría que leer del cerebro de la empresa. Ordenalas de la más fácil a la más difícil.
```

**Tenés que ver:** una lista de ideas para elegir en la práctica.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| BotFather dice que el usuario no es válido | Que termine en `bot`, sin tildes, espacios ni guiones medios, de 5 a 32 caracteres. |
| El usuario ya está en uso | Agregá tu ciudad o un número. |
| Claude dice que el token no funciona (Unauthorized) | Abrí el `.env` de nuevo y revisá que el token esté completo, sin espacios. |
| Claude no encuentra tu chat ID | Mandale un mensaje nuevo al bot y pedile que lo busque otra vez. Si el bot ya está conectado a n8n o a Cloudflare, usá @userinfobot. |
| Perdiste el token o se filtró | En @BotFather, `/token`, elegí tu bot y guardá el nuevo en el gestor y en el `.env`. El viejo deja de andar. |
| Pegaste el token en el chat sin querer | Generá uno nuevo con `/token` en @BotFather. |

## Para seguir solo
- Con `/mybots` en @BotFather cambiás la foto y la descripción del bot.
- Un bot por función (avisos internos, clientes): es más fácil de controlar.
- Si lo agregás a un grupo, el chat ID del grupo es otro número.

## Fuentes
Consultadas el 18/11/2026.
- Crear bots con @BotFather: https://core.telegram.org/bots/features
- Bot API (`getMe`, `getUpdates`): https://core.telegram.org/bots/api
- Preguntas frecuentes y costos: https://core.telegram.org/bots/faq
