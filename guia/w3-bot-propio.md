---
titulo: "Tu propia plataforma de bots (como la que armamos para un hospital)"
bloque: WhatsApp
tiempo: "De 3 a 5 días de trabajo, más las aprobaciones de Meta. El primer día (base, primer chat y WhatsApp de prueba): unas 2 horas"
para: Quien quiera ir más allá (camino avanzado). Ideal para quien quiere vender bots a otros negocios.
necesitas: s2-claude-code, s3-herramientas-base, s4-github, s9-api-anthropic, w1-opciones
resultado: "Tu propia plataforma en internet, con varios negocios, módulos (conocimiento, contactos, pedidos, turnos), paneles, WhatsApp, Instagram, Messenger, chat web y avisos automáticos."
---

Es el mismo camino que seguimos para un hospital: **tu propia plataforma de turnos**, que además sirve para pedidos, consultas y captura de interesados. Con ella una agencia maneja los bots de muchos negocios (una tienda, un consultorio, una inmobiliaria) por WhatsApp, Instagram, Messenger y la web.
No hace falta saber programar: Claude escribe el código desde la pestaña **Code** y vos probás cada etapa. Pero son **días**. Si solo querés un bot para tu negocio, mirá [dlastcrm](#w2-bot-dlastcrm) o la [API oficial directa](#w1-opciones).

> **Ojo:** **hoy en el taller** hacés la **Versión MVP** de [Cierre: tu bot de WhatsApp](#d7-whatsapp): las instrucciones de tu bot, probadas en Telegram con n8n. Esta página es para **después**. Esas instrucciones te sirven para cargar tu primer negocio (Paso 9).

> **Tip:** la regla de oro: **Claude conversa, el código decide.** El bot contesta solo con la información del negocio y solo hace las acciones activadas. No puede dar un turno que no existe ni vender algo sin stock.

> **Datos:** el bot pide lo mínimo (nombre, qué busca, día y hora). En un consultorio, que nunca pida síntomas ni datos de salud. Los negocios de ejemplo son inventados.

## Qué hace la plataforma
| Quién | Qué tiene |
|---|---|
| **Vos, la agencia** | Panel `/agencia` para crear negocios, elegir qué hace cada bot y conectar sus cuentas. |
| **Cada negocio** | Su panel `/n/<id>/admin` con mensajes, registros, lo que sabe el bot y la configuración. |
| **Sus clientes** | Escriben por WhatsApp, Instagram, Messenger o la web. |

Cada negocio prende los **módulos** que necesita: **Conocimiento** (contesta dudas), **Pedidos** (catálogo con stock), **Turnos** (agenda, cancela y recuerda) y **Contactos** (guarda interesados).

## Antes de empezar
- [ ] Plan Pro o Max de Claude y la app de escritorio con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).
- [ ] Node.js (versión **LTS**) instalado con doble clic desde [nodejs.org](https://nodejs.org) ([Herramientas base](#s3-herramientas-base)).
- [ ] GitHub y GitHub Desktop ([GitHub](#s4-github)).
- [ ] Clave de API de Anthropic con crédito ([API de Anthropic](#s9-api-anthropic)).
- [ ] Una cuenta de Facebook para Meta for Developers.
- [ ] Para publicar: cuenta en [Railway](https://railway.com), tarjeta para Meta y cuenta en [cron-job.org](https://cron-job.org).

> **Costo:** (nov 2026) Claude Pro 20 USD/mes o Max 100 USD/mes para construir. API de Claude por uso. Railway Hobby, unos 5 USD/mes ([precios](https://railway.com/pricing)). Meta for Developers, GitHub y cron-job.org, gratis. WhatsApp por mensaje ([precios de Meta](https://developers.facebook.com/docs/whatsapp/pricing)). Detalle en **Cuánto cuesta por mes**, al final.

> **Ojo:** las claves (`ANTHROPIC_API_KEY`, `WA_TOKEN`, `META_APP_SECRET` y las contraseñas) van **solo** en el archivo `.env` de tu compu y en las variables de Railway. **Nunca** en el chat ni en GitHub. Siempre con el mismo patrón: Claude crea la línea vacía, te abre el archivo en el editor, pegás vos y le decís `listo`.

## Paso 1 · Creá el proyecto y abrilo en la pestaña Code
1. En **GitHub Desktop** › **File › New repository**: nombre `plataforma-bots`, en **Local path** tu carpeta **Documentos**, **Git ignore** en **Node**. **Create repository**.
2. En la app de Claude, tocá **Code**, elegí **Local › Open folder…** y abrí `plataforma-bots`.
3. Escribí: `¿Qué versión de Node.js tengo?`

**Tenés que ver:** Claude te responde una versión (por ejemplo `v24.x`). Si dice que no está, instalá Node desde [nodejs.org](https://nodejs.org) y abrí una conversación nueva.

## Paso 2 · Pegá el plan del producto
Claude lo guarda como `CLAUDE.md` y lo lee solo cada vez que empezás. Pegá esto y respondé sus dudas:

```prompt
Guardá el texto que sigue como CLAUDE.md, sin cambiarlo. Todavía no programes nada. Después decime qué partes no te quedan claras.

# Plataforma de bots

## Qué es
Una plataforma para una agencia que crea y maneja, desde un solo servidor, bots de atención para muchos negocios de cualquier rubro (tiendas, consultorios, inmobiliarias, estudios, gimnasios, servicios). Cada negocio tiene un bot que responde por WhatsApp, Instagram, Messenger y un chat web: contesta con la información del negocio, hace las acciones que el negocio activó y pasa la conversación a una persona cuando hace falta.

## Quién la usa
- La agencia: panel /agencia para crear negocios a partir de una plantilla de rubro, conectar sus canales, ver quién espera a una persona y entrar al panel de cualquier negocio.
- El personal de cada negocio: panel /n/<id>/admin con Bandeja (conversaciones), Registros (contactos, pedidos y turnos), Conocimiento y Configuración.
- Los clientes de cada negocio: escriben por sus canales, preguntan y hacen trámites.

## Principio central: Claude conversa, el código decide
Claude lleva la conversación y usa herramientas. Lo que el bot sabe sale de la base de conocimiento del negocio y lo que hace sale de herramientas con reglas en el código: Claude nunca inventa datos, precios ni disponibilidad.

## Módulos (cada negocio activa los que necesita)
- Conocimiento (siempre activo): buscar_en_conocimiento(consulta) devuelve los fragmentos relevantes de la base del negocio (preguntas frecuentes, servicios o productos, horarios, políticas y textos libres). Si la respuesta no está, el bot lo dice y ofrece derivar.
- Contactos: registrar_contacto(nombre, telefono_o_email, interes) guarda los datos de alguien interesado, con los campos que pida el negocio.
- Pedidos: catálogo con productos, precios y stock. crear_pedido(items, nombre, entrega) valida stock y precios antes de guardar y devuelve un código; consultar_pedido(codigo) muestra el estado (nuevo, en preparación, listo, entregado). No cobra: el pago se coordina aparte.
- Turnos: consultar_disponibilidad, agendar_turno, listar_mis_turnos, cancelar_turno y confirmar_asistencia, con horarios, días cerrados, intervalo, capacidad simultánea y anticipación mínima.
- Atención humana (siempre activo): derivar_a_humano(motivo), solo dentro del horario de atención humana; fuera de ese horario, el bot avisa cuándo lo van a atender.
Un cliente solo puede ver y cambiar sus propios pedidos, turnos y datos.

## Configuración de cada negocio (JSON, editable desde su panel)
Nombre, rubro, descripción, dirección, contacto, zona horaria (por defecto America/Argentina/Buenos_Aires), tono del bot, horarios de atención, módulos activos, base de conocimiento, catálogo (si usa Pedidos), reglas de turnos (si usa Turnos), campos a pedir en Contactos, atención humana (horarios y casos en que se deriva siempre), cosas que el bot nunca debe hacer e instrucciones extra. El system prompt se arma con estos datos y usa la caché de prompts de Anthropic. Claude solo recibe las herramientas de los módulos activos.

## Plantillas de rubro
Al crear un negocio se elige una plantilla que activa módulos y trae una configuración de ejemplo: Atención y preguntas frecuentes, Ventas y pedidos, Turnos y reservas, Captura de contactos. Después todo se puede cambiar.

## Atención humana
Cuando el bot deriva, la conversación pasa a modo humano: el bot deja de responderle a ese cliente y la conversación aparece primero en la Bandeja, con sonido y notificación. Lo que responde el personal desde el panel sale por el mismo canal. "Devolver al bot" lo reactiva y Claude recibe lo que se habló mientras tanto.

## Varios negocios
Cada negocio es una carpeta dentro de NEGOCIOS_DIR (por defecto ./negocios) con negocio.json (configuración y conocimiento), datos.json (contactos, conversaciones, pedidos, turnos y derivaciones) y acceso.json (contraseña cifrada del panel y canales vinculados). Cada pedido y cada mensaje se procesa dentro del contexto de su negocio: un negocio nunca ve datos de otro.

## Canales
- Chat web en /n/<id>/, widget en /n/<id>/widget.js (una línea para pegar en la web del negocio) y página de ejemplo en /n/<id>/ejemplo.
- Un solo webhook de Meta en /webhook/meta para WhatsApp Cloud API, Instagram y Messenger, verificado con META_VERIFY_TOKEN y con la firma de cada mensaje controlada con META_APP_SECRET (o IG_APP_SECRET).
- Cada mensaje se asigna a su negocio por phone_number_id (WhatsApp), id de cuenta (Instagram) o id de página (Messenger).
- El webhook responde 200 enseguida, ignora mensajes repetidos por su id y procesa un mensaje por vez por cliente.
- Solo texto: si llega un audio o una imagen, el bot pide que lo escriban.
- En Instagram y Messenger solo se puede escribir hasta 24 horas después del último mensaje del cliente.

## Avisos
POST /agencia/api/avisos, con autenticación básica (usuario "agencia", contraseña AGENCIA_PASSWORD), manda los avisos pendientes de todos los negocios: recordatorios de los turnos de mañana y avisos de pedidos que pasaron a "listo". El cliente responde y el bot sigue la conversación.

## Seguridad
Contraseñas cifradas, sesiones firmadas con SECRETO_SESIONES y paneles solo con sesión. El .env, node_modules, negocios/ y data/ nunca se suben a GitHub.

## Tecnología
Node.js LTS, TypeScript ejecutado con tsx (en dependencies, no en devDependencies, para que el servidor lo instale), Express y el SDK oficial de Anthropic (@anthropic-ai/sdk). Páginas en HTML y JavaScript simple, sin frameworks. Datos en archivos JSON: es un MVP.
Scripts: npm run dev, npm start, npm test (pruebas de las reglas sin llamar a Claude) y npm run demo (negocios de ejemplo).
Variables de entorno en .env, con un .env.example sin valores: ANTHROPIC_API_KEY, CLAUDE_MODEL (por defecto claude-opus-5-5), CLAUDE_EFFORT (por defecto low), PORT (por defecto 3000), AGENCIA_PASSWORD, SECRETO_SESIONES, NEGOCIOS_DIR, META_VERIFY_TOKEN, META_APP_SECRET, IG_APP_SECRET, WA_TOKEN y META_API_VERSION.

## Forma de trabajo
Construimos por etapas. En cada una: primero un plan corto, después el código y al final cómo probarlo. Textos de la interfaz en castellano rioplatense. Explicale todo al dueño del proyecto como a alguien que no programa.
```

Cuando no tenga más dudas, escribile `Hacé un commit: Plan del producto`.

> **Tip:** el plan usa Claude Opus 5.5 para conversar. Para gastar menos, cambiá `CLAUDE_MODEL` a `claude-sonnet-5-5` en el `.env` (el cálculo de costos de abajo está hecho con Sonnet).

**Tenés que ver:** `CLAUDE.md` en la carpeta y el commit en GitHub Desktop.

## Paso 3 · La base, el primer chat y tu clave
```prompt
Etapa 1 del plan en CLAUDE.md: package.json con los scripts del plan, TypeScript y Express, el .gitignore, un .env.example sin valores y una página /chat donde escribo y Claude responde (todavía sin negocios). Creá el .env copiando el .env.example, confirmá que está en el .gitignore y abrime el .env en el editor de texto de mi compu para que pegue mi clave después de ANTHROPIC_API_KEY=. Mostrame el plan antes de programar.
```

Pegá tu clave en el editor (empieza con `sk-ant-`), guardá y escribile `listo, arrancá el servidor`. Abrí `http://localhost:3000/chat` en el navegador.

**Tenés que ver:** escribís "Hola" y el bot responde. Pedí `Hacé un commit: Etapa 1`.

## Paso 4 · Construí el resto en etapas
En cada etapa: conversación nueva (`/clear`) → pegá el pedido → aprobá su plan (y los permisos que pide) → probalo → `Hacé un commit: Etapa N`. Si algo se rompe, contale qué esperabas y qué pasó; si se complica, pedile que vuelva al último commit.

```prompt
Etapa [N] del plan en CLAUDE.md: [QUÉ, DE LA TABLA]. Sumá pruebas a npm test (sin llamar a Claude). Si necesitás una clave nueva, creá la línea vacía en el .env y abrímelo en el editor: no me la pidas en el chat. Mostrame el plan antes de programar.
```

| Etapa | Qué pedir | Tenés que ver |
|---|---|---|
| 2 | El agente con base de conocimiento: configuración del negocio en JSON con una tienda de ejemplo inventada, system prompt desde esa configuración, herramientas `buscar_en_conocimiento` y `derivar_a_humano`, conversaciones guardadas. | En `/chat`, contesta con los datos del ejemplo y, si no sabe algo, lo dice. |
| 3 | Los módulos Contactos, Pedidos y Turnos, con reglas en el código. Pruebas de stock insuficiente, precio que no coincide y turno fuera de horario. | Un pedido con código y el de stock insuficiente rechazado. |
| 4 | Varios negocios en `NEGOCIOS_DIR`, panel `/agencia` con `AGENCIA_PASSWORD`, las 4 plantillas de rubro y sesiones con `SECRETO_SESIONES` (generalo vos). | Dos negocios con plantillas distintas que no ven los datos del otro. |
| 5 | El panel de cada negocio: Bandeja con avisos, atención humana con "Devolver al bot", Registros, Conocimiento y Configuración. Que funcione en el celular. | Respondés desde la Bandeja y llega al chat. |
| 6 | El widget: `/n/<id>/widget.js` y la página `/n/<id>/ejemplo`. | Chateás desde la página de ejemplo y aparece en la Bandeja. |
| 7 | Los canales de Meta: un webhook `/webhook/meta` para WhatsApp, Instagram y Messenger, con firma y sin duplicados. Pruebas con mensajes simulados. | Las pruebas de los tres canales en OK. |
| 8 | Los avisos: `POST /agencia/api/avisos` para recordatorios de turnos y pedidos listos. | Marcás un pedido como listo y el aviso aparece en el chat. |
| 9 | `npm run demo` con tres negocios inventados (tienda, consultorio, inmobiliaria). | La demo con los tres negocios y sus registros. |
| 10 | Revisión final de seguridad y errores, `tsx` en dependencies y un README. | Pruebas en OK y el `.env` **no** aparece en GitHub Desktop. |

## Paso 5 · Probá el WhatsApp de prueba de Meta (gratis)
1. En [developers.facebook.com](https://developers.facebook.com/), **Create App** › **Connect with customers through WhatsApp** › tu portfolio.
2. En **API Setup**, **Generate access token**, agregá tu celular en **To** y verificalo. Dejá la pantalla abierta.
3. En la pestaña **Code**:

```prompt
Creá scripts/probar-whatsapp.ts y el comando npm run probar-whatsapp, que mande la plantilla hello_world por la WhatsApp Cloud API con WA_TOKEN del .env y la versión de Graph API vigente (buscala en la documentación de Meta y ponela en META_API_VERSION). Abrime el .env en el editor para que pegue el token después de WA_TOKEN=. Cuando te diga listo, pedime el Phone number ID y mi celular con código de país, y corrélo. Explicame la respuesta de Meta en castellano. Nunca me muestres el token.
```

**Tenés que ver:** `hello_world` en tu WhatsApp, mandado por tu código. El token temporal vence en horas: el permanente se crea en el Paso 7.

## Paso 6 · Publicá en Railway
1. En GitHub Desktop, **Publish repository** con **Keep this code private** marcado.
2. En [railway.com](https://railway.com), plan **Hobby**: **New Project › Deploy from GitHub repo** › `plataforma-bots`.
3. En **Variables › Raw Editor**, copiá y pegá el contenido de tu `.env` desde el editor de texto, **sin** la línea `PORT` y con `NEGOCIOS_DIR=/data/negocios`.
4. Agregá un **Volume** en `/data` (sin él, cada actualización borra los negocios).
5. **Settings › Networking › Generate Domain**. Esa dirección es `[TU-DOMINIO]`. **Deploy**.

**Tenés que ver:** `https://[TU-DOMINIO]/agencia` abre desde el celular.

## Paso 7 · Conectá Meta y salí a producción
1. En tu app de Meta, sumá **Messenger** e **Instagram**. Copiá el **App secret** e inventá un verify token; cargalos en **Variables** de Railway como `META_APP_SECRET` y `META_VERIFY_TOKEN`.
2. **WhatsApp › Configuration:** webhook `https://[TU-DOMINIO]/webhook/meta`, tu verify token, **Verify and save** y suscripción a **messages**.
3. Pegá el **Phone number ID** en la ficha del negocio, en `/agencia`, y escribile al número de prueba.
4. Para producción: número real, tarjeta en el **Billing Hub** de Meta (se puede en pesos), token permanente de un **usuario del sistema** (a Railway, nunca al chat), verificación del negocio y **App Review**.

> **Ojo:** las pantallas de Meta cambian seguido. Si no encontrás algo, pedile a Claude: "¿dónde está [LO QUE BUSCO] en Meta for Developers hoy?".

**Tenés que ver:** el bot te contesta por WhatsApp y **al día siguiente sigue contestando**.

## Paso 8 · Avisos automáticos
En [cron-job.org](https://cron-job.org), un trabajo **POST** a `https://[TU-DOMINIO]/agencia/api/avisos`, todos los días a las 10:00, usuario `agencia` y tu `AGENCIA_PASSWORD`.

**Tenés que ver:** el historial de cron-job.org con código **200**.

## Paso 9 · Tu primer negocio real
En `/agencia`, **Nuevo negocio** con la plantilla de su rubro. Para cargar lo que sabe el bot, en la pestaña **Code** abrí la carpeta de su cerebro y pedí: `Armame la configuración del negocio para la plataforma de bots a partir de bot/instrucciones-del-bot.md y del cerebro.` Conectá sus canales y pasale el link de su panel por un canal seguro.

**Tenés que ver:** el bot contesta con los datos reales y hace sus acciones.

## Cuánto cuesta por mes
Ejemplo inventado: 3 negocios, 300 conversaciones cada uno, con Claude Sonnet 5.5.

| Concepto | Por mes (nov 2026) |
|---|---|
| Servidor (Railway Hobby) | 5 USD ([precios](https://railway.com/pricing)) |
| Claude para los bots (API) | 25 a 70 USD ([precios](https://claude.com/pricing)) |
| Mensajes de WhatsApp | unos 38 USD (verificá en la [página de Meta](https://developers.facebook.com/docs/whatsapp/pricing)) |
| **Total de la operación** (sin el plan para construir) | **70 a 115 USD** |

## Cómo sé que funcionó
En `localhost:3000/chat` (o en tu dominio), preguntale algo que **no** está en la información del ejemplo:

```text
Hola, ¿hacen envíos a Ushuaia en el día?
```

No puede inventarlo: tiene que decir que no tiene ese dato y ofrecer una persona. Completa: un cliente pide por WhatsApp, aparece en **Registros** y al otro día le llega el aviso.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude rompió algo que andaba | Contale qué dejó de andar. Si no se arregla, pedile volver al último commit. |
| El bot dice "hubo un problema técnico" | Pedile a Claude que revise si la clave del `.env` tiene valor (sin mostrarla) y que la Console tenga saldo. |
| El bot inventa | Sumá ese dato a su **Conocimiento**. Si sigue, pedile a Claude reforzar la regla con una prueba. |
| Meta no acepta el webhook | Servidor prendido y verify token igual en Meta y en Railway. |
| WhatsApp dejó de contestar al otro día | Era el token temporal: creá el permanente (Paso 7). |
| Se borraron los negocios al actualizar | Falta el **Volume** en `/data` (Paso 6). |

## Para seguir solo
- **Base de datos de verdad:** con más de 10 negocios, pedile a Claude migrar de JSON a Supabase ([Cuentas en la nube](#s5-cuentas-nube)).
- **Cobros online:** sumá un link de pago al pedido, de a una cosa y con pruebas.
- **Vendelo:** con la demo de la Etapa 9 tenés qué mostrar. Tu precio: servidor + Claude + Meta + tu tiempo de soporte.
