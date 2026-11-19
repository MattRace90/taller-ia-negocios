---
titulo: "Bots de WhatsApp: qué camino te conviene"
bloque: WhatsApp
tiempo: 20 min de lectura (la Cloud API directa, si la armás, lleva 1 a 2 horas más)
para: Todos (cierre del taller)
necesitas: d7-whatsapp
resultado: Sabés qué camino te conviene para tener un bot de WhatsApp, cuánto cuesta, qué riesgo corrés con cada uno y cuál es el primer paso.
---

Tus clientes están en WhatsApp. Hoy armaste el agente en Telegram porque WhatsApp no se arma en una hora: pide un número dedicado, plantillas aprobadas por Meta y algo que reciba los mensajes las 24 horas.
Lo difícil ya lo tenés: el prompt del agente, el conocimiento público y los casos de prueba de [la práctica del agente](#p3-agente-preguntas) pasan tal cual. Lo que elegís acá es **el caño** por donde entran y salen los mensajes. Ejemplo: Fondus necesita varios asesores en un mismo número y no puede arriesgar ese número; Viajes TDH Docta quiere un bot que conteste paquetes y fechas a cualquier hora. No les conviene lo mismo.

> **Tip:** palabras que vas a ver en esta página:
> - **API:** la puerta para que un programa hable con otro (acá, tu bot con WhatsApp). La **Cloud API** es la API oficial de WhatsApp, de Meta.
> - **Webhook:** la dirección de internet a la que Meta le avisa a tu bot cada mensaje nuevo.
> - **Token:** una clave larga que demuestra que sos vos. Se cuida como una contraseña: nunca en el chat ni en GitHub.
> - **Worker:** el programita tuyo que vive en Cloudflare y contesta los mensajes. Lo armaste en [la práctica del agente](#p3-agente-preguntas).
> - **MCP:** el enchufe para que Claude use otra app ([Las piezas](#t2-piezas)).
> - **Servidor o VPS:** una compu alquilada en internet que está prendida todo el día.
> - **Plantilla:** un mensaje armado de antemano que Meta revisa y aprueba.

> **Datos:** precios y condiciones verificados el 18/11/2026 en las webs oficiales (links al final). Cambian seguido: revisalos antes de contratar. Precios en dólares, sin impuestos.

## Antes de elegir
- [ ] Las instrucciones de tu bot escritas desde tu cerebro ([Cierre: tu bot de WhatsApp](#d7-whatsapp)). Sirven para cualquier opción.
- [ ] Solo si vas a armar la **Cloud API directa** (más abajo): tu agente de Telegram pasa los 10 casos de prueba ([Un agente que responde y filtra](#p3-agente-preguntas)).
- [ ] Sabés si querés que la IA **conteste sola** o que **ayude a tu equipo** a contestar más rápido.
- [ ] Sabés cuántas conversaciones por mes recibís (para estimar el costo).
- [ ] Sabés qué número vas a usar. **Nunca** tu WhatsApp personal.

## Lo que cambió en WhatsApp en 2026 (leelo antes de decidir)
- **Se paga por mensaje.** Meta cobra lo que el negocio manda, según el tipo de mensaje (marketing, utilidad, autenticación, servicio) y el país de quien lo recibe. Lo que el cliente te escribe es gratis.
- **Desde el 1/10/2026 las respuestas también se pagan.** Cada número tiene **1.000 mensajes de servicio gratis por mes** (no se acumulan). Desde el 1.001 se cobran, a la misma tarifa que los de utilidad. Los mensajes de utilidad dentro de las 24 horas también pasaron a cobrarse. Sin un método de pago cargado en Meta, las respuestas pueden dejar de entregarse.
- **Argentina se puede pagar en pesos** desde el 1/4/2026, y tiene tarifa propia en la tabla de Meta.
- **Fuera de las 24 horas** desde el último mensaje del cliente, solo podés mandar **plantillas**: mensajes armados de antemano que Meta revisa y aprueba.
- **Bots de IA: sí, si atienden a tus clientes.** Desde el 15/1/2026 Meta prohíbe los asistentes de IA "de propósito general" (tipo ChatGPT dentro de WhatsApp). Un agente que responde consultas de tu negocio está permitido.
- **Meta tiene su propio agente de IA** (Meta Business Agent) y desde el 1/8/2026 lo cobra por uso (ver el **Extra** de las opciones).

> **Costo:** precio por mensaje en Argentina, en dólares: marketing, entre 0,06 y 0,07; utilidad, autenticación y servicio (después de los 1.000 gratis), entre 0,026 y 0,030. Son las cifras que publican proveedores oficiales de WhatsApp: la tabla oficial de Meta está en un archivo descargable que no pudimos leer. Verificalo en la [página oficial de precios](https://developers.facebook.com/docs/whatsapp/pricing). Ejemplo: 1.000 mensajes de marketing por mes, unos 60 a 70 dólares.

## Oficial o no oficial: la única pregunta que importa primero
- **Oficial** = WhatsApp Business Platform de Meta (la "Cloud API"). Meta sabe que sos un negocio, cobra por mensaje y no te bloquea el número por usar un bot, mientras respetes sus reglas.
- **No oficial** = conectar el número **escaneando un QR**, como si fuera WhatsApp Web. Es rápido y no paga a Meta, pero los términos de WhatsApp prohíben el acceso "por medios automatizados". Si WhatsApp lo detecta, **te suspende el número y perdés todos sus chats**.

> **Ojo:** las conexiones no oficiales sirven para probar con un número que no te importe perder. Nunca con el número principal del negocio, nunca para envíos masivos ni a gente que no te escribió.

## Las 6 opciones
Cada una tiene su página con el paso a paso. Acá, el resumen para comparar.

### 1. dlastcrm, el CRM de nuestra agencia (dos integraciones)
**Qué es:** el CRM que usamos en la agencia con nuestros clientes. Bandeja compartida para todo el equipo (WhatsApp, Instagram, Facebook, chat de la web), bot con IA, agenda de turnos, embudo de ventas y seguimientos automáticos. La agencia ofrece **las dos integraciones de WhatsApp** y la conecta con vos:
- **Integración oficial** (WhatsApp Business Platform de Meta). Es la que recomendamos para tu **número principal**. Permite "coexistencia": seguís usando la app WhatsApp Business en el celular y el CRM a la vez.
- **Integración por QR** (vincula el celular como WhatsApp Web). Se conecta en minutos y no paga mensajes a Meta, pero **no es oficial**: riesgo de bloqueo. Solo para un número nuevo o secundario.
- **A favor:** no programás nada, el bot se arma desde pantallas, cada chat queda en la ficha del contacto y te acompañamos en la puesta en marcha.
- **En contra:** es un servicio mensual. Tu bot vive dentro de la plataforma. La IA del bot se paga por uso, aparte.
- **Precio (nov 2026):** se cotiza con la agencia, según usuarios y números. La IA del bot y, en la integración oficial, los mensajes de Meta se pagan aparte, por uso.
- **Paso a paso:** [Tu bot de WhatsApp con dlastcrm](#w2-bot-dlastcrm).

### 2. API oficial de WhatsApp (Meta Cloud API), directa
**Qué es:** la conexión oficial y directa con Meta, sin intermediarios. Tu agente de [la práctica](#p3-agente-preguntas) (el Worker de Cloudflare) recibe y manda los mensajes.
- **A favor:** vía oficial, sin intermediarios, control total del prompt, las pruebas y los datos.
- **En contra:** la parte técnica es tuya: webhook, token, plantillas, verificación del negocio, errores.
- **Riesgo de bloqueo:** bajo, si respetás las políticas de Meta.
- **Precio (nov 2026):** solo los mensajes de Meta ([precios oficiales](https://developers.facebook.com/docs/whatsapp/pricing)). El Worker de Cloudflare es gratis para empezar.
- **Paso a paso:** más abajo en esta página, en **De Telegram a WhatsApp en 5 pasos**.

### 3. Tu propia plataforma (como la que armamos para un hospital)
**Qué es:** como la que armamos para un hospital: **tu propia plataforma de turnos**, que también sirve para pedidos, consultas y captura de interesados. La construís con Claude Code: tu servidor, la Cloud API oficial de Meta, un panel para cada negocio y otro para la agencia. Es el camino para vender bots a muchos negocios.
- **A favor:** oficial, tuyo y a tu medida. "Claude conversa, el código decide": el bot no puede dar un turno que no existe ni vender algo sin stock.
- **En contra:** camino avanzado: **días de trabajo**. Lo mantenés vos. Para salir a producción, Meta pide verificar el negocio y revisar la app.
- **Precio (nov 2026):** servidor en Railway, unos 5 USD por mes ([precios](https://railway.com/pricing)) + la API de Claude por uso + los mensajes de Meta. El ejemplo (3 negocios, 300 conversaciones cada uno) da entre 70 y 115 USD por mes.
- **Paso a paso:** [Tu propia plataforma de bots](#w3-bot-propio). En el taller hacés la base y el número de prueba de Meta.

### 4. Zernio (oficial, vía API o MCP)
**Qué es:** una API y un MCP para manejar muchas redes, con bandeja de mensajes. WhatsApp lo conecta por la **vía oficial** de Meta, con un alta guiada. Tiene un número de prueba gratis para probar sin Meta.
- **A favor:** oficial, más simple que la API directa, plan gratis para empezar, Claude Code maneja la bandeja por MCP.
- **En contra:** dependés de un intermediario. No acepta números personales. El bot automático lo armás vos.
- **Riesgo de bloqueo:** bajo.
- **Precio (nov 2026):** 2 cuentas gratis; de la 3 a la 10, 6 USD por cuenta por mes. 10.000 mensajes por mes gratis; después, 1 USD cada 10.000. Meta cobra aparte ([precios](https://zernio.com/pricing)).
- **Paso a paso:** [Tu bot de WhatsApp con Zernio](#w4-zernio).

### 5. Unipile (no oficial, por QR)
**Qué es:** una API para WhatsApp, LinkedIn, Instagram y mail. WhatsApp se conecta con un QR, como WhatsApp Web. Su propia página dice que usa **ingeniería inversa**.
- **A favor:** se conecta en minutos, sin Meta ni plantillas, precio fijo sin costo por mensaje.
- **En contra:** no oficial. Hay que programar el puente con tu bot.
- **Riesgo de bloqueo:** **alto**. Solo con un número secundario.
- **Precio (nov 2026):** 49 EUR por mes (unos 55 USD) hasta 10 cuentas. Prueba gratis de 7 días sin tarjeta ([precios](https://www.unipile.com/pricing-api/)).
- **Paso a paso:** [Tu bot de WhatsApp con Unipile](#w5-unipile).

### 6. Evolution API (código abierto, dos modos)
**Qué es:** un programa gratis que instalás en tu compu (para probar, con Docker) o en un servidor. Modo **Baileys** (por QR, no oficial) o modo **Cloud API** (oficial, con la API de Meta).
- **A favor:** el programa es gratis y es tuyo. Muchas integraciones (n8n, Chatwoot, Typebot).
- **En contra:** instalar y mantener un servidor. Si se cae a las 3 de la mañana, se cae tu atención.
- **Riesgo de bloqueo:** **alto** en modo Baileys; bajo en modo Cloud API.
- **Precio (nov 2026):** el programa, gratis ([GitHub oficial](https://github.com/evolution-foundation/evolution-api)). Un VPS de 2 GB, unos 11 a 12 USD por mes; en modo Cloud API, más los mensajes de Meta.
- **Paso a paso:** [Tu bot de WhatsApp con Evolution API](#w6-evolution-api).

### Extra: el agente de IA de Meta (Meta Business Agent)
**Qué es:** el agente de IA que hace Meta. Le das información del negocio, preguntas frecuentes, tu web y archivos; responde 24/7 y pasa la charla a una persona. Está en la app WhatsApp Business (**Herramientas › agente de IA**, sin programar) y en una versión para empresas ([documentación oficial](https://developers.facebook.com/documentation/meta-business-agent/overview)).
- **A favor:** oficial y sin programar.
- **En contra:** no usa tu cerebro ni tus casos de prueba. En la versión para empresas **quedan afuera finanzas, gobierno, salud, alcohol, apuestas, medicamentos de venta libre y servicios matrimoniales** (Fondus, por ser financiera, no califica). En la app, al activarlo se desvinculan los dispositivos enlazados y se apagan las listas de difusión y los mensajes automáticos.
- **¿Está en Argentina?** Meta no publica la lista de países. Si te aparece la opción en las herramientas de WhatsApp Business, lo tenés.
- **Precio (nov 2026):** en la versión para empresas, **2 USD por millón de tokens** desde el 1/8/2026; Meta estima unos 4 a 5 centavos de dólar por mensaje ([precios oficiales](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing/non-template-messages/)). En la app: verificá en tu app si te lo cobran.

## Árbol de decisión
1. **¿El número que vas a usar no lo podés perder** (es el del negocio, tiene años de chats)?
   → **Sí:** solo vía oficial (dlastcrm con la integración oficial, API directa, plataforma propia, Zernio o Evolution en modo Cloud API). Seguí al 2.
   → **No, es un número de prueba:** podés probar cualquier opción, incluso las de QR (dlastcrm por QR, Unipile, Evolution en modo Baileys). Igual seguí al 2 para elegir la definitiva.
2. **¿Querés programar o mantener algo?**
   → **No:** ¿tenés varios vendedores o querés agenda, embudo y seguimientos en un lugar? → **dlastcrm**. ¿Sos un negocio chico con catálogo y te alcanza con respuestas generales? → **Meta Business Agent**, si te aparece.
   → **Un poco:** ¿ya publicás en redes o querés manejar WhatsApp desde Claude? → **Zernio**.
   → **Sí:** ¿un solo negocio, el tuyo? → **API oficial directa** con el agente de la práctica. ¿Querés todo en tu propio servidor? → **Evolution API**. ¿Querés vender bots a muchos negocios? → **Plataforma propia**.
3. **¿Tu negocio es financiero o de salud?** → descartá Meta Business Agent para empresas y revisá dos veces las reglas de Meta antes de automatizar.

## Tabla resumen
| Opción | ¿Oficial? | ¿Hay que programar? | Riesgo de bloqueo | Tiempo para tenerlo andando | Costo aproximado (nov 2026), además de los mensajes de Meta | Ideal para |
|---|---|---|---|---|---|---|
| [dlastcrm](#w2-bot-dlastcrm) | Sí (integración oficial) / No (por QR) | No | Bajo (oficial) / Alto (QR) | 90 a 120 min + reunión con la agencia | Se cotiza con la agencia + IA por uso | Equipos con varios vendedores que quieren todo en un lugar |
| API oficial directa | Sí | Sí (Claude Code ayuda) | Bajo | 1 a 2 horas, con la práctica hecha | 0 de plataforma (Worker gratis para empezar) | Quien ya tiene el agente de la práctica y quiere control total |
| [Plataforma propia](#w3-bot-propio) | Sí | Sí, varios días | Bajo | 3 a 5 días + aprobaciones de Meta | Servidor ~5 USD/mes + Claude por uso | Agencias que quieren vender bots propios |
| [Zernio](#w4-zernio) | Sí | Poco (API o MCP) | Bajo | 60 min con su número de prueba | Gratis hasta 2 cuentas y 10.000 mensajes | Quien ya publica en redes y quiere WhatsApp oficial |
| [Unipile](#w5-unipile) | No | Sí | **Alto** | 60 a 90 min | Desde 49 EUR/mes (~55 USD) | Pruebas rápidas con un número secundario |
| [Evolution API](#w6-evolution-api) | Según el modo | Sí, y mantener un servidor | **Alto** (Baileys) / Bajo (Cloud API) | 2 a 3 horas en tu compu | Gratis; VPS ~11 a 12 USD/mes | Equipos técnicos que quieren todo propio |
| Meta Business Agent | Sí | No | Bajo | Minutos, si te aparece | 2 USD por millón de tokens (versión para empresas) | Negocios chicos con catálogo |

## De Telegram a WhatsApp en 5 pasos (Cloud API directa)
Con la API oficial y el mismo Worker de Cloudflare de la práctica. Es para quien ya hizo [Un agente que responde y filtra](#p3-agente-preguntas) completo, con el bot publicado. Si elegís dlastcrm o Zernio, los pasos 1 y 3 los resuelve la plataforma.

### Paso 1 · Creá la app de WhatsApp en Meta
1. Entrá a [developers.facebook.com](https://developers.facebook.com/) con tu Facebook y registrate como desarrollador.
2. Tocá **Create App**, elegí **Connect with customers through WhatsApp** y tu portfolio de negocio.
3. En **API Setup**, tocá **Generate access token**, agregá tu celular como número de destino (**To**) y tocá **Send message**.
4. Anotá el **Phone number ID** del número de prueba. Es un código de identificación que te da Meta, no tu teléfono.

> **Ojo:** el **access token** que generaste es una clave. No lo pegues en el chat de Claude. Lo vas a cargar vos en el Paso 3.

**Tenés que ver:** el mensaje de prueba `hello_world` en tu WhatsApp.

### Paso 2 · Que Claude Code sume WhatsApp al Worker
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
En agente/bot agregá soporte para WhatsApp Cloud API al Worker, sin romper Telegram. Una ruta /whatsapp que: (1) responda la verificación del webhook de Meta (GET con hub.mode, hub.verify_token y hub.challenge) comparando con el secreto WHATSAPP_VERIFY_TOKEN; (2) reciba los mensajes de texto (POST), use el mismo SYSTEM_PROMPT, la misma memoria en KV y la misma regla DERIVAR; (3) conteste con la Graph API usando los secretos WHATSAPP_TOKEN y WHATSAPP_PHONE_NUMBER_ID. Revisá en la documentación oficial de Meta la versión actual de la Graph API y el formato del webhook antes de escribir el código. Los avisos de derivación siguen yendo a mi Telegram. Generá WHATSAPP_VERIFY_TOKEN en .dev.vars, confirmá que .dev.vars está en .gitignore y decime qué secretos tengo que cargar con wrangler secret put. No me pidas que te pegue tokens en el chat. No publiques hasta que te diga.
```

**Tenés que ver:** la ruta nueva en `src/index.js` y la lista de secretos para cargar.

### Paso 3 · Conectá el webhook en Meta
1. Abrí **una segunda terminal** y entrá a la carpeta del bot:

<div data-os="mac">

```bash
cd ~/Documents/cerebro-[TU-EMPRESA]/agente/bot
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\cerebro-[TU-EMPRESA]\agente\bot
```

</div>

2. Cargá cada secreto nuevo con este comando, uno por vez. Cambiá `[NOMBRE-DEL-SECRETO]` por cada nombre que te dio Claude (por ejemplo `WHATSAPP_TOKEN`). Cuando te pida el valor, pegalo ahí, en la terminal: el token lo copiás de Meta (**API Setup**), el Phone number ID es el que anotaste y el verify token está en tu `.dev.vars`.

```bash
npx wrangler secret put [NOMBRE-DEL-SECRETO]
```

3. Publicá con `npm run deploy` (en Windows, si da error de scripts, usá `npm.cmd run deploy`).
4. En tu app de Meta, en **WhatsApp › Configuration**, sección del webhook: pegá la URL `https://[TU-WORKER].workers.dev/whatsapp` (`[TU-WORKER]` sale de la dirección de tu bot publicado en la práctica, la que termina en `.workers.dev`) y tu `WHATSAPP_VERIFY_TOKEN` (está en tu `.dev.vars`), tocá **Verify and save** y suscribite al campo **messages**.

> **Ojo:** los nombres de las pantallas de Meta cambian seguido. Si no los ves igual, buscá "Webhook" dentro de la sección de WhatsApp de tu app.

**Tenés que ver:** el webhook verificado en Meta.

### Paso 4 · Probá de nuevo antes de abrirlo al público
1. En la terminal de `agente/bot`, corré `npm run probar`: los mismos 10 casos tienen que seguir pasando.
2. Desde tu WhatsApp, escribile al número de prueba las mismas preguntas que le hiciste al bot de Telegram.

**Tenés que ver:** las mismas respuestas que en Telegram y el aviso de derivación en tu Telegram.

### Paso 5 · Pasá a producción
1. Sumá tu número del negocio (uno que no esté en la app de WhatsApp, o con coexistencia).
2. Cambiá el token temporal por uno permanente: el temporal vence enseguida. El permanente se crea con un **usuario del sistema** (una cuenta para programas, no para personas) en la configuración de tu Meta Business.
3. Cargá un método de pago en Meta (en Argentina se puede en pesos).
4. Verificá el negocio en Meta si vas a escribirle a muchas personas.
5. Si vas a escribir vos primero (recordatorios, seguimientos), creá las plantillas y esperá la aprobación.

**Tenés que ver:** tu número del negocio respondiendo con el agente.

## Cómo sé que funcionó
Hacé esta prueba con cualquiera de las opciones. Desde un celular que no sea el del negocio, mandale este WhatsApp al número del bot:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario que está en tu cerebro (no uno inventado) y avisarte que alguien pidió una persona.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Meta no verifica el webhook | El verify token del servidor tiene que ser idéntico al que pegaste en Meta, y la URL tiene que terminar en `/whatsapp`. |
| Funcionaba y dejó de responder al día siguiente | Se venció el token temporal. Generá uno permanente (paso 5.2) y cargalo con `npx wrangler secret put WHATSAPP_TOKEN`. |
| No le llega el mensaje a un cliente que escribió hace días | Pasaron más de 24 horas: solo podés mandarle una plantilla aprobada. |
| El número de prueba no le escribe a un amigo | El número de prueba solo le escribe a los destinatarios que agregaste y verificaste en la app. |
| Desde octubre dejaron de salir las respuestas | Falta el método de pago en Meta: desde el 1/10/2026 los mensajes de servicio se cobran después de los primeros 1.000. |
| En Windows: "la ejecución de scripts está deshabilitada" al usar `npm` o `npx` | Usá `npm.cmd` y `npx.cmd` en vez de `npm` y `npx` (ej.: `npx.cmd wrangler secret put WHATSAPP_TOKEN`). |
| Un número conectado por QR quedó "desconectado" o restringido | Volvé a vincularlo. Si WhatsApp lo restringió, pasá a la vía oficial con otro número: el bloqueo no se revierte desde ninguna plataforma. |

## Para seguir solo
- **Hacé la cuenta antes de elegir:** conversaciones por mes × mensajes por conversación × tarifa de Meta. Muchas veces el costo de los mensajes pesa más que la plataforma.
- **Arrancá con un número nuevo** y dejá el de siempre en la app hasta que el bot pase un mes sin errores graves.
- **Medí las derivaciones:** si el bot deriva más de la mitad de las consultas, el problema no es el canal sino el cerebro. Completá los `PENDIENTE` primero ([Armá el cerebro](#p1-cerebro)).

## Fuentes (consultadas el 18/11/2026)
- Meta, WhatsApp Cloud API, guía para empezar: https://developers.facebook.com/docs/whatsapp/cloud-api/get-started/
- Meta, precios de WhatsApp Business Platform: https://developers.facebook.com/docs/whatsapp/pricing
- Meta, cambios de precios 2026 (1/10/2026, pesos argentinos desde 1/4/2026): https://developers.facebook.com/docs/whatsapp/pricing/updates-to-pricing
- Meta, precios de Meta Business Agent y mensajes de servicio: https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing/non-template-messages/
- Meta, Meta Business Agent: https://developers.facebook.com/documentation/meta-business-agent/overview
- Meta, términos de WhatsApp Business Platform (proveedores de IA): https://www.facebook.com/legal/Meta-Terms-for-WhatsApp-Business-Platform
- WhatsApp, ayuda sobre el agente de IA en WhatsApp Business: https://faq.whatsapp.com/291930066973116
- Términos de servicio de WhatsApp: https://www.whatsapp.com/legal/terms-of-service
- Tarifas de Argentina según proveedores: https://help.sleekflow.io/en_US/pricing · https://www.infobip.com/whatsapp-business/pricing
- Zernio: https://zernio.com/pricing · https://docs.zernio.com/platforms/whatsapp · https://docs.zernio.com/mcp (detalle en [Zernio](#w4-zernio))
- Unipile, precios: https://www.unipile.com/pricing-api/ (detalle en [Unipile](#w5-unipile))
- Evolution API (GitHub y documentación): https://github.com/evolution-foundation/evolution-api · https://docs.evolutionfoundation.com.br (detalle en [Evolution API](#w6-evolution-api))
- Precios de VPS: https://www.digitalocean.com/pricing/droplets · https://www.hetzner.com/cloud/regular-performance/
- Railway, precios: https://railway.com/pricing
