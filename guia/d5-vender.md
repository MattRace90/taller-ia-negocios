---
titulo: "Desafío: vendé más con propuestas y seguimiento"
bloque: Desafío
tiempo: 30 a 90 min
para: Todos
necesitas: p1-cerebro
resultado: Propuestas que salen el mismo día de la reunión y un sistema que te dice cada mañana a quién volver a escribirle y qué decirle.
---

La mayoría de las ventas no se pierden por precio: se pierden porque la propuesta tardó tres días o porque nadie volvió a escribirle a quien consultó y no compró.
El desafío: resolver una de las dos puntas. O la propuesta sale el mismo día, o el seguimiento deja de depender de la memoria.

**En 30 segundos**
- **Qué te llevás:** una propuesta armada desde lo que se habló en una reunión, o una planilla que te dice a quién volver a escribirle y qué decirle.
- **Cuánto tarda:** 30 min la propuesta (Rápido), 90 min el seguimiento (Completo).
- **Por dónde empezar:** si vendés en reuniones, abrí [Tu asistente en Telegram](#p2-asistente-telegram) y andá directo al Paso 3.

## Qué problema resuelve
- Propuestas o presupuestos que se arman a mano, distintos cada vez y tarde.
- Consultas que no compraron y nunca nadie recontactó.
- Clientes que compraron una vez y no volvieron.

## Elegí tu camino

| Nivel | Qué hacés | Tutorial |
|---|---|---|
| **Rápido · 30 min** | Instalás la skill `propuesta-comercial` (una receta escrita que Claude sigue) y la usás directo en Claude Code: pegás lo que se habló en la reunión y te devuelve la propuesta con tu marca y tus precios. No hace falta Telegram. | [Tu asistente en Telegram](#p2-asistente-telegram), solo el Paso 3 |
| **Completo · 90 min** | El sistema de seguimiento: Claude separa a quien no compró según dónde quedó, escribe 3 mensajes por grupo en tu voz y arma la planilla. | [Seguimiento a quien no compró](#p8-seguimiento) |
| **Pro · para después** | La propuesta desde el celular con `/propuesta` en Telegram, y el aviso de cada mañana programado para que llegue solo. | [Tu asistente en Telegram](#p2-asistente-telegram) · [Tareas programadas](#t4-tareas-programadas) |

> **Tip:** si cerrás ventas en reuniones o llamadas, empezá por la propuesta. Si recibís muchas consultas que se enfrían, empezá por el seguimiento.

## Qué cuentas necesitás
- [ ] Claude Code ([Claude Code](#s2-claude-code)). Alcanza para el Rápido y el Completo.
- [ ] Tu cerebro con precios, objeciones y voz cargados ([Usá tu borrador](#c2-tu-borrador)).
- [ ] Para el seguimiento: una lista de quienes consultaron y no compraron (exportada de tu CRM, de tu planilla o armada a mano). Para practicar, inventada.
- [ ] Para el Pro: n8n, Telegram y clave de API ([n8n](#s6-n8n) · [Telegram](#s7-telegram) · [Clave de API](#s9-api-anthropic)).

## Lo lograste si…
- [ ] Tenés una propuesta armada a partir de una reunión (real o inventada) que mandarías casi sin tocar.
- [ ] O tenés tu lista separada en grupos, con 3 mensajes por grupo que suenan a vos.
- [ ] Sabés a quién le escribís mañana y qué le decís.
- [ ] **Vos** mandás los mensajes: nada sale solo desde tu WhatsApp.

> **Ojo:** mandar mensajes automáticos desde un WhatsApp común puede hacer que te bloqueen el número. Para automatizar el envío, mirá [Cierre: tu bot de WhatsApp](#d7-whatsapp).

## Ideas por tipo de negocio
Ejemplos inventados:
- **Escuela o capacitación a empresas:** la propuesta In Company sale de la transcripción de la llamada, con módulos, fechas y precio.
- **Agencia de viajes:** recontacto a las 24 h, 48 h y 5 días a quien pidió presupuesto y no confirmó, y un mensaje a quien viajó el año pasado.
- **Coaching o formación:** seguimiento a quien consultó y dijo "es caro", con un testimonio y la respuesta a esa objeción.
- **Venta consultiva:** recontacto ordenado a quien no atendió la primera llamada.
- **Marketplace o app:** primer mensaje personalizado para cada local que querés sumar, mencionando algo concreto de su perfil.

> **Datos:** la lista de clientes es información personal. Para practicar, inventala. Con datos reales, trabajá en tu compu y nunca la subas a GitHub.

## Pedí ayuda a la mesa cuando…
- No sabés cómo exportar tu lista de contactos de tu sistema.
- La propuesta sale sin tu logo o con precios inventados.
- El aviso de cada mañana no llega.
