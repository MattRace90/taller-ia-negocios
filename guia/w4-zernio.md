---
titulo: "Tu bot de WhatsApp con Zernio (vía oficial)"
bloque: WhatsApp
tiempo: "60 min con el número de prueba de Zernio. Tu número real: 30 min más las verificaciones de Meta"
para: Quien ya publica en redes o quiere WhatsApp oficial sin armar la API de Meta a mano (por ejemplo, Viajes TDH Docta y Celve)
necesitas: p1-cerebro, s2-claude-code, w1-opciones
resultado: Zernio conectado a Claude, un bot que contesta con tu cerebro probado en el número de prueba de Zernio, y los pasos para pasar tu número real por la vía oficial de Meta.
---

Zernio conecta muchas redes (Instagram, Facebook, WhatsApp y más) con una sola API y un MCP. Para WhatsApp usa la **vía oficial de Meta**: no te bloquean el número por usar un bot. Lo conectás a Claude y probás tu bot gratis con su número de prueba.
Ejemplo: Viajes TDH Docta recibe "¿tienen salidas a Bariloche en julio?" a las 23 h. El bot contesta con el cerebro, pide fecha y cantidad de personas, y avisa a la vendedora.

> **Ojo:** **hoy en el taller** hacés la **Versión MVP** de [Cierre: tu bot de WhatsApp](#d7-whatsapp): las instrucciones de tu bot, probadas en Telegram con n8n. Esta página es para **después**. Todo lo técnico se lo pedís a Claude en la pestaña **Code**; las claves, nunca en el chat.

## Cuánto cuesta (nov 2026)
- **Cuentas:** las 2 primeras gratis, sin tarjeta. De la 3 a la 10, 6 USD por mes cada una (cada red conectada cuenta como una).
- **Mensajes:** 10.000 enviados por mes gratis; después, 1 USD cada 10.000. Los recibidos, gratis.
- **Meta cobra aparte** las plantillas y, desde el 1/10/2026, los mensajes de servicio pasados los 1.000 por mes ([cómo se cobra](#w1-opciones)).
- **Número de prueba:** gratis. Precios oficiales: [zernio.com/pricing](https://zernio.com/pricing).

| A favor | En contra |
|---|---|
| Vía oficial: riesgo de bloqueo bajo. | Dependés de un intermediario. |
| El alta con Meta la guía Zernio. | No acepta un WhatsApp personal. |
| Tiene MCP: Claude lee y contesta la bandeja. | El bot automático lo armás vos (con Claude). |
| Plan gratis y número de prueba sin trámites. | Documentación en inglés. |

## Antes de empezar
- [ ] `bot/instrucciones-del-bot.md` de [Cierre: tu bot de WhatsApp](#d7-whatsapp), o tu cerebro ([Armá el cerebro](#p1-cerebro)).
- [ ] La app de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).
- [ ] Un celular con WhatsApp para recibir las pruebas.
- [ ] Solo para el modo automático (Paso 5): el agente de [la práctica del agente](#p3-agente-preguntas) publicado en Cloudflare.
- [ ] Solo para tu número real (Paso 7): acceso de administrador a tu portfolio en [business.facebook.com](https://business.facebook.com) ([Meta y Google](#s14-meta-y-google)) y una tarjeta para Meta.

## Paso 1 · Creá la cuenta y la clave de API
1. Registrate en [zernio.com](https://zernio.com) con el mail del negocio.
2. Abrí [zernio.com/dashboard/api-keys](https://zernio.com/dashboard/api-keys) › **Create API key**. Dejá la pantalla abierta: la clave (empieza con `sk_`) se ve una sola vez.
3. En la app de Claude, tocá **Code**, elegí **Local › Open folder…** y abrí `cerebro-[TU-EMPRESA]`. Pegá:

```prompt
Creá el archivo agente/zernio/.env con la línea ZERNIO_API_KEY= vacía, sumalo al .gitignore y abrímelo en el editor de texto de mi compu. No me pidas la clave en el chat.
```

4. Pegá la clave después del `=` (sin espacios), guardá y escribile a Claude `listo`.

> **Ojo:** verificá en pantalla los nombres de los botones de Zernio: la web está en inglés y cambia seguido.

**Tenés que ver:** Claude confirma que la línea tiene valor, sin mostrarlo.

## Paso 2 · Probá con el número de prueba (gratis)
El número de prueba de Zernio le escribe solo a tu celular, hasta 50 mensajes por día, durante 7 días. Cambiá `[TU-CELULAR]` (en Argentina, con el 9: `+549351XXXXXXX`):

```prompt
En agente/zernio armá una prueba con el número de prueba (sandbox) de WhatsApp de Zernio. Antes, leé https://docs.zernio.com/platforms/whatsapp/sandbox.mdx. Usá Node.js y el SDK oficial @zernio/node, con la clave de agente/zernio/.env (nunca la muestres). Abrí una sesión para mi celular [TU-CELULAR] y avisame que conteste el WhatsApp que me llega. Cuando te diga "contesté", revisá que la sesión esté activa y mandame la plantilla de prueba. Explicame cada respuesta de Zernio en castellano. Si algo da error, pará y preguntame.
```

**Tenés que ver:** un WhatsApp del número de prueba en tu celular y la sesión **active**.

## Paso 3 · Conectá Zernio a Claude por MCP
1. Pegá:

```prompt
Agregá el MCP de Zernio a mi Claude Code para todos mis proyectos: claude mcp add --transport http --scope user zernio https://mcp.zernio.com/mcp. Decime qué salió, en simple.
```

2. Abrí una conversación nueva, escribí `/mcp`, elegí **zernio** e iniciá sesión con tu cuenta de Zernio en el navegador.
3. Preguntá: `¿Qué cuentas tengo en Zernio y qué herramientas del MCP sirven para leer y contestar WhatsApp?`

> **Ojo:** Zernio no publica la lista de herramientas de WhatsApp del MCP. Usá esta respuesta para ver cuáles hay en tu cuenta.

**Tenés que ver:** **zernio** conectado en `/mcp` y la lista de tus cuentas.

## Paso 4 · Modo asistido: Claude propone, vos aprobás
La forma más segura de empezar. Mandale un WhatsApp al número de prueba como si fueras un cliente y pegá:

```prompt
Sos el asistente de atención de mi empresa por WhatsApp. Leé bot/instrucciones-del-bot.md. Con el MCP de Zernio, buscá las conversaciones de WhatsApp que esperan respuesta. Para cada una, mostrame el último mensaje y la respuesta que proponés, SOLO con lo que dice ese archivo; si no está, proponé derivar a una persona. No mandes nada hasta que te diga "mandala". Si pasaron más de 24 horas, avisame que solo se puede mandar una plantilla.
```

**Tenés que ver:** la respuesta propuesta y, cuando escribís "mandala", el mensaje en tu celular.

## Paso 5 · Modo automático: el bot contesta solo
El agente de [la práctica del agente](#p3-agente-preguntas) contesta también los WhatsApp de Zernio.

```prompt
En agente/bot agregá al Worker una ruta /zernio para contestar WhatsApp a través de Zernio, sin romper Telegram. Antes, leé https://docs.zernio.com/webhooks/inbox/message-received.mdx, https://docs.zernio.com/webhooks.mdx y https://docs.zernio.com/platforms/whatsapp/inbox.mdx.
- Verificá la firma X-Zernio-Signature (HMAC-SHA256 del cuerpo con ZERNIO_WEBHOOK_SECRET); si no coincide, 401.
- Respondé 200 enseguida y procesá después. Solo "message.received", platform "whatsapp", direction "incoming"; ignorá metadata.standby en true y los duplicados (id en KV).
- Mismo SYSTEM_PROMPT, memoria en KV y regla DERIVAR que Telegram; los avisos siguen yendo a mi Telegram.
- Contestá con POST https://zernio.com/api/v1/inbox/conversations/{conversationId}/messages y Authorization: Bearer ZERNIO_API_KEY. Si llega audio o foto, pedí que lo escriban.
Generá ZERNIO_WEBHOOK_SECRET al azar en .dev.vars y copiá ZERNIO_API_KEY desde agente/zernio/.env, sin mostrarme ninguno. Corré npm run probar (10 de 10), cargá los dos secretos en Cloudflare y publicá. Al final dame la URL que termina en /zernio.
```

**Tenés que ver:** las pruebas en 10 de 10, los secretos cargados y la URL del Worker.

## Paso 6 · Registrá el webhook y probalo
```prompt
Registrá en Zernio un webhook llamado "Bot WhatsApp" con la URL de mi Worker terminada en /zernio, el evento message.received y como secreto el valor de ZERNIO_WEBHOOK_SECRET de .dev.vars (POST /v1/webhooks/settings), leyendo los valores de los archivos sin mostrármelos. Después mandá una prueba con POST /v1/webhooks/test y decime qué pasó.
```

Después, desde tu celular, hacele al número de prueba 3 preguntas de tus casos y pedí hablar con una persona.

**Tenés que ver:** el bot contesta solo, con tu cerebro, y el aviso de derivación llega a tu Telegram.

## Paso 7 · Conectá tu número real (alta con Meta)
1. En Zernio, **Connections** › tarjeta **WhatsApp** › **+ Connect** › **Use my own number** › **Continue to WhatsApp setup**.
2. En la ventana de Meta: iniciá sesión, elegí tu portfolio y la cuenta de WhatsApp Business.
3. Elegí cómo: **solo API** (número nuevo, que no esté en la app) o **coexistencia** (**Connect existing WhatsApp Business app account**, escaneás un QR desde la app WhatsApp Business: seguís usándola en el celular).
4. Cargá un método de pago en Meta (se puede en pesos). Tu webhook ya escucha todas tus cuentas.

> **Ojo:** los pasos de Meta cambian seguido: verificalos en pantalla. Cada perfil de Zernio admite un solo número de WhatsApp.

**Tenés que ver:** tu WhatsApp como **connected** en **Connections**.

## Cómo sé que funcionó
Desde un celular que no sea el del negocio, mandale al número conectado:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario de tu cerebro, avisar que te pasa con alguien y mandarte el aviso a Telegram.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El Worker responde 401 | El secreto del webhook no coincide. Pedile a Claude que lo vuelva a registrar desde `.dev.vars`. |
| El bot se contesta a sí mismo | Falta ignorar direction "outgoing". Pedile a Claude que lo agregue con una prueba. |
| El número de prueba dejó de contestar | La sesión dura 7 días y 50 mensajes por día. Pedile a Claude que abra una sesión nueva. |
| Sale `one_whatsapp_per_profile` | Ese perfil ya tiene un WhatsApp: usá otro perfil de Zernio. |
| Error `(#200) You do not have the necessary permission` | Meta rechazó el PIN de verificación en dos pasos. Mirá la [documentación de Zernio](https://docs.zernio.com/platforms/whatsapp/connect). |

## Para seguir solo
- **Una semana en modo asistido** antes de prenderlo solo.
- **Sumá Instagram y Facebook:** pedile a Claude que la ruta `/zernio` acepte también platform "instagram".
- **Publicá desde Claude:** con el mismo MCP, "programá este post en Instagram para el viernes a las 19" ([guía del MCP](https://docs.zernio.com/mcp)).

## Fuentes (consultadas el 18/11/2026)
- Zernio: https://zernio.com/pricing · https://docs.zernio.com/quickstart · https://docs.zernio.com/platforms/whatsapp/sandbox · https://docs.zernio.com/platforms/whatsapp/connect · https://docs.zernio.com/platforms/whatsapp/inbox · https://docs.zernio.com/webhooks · https://docs.zernio.com/mcp
