---
titulo: "Tu bot de WhatsApp con Unipile (no oficial, por QR)"
bloque: WhatsApp
tiempo: "60 a 90 min (con el agente de la práctica ya publicado, o con n8n)"
para: Quien quiere probar rápido con un número secundario, o ya usa Unipile para LinkedIn
necesitas: p3-agente-preguntas, w1-opciones
resultado: Un número secundario de WhatsApp conectado a Unipile por QR y un bot que contesta con tu cerebro, sabiendo qué riesgo corrés y cómo cuidar el número.
---

Unipile conecta WhatsApp, LinkedIn, Instagram y mail con una sola API. WhatsApp se conecta **escaneando un QR**, como WhatsApp Web: en 5 minutos, sin Meta y sin plantillas. El precio de esa velocidad: **no es oficial** y WhatsApp puede bloquear el número.
Ejemplo: La Consejera del Éxito quiere ver cómo contestaría un bot las dudas de su programa. Lo prueba una semana con un chip nuevo, no con su número de siempre.

> **Ojo:** **hoy en el taller** hacés la **Versión MVP** de [Cierre: tu bot de WhatsApp](#d7-whatsapp): las instrucciones de tu bot, probadas en Telegram con n8n. Esta página es para **después**. Todo lo técnico se lo pedís a Claude en la pestaña **Code**; las claves, nunca en el chat.

> **Ojo:** la propia web de Unipile dice que WhatsApp funciona por **ingeniería inversa**. Si WhatsApp lo detecta, **suspende el número y perdés sus chats**. Solo con un número que no te importe perder. Para tu número principal: [dlastcrm](#w2-bot-dlastcrm) oficial o [Zernio](#w4-zernio).

## Cuánto cuesta (nov 2026)
- **Prueba gratis de 7 días**, sin tarjeta.
- Después, **49 EUR por mes (unos 55 USD) hasta 10 cuentas**. Cada número es una cuenta.
- **Sin costo por mensaje** ni cobro de Meta.

Precios oficiales, sin IVA: [unipile.com/pricing-api](https://www.unipile.com/pricing-api/).

## Antes de empezar
- [ ] Un **número secundario** con WhatsApp (chip nuevo). **Nunca** el principal ni tu WhatsApp personal.
- [ ] `bot/instrucciones-del-bot.md` de [Cierre: tu bot de WhatsApp](#d7-whatsapp), o el agente de [la práctica](#p3-agente-preguntas).
- [ ] Para la variante A: el agente de [la práctica del agente](#p3-agente-preguntas) publicado en Cloudflare. Para la B: [n8n](#s6-n8n) conectado a Claude por MCP.
- [ ] La app de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).

## Paso 1 · Creá la cuenta y conectá el WhatsApp por QR
1. Registrate en [dashboard.unipile.com/signup](https://dashboard.unipile.com/signup). Anotá el **DSN** que aparece arriba (algo como `api1.unipile.com:1XXXX`).
2. En **Accounts**, elegí conectar **WhatsApp**. Aparece un QR.
3. En el celular del número secundario: **Configuración › Dispositivos vinculados › Vincular un dispositivo** (en Android, desde los tres puntos **⋮**) y apuntá al QR.

> **Ojo:** verificá en pantalla el nombre del botón para agregar una cuenta: Unipile no lo documenta.

**Tenés que ver:** la cuenta de WhatsApp conectada en **Accounts** y Unipile en los **Dispositivos vinculados** del celular.

## Paso 2 · Guardá el token sin pasarlo por el chat
1. En [dashboard.unipile.com/access-tokens](https://dashboard.unipile.com/access-tokens), **Generate a token**. Dejá la pantalla abierta.
2. En la app de Claude, tocá **Code**, elegí **Local › Open folder…** y abrí `cerebro-[TU-EMPRESA]`. Pegá:

```prompt
Creá agente/unipile/.env con las líneas UNIPILE_DSN= y UNIPILE_API_KEY= vacías, sumalo al .gitignore y abrímelo en el editor de texto de mi compu. No me pidas los valores en el chat.
```

3. Pegá el DSN y el token después de cada `=`, guardá y escribile `listo`.

**Tenés que ver:** Claude confirma que las dos líneas tienen valor, sin mostrarlos.

## Paso 3 · Probá la conexión
```prompt
Con agente/unipile/.env (sin mostrar los valores), consultá la API de Unipile con el encabezado X-API-KEY. Antes, leé https://developer.unipile.com/docs/whatsapp y decime si mi cuenta usa la API v1 o v2. Decime cuál es mi cuenta de WhatsApp y su account_id, y cuántos chats tiene, sin mostrar nombres, teléfonos ni mensajes. Guardá el account_id como UNIPILE_ACCOUNT_ID en el mismo .env.
```

**Tenés que ver:** el `account_id` de tu WhatsApp y la cantidad de chats.

## Paso 4 · El bot mínimo (elegí una variante)
**Variante A · Con el Worker de Cloudflare** (si hiciste la práctica):

```prompt
En agente/bot agregá al Worker una ruta /unipile para contestar WhatsApp a través de Unipile, sin romper Telegram. Antes, leé https://developer.unipile.com/docs/new-messages-webhook, https://developer.unipile.com/docs/send-messages y https://developer.unipile.com/docs/webhooks-2.
- Rechazá con 401 todo pedido sin el encabezado Unipile-Auth igual a UNIPILE_WEBHOOK_SECRET. Respondé 200 enseguida y procesá después.
- Solo event "message_received" de UNIPILE_ACCOUNT_ID. Ignorá mis propios mensajes (sender.attendee_provider_id igual a account_info.user_id), los grupos y los duplicados (message_id en KV).
- Mismo SYSTEM_PROMPT, memoria en KV y regla DERIVAR que Telegram; avisos a mi Telegram.
- Contestá en el mismo chat_id con la API de mensajes de Unipile (v1 o v2, según mi cuenta), esperando 3 a 8 segundos al azar y no más de 1 respuesta cada 5 segundos por chat. Si llega audio o foto, pedí que lo escriban.
Generá UNIPILE_WEBHOOK_SECRET al azar en .dev.vars y copiá UNIPILE_DSN, UNIPILE_API_KEY y UNIPILE_ACCOUNT_ID desde agente/unipile/.env, sin mostrarme nada. Corré npm run probar (10 de 10), cargá los secretos en Cloudflare y publicá. Dame la URL que termina en /unipile.
```

**Variante B · Con n8n** (sin Worker):

```prompt
Con el MCP de n8n, creá el flujo "Bot WhatsApp Unipile": Webhook (POST) que responde 200 enseguida; filtro que deja pasar solo "message_received", ignora mis propios mensajes y los grupos, y rechaza pedidos sin el encabezado Unipile-Auth correcto; nodo de Claude (Anthropic) con Claude Haiku y, como instrucciones, bot/instrucciones-del-bot.md; HTTP Request que contesta en el mismo chat con la API de mensajes de Unipile; y aviso a mi Telegram si hay que derivar. La clave de Unipile, como credencial de n8n: creá un archivo temporal con la línea vacía y abrímelo en el editor, nunca me la pidas en el chat. Leé antes https://developer.unipile.com/docs/new-messages-webhook. Dejalo sin activar y dame la URL de producción del Webhook.
```

> **Ojo:** el nodo de Claude y las credenciales de n8n se ven distinto según la versión. Si algo no aparece, pedile a Claude que lo busque en la documentación de n8n.

**Tenés que ver:** en A, la URL del Worker y los secretos cargados. En B, el flujo creado y la URL del Webhook.

## Paso 5 · Registrá el webhook en Unipile y probalo
```prompt
Registrá un webhook en Unipile (source "messaging") con request_url [URL-DEL-BOT] y los encabezados Unipile-Auth (el valor de UNIPILE_WEBHOOK_SECRET) y Content-Type application/json. Leé los valores de los archivos sin mostrármelos y revisá antes https://developer.unipile.com/docs/webhooks-2. Decime el id del webhook. Si es la variante de n8n, activá el flujo.
```

Cambiá `[URL-DEL-BOT]` por la URL del Paso 4. Después, desde otro teléfono, escribile al número secundario 3 preguntas de tus casos y pedí hablar con una persona.

**Tenés que ver:** respuestas con tu cerebro, unos segundos después, y el aviso de derivación en tu Telegram.

## Cómo cuidar el número
- **Número secundario siempre.** El bloqueo no se revierte desde Unipile.
- **Solo contestá** a quien te escribió. Nada de envíos masivos, bases compradas ni mensajes en frío.
- **De a poco:** pocas conversaciones los primeros días.
- **Celular prendido, con internet y WhatsApp actualizado.**
- **Plan B:** si el bot sirve, pasalo a la vía oficial ([Zernio](#w4-zernio), [dlastcrm](#w2-bot-dlastcrm) o la [API oficial](#w1-opciones)). Las instrucciones pasan tal cual.

> **Ojo:** esto baja el riesgo, no lo elimina.

## Cómo sé que funcionó
Desde un celular que no sea el conectado:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario de tu cerebro, avisar que te pasa con alguien, mandarte el aviso a Telegram y **no** contestarse a sí mismo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El bot se contesta a sí mismo | Pedile a Claude que pause el webhook, arregle el filtro de mensajes propios con una prueba y publique de nuevo. |
| No llega nada al bot | Pedile a Claude que mire los registros del Worker (wrangler tail). Si dice 401, el `Unipile-Auth` no coincide. |
| La cuenta aparece desconectada | Revisá internet en el celular y volvé a escanear el QR. |
| WhatsApp avisa que el número está restringido | Desconectá el bot. No reconectes ese número: pasá a la vía oficial con otro. |
| Error al mandar la respuesta | Puede que tu cuenta use la API v2: pedile a Claude que revise esa versión. |

## Para seguir solo
- **Antes de que termine la prueba de 7 días**, decidí: ¿49 EUR por mes o vía oficial? Medí cuántas consultas contestó y cuántas derivó.
- **LinkedIn con la misma API:** si vendés a empresas, el mismo bot puede avisarte de mensajes nuevos.
- **Cada error, un caso de prueba:** sumalo a tus casos y pedile a Claude que corra las pruebas antes de publicar.

## Fuentes (consultadas el 18/11/2026)
- Unipile: https://www.unipile.com/pricing-api/ · https://developer.unipile.com/docs/getting-started · https://developer.unipile.com/docs/whatsapp · https://developer.unipile.com/docs/new-messages-webhook · https://developer.unipile.com/docs/webhooks-2 · https://developer.unipile.com/docs/send-messages
- Términos de WhatsApp: https://www.whatsapp.com/legal/terms-of-service
