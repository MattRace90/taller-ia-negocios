---
titulo: Tu bot de WhatsApp con dlastcrm
bloque: WhatsApp
tiempo: "90 a 120 min (bot probado; camino mínimo: 45 min) + una reunión con la agencia para conectar WhatsApp"
para: Todos (sobre todo Fondus, La Consejera del Éxito y Manuel Martínez Oratoria, que pidieron un bot de WhatsApp)
necesitas: p1-cerebro, w1-opciones
resultado: Un bot con IA dentro de dlastcrm que contesta con tu cerebro, anota lo que busca cada cliente, avisa a tu equipo cuando alguien quiere comprar, pasa la charla a una persona y queda listo para conectar a tu WhatsApp.
---

dlastcrm es el CRM que usamos en la agencia: todos los chats (WhatsApp, Instagram, la web) en una bandeja, con la ficha de cada cliente y los seguimientos automáticos. Hoy armás adentro tu bot de atención, lo entrenás con tu cerebro y lo probás sin tocar WhatsApp. Cuando pasa las pruebas, lo conectamos juntos a tu número.
Ejemplo: en Fondus, el bot contesta "¿es un préstamo?" y "¿es una estafa?" con lo que dice el cerebro, anota qué plan busca la persona y, si quiere avanzar, se la asigna a un asesor y le avisa. El asesor escribe desde la misma bandeja y el bot se calla.

> **Datos:** en el bot va cómo funciona tu negocio, no datos de clientes. Nunca le escribas CBU, alias, contraseñas ni datos personales de nadie en las instrucciones.

## Qué hace la agencia y qué hacés vos
| Lo hacés vos (en el taller o en casa) | Lo hace la agencia (con vos) |
|---|---|
| Escribir las instrucciones del bot con Claude, desde tu cerebro | Darte el usuario de dlastcrm |
| Crear el bot, la base de conocimiento, etiquetas, campos y el workflow | Conectar tu número de WhatsApp (oficial o por QR) |
| Probarlo en el panel y en la página de prueba | Elegir en qué número contesta cada bot y a qué vendedor va cada chat |
| Leer 5 conversaciones por día y ajustar | Revisar la configuración antes de prenderlo para clientes reales |
| Mantener la base al día (horarios, precios, promos) | Armar lo avanzado: varios números, stock, reportes |

## Antes de empezar
- [ ] Tu usuario y contraseña de dlastcrm (entrás por **[app.dlastcrm.com](https://app.dlastcrm.com)**). Si no lo tenés, pedíselo a Mati.
- [ ] Una computadora con Chrome (es más cómodo que el celular).
- [ ] Tu cerebro armado, con `ventas/preguntas-frecuentes.md`, `ventas/objeciones.md` y `datos/reglas.md` ([Armá el cerebro](#p1-cerebro)). Si hiciste [el agente de Telegram](#p3-agente-preguntas), también sirven `agente/prompt-del-agente.md` y `agente/conocimiento-publico.md`.
- [ ] Claude Code abierto en la carpeta del cerebro ([Instalá Claude Code](#s2-claude-code)), o Claude en el navegador con esos archivos subidos.
- [ ] Una tarjeta para cargar saldo en la billetera de la cuenta (la IA del bot se paga por uso).
- [ ] Quién de tu equipo atiende cuando el bot no sabe, y que tenga usuario en dlastcrm.

> **Costo:** dlastcrm no tiene precio de lista: se cotiza con la agencia, según cuántos usuarios y números necesitás. Si hay alguna condición especial para quienes vinieron al taller, te la confirma Mati por escrito. La **IA** del bot se paga por uso desde la billetera de la cuenta (depende de cuánto conteste el bot). **WhatsApp**: con la integración oficial, Meta cobra cada mensaje según su tarifa ([cómo se cobra](#w1-opciones)); el costo de la integración te lo pasamos al conectarla. La agencia no cobra extra por acompañarte.

> **Ojo:** si arriba ves una franja roja que dice **Your payment method is missing! Please add your card.**, falta cargar la tarjeta. Tocá **Resolve** y seguí los pasos. La recarga automática de la billetera probablemente está en **Configuración › Facturación**: verificalo en tu cuenta.

## Paso 1 · Poné la cuenta en español
1. En el menú de la izquierda, abajo de todo, tocá **Settings** (Configuración).
2. Tocá **Business Profile** (Perfil de empresa), arriba de todo.
3. En el recuadro de la derecha, en **Platform Language** (Idioma de la plataforma), escribí `Span` y elegí **Spanish**.
4. Revisá que **Time Zone** (Zona horaria) diga `America/Argentina/Buenos_Aires`.
5. Tocá el botón azul **Update** (Actualizar) al pie de ese mismo recuadro, a la derecha. El botón de la izquierda guarda otra cosa.
6. Recargá la página:

<div data-os="mac">

Tocá **Cmd + R**.

</div>
<div data-os="win">

Tocá **F5**.

</div>

> **Tip:** aunque la cuenta esté en español, algunos botones siguen en inglés ("Contacts", "Steps", "Settings"). Son los mismos.

**Tenés que ver:** el menú de la izquierda dice **Conversaciones**, **Contactos**, **Agentes de IA** y **Configuración**.

## Paso 2 · Que Claude escriba las instrucciones del bot desde tu cerebro
El bot es un empleado nuevo, muy rápido y muy literal: sabe solo lo que le escribiste y, si algo no le quedó claro, inventa. Las instrucciones son su manual. En vez de escribirlas a mano, que las saque Claude de tu cerebro.

1. Abrí la terminal (en Mac, **Terminal**; en Windows, **PowerShell**; si no sabés cómo, mirá el Paso 1 de [Instalá Claude Code](#s2-claude-code)) y abrí Claude Code en la carpeta del cerebro:

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

2. Copiá este prompt. Antes de mandarlo, cambiá `[CON / SIN]` por "con" o "sin" (¿tu marca usa emojis?) y `[NOMBRE DE QUIEN ATIENDE]` por el nombre de la persona de tu equipo que sigue la charla:

```prompt
Vas a escribir las instrucciones de un bot de atención por WhatsApp para mi negocio, que va a vivir dentro de dlastcrm (un CRM). Leé todo el cerebro: negocio/, marca/, ventas/preguntas-frecuentes.md, ventas/objeciones.md, datos/reglas.md y, si existen, agente/prompt-del-agente.md y agente/conocimiento-publico.md.

Escribí el archivo agente/dlastcrm/instrucciones-bot.md con exactamente estos 4 bloques, en español rioplatense con voseo:

BLOQUE 1: PERSONALIDAD Y ESTILO. Nombre del bot, a quién atiende, tono de mi marca. Mensajes de 2 o 3 renglones como máximo, una sola pregunta por mensaje, [CON / SIN] emojis. Si le preguntan si es un bot, dice la verdad.

BLOQUE 2: QUÉ TENÉS QUE LOGRAR. Los pasos en orden: saludar y preguntar qué busca; guardar lo que busca en el campo "Busca"; preguntar para cuándo lo necesita y guardarlo en el campo "Plazo"; responder dudas con la base de conocimiento; si quiere comprar, reservar o avanzar, usar la acción "Cliente interesado" y cerrar con un mensaje que diga que [NOMBRE DE QUIEN ATIENDE] le escribe en un rato. Después de ese mensaje no hace más preguntas. Si le preguntan algo en el medio, contesta corto y vuelve al paso en que estaba.

BLOQUE 3: DATOS DEL NEGOCIO. Nombre, dirección, horarios, qué vendemos y para quién, medios de pago, envíos o modalidad. Reglas fijas: nunca da precios ni confirma disponibilidad o stock (dice que se lo confirma [NOMBRE DE QUIEN ATIENDE]); nunca da datos bancarios, alias ni CBU y nunca confirma que un pago llegó (pasa la conversación al equipo); si no sabe algo, no lo inventa. Sumá todo lo que en datos/reglas.md y ventas/objeciones.md dice que nunca se puede decir o prometer.

BLOQUE 4: CASOS ESPECIALES. Pide hablar con una persona; reclamo o enojo; compra por mayor o empresa; proveedor, búsqueda de trabajo o encuesta; solo dice gracias o manda un emoji. Para cada uno, qué hace el bot en una línea.

Reglas para vos: no escribas montos ni números sueltos en las instrucciones (el bot los confunde). No inventes nada que no esté en el cerebro: donde falte un dato, poné [PENDIENTE: qué falta]. Que no pase de 1.500 palabras. Al final, decime la lista de PENDIENTES.
```

3. Completá los `[PENDIENTE]`. La forma más fácil: decile a Claude "Preguntame de a uno los PENDIENTE y completalos con mis respuestas".

**Tenés que ver:** el archivo `agente/dlastcrm/instrucciones-bot.md` con los 4 bloques y sin `[PENDIENTE]`.

> **Tip:** ¿no usás Claude Code? En Claude (claude.ai), creá un proyecto, subí los archivos del cerebro y pegá el mismo prompt cambiando "Escribí el archivo…" por "Devolveme el texto…".

## Paso 3 · Creá el bot
1. En el menú de la izquierda, tocá **Agentes de IA** (AI Agents).
2. Arriba, tocá la pestaña **Conversation AI**.
3. Tocá el botón azul **+ Crear agente** (Create Agent), arriba a la derecha.
4. En la ventana **Crear nuevo agente**, en **Agente basado en prompts** (a la izquierda), tocá **Crear nuevo agente**.
5. Elegí **Empezar desde cero** y tocá **Continuar**.
6. Arriba a la izquierda dice "Nuevo empleado…". Tocá el lápiz, borrá ese nombre y escribí `Bot Principal - Atención`.
7. En **Nombre de la empresa**, escribí el nombre de tu negocio.
8. Tocá **Guardar**, arriba a la derecha.
9. **Muy importante:** en la columna del medio, abrí **Modo**. Los bots nuevos vienen en **Deshabilitado** y así no contestan. Elegí **Piloto automático** y tocá **Guardar**.

**Tenés que ver:** en **Agentes de IA › Conversation AI › Lista de agentes** aparece tu bot.

## Paso 4 · Pegá las instrucciones
1. Abrí `agente/dlastcrm/instrucciones-bot.md` y copiá todo el texto.
2. En el bot, hacé clic en el recuadro grande de la izquierda y pegalo:

<div data-os="mac">

**Cmd + V**

</div>
<div data-os="win">

**Ctrl + V**

</div>

3. Tocá **Guardar**.

**Tenés que ver:** el contador de arriba (por ejemplo "548/8000 palabras") bien lejos del máximo y ningún `[ ]` en el texto.

## Paso 5 · Cargá la base de conocimiento
La base es la carpeta de consulta del bot. Las instrucciones dicen **cómo** se comporta; la base, **qué** sabe.

1. Pedile a Claude las preguntas y respuestas:

```prompt
Con el cerebro (sobre todo ventas/preguntas-frecuentes.md, ventas/objeciones.md y agente/conocimiento-publico.md si existe), armá agente/dlastcrm/base-de-conocimiento.md con las 15 preguntas que más nos hacen, cada una con su respuesta corta (2 o 3 renglones), en el tono de la marca. Formato: "P:" y "R:". Escribí la pregunta como la escribe un cliente real por WhatsApp. Nada de datos bancarios ni datos internos. Si una respuesta no está en el cerebro, no la inventes: marcala [PENDIENTE].
```

2. En dlastcrm, volvé a **Agentes de IA** y tocá la pestaña **Base de Conocimiento**.
3. Tocá **+ Crear base de conocimiento**, arriba a la derecha. En **Nombre** escribí `Preguntas frecuentes` y tocá **Añadir**.
4. Se abre la base con cinco tarjetas. En **Preguntas frecuentes**, tocá el **+**.
5. Escribí la pregunta arriba y la respuesta abajo. Tocá **Guardar**. Repetí con el **+** para cada pregunta (se guardan solas). Empezá por las 5 más importantes.
6. Conectá la base con el bot: volvé a tu bot (**Conversation AI › Lista de agentes › Bot Principal - Atención**). En la columna del medio, abrí **Activadores de la base de conocimientos** y tocá **Añadir activador**.
7. En **Seleccionar base de conocimientos**, elegí "Preguntas frecuentes". En **Instrucciones (opcional)**, pegá:

```prompt
Usala siempre que te pregunten por horarios, dirección, modalidad, envíos, medios de pago, requisitos o cómo funciona el servicio.
```

8. Tocá **Guardar** en la ventana y después **Guardar** arriba a la derecha.

> **Tip:** si algún día querés que el bot dé precios, ponelos en la base, en una sola pregunta, y actualizala el mismo día que cambian. Nunca en las instrucciones.

**Tenés que ver:** en **Activadores de la base de conocimientos** aparece tu base.

> **Tip:** **camino mínimo.** Si tenés poco tiempo, saltá al Paso 9 y probalo. Los pasos 6, 7 y 8 los hacés después.

## Paso 6 · Creá las etiquetas y los campos que llena el bot
Una **etiqueta** es una marquita para agrupar contactos. Un **campo personalizado** es un dato extra de la ficha, con un valor.

**Las etiquetas**
1. Andá a **Configuración › Etiquetas**.
2. Tocá **+ Crear etiqueta**, arriba a la derecha.
3. En **Nombre de la etiqueta**, escribí la primera y tocá **Crear etiqueta**. Esperá que se cierre la ventana y repetí con las otras:

```
bot-interesado
bot-derivar-humano
bot-reclamo
```

**Los campos**
1. Andá a **Configuración › Campos personalizados** y tocá la pestaña **Contacto**.
2. Tocá **+ Crear campo**. Revisá que **Añadir al objeto** diga **Contacto**.
3. En **Nombre del campo**, escribí `Busca`. En **Nombre de la carpeta**, elegí **Additional Info**. Tocá **Crear campo personalizado**.
4. Repetí con `Plazo`.

> **Ojo:** debajo del nombre aparece la **Clave** (por ejemplo `busca` y `plazo`). Anotala tal cual: la usás en el Paso 7. Si es distinta, usá la que ves.

**Tenés que ver:** en **Campos personalizados › Contacto** aparecen "Busca" y "Plazo", y en **Etiquetas**, las tres etiquetas.

## Paso 7 · Armá el workflow del cliente interesado
Un **workflow** es una receta automática: "cuando pasa esto, hacé esto otro". Cuando el bot detecta a alguien que quiere comprar, este workflow lo etiqueta, lo pone en el tablero de ventas, se lo asigna a la persona que atiende y le avisa.

**A. El tablero de ventas (pipeline: las columnas por las que pasa cada cliente, de "Consulta" a "Ganado")**
1. Andá a **Configuración › Clientes Potenciales & Pipelines** y tocá la pestaña **Pipelines**.
2. Tocá **+ Crear secuencia**. En **Nombre del embudo**, escribí `Ventas`.
3. Las cuatro etapas vienen en inglés. Hacé clic en cada una y escribí: `Consulta`, `Interesado`, `Propuesta`, `Ganado`.
4. Tocá **+ Añadir etapa** y escribí `Perdido`. Tocá **Crear**.

**B. El workflow**
1. En el menú de la izquierda, tocá **Automatización** (Automation).
2. Tocá **Crear carpeta**, escribí `Bot Principal` y tocá **Crear**.
3. Tocá **+ Crear flujo de trabajo** y elegí **Empezar desde cero**.
4. Arriba al centro, tocá el lápiz y escribí `Bot Principal - Cliente interesado`.
5. **No agregues un activador:** a este workflow lo dispara el bot.
6. Tocá el **+** de la línea, buscá cada acción y tocá **Guardar acción** en cada una. Estas cuatro, en orden:
   1. **Añadir etiqueta de contacto** → `bot-interesado`.
   2. **Create opportunity** (sale en inglés) → Pipeline "Ventas", Stage "Interesado".
   3. **Asignar al usuario** → la persona que atiende.
   4. **Enviar notificación interna** → Tipo **Notification**, Título `Cliente interesado`, Página de redirección **Conversación**, Para tipo de usuario **Propietarios asignados**, y en Mensaje:

```
El bot detectó un cliente interesado: {{contact.name}}. Busca: {{contact.busca}}. Plazo: {{contact.plazo}}. Entrá a Conversaciones para escribirle.
```

7. Tocá **Guardar**, arriba a la derecha, y pasá el interruptor de **Borrador** a **Publicar**.

> **Ojo:** no uses la acción **Oportunidad de crear/actualizar**: la pantalla avisa que la van a dar de baja.

**C. Conectá el bot con el workflow y los campos**
1. Volvé a tu bot. En **Acciones**, tocá **+ Configure sus acciones**.
2. Elegí **Activar un flujo de trabajo**: Nombre de la acción `Cliente interesado`; flujo "Bot Principal - Cliente interesado"; y en **Cuándo iniciar el flujo de trabajo**:

```
Cuando la persona quiere comprar, reservar o avanzar con una propuesta, después de haber preguntado qué busca y para cuándo.
```

3. Tocá **Guardar** y cerrá con la X.
4. Tocá otra vez **+ Configure sus acciones** y elegí **Información de contacto**: Nombre `Guardar lo que busca`, campo "Busca", qué actualizar `Lo que busca el cliente, en pocas palabras`, y dos ejemplos de salida (tocá **+ Añadir otro** para el segundo).
5. Sin cerrar, tocá **+ Añadir nuevo campo** y hacé lo mismo con "Plazo" (ejemplos: `este mes`, `marzo`). Tocá **Guardar**.

> **Tip:** esta acción solo llena campos vacíos. Si el cliente cambia de idea, corregilo a mano en su ficha. Cada bot admite hasta 5 acciones **Activar un flujo de trabajo**: usalas para lo importante.

**Tenés que ver:** el workflow dice **Publicado** y en **Acciones** del bot aparecen "Cliente interesado" y las dos de **Información de contacto**.

## Paso 8 · Reglas de derivación a una persona
**A. La derivación**
1. En el bot, **+ Configure sus acciones › Transferencia a humano**.
2. Vienen tres situaciones armadas, apagadas. Con **Solicitud de humano** elegida a la izquierda, activá **Habilitar escenario**.
3. Completá:
   - **Asignar Conversación a un Usuario Específico:** la persona que atiende.
   - **Destildá** "Omita la asignación si el contacto tiene un usuario asignado" (viene tildada).
   - **Mensaje final:** `Te paso con alguien del equipo para que te ayude. En un rato te escriben por acá.`
   - **Reactivar el bot después de:** 24 horas.
   - **Añada etiquetas personalizadas:** sacá la que viene y agregá `bot-derivar-humano` (en el buscador escribí `derivar`, sin el guion).
4. Tocá **Guardar**. Hacé lo mismo con **Falta de información**.

> **Ojo:** para reclamos o compras por mayor podés crear otra situación con **+ Nuevo Escenario**. No lo probamos de punta a punta: verificalo con una prueba real.

**B. Que el bot se calle cuando escribe una persona**
1. En el bot, abrí **Sincronización y ritmo**.
2. En **Mandar al bot a dormir cuando envíe un**, activá **Mensaje manual**. Dejá apagado **Mensaje de flujo de trabajo**.
3. En **Reactivar el bot después de**, poné **24 Horas** y tocá **Guardar**.

**Tenés que ver:** en Acciones aparece "Transferencia a humano" activada, y en **Sincronización y ritmo**, "Mensaje manual" con 24 horas.

## Paso 9 · Probalo en el panel (gratis, sin clientes)
1. Pedile a Claude tus casos de prueba:

```prompt
Con el cerebro, escribí agente/dlastcrm/casos-de-prueba.md: 10 mensajes como los escribe un cliente real por WhatsApp (con errores de tipeo), y para cada uno qué tiene que hacer el bot. Incluí: 3 preguntas frecuentes, 1 pregunta de precio, 1 que pida datos bancarios, 1 objeción fuerte, 1 reclamo enojado, 1 que pida hablar con una persona, 1 que quiera avanzar y 1 que no tenga nada que ver con el negocio. Si existe agente/casos-de-prueba.md de la práctica de Telegram, partí de ahí.
```

2. En la pantalla del bot, a la derecha, está **Pruebe su agente**. Escribí cada caso en **Enviar un mensaje**, de a uno.
3. Revisá: ¿una sola pregunta por mensaje? ¿No da precios ni datos bancarios? ¿Usa tus horarios reales? ¿En el reclamo te pasa con alguien?
4. Si algo está mal, corregí las instrucciones o la base, guardá y probá de nuevo.

> **Ojo:** el panel **no ejecuta los workflows**: no pone etiquetas ni avisa. Eso se prueba en el Paso 10.

**Tenés que ver:** los 10 casos con la respuesta esperada.

## Paso 10 · Prueba real con una página de chat (gratis, sin Meta)
Creás una página interna, sin dominio, con la burbuja de chat de tu bot. Nadie la encuentra salvo vos.

**A. La burbuja de chat**
1. En el menú de la izquierda, tocá **Sitios** y arriba la pestaña **Widget de chat**. Tocá **+ Nuevo** y elegí **Chat en directo**.
2. Arriba, tocá el lápiz y llamalo `Prueba del bot`.
3. A la izquierda, pestaña **Agente**: elegí "Bot Principal - Atención" y tocá **Guardar**. Aparece "Agente conectado". Tocá **Atrás**.

**B. La página de prueba**
1. En **Sitios**, pestaña **Embudos**, tocá **+ Nuevo embudo** › **Desde cero**, nombre `Prueba del bot`, **Crear**.
2. Pestaña **Configuración** (puede decir Settings): en **Widget de chat** elegí "Prueba del bot" y tocá **Guardar**, abajo.
3. Pestaña **Pasos** (puede decir Steps): **+ Agregar nuevo paso o importar**, nombre `Prueba del chat`, **Crear paso de embudo**, **Crear desde cero**.
4. En el editor, tocá **Sección en blanco**, después el ícono del disquete y **Publicar**. Tocá **Atrás**.

**C. Chateá con tu bot**
1. En el paso "Prueba del chat", tocá el ícono de abrir, al lado de **Editar**. La página se abre en otra pestaña.
2. Abajo a la derecha aparece la burbuja. Escribí como un cliente que quiere avanzar (ejemplo inventado para una agencia de viajes):

```
Hola, quería info de un viaje a Bariloche
Para julio, somos 4
Dale, quiero reservar
```

3. El bot tiene que cerrar con el mensaje de "te escribe en un rato".
4. Volvé a dlastcrm y revisá: en **Contactos** hay un contacto nuevo ("Guest Visitor…") con la etiqueta `bot-interesado`, los campos llenos y la oportunidad en "Ventas › Interesado". En la campanita de arriba a la derecha llegó el aviso.
5. Si algo no pasó: **Automatización › Bot Principal - Cliente interesado › Registros de ejecución**. Cada paso tiene que decir **Ejecutado**.

> **Tip:** la burbuja sale en inglés ("Have a question?"). No pasa nada. Si dice "Your chat has ended", tocá **CLICK HERE** para empezar otra charla.

**Tenés que ver:** contacto con etiqueta, en el pipeline, con aviso, y registros en **Ejecutado**. Tu bot funciona.

## Paso 11 · Conectá WhatsApp (con la agencia)
La conexión la hacemos con vos, para que quede bien desde el primer día. Cuando tu bot pase el Paso 10, escribile a Mati y coordinan: **Mati Carrera · WhatsApp +54 9 351 213-8791 · soy@maticarrera.com**.

La agencia ofrece las dos integraciones de WhatsApp de dlastcrm: la **oficial** (API de Meta), que recomendamos para tu número principal, y la **de QR** (no oficial, con riesgo de bloqueo), para un número nuevo o secundario. Elegimos juntos ([la comparativa completa](#w1-opciones)):

| | Integración oficial (Meta) | Integración por QR |
|---|---|---|
| Cómo se conecta | Alta guiada de Meta desde dlastcrm | Escaneás un QR con el celular, como WhatsApp Web |
| ¿Oficial? | Sí | **No** |
| Riesgo de bloqueo | Bajo | Alto si hay envíos en frío o masivos |
| Costo de mensajes | Tarifa de Meta por mensaje | Sin costo de Meta |
| Seguís usando la app en el celular | Sí, con "coexistencia" | Sí (es un dispositivo vinculado) |
| Recomendada para | Tu número principal | Un número nuevo o secundario, con cuidado |

**Qué tener listo para ese día**
- [ ] El celular con el WhatsApp del negocio, desbloqueado, con batería e internet.
- [ ] El bot probado (Paso 10).
- [ ] Saldo en la billetera de la cuenta.
- [ ] Para la integración oficial: acceso de administrador al portfolio de tu negocio en Meta (business.facebook.com) y una tarjeta para cargar en Meta.

**Si vamos por la integración oficial**
1. Desde dlastcrm iniciamos el alta guiada de Meta. Vos iniciás sesión con tu Facebook, elegís el portfolio del negocio y el número.
2. Meta te manda un código al número para confirmarlo.
3. Cargás el método de pago en Meta (en Argentina se puede en pesos).
4. Nosotros asignamos el bot a ese canal en la pestaña **Implementar** del bot.

> **Ojo:** el nombre exacto del menú de WhatsApp dentro de **Configuración** de dlastcrm y los pasos de Meta cambian seguido: los hacemos en pantalla con vos.

**Si vamos por la integración por QR**
1. La agencia suma tu cuenta al panel de la integración de WhatsApp de dlastcrm y te pasa el enlace.
2. En ese panel, en **WhatsApp Devices**, tocás el ícono de WhatsApp del dispositivo **Main**. Aparece un QR.
3. En el celular: **WhatsApp › Configuración › Dispositivos vinculados › Vincular un dispositivo**, y apuntás al QR.
4. Cuando el número aparece como **Connected**, tocás **Save Changes**. El estado pasa de **Disconnected** a **Online**.
5. Activás **Lead Capture** en el dispositivo y tocás **Save Changes**. Sin esto, solo entran chats de contactos que ya existen en el CRM.
6. La agencia configura dlastcrm para que los mensajes salgan por WhatsApp (en **Configuración › Números de teléfono › Configuración avanzada**, el proveedor de mensajes). Si no se toca **Guardar**, todo sigue saliendo por el canal anterior.

> **Ojo:** ese número queda como dispositivo por defecto para todos los envíos, salvo que un usuario esté asignado a otro. Con **+ Add Device** se suman más números, uno por vendedor.

**Cómo cuidar el número (sobre todo por QR)**
- Nada de envíos en frío: escribile solo a quien te escribió o te dejó su número. Nunca a bases compradas.
- Número nuevo, de a poco: pocos mensajes por día al principio.
- Mensajes con nombre y contexto. El mismo texto a cientos de personas es la señal más clara para que te bloqueen.
- Teléfono con batería e internet. Si se desvincula, los mensajes dejan de salir.

**Tenés que ver:** mandás un mensaje desde **Conversaciones** a otro celular, respondés desde ese celular y la respuesta aparece en dlastcrm.

## Cómo sé que funcionó
Desde un celular que no sea el del negocio, escribile al WhatsApp conectado:

```
Hola, ¿qué horario tienen? ¿Me pasan el CBU para pagar?
```

El bot tiene que contestar el horario de tu base, **no** dar datos bancarios y pasarte la conversación. En dlastcrm: el contacto con la etiqueta `bot-derivar-humano`, asignado a quien atiende, y el bot dormido cuando le respondés a mano.

**Checklist antes de prenderlo para clientes reales**
- [ ] El **Modo** del bot es **Piloto automático**.
- [ ] Las instrucciones tienen los 4 bloques, sin `[ ]` y sin montos sueltos, con la regla de no dar datos bancarios.
- [ ] La base de conocimiento está completa y conectada al bot.
- [ ] El workflow dice **Publicado** y está conectado a la acción "Cliente interesado".
- [ ] La **Transferencia a humano** está activada, asigna a alguien y tiene destildado "Omita la asignación".
- [ ] **Mandar al bot a dormir** con **Mensaje manual**, 24 horas.
- [ ] La zona horaria es la de Argentina.
- [ ] En **Implementar** solo están los canales que querés.
- [ ] Hiciste la prueba del panel y la real, y los **Registros de ejecución** dicen **Ejecutado**.
- [ ] La billetera tiene saldo.
- [ ] Tu equipo sabe que, si escribe a mano, el bot se calla 24 horas.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El bot no contesta nada | Revisá que el **Modo** sea **Piloto automático** (Paso 3) y que la billetera tenga saldo. |
| Da un precio equivocado o inventa un dato | Sacá los montos de las instrucciones. Los precios van en la base, en una sola pregunta y al día. Agregá ese caso a tus pruebas. |
| Inventó datos de pago | Falta la regla "nunca das datos bancarios ni confirmás pagos" en el Bloque 3. Agregala y probá con "pasame el CBU". |
| El workflow "no hace nada" | Quedó en **Borrador**: publicalo. El bot solo ve workflows publicados. En el panel de prueba los workflows no corren: probá con la página del Paso 10. |
| Deriva, pero nadie se entera | Usá siempre la misma etiqueta de derivación, destildá "Omita la asignación" y cargá el teléfono de cada persona en **Configuración › Usuarios**. |
| Habla encima de tu vendedor | Activá **Mensaje manual** en **Sincronización y ritmo** (Paso 8B). |
| Contesta en un número que no debía | Cada bot tiene que contestar solo en su número: revisalo con la agencia en **Implementar**. |
| (QR) El dispositivo dice **Disconnected** | Volvé a escanear el QR y revisá que el celular tenga internet. |
| (QR) Los mensajes siguen saliendo por el canal anterior | Falta elegir WhatsApp como proveedor y tocar **Guardar** (lo revisa la agencia). |
| (QR) No entran chats de números nuevos | Activá **Lead Capture** en el dispositivo y guardá. |

> **Ojo:** cuidado con tres cosas que ya nos pasaron. **Workflows en loop:** dejá **Permitir reentrada** apagado. **Workflows viejos activos:** si tu cuenta ya tenía automatizaciones publicadas (por ejemplo, un WhatsApp de bienvenida), tus pruebas las disparan; revisalas antes. **Costos:** un envío masivo o un workflow mal armado puede vaciar la billetera; probá siempre con un solo contacto.

## Para seguir solo
- **10 minutos por día:** leé 5 conversaciones del bot y anotá lo que contestó mal. Una vez por semana, pedile a Claude que te proponga los arreglos (copiá las conversaciones **sin nombres ni teléfonos**):

```prompt
Te pego 5 conversaciones de mi bot de WhatsApp (ya les saqué nombres y teléfonos) y mis notas de lo que salió mal. Leé agente/dlastcrm/instrucciones-bot.md y agente/dlastcrm/base-de-conocimiento.md. Proponeme UN solo cambio por problema: una pregunta nueva para la base o una regla nueva para las instrucciones. Mostrame el texto exacto para pegar en dlastcrm y sumá cada caso a agente/dlastcrm/casos-de-prueba.md.

[PEGÁ LAS CONVERSACIONES Y TUS NOTAS]
```

- **Varios números o varias líneas** (por ejemplo, público y mayoristas): una etiqueta de canal por número (`canal-principal`, `canal-mayorista`), un pipeline por línea y todo nombrado con la línea adelante ("Bot Mayorista - Atención"). Las etiquetas son del contacto, no del mensaje: si alguien escribió por los dos números, tiene las dos. Lo configuramos con vos.
- **Lo que viene después:** stock real, seguimientos automáticos (en Instagram, antes de las 24 horas), avisos por WhatsApp al equipo y reportes. Todo se puede, pero lleva trabajo técnico: si querés que lo armemos nosotros, escribinos.
