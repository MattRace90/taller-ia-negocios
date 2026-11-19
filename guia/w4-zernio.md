---
titulo: "Tu bot de WhatsApp con Zernio (vía oficial)"
bloque: WhatsApp
tiempo: "60 min con el número de prueba de Zernio. Conectar tu número real: 30 min más las verificaciones de Meta"
para: Quien ya publica en redes o quiere WhatsApp oficial sin armar la API de Meta a mano (por ejemplo, Viajes TDH Docta y Celve)
necesitas: p1-cerebro, s2-claude-code, w1-opciones
resultado: Zernio conectado a Claude Code, un bot que contesta con tu cerebro probado en el número de prueba de Zernio, y los pasos para pasar tu número real por la vía oficial de Meta.
---

Zernio es un servicio que conecta muchas redes (Instagram, Facebook, WhatsApp y más) con una sola API y un MCP. Para WhatsApp usa la **vía oficial de Meta**, así que no te bloquean el número por usar un bot. Hoy lo conectás a Claude Code y armás un bot que contesta con tu cerebro, probándolo gratis con el número de prueba de Zernio.
Ejemplo: Viajes TDH Docta recibe "¿tienen salidas a Bariloche en julio?" a las 23 h. El bot contesta con lo que dice el cerebro, pide fecha y cantidad de personas, y avisa a la vendedora a la mañana.

> **Tip:** palabras que vas a ver en esta página:
> - **API:** la puerta para que un programa hable con otro. **Clave de API:** la contraseña de esa puerta. Empieza con `sk_`.
> - **MCP:** el enchufe para que Claude use otra app ([Las piezas](#t2-piezas)).
> - **Sandbox (número de prueba):** un número de WhatsApp de Zernio, compartido y gratis, que solo le escribe a tu celular durante 7 días.
> - **Webhook:** la dirección a la que Zernio le avisa a tu bot cada mensaje nuevo.
> - **Worker:** el programita tuyo que vive en Cloudflare y contesta los mensajes. Lo armaste en [la práctica del agente](#p3-agente-preguntas).
> - **Alta guiada de Meta (Embedded Signup):** la ventana de Meta donde elegís tu negocio y tu número para conectarlos por la vía oficial.

> **Datos:** el bot contesta con lo que está en tu cerebro. Nunca pegues claves en el chat de Claude y no copies conversaciones con nombres o teléfonos de clientes en tus pruebas.

## Cuánto cuesta (nov 2026)
- **Cuentas:** las 2 primeras cuentas conectadas, gratis y sin tarjeta. De la 3 a la 10, 6 USD por mes cada una. Cada red conectada (tu WhatsApp, tu Instagram) cuenta como una cuenta.
- **Mensajes:** los primeros 10.000 mensajes enviados por mes, gratis. Después, 1 USD cada 10.000. Los que recibís son gratis.
- **Meta cobra aparte:** las plantillas (mensajes fuera de las 24 horas) las cobra Meta directo a tu cuenta de WhatsApp Business. Desde el 1/10/2026, Meta también cobra los mensajes de servicio después de los primeros 1.000 por número y por mes ([cómo se cobra](#w1-opciones)).
- **Números:** si comprás un número en Zernio, desde 3 USD por mes según el país. Podés usar tu propio número y no pagar esto.
- **El número de prueba (sandbox):** gratis.

Precios oficiales: [zernio.com/pricing](https://zernio.com/pricing). Sin impuestos, en dólares.

## Pros y contras
| A favor | En contra |
|---|---|
| Vía oficial de Meta: riesgo de bloqueo bajo. | Dependés de un intermediario: si Zernio cambia precios o se cae, te afecta. |
| Más simple que armar la API de Meta a mano: el alta con Meta la guía Zernio. | No acepta un WhatsApp personal: necesitás una cuenta de WhatsApp Business dentro de un portfolio de Meta. |
| Tiene MCP: Claude Code puede leer y contestar la bandeja. | El bot automático lo armás vos (con Claude Code). |
| Plan gratis para empezar y número de prueba sin trámites. | La documentación está en inglés. |
| Además de WhatsApp, publica y mide en tus redes. | Si usás "coexistencia" (app y API a la vez), se apagan los grupos y las llamadas por la API. |

## Antes de empezar
- [ ] Tu cerebro armado ([Armá el cerebro](#p1-cerebro)) y, si lo hiciste, las instrucciones del bot de [Cierre: tu bot de WhatsApp](#d7-whatsapp) en `bot/instrucciones-del-bot.md`.
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] Un celular con WhatsApp para recibir los mensajes de prueba.
- [ ] Solo para el bot automático (Paso 6): el agente de [la práctica del agente](#p3-agente-preguntas) publicado en Cloudflare.
- [ ] Solo para tu número real (Paso 9): acceso de administrador a tu portfolio en [business.facebook.com](https://business.facebook.com) ([Meta y Google](#s14-meta-y-google)) y una tarjeta para cargar en Meta.

## Paso 1 · Creá tu cuenta de Zernio
1. Entrá a [zernio.com](https://zernio.com) y tocá el botón para registrarte.
2. Creá la cuenta con tu mail del negocio.
3. Entrá al panel.

> **Ojo:** verificá en pantalla el nombre exacto del botón de registro y de los menús: la web está en inglés y cambia seguido.

**Tenés que ver:** el panel de Zernio con el menú **Connections** (conexiones).

## Paso 2 · Creá tu clave de API
1. Abrí [zernio.com/dashboard/api-keys](https://zernio.com/dashboard/api-keys).
2. Tocá **Create API key**.
3. Copiá la clave **ahora**: empieza con `sk_` y no se vuelve a mostrar. Guardala en tu gestor de contraseñas o en una nota privada.

> **Ojo:** la clave es como la llave de tu WhatsApp. No se la pegues a Claude en el chat ni la subas a GitHub. En el próximo paso la ponés vos en un archivo.

**Tenés que ver:** la clave nueva en la lista de **API keys** (solo se ve el principio).

## Paso 3 · Probá con el número de prueba de Zernio (gratis)
Zernio tiene un número de WhatsApp compartido para probar sin Meta, sin comprar nada y sin pagar. Le escribe solo a tu celular, hasta 50 mensajes por día, durante 7 días.

1. Abrí la terminal (en Mac, **Terminal**; en Windows, **PowerShell**; si no sabés cómo, mirá el Paso 1 de [Instalá Claude Code](#s2-claude-code)), creá la carpeta y abrí el archivo de claves:

<div data-os="mac">

```bash
mkdir -p ~/Documents/cerebro-[TU-EMPRESA]/agente/zernio
cd ~/Documents/cerebro-[TU-EMPRESA]/agente/zernio
touch .env
open -e .env
```

</div>
<div data-os="win">

```powershell
New-Item -ItemType Directory -Force $HOME\Documents\cerebro-[TU-EMPRESA]\agente\zernio
cd $HOME\Documents\cerebro-[TU-EMPRESA]\agente\zernio
notepad .env
```

En Windows, si el Bloc de notas pregunta si querés crear el archivo, tocá **Sí**.

</div>

2. Escribí esta línea, pegá tu clave después del `=` (sin espacios ni comillas), guardá y cerrá:

```text
ZERNIO_API_KEY=[TU-CLAVE]
```

3. Abrí Claude Code en la carpeta del cerebro:

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

4. Pegá este prompt. Cambiá `[TU-CELULAR]` por tu número con código de país y sin espacios. En Argentina, con el 9: `+549351XXXXXXX`.

```prompt
En agente/zernio armá una prueba de WhatsApp con el número de prueba (sandbox) de Zernio. Antes de escribir código, leé https://docs.zernio.com/platforms/whatsapp/sandbox.mdx y seguilo.
1. Usá Node.js y el SDK oficial @zernio/node. La clave está en agente/zernio/.env como ZERNIO_API_KEY: leela de ahí, nunca la muestres ni la escribas en el código. Confirmá que .env está en el .gitignore.
2. Un comando npm run sandbox que: busque el número de prueba con GET /v1/phone-numbers, abra una sesión para mi celular [TU-CELULAR] con POST /v1/whatsapp/sandbox/sessions y me diga que conteste el WhatsApp que me llega.
3. Un comando npm run sandbox-estado que me diga si la sesión ya está activa.
4. Un comando npm run sandbox-enviar que, con la sesión activa, me mande la plantilla de prueba con POST /v1/inbox/conversations.
Explicame cada respuesta de Zernio en castellano. Si algo da error, pará y preguntame.
```

5. Corré `npm run sandbox` (te lo indica Claude), contestá el WhatsApp que te llega con cualquier texto, corré `npm run sandbox-estado` y después `npm run sandbox-enviar`.

> **Tip:** en Windows, si `npm` da "la ejecución de scripts está deshabilitada", usá `npm.cmd` (ej.: `npm.cmd run sandbox`).

**Tenés que ver:** un WhatsApp desde el número de prueba de Zernio en tu celular, y `sandbox-estado` diciendo que la sesión está **active**.

## Paso 4 · Conectá Zernio a Claude Code por MCP
Con el MCP, Claude Code puede leer tus cuentas y tu bandeja de Zernio conversando, sin código.

1. Salí de Claude Code con `/exit`. En la misma terminal, pegá (igual en Mac y Windows):

```bash
claude mcp add --transport http zernio https://mcp.zernio.com/mcp
```

2. Abrí Claude Code de nuevo con `claude`, escribí `/mcp`, elegí **zernio** e iniciá sesión con tu cuenta de Zernio en el navegador que se abre.
3. Preguntale:

```prompt
¿Qué cuentas tengo conectadas en Zernio? Y decime qué herramientas del MCP de Zernio sirven para leer y contestar conversaciones de WhatsApp.
```

> **Ojo:** la documentación de Zernio no publica la lista de herramientas de WhatsApp del MCP. Usá la respuesta de este prompt para ver cuáles hay en tu cuenta antes de armar algo encima.

**Tenés que ver:** en `/mcp`, **zernio** como conectado, y Claude te lista tus cuentas y las herramientas de la bandeja.

## Paso 5 · Modo asistido: Claude propone, vos aprobás
La forma más segura de empezar: Claude lee las conversaciones nuevas, escribe la respuesta con tu cerebro y **solo la manda si le decís que sí**. Ideal para la primera semana.

1. Mandale un WhatsApp al número de prueba desde tu celular, como si fueras un cliente (por ejemplo: "hola, ¿qué horario tienen?").
2. Pegá en Claude Code:

```prompt
Sos el asistente de atención de mi empresa por WhatsApp. Leé bot/instrucciones-del-bot.md (si no existe, agente/prompt-del-agente.md y agente/conocimiento-publico.md). Con el MCP de Zernio, buscá las conversaciones de WhatsApp que esperan respuesta. Para cada una, mostrame el último mensaje del cliente y la respuesta que proponés, escrita SOLO con lo que dicen esos archivos. Si no está en mi cerebro, proponé derivar a una persona. No mandes nada hasta que yo te diga "mandala". Fuera de las 24 horas desde el último mensaje del cliente, avisame que solo se puede mandar una plantilla.
```

**Tenés que ver:** la respuesta propuesta. Cuando escribís "mandala", te llega a tu celular.

## Paso 6 · Modo automático: el bot contesta solo (con el Worker de la práctica)
Ahora el mismo agente de Telegram de [la práctica del agente](#p3-agente-preguntas) contesta también los WhatsApp de Zernio. Zernio le avisa al Worker cada mensaje nuevo (webhook) y el Worker contesta por la API.

1. En Claude Code, pegá:

```prompt
En agente/bot agregá al Worker una ruta /zernio para contestar WhatsApp a través de Zernio, sin romper Telegram. Antes de escribir código, leé https://docs.zernio.com/webhooks/inbox/message-received.mdx, https://docs.zernio.com/webhooks.mdx y https://docs.zernio.com/platforms/whatsapp/inbox.mdx.
- Verificá la firma: el encabezado X-Zernio-Signature es el HMAC-SHA256 en hexadecimal del cuerpo crudo, con el secreto ZERNIO_WEBHOOK_SECRET. Si no coincide, respondé 401.
- Respondé 200 enseguida y procesá después (ctx.waitUntil).
- Ignorá todo lo que no sea event "message.received", platform "whatsapp" y direction "incoming". Ignorá los mensajes con metadata.standby en true.
- Evitá duplicados guardando el id del evento en KV.
- Usá el mismo SYSTEM_PROMPT, la misma memoria en KV y la misma regla DERIVAR que Telegram. Los avisos de derivación siguen yendo a mi Telegram.
- Contestá con POST https://zernio.com/api/v1/inbox/conversations/{conversationId}/messages, con el accountId de la conversación y el texto, y el encabezado Authorization: Bearer ZERNIO_API_KEY.
- Si llega un audio o una foto, pedí que lo escriban.
Generá ZERNIO_WEBHOOK_SECRET al azar y guardalo en .dev.vars. Confirmá que .dev.vars está en el .gitignore. Decime qué secretos tengo que cargar con wrangler secret put. No me pidas que te pegue claves en el chat. No publiques hasta que te diga.
```

2. Abrí **una segunda terminal**, entrá a la carpeta del bot y cargá los dos secretos, uno por vez. Cuando te pida el valor, pegá tu clave de Zernio (Paso 2) y después el secreto que está en tu `.dev.vars`:

<div data-os="mac">

```bash
cd ~/Documents/cerebro-[TU-EMPRESA]/agente/bot
npx wrangler secret put ZERNIO_API_KEY
npx wrangler secret put ZERNIO_WEBHOOK_SECRET
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\cerebro-[TU-EMPRESA]\agente\bot
npx.cmd wrangler secret put ZERNIO_API_KEY
npx.cmd wrangler secret put ZERNIO_WEBHOOK_SECRET
```

</div>

3. Corré `npm run probar` (los 10 casos de Telegram tienen que seguir pasando) y publicá con `npm run deploy` (en Windows, `npm.cmd`).

**Tenés que ver:** `Success!` después de cada secreto y la URL del Worker, la que termina en `.workers.dev`.

## Paso 7 · Registrá el webhook en Zernio
Le decís a Zernio a qué dirección avisar cada mensaje nuevo.

1. Abrí [zernio.com/dashboard/webhooks](https://zernio.com/dashboard/webhooks) y creá un webhook nuevo.
2. Completá:
   - **Nombre:** `Bot WhatsApp`.
   - **URL:** `https://[TU-WORKER].workers.dev/zernio` (`[TU-WORKER]` sale de la dirección del Paso 6).
   - **Eventos:** `message.received`.
   - **Secreto:** el mismo valor de `ZERNIO_WEBHOOK_SECRET` que está en tu `.dev.vars`.
3. Guardá.

> **Ojo:** verificá los nombres de los campos en pantalla: la documentación de Zernio no los detalla. Si no lo encontrás, pedile a Claude Code: "Registrá el webhook con POST /v1/webhooks/settings (name, url, events y secret, leyendo los valores de los archivos sin mostrármelos) y mandá una prueba con POST /v1/webhooks/test".

**Tenés que ver:** el webhook en la lista, con el evento `message.received`.

## Paso 8 · Probá el bot automático
1. Desde tu celular, escribile al número de prueba de Zernio (la sesión dura 7 días: si venció, corré `npm run sandbox` de nuevo).
2. Hacé 3 preguntas de tus casos de prueba y pedí hablar con una persona.

**Tenés que ver:** el bot te contesta solo, con tu cerebro, y te llega a Telegram el aviso de derivación.

## Paso 9 · Conectá tu número real (alta con Meta)
Cuando el bot pasó las pruebas, conectás el número del negocio por la vía oficial. Zernio abre la ventana de Meta y te guía.

1. En el panel de Zernio, andá a **Connections**, abrí la tarjeta **WhatsApp** y tocá **+ Connect**.
2. Elegí **Use my own number** (usar mi número). Si preferís uno nuevo, **Get a new number** te muestra el precio por país antes de confirmar.
3. Tocá **Continue to WhatsApp setup**. Se abre el alta guiada de Meta: iniciá sesión con tu Facebook, elegí tu portfolio del negocio y creá o elegí la cuenta de WhatsApp Business.
4. Elegí cómo conectar el número:
   - **Solo API (recomendado para un número nuevo):** el número no puede estar en la app de WhatsApp. No elijas "Connect existing WhatsApp Business app account".
   - **Coexistencia (seguís usando la app WhatsApp Business en el celular):** elegí **Connect existing WhatsApp Business app account**. Meta muestra un QR. En la app WhatsApp Business, andá a **Configuración › Dispositivos vinculados** y escanealo. Funciona solo con la app **WhatsApp Business**, no con el WhatsApp común.
5. Cargá un método de pago en Meta para los mensajes que cobra (en Argentina se puede en pesos).
6. Tu webhook del Paso 7 ya escucha todas tus cuentas: el bot contesta también en el número real.

> **Ojo:** verificá en pantalla los pasos de Meta (código de verificación por SMS o llamada, nombre visible del negocio): Meta los cambia seguido. Cada perfil de Zernio admite un solo número de WhatsApp.

**Tenés que ver:** en **Connections**, tu WhatsApp como **connected**.

## Cómo sé que funcionó
Desde un celular que no sea el del negocio, mandale este WhatsApp al número conectado:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario que está en tu cerebro (no uno inventado), avisar que te pasa con alguien y mandarte el aviso a tu Telegram.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El Worker responde 401 y no contesta | El secreto del webhook en Zernio no es idéntico a `ZERNIO_WEBHOOK_SECRET`. Copialo de nuevo y volvé a cargarlo con `npx wrangler secret put ZERNIO_WEBHOOK_SECRET`. |
| El bot se contesta a sí mismo en loop | Falta ignorar los mensajes con direction "outgoing". Pedile a Claude Code que lo agregue con una prueba. |
| El número de prueba dejó de contestarte | La sesión dura 7 días y 50 mensajes por día. Corré `npm run sandbox` de nuevo al otro día. |
| Al conectar sale `one_whatsapp_per_profile` | Ese perfil ya tiene un WhatsApp. Conectalo en otro perfil de Zernio. |
| Los mensajes fallan con `(#200) You do not have the necessary permission` | Meta rechazó el PIN de verificación en dos pasos del número. Registralo de nuevo con el PIN, como explica la [documentación de Zernio](https://docs.zernio.com/platforms/whatsapp/connect). |
| No le llega la respuesta a alguien que escribió hace días | Pasaron más de 24 horas: solo se le puede mandar una plantilla aprobada por Meta. |
| En Windows: "la ejecución de scripts está deshabilitada" | Usá `npm.cmd` y `npx.cmd` en vez de `npm` y `npx`. |

## Para seguir solo
- **Una semana en modo asistido** antes de prenderlo solo: así ves qué contesta mal sin que lo vea un cliente.
- **Sumá Instagram y Facebook:** el mismo webhook recibe los mensajes de las redes que conectes. Pedile a Claude Code que acepte también platform "instagram" en la ruta `/zernio`.
- **Publicá desde Claude:** con el mismo MCP podés programar posteos ("programá este post en Instagram para el viernes a las 19"). Mirá qué más se puede en la [guía del MCP](https://docs.zernio.com/mcp).

## Fuentes (consultadas el 18/11/2026)
- Zernio, precios: https://zernio.com/pricing
- Zernio, inicio rápido y clave de API: https://docs.zernio.com/quickstart
- Zernio, número de prueba de WhatsApp: https://docs.zernio.com/platforms/whatsapp/sandbox
- Zernio, conectar WhatsApp: https://docs.zernio.com/platforms/whatsapp/connect
- Zernio, bandeja de WhatsApp: https://docs.zernio.com/platforms/whatsapp/inbox
- Zernio, webhooks y evento message.received: https://docs.zernio.com/webhooks · https://docs.zernio.com/webhooks/inbox/message-received
- Zernio, MCP: https://docs.zernio.com/mcp
