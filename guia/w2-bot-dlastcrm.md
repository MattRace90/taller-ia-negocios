---
titulo: Tu bot de WhatsApp con dlastcrm
bloque: WhatsApp
tiempo: "90 a 120 min (camino mínimo: 45 min) + una reunión con la agencia para conectar WhatsApp"
para: Todos (sobre todo Fondus, La Consejera del Éxito y Manuel Martínez Oratoria, que pidieron un bot de WhatsApp)
necesitas: p1-cerebro, w1-opciones
resultado: Un bot con IA dentro de dlastcrm que contesta con tu cerebro, anota lo que busca cada cliente, avisa a tu equipo, pasa la charla a una persona y queda listo para conectar a tu WhatsApp.
---

dlastcrm es el CRM de la agencia: todos los chats (WhatsApp, Instagram, la web) en una bandeja, con la ficha de cada cliente y seguimientos automáticos. Armás tu bot adentro, lo entrenás con tu cerebro y lo probás sin tocar WhatsApp. Cuando pasa las pruebas, lo conectamos juntos a tu número.
Ejemplo: en Fondus, el bot contesta "¿es un préstamo?" con lo que dice el cerebro, anota qué plan busca la persona y, si quiere avanzar, se la asigna a un asesor. El asesor escribe desde la misma bandeja y el bot se calla.

> **Ojo:** **hoy en el taller** hacés la **Versión MVP** de [Cierre: tu bot de WhatsApp](#d7-whatsapp): las instrucciones de tu bot, probadas en Telegram con n8n. Esta página es para **después**, y todo se hace en la web de dlastcrm: sin terminal.

> **Datos:** en el bot va cómo funciona tu negocio, no datos de clientes. Nunca escribas CBU, alias, contraseñas ni datos personales en las instrucciones.

## Qué hacés vos y qué hace la agencia
| Vos | La agencia (con vos) |
|---|---|
| Escribir las instrucciones con Claude, desde tu cerebro | Darte el usuario de dlastcrm |
| Crear el bot, la base, etiquetas, campos y el workflow | Conectar tu WhatsApp (oficial o por QR) |
| Probarlo y leer 5 conversaciones por día | Revisar todo antes de prenderlo para clientes reales |
| Mantener la base al día (horarios, precios, promos) | Lo avanzado: varios números, stock, reportes |

## Antes de empezar
- [ ] Tu usuario de dlastcrm (entrás por **[app.dlastcrm.com](https://app.dlastcrm.com)**). Si no lo tenés, pedíselo a Mati.
- [ ] Una computadora con Chrome.
- [ ] `bot/instrucciones-del-bot.md` de [Cierre: tu bot de WhatsApp](#d7-whatsapp), o tu cerebro con `ventas/` y `datos/reglas.md` ([Armá el cerebro](#p1-cerebro)).
- [ ] La app de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)), o Claude en el navegador con un proyecto.
- [ ] Una tarjeta para cargar saldo en la billetera de la cuenta (la IA del bot se paga por uso).
- [ ] Quién de tu equipo atiende cuando el bot no sabe, con usuario en dlastcrm.

> **Costo:** dlastcrm se cotiza con la agencia, según usuarios y números. La **IA** del bot se paga por uso desde la billetera. Con la integración oficial, **Meta** cobra cada mensaje ([cómo se cobra](#w1-opciones)). La agencia no cobra extra por acompañarte.

> **Ojo:** si arriba ves una franja roja **Your payment method is missing!**, tocá **Resolve** y cargá la tarjeta.

## Paso 1 · Poné la cuenta en español
1. Menú de la izquierda, abajo de todo: **Settings** (Configuración) › **Business Profile**.
2. En **Platform Language**, escribí `Span` y elegí **Spanish**. Revisá que **Time Zone** diga `America/Argentina/Buenos_Aires`.
3. Tocá el botón azul **Update** al pie de ese recuadro, a la derecha.
4. Recargá la página (Mac: **Cmd + R**; Windows: **F5**).

**Tenés que ver:** el menú dice **Conversaciones**, **Contactos**, **Agentes de IA** y **Configuración**. Algunos botones siguen en inglés: son los mismos.

## Paso 2 · Que Claude escriba las instrucciones desde tu cerebro
1. En la app de Claude, tocá **Code**, elegí **Local › Open folder…** y abrí `cerebro-[TU-EMPRESA]`.
2. Cambiá `[CON / SIN]` (¿tu marca usa emojis?) y `[QUIEN ATIENDE]`, y pegá:

```prompt
Escribí las instrucciones de un bot de atención por WhatsApp que va a vivir dentro de dlastcrm (un CRM). Partí de bot/instrucciones-del-bot.md si existe y completá con mi cerebro (negocio/, marca/, ventas/, datos/reglas.md). Guardalas en agente/dlastcrm/instrucciones-bot.md con 4 bloques, en rioplatense con voseo:
1. PERSONALIDAD: nombre del bot, tono de mi marca, mensajes de 2 o 3 renglones, una pregunta por mensaje, [CON / SIN] emojis. Si le preguntan si es un bot, dice la verdad.
2. QUÉ LOGRAR: saludar y preguntar qué busca (guardarlo en el campo "Busca"); preguntar para cuándo (campo "Plazo"); responder dudas con la base de conocimiento; si quiere avanzar, usar la acción "Cliente interesado" y avisar que [QUIEN ATIENDE] le escribe en un rato. Después de eso no pregunta más.
3. DATOS DEL NEGOCIO: nombre, dirección, horarios, qué vendemos, medios de pago. Nunca da precios ni confirma stock, nunca da datos bancarios ni confirma pagos, nunca inventa. Sumá lo que mi cerebro dice que no se puede prometer.
4. CASOS ESPECIALES: pide una persona, reclamo, compra por mayor, proveedor o búsqueda de trabajo, solo dice gracias. Una línea cada uno.
Sin montos ni números sueltos. Donde falte un dato, [PENDIENTE: qué falta]. Máximo 1.500 palabras. Después preguntame los PENDIENTE de a uno y completalos.
```

**Tenés que ver:** `agente/dlastcrm/instrucciones-bot.md` con los 4 bloques y sin `[PENDIENTE]`.

> **Tip:** ¿sin la pestaña Code? En Claude en el navegador, creá un proyecto, subí los archivos del cerebro y pedí "Devolveme el texto" en vez de "Guardalas".

## Paso 3 · Creá el bot y pegá las instrucciones
1. **Agentes de IA** › pestaña **Conversation AI** › **+ Crear agente** › **Agente basado en prompts** › **Crear nuevo agente** › **Empezar desde cero** › **Continuar**.
2. Tocá el lápiz de arriba a la izquierda y llamalo `Bot Principal - Atención`. Completá **Nombre de la empresa**.
3. Abrí `instrucciones-bot.md`, copiá todo y pegalo en el recuadro grande de la izquierda.
4. **Muy importante:** en la columna del medio, en **Modo**, elegí **Piloto automático** (viene en **Deshabilitado** y así no contesta).
5. Tocá **Guardar**, arriba a la derecha.

**Tenés que ver:** tu bot en **Lista de agentes** y el contador de palabras lejos del máximo.

## Paso 4 · Cargá la base de conocimiento
Las instrucciones dicen **cómo** se comporta; la base, **qué** sabe.

1. En la pestaña **Code**, pedí:

```prompt
Con mi cerebro, armá agente/dlastcrm/base-de-conocimiento.md con las 15 preguntas que más nos hacen, escritas como las escribe un cliente por WhatsApp, cada una con respuesta de 2 o 3 renglones en el tono de la marca. Formato "P:" y "R:". Nada de datos bancarios ni internos. Lo que no esté, [PENDIENTE].
```

2. En dlastcrm: **Agentes de IA** › pestaña **Base de Conocimiento** › **+ Crear base de conocimiento**, nombre `Preguntas frecuentes`, **Añadir**.
3. En la tarjeta **Preguntas frecuentes**, tocá **+**, cargá pregunta y respuesta y **Guardar**. Empezá por las 5 más importantes.
4. Volvé al bot › **Activadores de la base de conocimientos** › **Añadir activador** › elegí "Preguntas frecuentes" y en **Instrucciones (opcional)** pegá:

```prompt
Usala siempre que te pregunten por horarios, dirección, modalidad, envíos, medios de pago, requisitos o cómo funciona el servicio.
```

5. **Guardar** en la ventana y **Guardar** arriba a la derecha.

> **Tip:** los precios, si algún día los da, van en la base (una sola pregunta, al día). Nunca en las instrucciones.

**Tenés que ver:** tu base en **Activadores de la base de conocimientos**.

> **Tip:** **camino mínimo:** saltá al Paso 8 y probalo. Los pasos 5 a 7, después.

## Paso 5 · Etiquetas y campos que llena el bot
1. **Configuración › Etiquetas › + Crear etiqueta**. Creá de a una: `bot-interesado`, `bot-derivar-humano`, `bot-reclamo`.
2. **Configuración › Campos personalizados** › pestaña **Contacto** › **+ Crear campo**. Nombre `Busca`, carpeta **Additional Info**, **Crear campo personalizado**. Repetí con `Plazo`.

> **Ojo:** anotá la **Clave** que aparece debajo de cada campo (por ejemplo `busca`). Si es distinta, usá la que ves en el Paso 6.

**Tenés que ver:** las tres etiquetas y los dos campos creados.

## Paso 6 · El workflow del cliente interesado
Un **workflow** es una receta automática. Este etiqueta al interesado, lo pone en el tablero de ventas, se lo asigna a quien atiende y le avisa.

**A. El tablero de ventas.** **Configuración › Clientes Potenciales & Pipelines** › **Pipelines** › **+ Crear secuencia**. Nombre `Ventas`, etapas `Consulta`, `Interesado`, `Propuesta`, `Ganado` y, con **+ Añadir etapa**, `Perdido`. **Crear**.

**B. El workflow.** **Automatización** › **+ Crear flujo de trabajo** › **Empezar desde cero**. Llamalo `Bot Principal - Cliente interesado`. **Sin activador** (lo dispara el bot). Con el **+**, sumá en orden:
1. **Añadir etiqueta de contacto** → `bot-interesado`.
2. **Create opportunity** → Pipeline "Ventas", Stage "Interesado".
3. **Asignar al usuario** → quien atiende.
4. **Enviar notificación interna** → Tipo **Notification**, Título `Cliente interesado`, para **Propietarios asignados**, con este mensaje:

```
El bot detectó un cliente interesado: {{contact.name}}. Busca: {{contact.busca}}. Plazo: {{contact.plazo}}. Entrá a Conversaciones para escribirle.
```

**Guardar** y pasá el interruptor de **Borrador** a **Publicar**.

> **Ojo:** no uses **Oportunidad de crear/actualizar**: la van a dar de baja.

**C. Conectalo al bot.** En el bot, **Acciones › + Configure sus acciones**:
- **Activar un flujo de trabajo:** nombre `Cliente interesado`, el flujo de arriba, y en **Cuándo iniciar**: `Cuando la persona quiere comprar, reservar o avanzar, después de haber dicho qué busca y para cuándo.`
- **Información de contacto:** campo "Busca" (qué actualizar: `Lo que busca el cliente, en pocas palabras`) y, con **+ Añadir nuevo campo**, "Plazo" (ejemplos: `este mes`, `marzo`).

**Tenés que ver:** el workflow **Publicado** y las acciones en el bot.

## Paso 7 · Derivación a una persona
1. En el bot, **+ Configure sus acciones › Transferencia a humano** › **Solicitud de humano** › **Habilitar escenario**.
2. Asigná a quien atiende, **destildá** "Omita la asignación si el contacto tiene un usuario asignado", mensaje final `Te paso con alguien del equipo. En un rato te escriben por acá.`, reactivar en 24 horas y etiqueta `bot-derivar-humano`. **Guardar**. Repetí con **Falta de información**.
3. En **Sincronización y ritmo**, activá **Mensaje manual** en **Mandar al bot a dormir**, con **24 Horas**. **Guardar**.

**Tenés que ver:** "Transferencia a humano" activada y el bot se duerme 24 horas cuando escribe una persona.

## Paso 8 · Probalo (gratis, sin clientes)
1. Pedile a Claude en la pestaña **Code**: `Con mi cerebro, escribí agente/dlastcrm/casos-de-prueba.md: 10 mensajes como los escribe un cliente real (3 preguntas frecuentes, 1 de precio, 1 que pida datos bancarios, 1 objeción, 1 reclamo, 1 que pida una persona, 1 que quiera avanzar, 1 que no tenga nada que ver) y qué tiene que hacer el bot en cada uno.`
2. En el bot, a la derecha, **Pruebe su agente**: mandá cada caso.
3. Si algo sale mal, corregí instrucciones o base, guardá y repetí.

> **Ojo:** el panel de prueba **no corre los workflows**. Para probarlos: **Sitios › Widget de chat › + Nuevo › Chat en directo**, conectale tu bot en la pestaña **Agente**, y ponelo en una página de **Sitios › Embudos** (nuevo embudo desde cero, en **Configuración** elegí el widget, un paso en blanco, **Publicar**). Abrí la página, escribí como alguien que quiere reservar y revisá en **Contactos** la etiqueta, los campos y la oportunidad.

**Tenés que ver:** los 10 casos bien y, en la página de prueba, el contacto con `bot-interesado` y el aviso en la campanita.

## Paso 9 · Conectá WhatsApp (con la agencia)
Cuando tu bot pase el Paso 8, escribile a Mati: **WhatsApp +54 9 351 213-8791 · soy@maticarrera.com**. Lo conectamos juntos en pantalla.

| | Integración oficial (Meta) | Integración por QR |
|---|---|---|
| Cómo | Alta guiada de Meta desde dlastcrm | Escaneás un QR, como WhatsApp Web |
| ¿Oficial? | Sí | **No** |
| Riesgo de bloqueo | Bajo | Alto si hay envíos masivos o en frío |
| Mensajes | Tarifa de Meta | Sin costo de Meta |
| Para | Tu número principal (con "coexistencia" seguís usando la app) | Un número nuevo o secundario |

**Ese día tené listo:** el celular del negocio con batería e internet, el bot probado, saldo en la billetera y, para la oficial, acceso de administrador a tu portfolio de Meta (business.facebook.com) y una tarjeta para Meta.

**Cuidá el número (sobre todo por QR):** solo contestá a quien te escribió, nada de bases compradas, pocos mensajes por día al principio y nunca el mismo texto a cientos.

**Tenés que ver:** mandás un mensaje desde **Conversaciones**, respondés desde otro celular y la respuesta aparece en dlastcrm.

## Cómo sé que funcionó
Desde un celular que no sea el del negocio, escribile al WhatsApp conectado:

```text
Hola, ¿qué horario tienen? ¿Me pasan el CBU para pagar?
```

Tiene que contestar el horario de tu base, **no** dar datos bancarios y pasarte la conversación: el contacto con `bot-derivar-humano`, asignado a quien atiende.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El bot no contesta nada | **Modo** en **Piloto automático** y saldo en la billetera. |
| Inventa un precio o un dato | Sacá los montos de las instrucciones; los precios, en la base. Sumá ese caso a tus pruebas. |
| El workflow "no hace nada" | Quedó en **Borrador**: publicalo. En el panel de prueba no corre: usá la página de prueba. Mirá **Registros de ejecución**. |
| Deriva, pero nadie se entera | Destildá "Omita la asignación" y cargá el teléfono de cada persona en **Configuración › Usuarios**. |
| Habla encima de tu vendedor | **Mensaje manual** en **Sincronización y ritmo** (Paso 7). |
| (QR) Dice **Disconnected** | Volvé a escanear el QR y revisá que el celular tenga internet. |

> **Ojo:** dejá **Permitir reentrada** apagado en los workflows, revisá las automatizaciones viejas antes de probar y probá siempre con un solo contacto: un workflow mal armado puede vaciar la billetera.

## Para seguir solo
- **10 minutos por día:** leé 5 conversaciones. Una vez por semana, pegáselas a Claude en la pestaña **Code** (**sin nombres ni teléfonos**) y pedile: `Leé agente/dlastcrm/instrucciones-bot.md y la base. Proponeme UN cambio por problema, con el texto exacto para pegar en dlastcrm, y sumá cada caso a casos-de-prueba.md.`
- **Varios números o líneas** (público y mayoristas): una etiqueta y un pipeline por línea. Lo configuramos con vos.
- **Lo que viene:** stock real, seguimientos, avisos al equipo y reportes. Si querés que lo armemos nosotros, escribinos.
