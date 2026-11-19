---
titulo: "Tu bot de WhatsApp con Unipile (no oficial, por QR)"
bloque: WhatsApp
tiempo: "60 a 90 min (necesitás el agente de la práctica ya publicado)"
para: Quien quiere probar rápido con un número secundario, o ya usa Unipile para LinkedIn
necesitas: p3-agente-preguntas, w1-opciones
resultado: Un número secundario de WhatsApp conectado a Unipile por QR y un bot que contesta con tu cerebro, sabiendo qué riesgo corrés y cómo cuidar el número.
---

Unipile conecta WhatsApp, LinkedIn, Instagram, mail y otros canales con una sola API. WhatsApp lo conecta **escaneando un QR**, como WhatsApp Web: en 5 minutos tenés el número enchufado, sin Meta y sin plantillas. El precio de esa velocidad: **no es oficial** y WhatsApp puede bloquear el número.
Ejemplo: La Consejera del Éxito quiere ver cómo contestaría un bot las dudas de su programa antes de decidir. Lo prueba una semana con un chip nuevo, no con su número de siempre.

> **Ojo:** la propia página de precios de Unipile dice que WhatsApp funciona por **ingeniería inversa**, no por la API oficial. Los términos de WhatsApp prohíben el acceso automatizado: si lo detecta, **suspende el número y perdés sus chats**. Usalo solo con un número que no te importe perder. Para tu número principal, mirá [dlastcrm](#w2-bot-dlastcrm) con la integración oficial o [Zernio](#w4-zernio).

> **Tip:** palabras que vas a ver en esta página:
> - **API:** la puerta para que un programa hable con otro. **Token de acceso (API key):** la contraseña de esa puerta.
> - **DSN:** la dirección de tu cuenta de Unipile (algo como `api1.unipile.com:1XXXX`). Te la da el panel.
> - **Webhook:** la dirección a la que Unipile le avisa a tu bot cada mensaje nuevo.
> - **Worker:** el programita tuyo que vive en Cloudflare y contesta. Lo armaste en [la práctica del agente](#p3-agente-preguntas).
> - **`.env`:** un archivo de tu compu donde guardás las claves. No se sube a GitHub.

## Cuánto cuesta (nov 2026)
- **Prueba gratis de 7 días**, sin tarjeta.
- Después, **49 EUR por mes (unos 55 USD) hasta 10 cuentas conectadas**. De la 11 a la 50, 5 EUR por cuenta. Cada número de WhatsApp es una cuenta.
- **Sin costo por mensaje** y sin cobro de Meta (no pasa por Meta).
- Se factura al final de cada período de 30 días, por la mayor cantidad de cuentas conectadas a la vez.

Precios oficiales, sin IVA: [unipile.com/pricing-api](https://www.unipile.com/pricing-api/).

## Pros y contras
| A favor | En contra |
|---|---|
| Se conecta en minutos, escaneando un QR. | **No oficial:** riesgo alto de bloqueo del número. |
| Sin plantillas ni ventana de 24 horas de Meta. | Si WhatsApp cambia algo, el servicio puede dejar de andar sin aviso. Meta no te da soporte. |
| Una sola API para WhatsApp, LinkedIn, Instagram y mail. | Hay que programar el puente con tu bot (Claude Code lo hace). |
| Precio fijo, sin costo por mensaje. | El mínimo es 49 EUR por mes aunque uses un solo número. |

## Antes de empezar
- [ ] Un **número secundario** con WhatsApp en un celular (un chip nuevo o uno que no uses). **Nunca** el número principal del negocio ni tu WhatsApp personal.
- [ ] El agente de [la práctica del agente](#p3-agente-preguntas) armado y publicado en Cloudflare (carpeta `agente/bot`, con `npm run probar` en 10 de 10). Si no lo tenés, hacé la variante con n8n del Paso 5.
- [ ] Claude Code abierto en la carpeta del cerebro ([Instalá Claude Code](#s2-claude-code)).
- [ ] Un mail para la prueba gratis de Unipile.

## Paso 1 · Creá tu cuenta de Unipile
1. Entrá a [dashboard.unipile.com/signup](https://dashboard.unipile.com/signup) y registrate. La prueba de 7 días no pide tarjeta.
2. Entrá al panel. Arriba vas a ver tu **DSN**: anotalo.

**Tenés que ver:** el panel de Unipile con tu DSN.

## Paso 2 · Conectá el WhatsApp secundario por QR
1. En el panel, abrí la sección **Accounts** y elegí conectar una cuenta de **WhatsApp**. Aparece un QR.
2. En el celular del número secundario, abrí WhatsApp:
   - **iPhone:** **Configuración › Dispositivos vinculados › Vincular un dispositivo**.
   - **Android:** tocá los tres puntos **⋮ › Dispositivos vinculados › Vincular un dispositivo**.
3. Apuntá la cámara al QR de la pantalla.

> **Ojo:** verificá en pantalla el nombre exacto del botón para agregar una cuenta: la documentación de Unipile no lo detalla. Si preferís no escanear, Unipile también acepta un **código de vinculación** con el número de teléfono.

**Tenés que ver:** la cuenta de WhatsApp en la lista de **Accounts**, conectada, y en el celular, Unipile entre los **Dispositivos vinculados**.

## Paso 3 · Guardá el token y el DSN en `.env`
1. Abrí [dashboard.unipile.com/access-tokens](https://dashboard.unipile.com/access-tokens) y tocá **Generate a token**. Copialo: guardalo en tu gestor de contraseñas.
2. Creá la carpeta y el archivo de claves:

<div data-os="mac">

```bash
mkdir -p ~/Documents/cerebro-[TU-EMPRESA]/agente/unipile
cd ~/Documents/cerebro-[TU-EMPRESA]/agente/unipile
touch .env
open -e .env
```

</div>
<div data-os="win">

```powershell
New-Item -ItemType Directory -Force $HOME\Documents\cerebro-[TU-EMPRESA]\agente\unipile
cd $HOME\Documents\cerebro-[TU-EMPRESA]\agente\unipile
notepad .env
```

Si el Bloc de notas pregunta si querés crear el archivo, tocá **Sí**.

</div>

3. Escribí estas dos líneas, con tus valores después del `=` (sin espacios ni comillas), guardá y cerrá:

```text
UNIPILE_DSN=[TU-DSN]
UNIPILE_API_KEY=[TU-CLAVE]
```

**Tenés que ver:** el archivo `.env` con las dos líneas completas.

## Paso 4 · Probá la conexión
Abrí Claude Code en la carpeta del cerebro:

<div data-os="mac">

```bash
cd ~/Documents/cerebro-[TU-EMPRESA]
claude
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\cerebro-[TU-EMPRESA]
claude
```

</div>

```prompt
En agente/unipile armá un script de prueba en Node.js, con el comando npm run probar-unipile, que lea UNIPILE_DSN y UNIPILE_API_KEY de agente/unipile/.env (nunca los muestres ni los escribas en el código; confirmá que .env está en el .gitignore). Antes de escribir código, leé la documentación oficial de Unipile (https://developer.unipile.com/docs/whatsapp y https://developer.unipile.com/docs/send-messages) y decime si mi cuenta usa la API v1 o v2. El script: (1) lista mis cuentas conectadas y me dice cuál es la de WhatsApp y su account_id; (2) me dice cuántos chats de WhatsApp tiene, sin mostrar nombres, teléfonos ni mensajes. El encabezado de autenticación es X-API-KEY.
```

**Tenés que ver:** el `account_id` de tu WhatsApp y la cantidad de chats. Anotá el `account_id`.

## Paso 5 · El bot mínimo
Elegí **una** de las dos variantes. Las dos usan el mismo patrón que [la práctica del agente](#p3-agente-preguntas): el mismo prompt, el mismo conocimiento y la regla de derivar.

**Variante A · Con el Worker de Cloudflare (recomendada si hiciste la práctica)**

```prompt
En agente/bot agregá al Worker una ruta /unipile para contestar WhatsApp a través de Unipile, sin romper Telegram. Antes de escribir código, leé https://developer.unipile.com/docs/new-messages-webhook, https://developer.unipile.com/docs/send-messages y https://developer.unipile.com/docs/webhooks-2.
- Seguridad: rechazá con 401 todo pedido que no traiga el encabezado Unipile-Auth igual al secreto UNIPILE_WEBHOOK_SECRET.
- Respondé 200 enseguida y procesá después (ctx.waitUntil).
- Procesá solo event "message_received" de la cuenta de WhatsApp (UNIPILE_ACCOUNT_ID). Ignorá los mensajes que mandó mi propia cuenta (cuando sender.attendee_provider_id es igual a account_info.user_id): si no, el bot se contesta a sí mismo. Ignorá los grupos.
- Evitá duplicados guardando el message_id en KV.
- Usá el mismo SYSTEM_PROMPT, la misma memoria en KV y la misma regla DERIVAR que Telegram. Los avisos de derivación siguen yendo a mi Telegram.
- Contestá en el mismo chat_id con POST https://UNIPILE_DSN/api/v1/chats/{chat_id}/messages y el texto, con el encabezado X-API-KEY (si mi cuenta usa la API v2, usá el formato de v2).
- Esperá entre 3 y 8 segundos al azar antes de contestar y no mandes más de 1 respuesta cada 5 segundos por chat.
- Si llega un audio o una foto, pedí que lo escriban.
Generá UNIPILE_WEBHOOK_SECRET al azar y guardalo en .dev.vars. Confirmá que .dev.vars está en el .gitignore. Decime qué secretos tengo que cargar con wrangler secret put (UNIPILE_DSN, UNIPILE_API_KEY, UNIPILE_ACCOUNT_ID, UNIPILE_WEBHOOK_SECRET). No me pidas claves en el chat. No publiques hasta que te diga.
```

Después, en **una segunda terminal**, entrá a `agente/bot` y cargá cada secreto con este comando, uno por vez. Cuando te pida el valor, pegalo ahí (el DSN y la clave están en `agente/unipile/.env`; el account_id lo anotaste en el Paso 4; el secreto está en `.dev.vars`):

<div data-os="mac">

```bash
cd ~/Documents/cerebro-[TU-EMPRESA]/agente/bot
npx wrangler secret put [NOMBRE-DEL-SECRETO]
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\cerebro-[TU-EMPRESA]\agente\bot
npx.cmd wrangler secret put [NOMBRE-DEL-SECRETO]
```

</div>

Corré `npm run probar` (los 10 casos tienen que seguir pasando) y publicá con `npm run deploy` (en Windows, `npm.cmd`).

**Variante B · Con n8n (sin Worker)**
Necesitás n8n conectado a Claude por MCP ([n8n](#s6-n8n), Paso 6). En Claude Code:

```prompt
Con el MCP de n8n, creá un flujo "Bot WhatsApp Unipile": (1) nodo Webhook (POST) que recibe los avisos de Unipile y responde 200 enseguida; (2) un filtro que deja pasar solo event "message_received", ignora los mensajes que mandó mi propia cuenta (sender.attendee_provider_id igual a account_info.user_id) y los grupos, y rechaza los pedidos sin el encabezado Unipile-Auth correcto; (3) un nodo de Claude (Anthropic) con Claude Haiku y, como instrucciones, el contenido de agente/prompt-del-agente.md y agente/conocimiento-publico.md; (4) un nodo HTTP Request que contesta en el mismo chat con POST https://[TU-DSN]/api/v1/chats/{chat_id}/messages y el encabezado X-API-KEY (la clave guardala como credencial de n8n, no en el flujo); (5) si la respuesta pide derivar, un aviso a mi Telegram. Leé antes https://developer.unipile.com/docs/new-messages-webhook. Dejalo sin activar y dame la URL de producción del Webhook.
```

> **Ojo:** el nodo de Claude y las credenciales de n8n se ven distinto según tu versión. Si algo no aparece, pedile a Claude que lo busque en la documentación de n8n.

**Tenés que ver:** en la variante A, la URL del Worker y `Success!` en cada secreto. En la B, el flujo creado y la URL del Webhook.

## Paso 6 · Registrá el webhook en Unipile
```prompt
Con agente/unipile/.env, registrá un webhook en Unipile con POST https://UNIPILE_DSN/api/v1/webhooks: request_url [URL-DEL-BOT], source "messaging", y en headers: Unipile-Auth con el valor de UNIPILE_WEBHOOK_SECRET de agente/bot/.dev.vars, y Content-Type con application/json. Leé los valores de los archivos sin mostrármelos. Antes, revisá en https://developer.unipile.com/docs/webhooks-2 que el formato siga igual. Al final decime el id del webhook creado.
```

Cambiá `[URL-DEL-BOT]` por `https://[TU-WORKER].workers.dev/unipile` (variante A) o por la URL del Webhook de n8n (variante B; ese secreto lo inventás vos y lo cargás también en el filtro de n8n). En la variante B, activá el flujo en n8n.

> **Tip:** también se pueden crear webhooks desde el panel de Unipile. Verificá en pantalla en qué sección están.

**Tenés que ver:** el id del webhook nuevo.

## Paso 7 · Probá desde otro celular
1. Desde otro teléfono, escribile al número secundario 3 preguntas de tus casos de prueba.
2. Pedí hablar con una persona.

**Tenés que ver:** respuestas con tu cerebro, unos segundos después de cada mensaje, y el aviso de derivación en tu Telegram.

## Riesgos y buenas prácticas (leelas antes de prenderlo)
- **Número secundario siempre.** Si lo bloquean, perdés ese número y sus chats. El bloqueo no se revierte desde Unipile.
- **Solo contestá.** El bot responde a quien te escribió. Nada de envíos masivos, bases compradas ni mensajes en frío: es la forma más rápida de que te bloqueen.
- **Número nuevo, de a poco.** Los primeros días, pocas conversaciones. No lo conectes y le mandes cien mensajes el mismo día.
- **Que parezca una persona:** respuestas cortas, con unos segundos de espera (ya está en el prompt del Paso 5) y nunca el mismo texto a muchos.
- **Celular prendido, con internet y WhatsApp actualizado.** Si se desvincula, el bot deja de contestar.
- **Plan B:** si el bot funciona y el negocio lo necesita, pasalo a la vía oficial ([Zernio](#w4-zernio), [dlastcrm](#w2-bot-dlastcrm) o la [API oficial](#w1-opciones)). El prompt y el conocimiento pasan tal cual.

> **Ojo:** estas prácticas bajan el riesgo, no lo eliminan. Los límites "seguros" que circulan en internet son observaciones de otros proveedores, no reglas de WhatsApp.

## Cómo sé que funcionó
Desde un celular que no sea el del número conectado, mandá:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario que está en tu cerebro, avisar que te pasa con alguien y mandarte el aviso a tu Telegram. Y no tiene que contestarse a sí mismo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El bot se contesta a sí mismo en loop | Falta ignorar los mensajes de tu propia cuenta (Paso 5). Pausá el webhook, pedile a Claude Code que lo arregle con una prueba y publicá de nuevo. |
| No llega nada al bot | Revisá con `npx wrangler tail` (en otra terminal) si entran pedidos. Si dice 401, el `Unipile-Auth` del webhook no coincide con `UNIPILE_WEBHOOK_SECRET`. |
| La cuenta aparece desconectada en Unipile | Revisá que el celular tenga internet y volvé a escanear el QR. |
| WhatsApp avisa que el número está restringido o bloqueado | Desconectá el bot. No lo reconectes con el mismo número: pasá a la vía oficial con otro. |
| Error al mandar la respuesta | Puede que tu cuenta use la API v2. Pedile a Claude Code que revise la documentación de envío de mensajes de esa versión. |
| En Windows: "la ejecución de scripts está deshabilitada" | Usá `npm.cmd` y `npx.cmd` en vez de `npm` y `npx`. |

## Para seguir solo
- **Antes de que termine la prueba de 7 días**, decidí: ¿pagás 49 EUR por mes o pasás a la vía oficial? Medí cuántas consultas contestó y cuántas derivó.
- **LinkedIn con la misma API:** si vendés a empresas, Unipile también conecta LinkedIn. El mismo bot puede avisarte de mensajes nuevos.
- **Cada error, un caso de prueba:** cuando el bot conteste mal, sumá esa pregunta a `agente/casos-de-prueba.md` y corré `npm run probar` antes de publicar.

## Fuentes (consultadas el 18/11/2026)
- Unipile, precios: https://www.unipile.com/pricing-api/
- Unipile, primeros pasos (DSN y token): https://developer.unipile.com/docs/getting-started
- Unipile, guía de WhatsApp: https://developer.unipile.com/docs/whatsapp
- Unipile, webhook de mensajes nuevos: https://developer.unipile.com/docs/new-messages-webhook
- Unipile, webhooks (encabezados y reintentos): https://developer.unipile.com/docs/webhooks-2
- Unipile, enviar mensajes: https://developer.unipile.com/docs/send-messages
- Términos de servicio de WhatsApp: https://www.whatsapp.com/legal/terms-of-service
