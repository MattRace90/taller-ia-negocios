---
titulo: "Cierre: tu bot de WhatsApp"
bloque: Desafío
tiempo: 60 min (16:30 a 17:30)
para: Todos
necesitas: p1-cerebro
resultado: Elegiste cómo vas a tener tu bot de WhatsApp, viste dos demos en vivo y te vas con el documento de instrucciones de tu bot escrito desde tu cerebro y probado.
---

Tus clientes están en WhatsApp. Es el cierre del día y lo hacemos todos juntos, hayas elegido el desafío que hayas elegido.
WhatsApp no se arma en una hora. Meta pide verificar el negocio, un número solo para el bot y plantillas aprobadas (mensajes armados de antemano que Meta revisa). Pero lo más difícil no es técnico: es **qué tiene que decir tu bot**. Eso sí lo resolvés hoy, y te lo llevás escrito.

**En 30 segundos**
- **Qué te llevás:** sabés qué opción de WhatsApp te conviene y tenés el documento de instrucciones de tu bot, escrito desde tu cerebro y probado.
- **Cuánto tarda:** 60 min, todos juntos (16:30 a 17:30).
- **Por dónde empezar:** mirá la tabla de abajo. A las 17:05 vas directo a **Escribí las instrucciones de tu bot**.

## Qué problema resuelve
- Consultas de WhatsApp que esperan horas o se pierden fuera de horario.
- Varias personas contestando lo mismo de formas distintas, o un solo número para todo el equipo.
- No saber qué opción de bot contratar ni cuánto cuesta.

## Los 3 momentos del cierre

| Hora | Qué pasa | Página |
|---|---|---|
| 16:30 | **Elegí tu camino.** Repasamos el menú de opciones de abajo: dlastcrm (el CRM de la agencia, oficial o por QR), la API oficial de Meta, tu propia plataforma, Zernio, Unipile y Evolution API. Pros, contras, riesgo de bloqueo y costos. | [Opciones de WhatsApp](#w1-opciones) |
| 16:45 | **Dos demos en vivo.** Un bot con dlastcrm y una plataforma propia, como la que armamos para un hospital: tu propia plataforma de turnos. Mirá, preguntá, no hace falta que lo hagas a la par. | [Bot con dlastcrm](#w2-bot-dlastcrm) · [Plataforma propia](#w3-bot-propio) |
| 17:05 | **Escribí las instrucciones de tu bot** desde tu cerebro y probalas. Esto lo hace cada uno. | Esta página, abajo |

## El menú: 6 opciones para tu bot
dlastcrm tiene dos formas de conectar, por eso hay 7 filas. Cada opción tiene su página con el paso a paso.

| Opción | En una línea | Tiempo | Costo (nov 2026) | Paso a paso |
|---|---|---|---|---|
| **1a. dlastcrm, integración oficial** | El CRM de la agencia: bandeja para todo el equipo, bot con IA y seguimientos. Oficial de Meta: la recomendada para tu número principal. | 90 a 120 min el bot + una reunión con la agencia para conectar | Se cotiza con la agencia + IA por uso + mensajes de Meta | [Bot con dlastcrm](#w2-bot-dlastcrm) |
| **1b. dlastcrm, integración por QR** | El mismo CRM, conectado escaneando un QR. Rápido y sin costo de Meta, pero **no oficial**: riesgo de bloqueo. Solo número secundario. | 90 a 120 min el bot + una reunión con la agencia para conectar | Se cotiza con la agencia + IA por uso | [Bot con dlastcrm](#w2-bot-dlastcrm) |
| **2. API oficial de Meta, directa** | Tu agente de Telegram de la práctica, pasado a WhatsApp sin intermediarios. | 1 a 2 horas, con la práctica hecha | Solo los mensajes de Meta (el Worker es gratis para empezar) | [De Telegram a WhatsApp](#w1-opciones) |
| **3. Tu propia plataforma** | Como la que armamos para un hospital: tu propia plataforma de turnos (y pedidos, consultas o contactos), para vender bots a muchos negocios. | Hoy 90 min (la base y el número de prueba); completa, 3 a 5 días | 70 a 115 USD/mes en el ejemplo de 3 negocios | [Plataforma propia](#w3-bot-propio) |
| **4. Zernio** | Vía oficial de Meta con alta guiada, MCP para Claude Code y número de prueba gratis. | 60 min con su número de prueba | Gratis hasta 2 cuentas y 10.000 mensajes + Meta aparte | [Zernio](#w4-zernio) |
| **5. Unipile** | Conecta tu WhatsApp por QR con una API. **No oficial**: riesgo alto. Solo número secundario. | 60 a 90 min | 49 EUR/mes (~55 USD), prueba de 7 días gratis | [Unipile](#w5-unipile) |
| **6. Evolution API** | Programa gratis que instalás vos, con Docker. Modo QR (no oficial) o Cloud API (oficial). | 2 a 3 horas en tu compu | Gratis; servidor ~11 a 12 USD/mes | [Evolution API](#w6-evolution-api) |

> **Tip:** también existe el agente de IA que hace Meta (Meta Business Agent), sin programar pero sin tu cerebro. Lo comparamos en [Opciones de WhatsApp](#w1-opciones).

## Elegí tu camino
Mientras ves las opciones, tildá lo que aplica a tu negocio:
- [ ] Quiero que el bot **conteste solo**, o que **ayude a mi equipo** a contestar más rápido.
- [ ] Varias personas tienen que atender **el mismo número**.
- [ ] Necesito que el bot **agende** (turnos, reuniones, visitas).
- [ ] Tengo (o puedo conseguir) **un número solo para el negocio**, que no sea mi WhatsApp personal.
- [ ] Sé cuántas conversaciones por mes recibo, para estimar el costo.
- [ ] Prefiero **no programar ni mantener** nada técnico.

> **Ojo:** las opciones que conectan tu WhatsApp escaneando un código QR (dlastcrm por QR, Unipile y Evolution API en modo Baileys) no son oficiales y pueden hacer que WhatsApp te bloquee el número. La agencia ofrece las dos integraciones de dlastcrm: la **oficial** de Meta, que recomendamos para tu número principal, y la **de QR**, solo para un número que no te importe perder. Antes de elegir, leé el riesgo en [Opciones de WhatsApp](#w1-opciones).

## Escribí las instrucciones de tu bot
Sea cual sea la opción, tu bot necesita lo mismo: un documento que diga quién es, qué responde, qué nunca dice y cuándo pasa la conversación a una persona. Lo escribe Claude **leyendo tu cerebro**. Si hiciste el [desafío del agente](#d2-agente), partí de ese prompt: este documento lo completa para WhatsApp.

1. Abrí la terminal (en Mac, **Terminal**; en Windows, **PowerShell**; si no sabés cómo, mirá el Paso 1 de [Instalá Claude Code](#s2-claude-code)) y abrí Claude Code en la carpeta de tu cerebro:

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

Cambiá `[TU-EMPRESA]` por el nombre de tu carpeta del cerebro (el que usaste en [Tu cerebro](#p1-cerebro)).

**Tenés que ver:** Claude Code abierto y, arriba, el nombre de tu carpeta del cerebro.

2. Pegá este prompt:

```prompt
Escribí el documento de instrucciones del bot de WhatsApp de mi empresa y guardalo en bot/instrucciones-del-bot.md. Usá SOLO lo que dice mi cerebro (CLAUDE.md, ventas/, negocio/, marca/). Lo que no esté, marcalo PENDIENTE: no inventes. Si ya existe un prompt de agente en esta carpeta, partí de ese.

Secciones:
1. Quién es el bot: nombre, de qué empresa, a quién atiende y su objetivo principal (por ejemplo: responder dudas y agendar, o calificar y pasar al vendedor).
2. Cómo habla: tono, vos o tú, largo máximo de cada mensaje (corto, como un WhatsApp), emojis sí o no, con 2 ejemplos sacados de marca/voz.md.
3. Mensaje de bienvenida y mensaje fuera de horario (con nuestro horario de atención).
4. Qué responde: cada pregunta frecuente con su respuesta oficial, en formato pregunta → respuesta.
5. Objeciones: objeción → cómo se responde.
6. Qué NUNCA dice ni promete: precios no confirmados, plazos, resultados, descuentos, temas legales o regulatorios, y cualquier regla de mi CLAUDE.md.
7. A quién no le vendemos y cómo se lo dice con respeto.
8. Qué datos pide para avanzar (solo los mínimos) y qué datos nunca pide (DNI, tarjetas, claves, datos de salud).
9. Cuándo pasa a una persona: lista de situaciones, a quién, en qué horario y el mensaje que manda al pasar.
10. Seguimiento: hasta 3 mensajes modelo para escribirle a alguien que no respondió, sabiendo que pasadas 24 horas WhatsApp solo deja mandar plantillas aprobadas.
11. 10 casos de prueba: mensaje del cliente → qué tiene que hacer el bot. Incluí 2 que no sean clientes, 1 enojado, 1 que pide algo que no hacemos y 1 que quiere comprar ya.
12. Pendientes: lo que falta definir antes de prenderlo.

Máximo 2 páginas. Al final, decime cuántos PENDIENTE quedaron.
```

**Tenés que ver:** Claude te avisa que creó `bot/instrucciones-del-bot.md` y te dice cuántos PENDIENTE quedaron.

3. Probalo con un juego de roles. Pegá esto en el mismo chat:

```prompt
Ahora actuá como el bot, siguiendo SOLO bot/instrucciones-del-bot.md. Yo soy un cliente. Cuando escriba "FIN", salí del personaje y decime qué respondiste mal y qué cambiarías en el documento.
```

Jugá 5 de los 10 casos de prueba. Lo que salga mal, corregilo en el documento: "Cambiá la sección 6: el bot nunca menciona [X]."

**Tenés que ver:** el bot te contestó como cliente, al escribir FIN te dijo qué corregir, y el archivo `bot/instrucciones-del-bot.md` tiene sus 12 secciones y pocos pendientes.

> **Tip:** este documento es lo que vas a cargar en la plataforma que elijas, sea dlastcrm, la API oficial u otra. Guardalo con el resto del cerebro, en tu GitHub **privado** ([Tu cerebro](#p1-cerebro), Paso 6). No tiene claves ni datos de clientes, así que puede ir ahí.

## Qué cuentas necesitás
- [ ] Hoy: solo Claude Code y tu cerebro.
- [ ] Para prenderlo después: un número dedicado al negocio, una cuenta de Meta Business ([Meta y Google](#s14-meta-y-google)) y la plataforma que elijas ([Opciones de WhatsApp](#w1-opciones)).

## Lo lograste si…
- [ ] Sabés qué opción de WhatsApp te conviene y por qué.
- [ ] Tenés `bot/instrucciones-del-bot.md` escrito desde tu cerebro.
- [ ] Lo probaste con al menos 5 casos y corregiste lo que falló.
- [ ] La lista de pendientes del bot tiene responsable y fecha.
- [ ] Sabés cuánto te va a costar por mes, aunque sea aproximado.

## Ideas por tipo de negocio
Ejemplos inventados:
- **Venta consultiva:** califica con 4 o 5 preguntas, aclara lo que el producto no es y agenda la videollamada con el vendedor.
- **Escuela o cursos:** responde fechas, lugar y formas de pago, y anota al interesado en la próxima cohorte.
- **Coaching o formación:** responde dudas del programa en la voz de la docente y pasa a una persona a quien pregunta por cuotas.
- **Agencia de viajes:** junta los datos para cotizar y avisa a la vendedora que corresponde.
- **Producción y reparto:** toma pedidos con zona y día de entrega, y manda el resumen al que reparte.
- **Marketplace o app:** responde a los locales interesados y agenda una llamada para darlos de alta.

## Pedí ayuda a la mesa cuando…
- No sabés qué opción elegir: contanos tu caso y te orientamos.
- El documento sale lleno de PENDIENTE: es señal de que al cerebro le faltan respuestas. Lo vemos juntos.
- Querés saber cuánto cuesta dlastcrm para tu equipo: no tiene precio de lista, se cotiza con la agencia.
