---
titulo: "Cierre: tu bot de WhatsApp"
bloque: Desafío
tiempo: 60 min (16:30 a 17:30)
para: Todos
necesitas: p1-cerebro
cuentas_mvp: s6-n8n, s7-telegram
cuentas_completa: s14-meta-y-google
resultado: Elegiste cómo vas a tener tu bot de WhatsApp, viste dos demos en vivo y te vas con las instrucciones de tu bot escritas desde tu cerebro y probadas en un bot de Telegram.
---

Tus clientes están en WhatsApp. Es el cierre del día y lo hacemos todos juntos.
WhatsApp no se arma en una hora: Meta pide verificar el negocio, un número solo para el bot y plantillas aprobadas (mensajes armados de antemano que Meta revisa). Pero lo más difícil no es técnico: es **qué tiene que decir tu bot**. Eso lo resolvés hoy.

**En 30 segundos**
- **Qué te llevás:** sabés qué opción de WhatsApp te conviene y tenés las instrucciones de tu bot, escritas desde tu cerebro y probadas.
- **Cuánto tarda:** 60 min, todos juntos (16:30 a 17:30).
- **Por dónde empezar:** a las 17:05, la **Versión MVP**, acá abajo.

## Los 3 momentos del cierre

| Hora | Qué pasa | Página |
|---|---|---|
| 16:30 | **El menú de opciones**: pros, contras, riesgo de bloqueo y costos. | [Opciones de WhatsApp](#w1-opciones) |
| 16:45 | **Dos demos en vivo**: un bot con dlastcrm y una plataforma propia de turnos, como la que armamos para un hospital. Mirá y preguntá. | [Bot con dlastcrm](#w2-bot-dlastcrm) · [Plataforma propia](#w3-bot-propio) |
| 17:05 | **Las instrucciones de tu bot**, escritas y probadas. Cada uno. | Versión MVP, abajo |

## El menú: 6 opciones para tu bot
dlastcrm tiene dos formas de conectar, por eso hay 7 filas.

| Opción | En una línea | Costo (nov 2026) | Paso a paso |
|---|---|---|---|
| **1a. dlastcrm, oficial** | El CRM de la agencia: bandeja para todo el equipo, bot con IA y seguimientos. La recomendada para tu número principal. | Se cotiza con la agencia + IA por uso + mensajes de Meta | [Bot con dlastcrm](#w2-bot-dlastcrm) |
| **1b. dlastcrm, por QR** | El mismo CRM, conectado con un QR. **No oficial**: riesgo de bloqueo. Solo número secundario. | Se cotiza con la agencia + IA por uso | [Bot con dlastcrm](#w2-bot-dlastcrm) |
| **2. API oficial de Meta** | Tu agente de Telegram pasado a WhatsApp, sin intermediarios. | Solo los mensajes de Meta | [Opciones de WhatsApp](#w1-opciones) |
| **3. Tu propia plataforma** | Turnos, pedidos o consultas, para vender bots a muchos negocios. | 70 a 115 USD/mes en el ejemplo de 3 negocios | [Plataforma propia](#w3-bot-propio) |
| **4. Zernio** | Vía oficial con alta guiada, MCP para Claude Code y número de prueba gratis. | Gratis hasta 2 cuentas y 10.000 mensajes + Meta aparte | [Zernio](#w4-zernio) |
| **5. Unipile** | Tu WhatsApp por QR con una API. **No oficial**: riesgo alto. | 49 EUR/mes (~55 USD), prueba de 7 días | [Unipile](#w5-unipile) |
| **6. Evolution API** | Programa gratis que instalás vos. Modo QR (no oficial) o Cloud API (oficial). | Gratis; servidor ~11 a 12 USD/mes | [Evolution API](#w6-evolution-api) |

> **Ojo:** las opciones por QR (dlastcrm por QR, Unipile, Evolution API en modo QR) no son oficiales y WhatsApp puede bloquearte el número. Para tu número principal, la vía oficial. Detalle en [Opciones de WhatsApp](#w1-opciones).

## Dos versiones: MVP y completa

| | MVP (hoy, rápido) | Completa |
|---|---|---|
| **Qué te llevás** | Las instrucciones de tu bot escritas desde tu cerebro y probadas en un bot de Telegram hecho con n8n. | Tu bot en WhatsApp con una de las 6 opciones del menú. |
| **Tiempo** | 25 min | De 1 hora a varios días, según la opción |
| **Cuentas que necesitás** | [n8n](#s6-n8n) · [Telegram](#s7-telegram) (las mismas del [desafío del agente](#d2-agente)) | [Meta Business](#s14-meta-y-google) + un número dedicado + la plataforma que elijas ([Opciones](#w1-opciones)) |
| **Costo** | Gratis: prueba de n8n Cloud y sus créditos de IA | Según la opción (ver el menú) |

### Versión MVP, paso a paso
1. **Escribí las instrucciones.** Abrí Claude Code en la carpeta de tu cerebro (como en [Tu cerebro](#p1-cerebro)) y pegá:

```prompt
Escribí las instrucciones del bot de WhatsApp de mi empresa y guardalas en bot/instrucciones-del-bot.md. Usá SOLO mi cerebro (CLAUDE.md, ventas/, negocio/, marca/). Lo que no esté, marcalo PENDIENTE: no inventes. Si ya hay un prompt de agente en esta carpeta, partí de ese.
Secciones:
1. Quién es el bot, de qué empresa y su objetivo (responder y agendar, o calificar y pasar al vendedor).
2. Cómo habla: tono, vos o tú, mensajes cortos, emojis sí o no, con 2 ejemplos de marca/voz.md.
3. Bienvenida y mensaje fuera de horario.
4. Preguntas frecuentes → respuesta oficial.
5. Objeciones → cómo se responden.
6. Qué NUNCA dice ni promete (precios no confirmados, plazos, resultados, descuentos, temas legales).
7. A quién no le vendemos y cómo decírselo con respeto.
8. Qué datos pide (los mínimos) y cuáles nunca (DNI, tarjetas, claves, salud).
9. Cuándo pasa a una persona, a quién y con qué mensaje.
10. 10 casos de prueba: mensaje del cliente → qué tiene que hacer el bot.
11. Pendientes.
Máximo 2 páginas. Al final, decime cuántos PENDIENTE quedaron.
```

**Tenés que ver:** Claude te avisa que creó `bot/instrucciones-del-bot.md` y cuántos PENDIENTE quedaron.

2. **Ponelas en un bot de Telegram.** Si hiciste el [desafío del agente](#d2-agente), pegá:

```prompt
Con el MCP de n8n, cambiá las instrucciones del AI Agent del workflow "agente-[TU-EMPRESA]" por el contenido de bot/instrucciones-del-bot.md. Mostrame el cambio antes de guardarlo.
```

Si no lo hiciste, seguí los pasos 1 a 3 de la Versión MVP del [desafío del agente](#d2-agente) y, en el prompt, pedí que las instrucciones salgan de `bot/instrucciones-del-bot.md`.

**Tenés que ver:** el flujo activo en n8n con las instrucciones nuevas.

3. **Probalo.** Desde tu celular, escribile al bot 5 de los 10 casos de prueba. Lo que salga mal, corregilo: "Cambiá la sección 6 de bot/instrucciones-del-bot.md: el bot nunca menciona [X]", y repetí el paso 2.

**Tenés que ver:** el bot responde como dicen tus instrucciones en al menos 4 de los 5 casos.

> **Tip:** ¿no llegás a armar el bot? Probalo en el mismo chat de Claude Code: "Actuá como el bot siguiendo SOLO bot/instrucciones-del-bot.md. Yo soy un cliente. Cuando escriba FIN, decime qué respondiste mal".

### Versión completa
Elegís una opción del menú y cargás ahí este mismo documento: [Bot con dlastcrm](#w2-bot-dlastcrm), [Plataforma propia](#w3-bot-propio), [Zernio](#w4-zernio), [Unipile](#w5-unipile) o [Evolution API](#w6-evolution-api). Comparativa completa: [Opciones de WhatsApp](#w1-opciones).

Arrancá por la MVP. Si te sobra tiempo, pasá a la completa: lo que hiciste te sirve.

## Lo lograste si…
- [ ] Sabés qué opción de WhatsApp te conviene y por qué.
- [ ] Tenés `bot/instrucciones-del-bot.md` escrito desde tu cerebro.
- [ ] Lo probaste con al menos 5 casos y corregiste lo que falló.
- [ ] Los pendientes tienen responsable y fecha.

> **Datos:** el documento no tiene claves ni datos de clientes: puede ir con el resto del cerebro a tu GitHub **privado** ([Tu cerebro](#p1-cerebro)).

## Ideas por tipo de negocio
Ejemplos inventados:
- **Venta consultiva:** califica con 4 o 5 preguntas y agenda la videollamada con el vendedor.
- **Escuela o cursos:** responde fechas, lugar y formas de pago, y anota al interesado en la próxima cohorte.
- **Agencia de viajes:** junta los datos para cotizar y avisa a la vendedora.
- **Producción y reparto:** toma pedidos con zona y día de entrega.

## Pedí ayuda a la mesa cuando…
- No sabés qué opción elegir: contanos tu caso y te orientamos.
- El documento sale lleno de PENDIENTE: al cerebro le faltan respuestas. Lo vemos juntos.
- Querés saber cuánto cuesta dlastcrm para tu equipo: se cotiza con la agencia.
