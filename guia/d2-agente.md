---
titulo: "Desafío: un agente que responde y filtra"
bloque: Desafío
tiempo: 30 a 90 min
para: Todos
necesitas: p1-cerebro
resultado: Un agente que contesta las preguntas frecuentes con tus respuestas oficiales, filtra a quien no es cliente y te pasa a quien quiere comprar. Probado antes de publicarlo.
---

La mitad de los mensajes que recibís son las mismas 10 preguntas. Y una parte de los que escriben no es tu cliente: busca otra cosa, no puede pagarlo o solo quiere el precio.
El desafío: armar un agente que contesta eso a cualquier hora, con **tus** respuestas, y que te avisa cuando aparece alguien que sí quiere comprar. Hoy lo probás en Telegram. En el cierre del día vemos cómo llevarlo a WhatsApp ([Cierre: tu bot de WhatsApp](#d7-whatsapp)).

**En 30 segundos**
- **Qué te llevás:** un agente (un asistente que contesta solo) que responde tus preguntas frecuentes con tus palabras y te avisa cuando alguien quiere comprar.
- **Cuánto tarda:** 30 min el Rápido (lo probás en tu compu), 90 min el Completo (publicado en Telegram).
- **Por dónde empezar:** abrí [Un agente que responde y filtra](#p3-agente-preguntas) y seguí el Paso 1.

## Qué problema resuelve
- Consultas que esperan horas (o hasta el día siguiente) porque nadie llega a contestar.
- Vendedores que pierden tiempo con gente que nunca iba a comprar.
- Respuestas distintas según quién conteste.

## Elegí tu camino

| Nivel | Qué hacés | Tutorial |
|---|---|---|
| **Rápido · 30 min** | Armás el "cerebro del agente": su prompt, lo que puede decir y 10 casos de prueba. Lo probás en Claude Code, sin publicar nada. | [Un agente que responde y filtra](#p3-agente-preguntas), Pasos 1 a 4 |
| **Completo · 90 min** | Lo mismo, más las pruebas automáticas, publicado en internet y conectado a un bot de Telegram que podés compartir. | [Un agente que responde y filtra](#p3-agente-preguntas), completo |
| **Pro · para después** | Llevalo a WhatsApp, o sumale voz para que atienda llamadas. | [Opciones de WhatsApp](#w1-opciones) · [Agentes de voz](#s13-vapi) |

> **Tip:** el Rápido no es "menos": es la parte más valiosa. Las respuestas y los casos de prueba que escribís hoy son los mismos que va a usar tu bot de WhatsApp.

## Qué cuentas necesitás
- [ ] Claude Code ([Claude Code](#s2-claude-code)). Alcanza para el Rápido.
- [ ] Para el Completo: un bot de Telegram nuevo ([Telegram](#s7-telegram)), una clave de API, que es la llave para que tu bot use Claude ([Clave de API](#s9-api-anthropic)), y cuenta de Cloudflare, donde queda publicado tu bot ([Cuentas en la nube](#s5-cuentas-nube)).
- [ ] Tu cerebro con las preguntas frecuentes y objeciones respondidas ([Usá tu borrador](#c2-tu-borrador), Paso 3). Sin respuestas oficiales, el agente no tiene qué decir.

## Lo lograste si…
- [ ] El agente contesta bien tus 10 preguntas frecuentes, con tus palabras.
- [ ] Ante una pregunta que no está en el cerebro, dice que no sabe y deriva a una persona. No inventa.
- [ ] Filtra con respeto a quien no es tu cliente.
- [ ] Cuando alguien quiere comprar, pide los datos que necesitás y te avisa.
- [ ] Nunca promete algo que tu negocio no puede cumplir (precios viejos, plazos, resultados).

## Ideas por tipo de negocio
Ejemplos inventados:
- **Venta consultiva (planes, seguros, inmobiliaria):** explica cómo funciona el producto, aclara lo que **no** es, responde "¿es una estafa?" con pruebas y agenda la reunión con el asesor.
- **Escuela o cursos:** fechas de inicio, horario, lugar, formas de pago y si se puede recuperar una clase.
- **Agencia de viajes:** junta de una vez todo lo que hace falta para cotizar (destino, fechas, cantidad de pasajeros, presupuesto) y se lo pasa a la vendedora.
- **Coaching o servicios profesionales:** responde dudas del programa y deriva a quien pregunta por precio especial.
- **Producción y reparto:** zonas y días de entrega, pedido mínimo y cómo hacer un pedido.

> **Datos:** el agente solo sabe lo que está en su conocimiento público. Nada de datos de clientes, precios internos ni márgenes ahí adentro.

## Pedí ayuda a la mesa cuando…
- Las pruebas fallan y no entendés por qué (las pruebas son los 10 casos que el agente tiene que contestar bien).
- Cloudflare o Telegram te dan un error al publicar.
- No sabés qué responder a una pregunta frecuente: eso no es técnico, es de tu negocio. Charlalo con tu equipo y anotalo como pendiente.
