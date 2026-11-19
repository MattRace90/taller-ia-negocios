---
titulo: "Desafío: vendé más con propuestas y seguimiento"
bloque: Desafío
tiempo: 30 a 90 min
para: Todos
necesitas: p1-cerebro
cuentas_mvp: ""
cuentas_completa: s6-n8n, s7-telegram, s9-api-anthropic, s14-meta-y-google
resultado: Propuestas que salen el mismo día de la reunión y una planilla que te dice a quién volver a escribirle y qué decirle.
---

Las ventas se pierden porque la propuesta tardó tres días o porque nadie volvió a escribir. El desafío: propuesta el mismo día y seguimiento sin depender de la memoria.

**En 30 segundos**
- **Cuánto tarda:** 30 min la MVP, 90 min la completa.
- **Por dónde empezar:** la **Versión MVP**, acá abajo. Solo necesitás la **pestaña Code** de la app de Claude.

## Dos versiones: MVP y completa

| | MVP (hoy, rápido) | Completa |
|---|---|---|
| **Qué te llevás** | La skill `propuesta-comercial` en la pestaña Code de Claude: pegás la reunión y sale la propuesta con tu marca y tus precios. | El seguimiento a quien no compró y `/propuesta` desde Telegram. |
| **Tiempo** | 30 min | 90 min |
| **Cuentas que necesitás** | Ninguna extra (la app de Claude) | Seguimiento: ninguna extra. Telegram: [n8n](#s6-n8n) · [Telegram](#s7-telegram) · [Clave de API](#s9-api-anthropic) · [Google](#s14-meta-y-google) |
| **Costo** | Tu plan de Claude | + n8n desde €20/mes (nov 2026) + centavos de API |

### Versión MVP, paso a paso
1. **Instalá la skill** `propuesta-comercial` (una receta escrita que Claude sigue). En el [Kit](#r-kit), tocá **Copiar** en `propuesta-comercial` y seguí **Cómo instalar una skill**: se lo pedís a Claude en la pestaña Code, sin terminal.

**Tenés que ver:** Claude te confirma la ruta donde quedó la skill.

2. **Pegá la reunión.** Abrí una sesión nueva en la **pestaña Code**, con la carpeta de tu cerebro elegida, y pegá:

```prompt
Usá la skill propuesta-comercial. Esto es lo que se habló en la reunión con [CLIENTE INVENTADO]: [PEGÁ TUS NOTAS O LA TRANSCRIPCIÓN]. Usá solo los precios y condiciones de mi cerebro; lo que no esté, marcalo PENDIENTE. Guardala en propuestas/ y decime qué me falta confirmar.
```

**Tenés que ver:** una propuesta nueva en `propuestas/` y la lista de PENDIENTE.

3. **Pulila.** Leela como si fueras el cliente. Pedí los cambios en una línea: "Más corta", "sacá el párrafo 2", "sumá la garantía".

**Tenés que ver:** una propuesta que mandarías casi sin tocar.

### Versión completa
Grupos de quien no compró, 3 mensajes por grupo y planilla: [Seguimiento](#p8-seguimiento). La propuesta desde el celular: [Tu asistente en Telegram](#p2-asistente-telegram) completo.

Arrancá por la MVP. Si te sobra tiempo, pasá a la completa: lo que hiciste te sirve.

## Lo lograste si…
- [ ] Tenés una propuesta armada desde una reunión (real o inventada).
- [ ] Los precios salen de tu cerebro: nada inventado.
- [ ] Lo que falta definir quedó como PENDIENTE.
- [ ] La mandarías casi sin tocar.

> **Ojo:** mandar mensajes automáticos desde un WhatsApp común puede hacer que te bloqueen el número. **Vos** mandás los mensajes. Para automatizar el envío: [Cierre: tu bot de WhatsApp](#d7-whatsapp).

## Ideas por tipo de negocio
Ejemplos inventados:
- **Escuela o capacitación a empresas:** la propuesta In Company sale de la llamada, con módulos, fechas y precio.
- **Agencia de viajes:** recontacto a las 24 h, 48 h y 5 días a quien pidió presupuesto y no confirmó.
- **Coaching o formación:** seguimiento a quien dijo "es caro", con un testimonio y la respuesta a esa objeción.

> **Datos:** la lista de clientes es información personal. Para practicar, inventala. Con datos reales, trabajá en tu compu y nunca la subas a GitHub.

## Pedí ayuda a la mesa cuando…
- La skill no se instala o Claude no la encuentra.
- La propuesta sale sin tu logo o con precios inventados.
