---
titulo: "Bots de WhatsApp: qué camino te conviene"
bloque: WhatsApp
tiempo: 15 min de lectura (la Cloud API directa, si la armás después, lleva 1 a 2 horas)
para: Todos (cierre del taller)
necesitas: d7-whatsapp
resultado: Sabés qué camino te conviene para tu bot de WhatsApp, cuánto cuesta, qué riesgo corrés y cuál es el primer paso.
---

Tus clientes están en WhatsApp, pero WhatsApp no se arma en una hora: pide un número dedicado, plantillas aprobadas por Meta y algo que reciba los mensajes las 24 horas. Lo difícil (qué dice tu bot) ya lo resolvés hoy. Acá elegís **el caño** por donde entran y salen los mensajes.
Ejemplo: Fondus necesita varios asesores en un mismo número y no puede arriesgarlo; Viajes TDH Docta quiere un bot que conteste paquetes a cualquier hora. No les conviene lo mismo.

> **Ojo:** **hoy en el taller** hacés la **Versión MVP** de [Cierre: tu bot de WhatsApp](#d7-whatsapp): las instrucciones de tu bot, probadas en Telegram con n8n. Esta página y las de cada opción son para **después**. Las instrucciones que escribiste hoy sirven para cualquier opción.

> **Datos:** precios verificados el 18/11/2026 en las webs oficiales (links al final). Cambian seguido: revisalos antes de contratar. En dólares, sin impuestos.

## Antes de elegir
- [ ] Tenés `bot/instrucciones-del-bot.md` escrito desde tu cerebro ([Cierre: tu bot de WhatsApp](#d7-whatsapp)).
- [ ] Sabés si querés que la IA **conteste sola** o que **ayude a tu equipo** a contestar.
- [ ] Sabés cuántas conversaciones por mes recibís (para estimar el costo).
- [ ] Sabés qué número vas a usar. **Nunca** tu WhatsApp personal.

## Lo primero: oficial o no oficial
- **Oficial** = la API de WhatsApp de Meta (la "Cloud API"). Meta sabe que sos un negocio, cobra por mensaje y no te bloquea por usar un bot si respetás sus reglas.
- **No oficial** = conectar el número **escaneando un QR**, como WhatsApp Web. Rápido y sin pagarle a Meta, pero los términos de WhatsApp lo prohíben. Si lo detecta, **te suspende el número y perdés sus chats**.

> **Ojo:** lo no oficial, solo para probar con un número que no te importe perder. Nunca con el número principal, nunca para envíos masivos.

## Lo que cambió en 2026
- **Se paga por mensaje** que manda el negocio, según el tipo (marketing, utilidad, autenticación, servicio). Lo que te escribe el cliente es gratis.
- **Desde el 1/10/2026 las respuestas también se pagan:** 1.000 mensajes de servicio gratis por número y por mes; después, a tarifa de utilidad. Sin método de pago en Meta, las respuestas pueden dejar de salir.
- **Fuera de las 24 horas** desde el último mensaje del cliente, solo podés mandar **plantillas** aprobadas por Meta.
- **Argentina se puede pagar en pesos** desde el 1/4/2026.
- **Bots de IA: sí, si atienden a tus clientes.** Meta prohíbe los asistentes "de propósito general" (tipo ChatGPT dentro de WhatsApp), no un bot de tu negocio.

> **Costo:** en Argentina, por mensaje: marketing, 0,06 a 0,07 USD; utilidad, autenticación y servicio (pasados los 1.000 gratis), 0,026 a 0,030 USD. Son cifras de proveedores oficiales: verificalo en la [página oficial de Meta](https://developers.facebook.com/docs/whatsapp/pricing). Ejemplo: 1.000 mensajes de marketing, unos 60 a 70 USD.

## Las opciones de un vistazo
| Opción | ¿Oficial? | ¿Programar? | Riesgo de bloqueo | Tiempo | Costo (nov 2026), además de Meta | Ideal para |
|---|---|---|---|---|---|---|
| **1a. [dlastcrm, oficial](#w2-bot-dlastcrm)** | Sí | No | Bajo | 90 a 120 min + reunión con la agencia | Se cotiza con la agencia + IA por uso | Equipos con varios vendedores, todo en un lugar |
| **1b. [dlastcrm, por QR](#w2-bot-dlastcrm)** | **No** | No | **Alto** | Igual | Igual, sin costo de Meta | Un número nuevo o secundario |
| **2. API oficial directa** (abajo) | Sí | Sí, lo hace Claude | Bajo | 1 a 2 horas | 0 de plataforma (Cloudflare gratis para empezar) | Quien ya tiene el agente de [la práctica](#p3-agente-preguntas) |
| **3. [Plataforma propia](#w3-bot-propio)** | Sí | Sí, varios días | Bajo | 3 a 5 días + Meta | 70 a 115 USD/mes (3 negocios) | Agencias que quieren vender bots |
| **4. [Zernio](#w4-zernio)** | Sí | Poco | Bajo | 60 min con su número de prueba | Gratis hasta 2 cuentas y 10.000 mensajes | Quien ya publica en redes |
| **5. [Unipile](#w5-unipile)** | **No** | Sí, lo hace Claude | **Alto** | 60 a 90 min | 49 EUR/mes (~55 USD) | Pruebas rápidas con número secundario |
| **6. [Evolution API](#w6-evolution-api)** | Según el modo | Sí, y mantener un servidor | **Alto** (QR) / Bajo (oficial) | 2 a 3 horas | Gratis; servidor ~11 a 12 USD/mes | Equipos con alguien técnico |
| **Extra. Meta Business Agent** | Sí | No | Bajo | Minutos, si te aparece | 2 USD por millón de tokens (versión para empresas) | Negocios chicos con catálogo |

**En una línea cada una:**
- **dlastcrm:** el CRM de la agencia. Bandeja para todo el equipo, bot con IA, agenda y seguimientos, sin programar. Con la integración oficial podés seguir usando la app en el celular ("coexistencia"). Lo conectamos con vos.
- **API oficial directa:** tu agente de Cloudflare conectado a Meta sin intermediarios. Control total; la parte técnica (webhook, token, plantillas) es tuya.
- **Plataforma propia:** como la que armamos para un hospital: turnos, pedidos y consultas para muchos negocios. "Claude conversa, el código decide". Días de trabajo.
- **Zernio:** vía oficial con alta guiada, número de prueba gratis y MCP para que Claude maneje la bandeja. Dependés de un intermediario.
- **Unipile:** tu WhatsApp por QR con una API. Su propia web dice que usa ingeniería inversa. Precio fijo, sin costo por mensaje.
- **Evolution API:** programa gratis que instalás vos. Modo QR (no oficial) o Cloud API (oficial). Si se cae a las 3 de la mañana, se cae tu atención.
- **Meta Business Agent:** el agente de IA de Meta, en la app WhatsApp Business (**Herramientas › agente de IA**). No usa tu cerebro. En la versión para empresas quedan afuera finanzas y salud, entre otros (Fondus no califica). Si no te aparece la opción, no está disponible para vos.

## Árbol de decisión
1. **¿Es un número que no podés perder** (el del negocio, con años de chats)?
   → **Sí:** solo vía oficial (dlastcrm oficial, API directa, plataforma propia, Zernio o Evolution en modo oficial).
   → **No, es de prueba:** podés probar las de QR. Igual elegí la definitiva con el punto 2.
2. **¿Querés programar o mantener algo?**
   → **No:** varios vendedores o agenda y seguimientos en un lugar → **dlastcrm**. Negocio chico con catálogo → **Meta Business Agent**, si te aparece.
   → **Un poco:** ya publicás en redes o querés manejar WhatsApp desde Claude → **Zernio**.
   → **Sí:** un solo negocio → **API directa**. Todo en tu servidor → **Evolution API**. Vender bots a muchos negocios → **plataforma propia**.
3. **¿Tu negocio es financiero o de salud?** → descartá Meta Business Agent y revisá dos veces las reglas de Meta.

## La API oficial directa, en 4 pasos
Para quien hizo [Un agente que responde y filtra](#p3-agente-preguntas) completo, con el bot publicado en Cloudflare. Todo se hace desde la pestaña **Code** de la app de Claude.

### Paso 1 · Creá la app de WhatsApp en Meta
1. Entrá a [developers.facebook.com](https://developers.facebook.com/) con tu Facebook y registrate como desarrollador.
2. **Create App** › **Connect with customers through WhatsApp** › tu portfolio de negocio.
3. En **API Setup**, tocá **Generate access token**, agregá tu celular en **To** y tocá **Send message**.
4. Dejá esa pantalla abierta: el **access token** y el **Phone number ID** los pegás en el Paso 2.

**Tenés que ver:** el mensaje `hello_world` en tu WhatsApp.

### Paso 2 · Guardá las claves sin pasarlas por el chat
1. En la app de Claude, tocá **Code**, elegí **Local › Open folder…** y abrí `cerebro-[TU-EMPRESA]`.
2. Pegá:

```prompt
En agente/bot/.dev.vars agregá las líneas WHATSAPP_TOKEN= y WHATSAPP_PHONE_NUMBER_ID= vacías, y WHATSAPP_VERIFY_TOKEN= con un valor al azar que generes vos. Confirmá que .dev.vars está en el .gitignore y abrime el archivo en el editor de texto de mi compu. No me muestres su contenido.
```

3. En el editor, pegá el token y el Phone number ID de Meta después de cada `=`, guardá y escribile a Claude `listo`.

**Tenés que ver:** Claude confirma que las dos líneas tienen valor, sin mostrarlos.

### Paso 3 · Que Claude sume WhatsApp al bot y lo publique
```prompt
En agente/bot agregá soporte para WhatsApp Cloud API al Worker, sin romper Telegram. Una ruta /whatsapp que: (1) responda la verificación del webhook de Meta comparando con WHATSAPP_VERIFY_TOKEN; (2) reciba los mensajes de texto y use el mismo SYSTEM_PROMPT, la misma memoria en KV y la misma regla DERIVAR; (3) conteste con la Graph API usando WHATSAPP_TOKEN y WHATSAPP_PHONE_NUMBER_ID. Revisá en la documentación oficial de Meta la versión vigente de la Graph API. Los avisos de derivación siguen yendo a mi Telegram. Corré npm run probar: los 10 casos tienen que seguir pasando. Después cargá en Cloudflare los secretos nuevos desde .dev.vars sin mostrarme los valores, publicá y dame la URL que termina en /whatsapp y el verify token para pegar en Meta.
```

**Tenés que ver:** las pruebas en 10 de 10, la URL del bot y el aviso de que los secretos quedaron cargados.

### Paso 4 · Conectá el webhook en Meta
1. En tu app de Meta, **WhatsApp › Configuration**: pegá la URL y el verify token que te dio Claude y tocá **Verify and save**.
2. Suscribite al campo **messages**.
3. Desde tu WhatsApp, escribile al número de prueba lo mismo que le preguntaste al bot de Telegram.

> **Ojo:** los nombres de las pantallas de Meta cambian seguido. Si no los ves igual, buscá "Webhook" dentro de la sección de WhatsApp de tu app.

**Tenés que ver:** las mismas respuestas que en Telegram y el aviso de derivación en tu Telegram.

**Para producción:** sumá tu número del negocio, cambiá el token temporal por uno permanente (de un **usuario del sistema** de tu Meta Business, guardado con el mismo patrón del Paso 2), cargá un método de pago en Meta y, si vas a escribir vos primero, creá las plantillas.

## Cómo sé que funcionó
Con cualquier opción, desde un celular que no sea el del negocio, mandale al número del bot:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario de tu cerebro (no uno inventado) y avisarte que alguien pidió una persona.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Meta no verifica el webhook | El verify token tiene que ser idéntico en Meta y en el bot, y la URL terminar en `/whatsapp`. |
| Funcionaba y al otro día dejó de responder | Se venció el token temporal. Generá uno permanente, pegalo en `.dev.vars` y pedile a Claude que lo cargue en Cloudflare. |
| No le llega la respuesta a alguien que escribió hace días | Pasaron más de 24 horas: solo se puede mandar una plantilla aprobada. |
| Desde octubre dejaron de salir respuestas | Falta el método de pago en Meta. |
| Un número por QR quedó restringido | El bloqueo no se revierte desde ninguna plataforma. Pasá a la vía oficial con otro número. |

## Para seguir solo
- **Hacé la cuenta:** conversaciones por mes × mensajes por conversación × tarifa de Meta. Muchas veces pesa más que la plataforma.
- **Arrancá con un número nuevo** y dejá el de siempre en la app hasta que el bot pase un mes sin errores graves.
- **Medí las derivaciones:** si el bot deriva más de la mitad, el problema es el cerebro, no el canal ([Armá el cerebro](#p1-cerebro)).

## Fuentes (consultadas el 18/11/2026)
- Meta, Cloud API: https://developers.facebook.com/docs/whatsapp/cloud-api/get-started/
- Meta, precios y cambios 2026: https://developers.facebook.com/docs/whatsapp/pricing · https://developers.facebook.com/docs/whatsapp/pricing/updates-to-pricing
- Meta Business Agent: https://developers.facebook.com/documentation/meta-business-agent/overview · https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing/non-template-messages/
- Términos de WhatsApp Business Platform: https://www.facebook.com/legal/Meta-Terms-for-WhatsApp-Business-Platform · https://www.whatsapp.com/legal/terms-of-service
- Tarifas de Argentina según proveedores: https://help.sleekflow.io/en_US/pricing · https://www.infobip.com/whatsapp-business/pricing
- Zernio: https://zernio.com/pricing · Unipile: https://www.unipile.com/pricing-api/ · Evolution API: https://github.com/evolution-foundation/evolution-api
- VPS: https://www.digitalocean.com/pricing/droplets · https://www.hetzner.com/cloud/regular-performance/ · Railway: https://railway.com/pricing
