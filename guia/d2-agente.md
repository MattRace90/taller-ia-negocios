---
titulo: "Desafío: un agente que responde y filtra"
bloque: Desafío
tiempo: 30 a 90 min
para: Todos
necesitas: p1-cerebro
cuentas_mvp: s6-n8n, s7-telegram
cuentas_completa: s3-herramientas-base, s5-cuentas-nube, s7-telegram, s9-api-anthropic, s13-vapi
resultado: Un bot de Telegram que contesta tus preguntas frecuentes con tus respuestas, filtra a quien no es cliente y te pasa a quien quiere comprar.
---

La mitad de los mensajes son las mismas 10 preguntas. El desafío: un agente que las contesta a cualquier hora, con **tus** respuestas, y te avisa cuando alguien quiere comprar. Hoy en Telegram; WhatsApp, en el [cierre](#d7-whatsapp).

**En 30 segundos**
- **Cuánto tarda:** 30 a 45 min la MVP, 90 min la completa.
- **Por dónde empezar:** la **Versión MVP**, acá abajo.

## Dos versiones: MVP y completa

| | MVP (hoy, rápido) | Completa |
|---|---|---|
| **Qué te llevás** | Un bot de Telegram con tu cerebro, armado por Claude en n8n. | Con pruebas automáticas, en Cloudflare. |
| **Tiempo** | 30 a 45 min | 90 min |
| **Cuentas que necesitás** | [n8n](#s6-n8n) · [Telegram](#s7-telegram) | [Telegram](#s7-telegram) · [Clave de API](#s9-api-anthropic) · [Cuentas en la nube](#s5-cuentas-nube) · [Herramientas base](#s3-herramientas-base) · voz: [Vapi](#s13-vapi) |
| **Costo** | Gratis (prueba de n8n Cloud + sus créditos de IA) | API de Anthropic por uso, Cloudflare gratis ([Stack y costos](#r-stack-y-costos)) |

### Versión MVP, paso a paso
1. **Las cuentas.** Tu bot en [Telegram](#s7-telegram) (Pasos 1 a 3). En [n8n](#s6-n8n), los Pasos 1, 3 y 6 (cuenta, credencial de Telegram y MCP). Saltá el 5.

**Tenés que ver:** en la app de Claude, **Customize › Connectors** muestra n8n conectado.

2. **Que Claude arme el bot.** En la app de Claude, abrí la **pestaña Code**, elegí la carpeta de tu cerebro y pegá:

```prompt
Con el MCP de n8n, creá un workflow llamado "agente-[TU-EMPRESA]": Telegram Trigger (mensaje nuevo) → AI Agent → respuesta por Telegram al mismo chat.
- Modelo: los créditos de IA gratis de n8n (Gateway credits; si no están, los gratis de OpenAI). Memoria simple por chat.
- Usá mi credencial de Telegram guardada en n8n.
- Instrucciones: armalas con mi cerebro (ventas/, negocio/). Corto, con vos, solo con esa información. Si no sabe, que derive a una persona. Si quiere comprar, que pida nombre y qué necesita.
Mostrame el plan antes de crearlo. No lo actives hasta que te diga.
```

**Tenés que ver:** el plan (3 o 4 nodos). Decile "dale". Cuando pida permiso para usar n8n, tocá **Permitir**, y te confirma el flujo creado.

> **Ojo:** las cuentas nuevas traen algunos créditos de IA gratis (**Use Gateway credits** en el nodo del modelo); n8n no publica cuántos ([doc](https://docs.n8n.io/deploy/use-n8n-cloud/gateway-credits), nov 2026). Si no aparecen o se terminan, usá tu [clave de API](#s9-api-anthropic).

3. **Prendelo.** En n8n, abrí el flujo y activalo con **Publish** (o el interruptor **Active**, según tu versión).

**Tenés que ver:** el flujo marcado como activo.

4. **Probalo.** Escribile 5 cosas: 2 preguntas frecuentes, 1 que no esté en tu cerebro, 1 de alguien que no es cliente y 1 de alguien que quiere comprar.

**Tenés que ver:** responde con tus palabras y no inventa. Para corregir, pedíselo en la misma pestaña Code: "Con el MCP de n8n, cambiá las instrucciones del agente: [QUÉ]".

### Versión completa
Pruebas automáticas antes de publicar y el agente en Cloudflare con tu clave: [Un agente que responde y filtra](#p3-agente-preguntas). Después: WhatsApp ([Opciones](#w1-opciones)) o voz para llamadas ([Vapi](#s13-vapi)).

Arrancá por la MVP. Si te sobra tiempo, pasá a la completa: lo que hiciste te sirve.

## Lo lograste si…
- [ ] Contesta tus preguntas frecuentes con tus palabras.
- [ ] Lo que no sabe, lo deriva. No inventa.
- [ ] Filtra con respeto a quien no es cliente.
- [ ] A quien quiere comprar le pide los datos.

## Ideas por tipo de negocio
Ejemplos inventados:
- **Venta consultiva:** aclara lo que el producto **no** es y agenda con el asesor.
- **Escuela o cursos:** fechas, horario, lugar y formas de pago.
- **Agencia de viajes:** junta destino, fechas y pasajeros para cotizar.

> **Datos:** nada de datos de clientes, precios internos ni márgenes en el agente.

## Pedí ayuda a la mesa cuando…
- El bot no contesta (¿el flujo está activo? ¿otro flujo usa el mismo bot?).
- No sabés qué responder a una pregunta: es de tu negocio, anotalo como pendiente.
