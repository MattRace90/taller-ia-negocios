---
titulo: "Tu propia plataforma de bots (como la que armamos para un hospital)"
bloque: WhatsApp
tiempo: "En el taller: 90 min (preparar, etapas 1 y 2 y el número de prueba de Meta). Completa: de 3 a 5 días de trabajo, más las aprobaciones de Meta"
para: Quien quiera ir más allá (camino avanzado). Ideal para quien quiere vender bots a otros negocios.
necesitas: s2-claude-code, s3-herramientas-base, s4-github, s9-api-anthropic, w1-opciones
resultado: "En el taller: un bot que corre en tu computadora, contesta solo con la información del negocio, y tu primer WhatsApp enviado desde el número de prueba de Meta. Después: la plataforma completa en internet, con varios negocios, módulos (conocimiento, contactos, pedidos, turnos), paneles, WhatsApp, Instagram, Messenger, chat web y avisos automáticos."
---

Es el mismo camino que seguimos para un hospital: **tu propia plataforma de turnos**, que además sirve para pedidos, consultas y captura de interesados. La construís con Claude Code y con ella una agencia arma y maneja los bots de atención de muchos negocios de cualquier rubro (una tienda, un consultorio, una inmobiliaria, una agencia de viajes), por WhatsApp, Instagram, Messenger y la web.
No hace falta saber programar: Claude Code escribe el código y vos probás cada etapa. Pero no son 90 minutos: son **días**. En el taller hacés la base y el número de prueba de Meta; el resto, a tu ritmo. Si solo querés un bot para tu negocio, mirá antes [dlastcrm](#w2-bot-dlastcrm) o la [API oficial directa](#w1-opciones).

> **Tip:** palabras que vas a ver en esta página:
> - **Sandbox (número de prueba):** Meta te da un número de WhatsApp de prueba, gratis, que solo le escribe a los números que vos autorizás.
> - **Servidor:** la compu (tuya o alquilada en internet) donde corre la plataforma. `localhost` quiere decir "en tu propia compu".
> - **`.env`:** un archivo de texto en tu compu donde se guardan las claves. Cada línea es una **variable de entorno**: un nombre y su valor (por ejemplo `WA_TOKEN=...`).
> - **Token:** una clave larga que demuestra que sos vos ante Meta. Se cuida como una contraseña.
> - **Webhook:** la dirección de tu servidor a la que Meta le avisa cada mensaje nuevo.
> - **Módulo:** una función que cada negocio prende o apaga: Conocimiento, Contactos, Pedidos, Turnos.
> - **Commit:** una foto guardada de cómo está tu proyecto, para volver atrás si algo se rompe. Se hace en GitHub Desktop.
> - **Deploy (publicar):** subir la plataforma a internet. Acá, a Railway.
> - **JSON:** un formato de texto ordenado para guardar datos.

> **Ojo:** la regla de oro: **Claude conversa, pero el código decide.** El bot contesta solo con lo que está en la información del negocio y solo hace las acciones que el negocio activó. No puede dar un turno que no existe ni vender algo sin stock, porque eso lo calcula el código, no la IA.

> **Datos:** el bot pide solo lo mínimo para cada trámite (nombre, qué busca, día y hora). Si lo usás en un consultorio, que nunca pida ni guarde síntomas, diagnósticos ni datos de salud: sumá esa regla en "cosas que el bot nunca debe hacer" de cada negocio. Todos los negocios de ejemplo de esta página son inventados.

## Qué hace la plataforma
| Quién | Qué tiene |
|---|---|
| **Vos, la agencia** | Un panel (`/agencia`) para crear negocios, elegir qué hace cada bot, conectar sus cuentas y darles soporte. |
| **Cada negocio** | Su panel (`/n/<id>/admin`) con los mensajes, los registros (contactos, pedidos o turnos), lo que sabe el bot y la configuración. |
| **Sus clientes** | Escriben por WhatsApp, Instagram, Messenger o la web, preguntan y hacen trámites. |

**Qué bots vas a poder armar.** Cada negocio prende los módulos que necesita y se combinan (una tienda puede tomar pedidos y además guardar contactos):

| Módulo | Qué hace | Ejemplos (inventados) |
|---|---|---|
| **Conocimiento** | Contesta horarios, precios, políticas y dudas con la información del negocio. Si no lo sabe, lo dice. | Estudio contable, gimnasio, escuela |
| **Pedidos** | Muestra el catálogo, toma pedidos con su código y avisa cuando están listos. | Tienda de ropa, rotisería, ferretería |
| **Turnos** | Ofrece horarios libres, agenda, cancela y recuerda el turno el día anterior. | Consultorio, peluquería, taller |
| **Contactos** | Guarda los datos de quien pregunta para que el negocio lo llame después. | Inmobiliaria, concesionaria, academia |

## Qué hacés en el taller y qué queda para después
| En el taller (90 min) | Después (días) |
|---|---|
| **Preparar:** Pasos 1 a 3 (programas, clave de Claude, plan del producto) | **Construir:** Etapas 3 a 10 (acciones, varios negocios, paneles, chat web, canales de Meta, avisos, demo y revisión) |
| **Construir:** Etapas 1 y 2 en tu computadora (el bot ya contesta con la información del negocio) | **Publicar:** Pasos 5 y 6 (probar todo y subirlo a Railway) |
| **Sandbox:** tu primer WhatsApp desde el número de prueba de Meta, gratis | **Conectar:** Pasos 7 a 12 (app de Meta, WhatsApp, Instagram, Messenger, primer negocio real, avisos automáticos y producción) |

## Antes de empezar
- [ ] Plan Pro o Max de Claude y la app de escritorio de Claude con Claude Code ([Instalá Claude Code](#s2-claude-code)).
- [ ] Node.js (la versión LTS) instalado ([Herramientas base](#s3-herramientas-base)).
- [ ] GitHub y GitHub Desktop ([GitHub](#s4-github)).
- [ ] Clave de API de Anthropic con crédito ([API de Anthropic](#s9-api-anthropic)). Se saca en el Paso 2.
- [ ] Una cuenta de Facebook personal para entrar a Meta for Developers.
- [ ] Para después: cuenta en [Railway](https://railway.com), tarjeta para el Billing Hub de Meta, una cuenta en [cron-job.org](https://cron-job.org) y, si querés, un dominio propio.

> **Costo:** (nov 2026) Claude Pro 20 USD/mes o Max 100 USD/mes para construir. La API de Claude, por uso y prepaga. Railway, plan Hobby, unos 5 USD/mes ([precios](https://railway.com/pricing)). Meta for Developers, Instagram, Messenger, GitHub y [cron-job.org](https://cron-job.org), gratis. WhatsApp, por mensaje ([precios de Meta](https://developers.facebook.com/docs/whatsapp/pricing)). Dominio propio, de 11 a 20 USD por año. Detalle en **Cuánto cuesta por mes**, al final.

**Las claves que vas a juntar.** Van en el archivo `.env` de tu computadora y en las variables de Railway. Cuidalas como una tarjeta de crédito: **nunca** las pegues en el chat ni las subas a GitHub.

| Clave | De dónde sale |
|---|---|
| `ANTHROPIC_API_KEY` | Claude Console (Paso 2) |
| `AGENCIA_PASSWORD` | La inventás vos (Etapa 4) |
| `SECRETO_SESIONES` | La genera Claude Code (Etapa 4) |
| `META_VERIFY_TOKEN` | La inventás vos (Paso 7) |
| `META_APP_SECRET` | Tu app de Meta (Paso 7) |
| `WA_TOKEN` | Temporal en el sandbox del taller; permanente, de un usuario del sistema de Meta (Paso 8) |

> **Tip:** **Fase 1 · Preparar.** Instalás lo necesario, sacás la clave de Claude y le contás a Claude Code qué vas a construir.

## Paso 1 · Instalá los programas y creá la carpeta
1. Si no los tenés, instalá Node.js (la versión que dice **LTS**) y GitHub Desktop ([Herramientas base](#s3-herramientas-base), [GitHub](#s4-github)).
2. En **GitHub Desktop** › **File › New repository**: en **Name** escribí `plataforma-bots`; en **Local path** elegí tu carpeta **Documentos**; en **Git ignore** elegí **Node**. Tocá **Create repository**.
3. Abrí Claude Code en esa carpeta. Con la app de escritorio: abrí la app de Claude, entrá a la pestaña **Code** y elegí la carpeta `plataforma-bots` ([Instalá Claude Code](#s2-claude-code), Paso 5). O desde la terminal:

<div data-os="mac">

```bash
cd ~/Documents/plataforma-bots
claude
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\plataforma-bots
claude
```

</div>

4. Preguntale:

```prompt
¿Qué versión de Node.js tengo?
```

**Tenés que ver:** Claude Code te responde con una versión (por ejemplo `v24.x`).

## Paso 2 · Sacá la clave de Claude
1. Entrá a [platform.claude.com](https://platform.claude.com) y creá la cuenta. Como organización, poné el nombre de tu agencia.
2. En **Billing** cargá 5 o 10 USD y activá la recarga automática.
3. En **API Keys › Create Key** copiá la clave: empieza con `sk-ant-` y se ve una sola vez. Guardala en tu gestor de contraseñas (o en una nota privada). **No** se la pegues a Claude Code en el chat: en la Etapa 1 la ponés vos en un archivo. Detalle en [API de Anthropic](#s9-api-anthropic).

> **Tip:** ¿tenés Max? Trae 100 USD por mes de crédito para la API: vinculalo en **[claude.ai](https://claude.ai) › Settings › Billing**. Ese crédito sirve para que los bots conversen.

**Tenés que ver:** la clave guardada y la Console con saldo.

## Paso 3 · Pegá el plan del producto
Es la descripción completa de la plataforma. Claude Code la guarda como `CLAUDE.md` y la lee sola cada vez que empezás. Pegá esto en Claude Code y respondé sus dudas:

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

Cuando Claude Code no tenga más dudas, en GitHub Desktop escribí `Plan del producto` y tocá **Commit to main**.

> **Tip:** el plan usa Claude Opus 5.5 para conversar. El cálculo de **Cuánto cuesta por mes** está hecho con Claude Sonnet 5.5, que es más barato: si querés gastar menos, cambiá `CLAUDE_MODEL` a `claude-sonnet-5-5` en el `.env`.

**Tenés que ver:** el archivo `CLAUDE.md` en la carpeta, Claude Code sin más dudas y el commit en GitHub Desktop.

## Paso 4 · Construí en 10 etapas
**Fase 2 · Construir.** Claude Code escribe todo. Vos hacés lo mismo en cada etapa:

**Conversación nueva** (`/clear`) → **pegá el pedido** → **aprobá su plan** → **probalo** → **Commit** en GitHub Desktop.

Si algo no sale, contale qué esperabas y qué pasó. Si se complica, pedile que vuelva a la última versión guardada.

**Tenés que ver:** antes de arrancar, GitHub Desktop sin cambios pendientes (todo commiteado).

## Etapa 1 · La base y el primer chat
```prompt
Etapa 1 del plan en CLAUDE.md: la base del proyecto.
- package.json con los scripts del plan, TypeScript y Express.
- El .gitignore y un .env.example con todas las variables del plan, sin valores.
- Una página /chat donde escribo y Claude me responde, todavía sin negocios ni herramientas.
Creá el .env copiando el .env.example y decime qué línea tengo que completar yo.
Mostrame el plan antes de programar.
```

Cuando termine, pegá tu clave **a mano** en el `.env`, después de `ANTHROPIC_API_KEY=`:

<div data-os="mac">

En **Finder › Documentos › plataforma-bots**, tocá **Cmd + Shift + .** para ver los archivos ocultos. Clic derecho en `.env` › **Abrir con › TextEdit**. Pegá la clave, guardá con **Cmd + S** y cerrá.

</div>
<div data-os="win">

En el **Explorador de archivos › Documentos › plataforma-bots**, clic derecho en `.env` › **Abrir con › Bloc de notas** (si no aparece: **Abrir con › Elegir otra aplicación › Bloc de notas**). Pegá la clave, guardá con **Ctrl + G** (o **Ctrl + S**) y cerrá.

</div>

Después escribile a Claude Code `arrancá el servidor` y abrí en el navegador `http://localhost:3000/chat`.

**Tenés que ver:** escribís "Hola" y Claude te responde en el navegador. **Commit** `Etapa 1`.

## Etapa 2 · El agente y su base de conocimiento
La más importante: el bot aprende a contestar solo con la información del negocio.

```prompt
Etapa 2 del plan en CLAUDE.md: el agente con base de conocimiento.
- La configuración del negocio en un JSON con los campos del plan, y un ejemplo de tienda con preguntas frecuentes, productos y horarios inventados.
- El system prompt armado desde esa configuración.
- Las herramientas buscar_en_conocimiento y derivar_a_humano, con sus reglas en el código.
- Conversaciones guardadas en un archivo JSON.
- Si Claude falla, el cliente recibe un mensaje amable y el error queda registrado.
- npm test con pruebas que no llamen a Claude: que la búsqueda encuentre el fragmento correcto, que una configuración inválida se rechace y que la derivación respete el horario.
Mostrame el plan antes de programar.
```

Probalo en `localhost:3000/chat`: preguntale algo que está en la información (un horario, un precio) y algo que no está. Después escribile a Claude Code `corré npm test`.

**Tenés que ver:** responde con los datos del ejemplo y, si no sabe algo, lo dice en vez de inventar. Las pruebas terminan en OK. **Commit** `Etapa 2`.

## En el taller · Tu primer WhatsApp desde el número de prueba de Meta
Esto es un adelanto del Paso 8, solo para el taller: que hoy veas a tu código mandar un WhatsApp. Meta te da gratis un **número de prueba** que le escribe a unos pocos números que vos verificás. Para que Meta te **mande** los mensajes de los clientes hace falta el servidor publicado: eso queda para los Pasos 6 a 8.

1. Entrá a [developers.facebook.com](https://developers.facebook.com/) y registrate como desarrollador (con tu Facebook).
2. Tocá **Create App**, elegí **Connect with customers through WhatsApp**, elegí (o creá) tu portfolio de negocio y tocá **Create app**.
3. En **Quickstart**, tocá **Start using the API**. En **API Setup**, tocá **Generate access token**.
4. En **To**, agregá tu celular y verificalo con el código que te llega por WhatsApp. Tocá **Send message**.
5. Copiá el **token temporal** y pegalo **a mano** en el `.env`, después de `WA_TOKEN=` (como en la Etapa 1). Anotá el **Phone number ID** del número de prueba.
6. Ahora que mande Claude Code el mensaje, con tu código:

```prompt
Creá un script en scripts/probar-whatsapp.ts y un comando npm run probar-whatsapp que mande la plantilla hello_world por la WhatsApp Cloud API usando WA_TOKEN del .env, el Phone number ID y el número de destino que le paso como argumentos, y la versión de la Graph API de META_API_VERSION (buscá en la documentación oficial de Meta cuál es la vigente y ponela en el .env). Que muestre la respuesta de Meta explicada en castellano. No leas ni me muestres el token. Después decime el comando exacto para correrlo con [PHONE-NUMBER-ID] y [MI-CELULAR-CON-CÓDIGO-DE-PAÍS].
```

7. Corré el comando que te dio, con tus datos.

> **Ojo:** el token temporal vence en pocas horas. Si mañana da error de autenticación, generá otro en **API Setup**. El permanente se crea en el Paso 8.

**Tenés que ver:** el mensaje `hello_world` en tu WhatsApp, mandado por tu propio código. **Commit** `Sandbox de WhatsApp`. **Hasta acá llega el taller.** Lo que sigue lo hacés a tu ritmo, en este orden.

## Etapa 3 · Las acciones: contactos, pedidos y turnos
Los módulos que cada negocio prende o apaga, con sus reglas en el código.

```prompt
Etapa 3 del plan en CLAUDE.md: los módulos de acciones.
- Contactos, Pedidos y Turnos, cada uno con sus herramientas y sus reglas en el código, tal como dice el plan.
- Cada negocio activa solo los módulos que usa: Claude no recibe las herramientas de los módulos apagados.
- Contactos, pedidos y turnos guardados en el archivo JSON del negocio.
- Sumá a npm test: stock insuficiente, precio que no coincide con el catálogo, turno fuera de horario y que un cliente no pueda ver ni cancelar lo de otro.
Mostrame el plan antes de programar.
```

Activá **Pedidos** en la tienda de ejemplo, hacé un pedido y después pedí más unidades de las que hay.

**Tenés que ver:** el pedido queda guardado con su código, el de stock insuficiente se rechaza y las pruebas dan OK. **Commit** `Etapa 3`.

## Etapa 4 · Varios negocios y el panel de la agencia
Abrí el `.env` como en la Etapa 1 y completá `AGENCIA_PASSWORD=` con una contraseña nueva, inventada para este panel (no reutilices una que ya usás). Guardá y cerrá. Después, conversación nueva:

```prompt
Etapa 4 del plan en CLAUDE.md: varios negocios.
- Cada negocio en su carpeta dentro de NEGOCIOS_DIR, con su chat en /n/<id>/.
- Un negocio nunca puede ver datos de otro: sumá pruebas de eso a npm test.
- Panel de la agencia en /agencia, con ingreso por AGENCIA_PASSWORD: lista de negocios con la dirección del chat y del panel de cada uno, "Nuevo negocio" (nombre, rubro, plantilla de rubro y contraseña de su panel) y cambio de la contraseña de cada negocio.
- Las cuatro plantillas de rubro del plan.
- Sesiones firmadas con SECRETO_SESIONES. Generá uno al azar y guardalo en el .env.
- Pasá la tienda de ejemplo a este formato.
Mostrame el plan antes de programar.
```

Entrá a `localhost:3000/agencia` y creá dos negocios con plantillas distintas, por ejemplo **Ventas y pedidos** y **Turnos y reservas**.

**Tenés que ver:** cada bot hace solo lo de su plantilla y no ve los datos del otro. **Commit** `Etapa 4`.

## Etapa 5 · El panel de cada negocio
Bandeja de mensajes, Registros, Conocimiento y Configuración, pensado para el celular.

```prompt
Etapa 5 del plan en CLAUDE.md: el panel de cada negocio en /n/<id>/admin, con su contraseña.
- Bandeja: las conversaciones de todos los canales, primero las que esperan a una persona, con sonido, notificación del navegador y contador en la pestaña (se activan con un botón "Activar avisos").
- La atención humana del plan: responder desde la Bandeja pausa el bot con ese cliente y "Devolver al bot" lo reactiva. El chat web muestra los mensajes que manda una persona del negocio.
- Registros: contactos, pedidos (con cambio de estado: nuevo, en preparación, listo, entregado) y turnos, según los módulos activos.
- Conocimiento: editar preguntas frecuentes, textos y catálogo. El bot usa los cambios al instante.
- Configuración: datos del negocio, módulos activos y reglas, validados antes de guardar.
- En el panel de la agencia: quién espera a una persona en cada negocio y un botón "Entrar al panel" que abre el panel de ese negocio sin pedir su contraseña.
Diseño limpio y que funcione en el celular. Mostrame el plan antes de programar.
```

Probá escribir en el chat "Quiero hablar con una persona", respondé desde la Bandeja y tocá **Devolver al bot**. Después sumá una pregunta frecuente en **Conocimiento** y hacésela al bot.

**Tenés que ver:** tu respuesta llega al chat y el bot ya usa la pregunta nueva. **Commit** `Etapa 5`.

## Etapa 6 · El chat para la web del negocio
Una línea que el negocio pega en su sitio y aparece un botón de chat.

```prompt
Etapa 6 del plan en CLAUDE.md: el widget.
- /n/<id>/widget.js: una línea para pegar en cualquier web, que muestra un botón y abre el chat del negocio.
- /n/<id>/ejemplo: una página de ejemplo con el widget puesto.
- En el panel de la agencia, un botón para copiar la línea del widget de cada negocio.
Que no rompa los estilos de la web donde se pega. Mostrame el plan antes de programar.
```

Probalo en la página de ejemplo: la dirección del chat terminada en `/ejemplo`.

**Tenés que ver:** chateás desde la página de ejemplo y la conversación aparece en la Bandeja. **Commit** `Etapa 6`.

## Etapa 7 · WhatsApp, Instagram y Messenger
Meta solo le habla a servidores publicados, así que acá se prueba con mensajes simulados. La prueba real es en los Pasos 8 y 9.

```prompt
Etapa 7 del plan en CLAUDE.md: los canales de Meta.
- Un solo webhook en /webhook/meta para WhatsApp Cloud API, Instagram y Messenger, con verificación por META_VERIFY_TOKEN y control de la firma con META_APP_SECRET o IG_APP_SECRET.
- Responder 200 enseguida, ignorar mensajes repetidos por su id y procesar un mensaje por vez por cliente.
- Asignar cada mensaje a su negocio por phone_number_id, id de cuenta de Instagram o id de página, e ignorar ecos y avisos de lectura.
- Mandar las respuestas por el mismo canal, con WA_TOKEN o el token propio del negocio.
- En el panel de la agencia, en la ficha de cada negocio: Phone number ID de WhatsApp, id y token de la página de Facebook, e id y token de la cuenta de Instagram.
- Que la Bandeja muestre de qué canal es cada conversación.
- Pruebas en npm test con mensajes simulados de los tres canales.
Usá la versión vigente de la Graph API de Meta, configurable con META_API_VERSION. Mostrame el plan antes de programar.
```

**Tenés que ver:** las pruebas de los tres canales terminan en OK. **Commit** `Etapa 7`.

## Etapa 8 · Los avisos a los clientes
El recordatorio del turno de mañana y el aviso de "tu pedido está listo".

```prompt
Etapa 8 del plan en CLAUDE.md: los avisos.
- POST /agencia/api/avisos con autenticación básica (usuario "agencia", contraseña AGENCIA_PASSWORD): manda los recordatorios de los turnos de mañana y los avisos de pedidos que pasaron a "listo", en todos los negocios, por el canal de cada cliente, y devuelve cuántos mandó por negocio.
- Un pedido marcado como listo en el panel avisa al cliente en ese momento.
- El cliente responde y el bot sigue la conversación con sus herramientas (por ejemplo, confirmar o cancelar un turno).
- En Instagram y Messenger, no mandarlo si pasaron más de 23 horas desde el último mensaje del cliente.
- Un botón en el panel de cada negocio para mandar los avisos a mano, y que los avisos también aparezcan en el chat web.
Mostrame el plan antes de programar.
```

Hacé un pedido en el chat web y marcalo como **listo** en **Registros**.

> **Ojo:** en WhatsApp, pasadas 24 horas desde el último mensaje del cliente, solo se pueden mandar **plantillas** aprobadas por Meta. Las plantillas para los avisos se suman en el Paso 12.

**Tenés que ver:** el aviso de pedido listo aparece en el chat. **Commit** `Etapa 8`.

## Etapa 9 · Los negocios de ejemplo
Una demo con tres negocios inventados, cada uno con un tipo de bot distinto, para probar todo y mostrársela a un posible cliente.

```prompt
Etapa 9 del plan en CLAUDE.md: npm run demo.
- Que arranque el servidor con tres negocios inventados en data/demo-negocios, separados de los reales: una tienda de ropa con Pedidos (id tienda-demo), un consultorio con Turnos (id consultorio-demo) y una inmobiliaria con Contactos (id inmobiliaria-demo).
- Con conversaciones de los tres canales, alguien esperando a una persona, y pedidos, turnos y contactos cargados.
- Que borre y vuelva a crear sus datos cada vez que arranca, y que muestre en la consola la contraseña de sus paneles.
Mostrame el plan antes de programar.
```

**Tenés que ver:** la demo muestra los tres negocios, cada uno con sus registros. **Commit** `Etapa 9`.

## Etapa 10 · La revisión final
Claude Code revisa la seguridad y los errores como lo haría otra persona.

```prompt
Etapa 10 del plan en CLAUDE.md: revisión antes de publicar.
- Revisá la seguridad: contraseñas, sesiones, firma de los mensajes de Meta, que nadie pueda entrar al panel de otro negocio y que el .env no se suba a GitHub.
- Revisá que el bot no pueda usar herramientas de módulos apagados ni ver datos de otros clientes.
- Buscá errores en el código y arreglá los importantes.
- Comprobá que npm start funcione en un servidor con NEGOCIOS_DIR=/data/negocios y que tsx esté en dependencies.
- Escribí un README con cómo arrancarlo, las variables y cómo está armado.
Explicame qué encontraste y qué cambiaste.
```

**Tenés que ver:** las pruebas dan OK y GitHub Desktop **no** muestra el `.env` entre los cambios. **Commit** `Etapa 10`.

> **Tip:** **Fase 3 · Publicar.** Probás todo en tu computadora y lo subís a internet para que Meta le pueda avisar de cada mensaje.

## Paso 5 · Probá todo en tu computadora
1. Escribile a Claude Code `arrancá la demo`.
2. Entrá a `localhost:3000/agencia` con tu `AGENCIA_PASSWORD`.
3. Hacé de cliente en `localhost:3000/n/tienda-demo/` y hacé un pedido.

**Tenés que ver:** el pedido aparece en los **Registros** de la tienda.

## Paso 6 · Subilo a internet con Railway
1. En GitHub Desktop tocá **Publish repository**, con **Keep this code private** marcado.
2. En [railway.com](https://railway.com), plan **Hobby**: **New Project › Deploy from GitHub repo** y elegí `plataforma-bots`.
3. En **Variables › Raw Editor** pegá el contenido de tu `.env`, **sin** la línea de `PORT` y con `NEGOCIOS_DIR=/data/negocios`. Railway es el único lugar fuera de tu compu donde van las claves: ahí quedan guardadas en secreto.
4. Agregá un **Volume** montado en `/data`. Sin él, cada actualización borra los negocios.
5. En **Settings › Networking** tocá **Generate Domain**. Esa dirección es `[TU-DOMINIO]`. Tocá **Deploy**.

**Tenés que ver:** `https://[TU-DOMINIO]/agencia` abre desde el celular.

> **Tip:** **Fase 4 · Conectar y salir a producción.** Una sola app de Meta, la de tu agencia, recibe los mensajes de todos los negocios. Lo que más demora son las aprobaciones de Meta.

## Paso 7 · Creá la app de Meta
1. Creá (o usá) el portfolio comercial en [business.facebook.com](https://business.facebook.com) y registrate en [developers.facebook.com](https://developers.facebook.com/).
2. **Create App** con tres casos de uso: **WhatsApp**, **Messenger** e **Instagram**. Si ya creaste la app en el taller (sandbox), usá esa y sumale Messenger e Instagram.
3. Copiá el **App secret** (en la configuración básica de la app) a `META_APP_SECRET` e inventá un `META_VERIFY_TOKEN`. Cargá los dos en **Variables** de Railway.
4. Completá la URL de la política de privacidad y publicá la app.

> **Ojo:** los nombres de las pantallas de Meta cambian seguido. Si no encontrás algo, pedile a Claude: "¿dónde está [LO QUE BUSCO] en Meta for Developers hoy?", que busque en la documentación oficial.

**Tenés que ver:** la app publicada y las dos claves en Railway.

## Paso 8 · Conectá WhatsApp
1. Primero gratis, con el número de prueba: en **WhatsApp › API Setup**, sumá tu celular y copiá el token temporal a `WA_TOKEN` en Railway.
2. En **WhatsApp › Configuration**, webhook `https://[TU-DOMINIO]/webhook/meta`, tu verify token, **Verify and save** y suscripción al campo **messages**.
3. Pegá el **Phone number ID** en la ficha del negocio, en el panel de la agencia, y escribile al número de prueba desde tu celular.
4. Después: número real, tarjeta en el **Billing Hub** de Meta (en Argentina se puede en pesos) y un token que no vence (un **usuario del sistema** de tu portfolio).

**Tenés que ver:** el bot te contesta por WhatsApp y **al día siguiente sigue contestando**.

## Paso 9 · Conectá Instagram y Messenger
Son gratis y van por la Página de Facebook del negocio.
1. **Messenger:** mismo webhook, token de la Página y suscripción a **messages**.
2. **Instagram:** cuenta profesional vinculada a la Página, con **Permitir acceso a los mensajes** activado en la app de Instagram.

**Tenés que ver:** le escribís a la Página y a la cuenta, y el bot contesta en los dos.

## Paso 10 · Probá la plataforma con un negocio real
1. En el panel de la agencia, **Nuevo negocio**, con la plantilla de su rubro.
2. Cargá lo que sabe el bot: preguntas frecuentes, productos o servicios, horarios y políticas. Activá los módulos que usa. Si el negocio tiene su cerebro armado ([Armá el cerebro](#p1-cerebro)), pedile a Claude que te arme la configuración desde ahí.
3. Conectá sus canales, pegá la línea del widget en su web y pasale el link de su panel y la contraseña (por un canal seguro).

**Tenés que ver:** el bot contesta con los datos reales del negocio y hace sus acciones.

## Paso 11 · Avisos automáticos
1. En [cron-job.org](https://cron-job.org), creá un trabajo **POST** a `https://[TU-DOMINIO]/agencia/api/avisos`, todos los días a las 10:00.
2. Usuario `agencia` y, como contraseña, tu `AGENCIA_PASSWORD`.

**Tenés que ver:** el historial de [cron-job.org](https://cron-job.org) muestra el código **200**.

## Paso 12 · Pasá a producción
1. Verificá tu negocio en Meta y pedí la revisión de la app (**App Review**), con un video del bot funcionando.
2. Para usar el WhatsApp de tus clientes desde tu app: alta como **Tech Provider** y registro integrado (Embedded Signup).
3. Pedile a Claude Code lo que falta, de a una cosa: plantillas de WhatsApp para los avisos, registro integrado, base de datos y, si hace falta, cobros online.

**Tenés que ver:** alguien sin ningún rol en tu app de Meta le escribe al bot y recibe respuesta.

## Cuánto cuesta por mes
Ejemplo (inventado): 3 negocios con 300 conversaciones cada uno, usando Claude Sonnet 5.5. Es una estimación: el gasto real se ve en la Console después de la primera semana.

| Concepto | Por mes (nov 2026) |
|---|---|
| Servidor (Railway Hobby) | 5 USD ([precios](https://railway.com/pricing)) |
| Claude para los bots (API) | 25 a 70 USD ([precios](https://claude.com/pricing)) |
| Mensajes de WhatsApp | unos 38 USD (tarifas de Argentina según proveedores; verificá en la [página de Meta](https://developers.facebook.com/docs/whatsapp/pricing)) |
| Instagram, Messenger, GitHub, [cron-job.org](https://cron-job.org) | Gratis |
| Plan de Claude para construir | 20 (Pro) o 100 (Max) USD |
| **Total de la operación** (sin el plan para construir) | **70 a 115 USD** |

> **Costo:** si la información de un negocio es muy larga, cada conversación cuesta un poco más. Con Max, sus 100 USD de crédito para la API alcanzan para el consumo de Claude de este ejemplo con Sonnet. Desde el 1/10/2026 Meta cobra los mensajes de servicio después de los primeros 1.000 por número y por mes ([detalle](#w1-opciones)).

## Cómo sé que funcionó
**En el taller:** en `localhost:3000/chat`, preguntale al bot algo que **no** está en la información del ejemplo:

```text
Hola, ¿hacen envíos a Ushuaia en el día?
```

El bot no puede inventarlo: tiene que decir que no tiene ese dato y ofrecer pasarte con una persona. Y tenés el `hello_world` en tu WhatsApp, mandado por tu código.

**Completa:** un cliente escribe por WhatsApp, hace un pedido o saca un turno, aparece en los **Registros** del negocio y, al día siguiente, le llega el aviso.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude Code rompió algo que andaba | Contale qué dejó de funcionar. Si no se arregla, pedile que vuelva a la última versión guardada (el último commit). |
| Llegaste al límite de uso de Claude Code | Esperá a que se renueve o pasá a Max. |
| El bot dice "hubo un problema técnico" | Revisá la clave en el `.env` y que la Console tenga saldo. Después reiniciá el servidor. |
| El bot inventa una respuesta | Agregá ese dato a su **Conocimiento**. Si sigue inventando, pedile a Claude Code que lo refuerce en las reglas, con una prueba en `npm test`. |
| Meta no acepta el webhook | Fijate que el servidor esté prendido y que el verify token sea igual en Meta y en Railway. |
| WhatsApp dejó de contestar al otro día | Era el token temporal. Creá el permanente (Paso 8). |
| Se borraron los negocios al actualizar | Falta el **Volume** en `/data` (Paso 6). |

## Para seguir solo
- **Base de datos de verdad.** Los archivos JSON sirven para el MVP. Con más de 10 negocios, pedile a Claude Code migrar a una base de datos (por ejemplo, Supabase, ver [Cuentas en la nube](#s5-cuentas-nube)).
- **Cobros online.** El módulo Pedidos no cobra: el pago se coordina aparte. Cuando un negocio lo pida, pedile a Claude Code sumar un link de pago al pedido, de a una cosa y con pruebas.
- **Vendelo.** Con la demo de la Etapa 9 tenés algo para mostrarle a un posible cliente. Calculá tu precio con la tabla de costos: servidor + Claude + mensajes de Meta + tu tiempo de soporte.
