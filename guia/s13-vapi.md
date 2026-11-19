---
titulo: "Vapi, agentes de voz por teléfono"
bloque: Setup
tiempo: 40 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude, s2-claude-code, s10-conectar-todo
resultado: Cuenta de Vapi con crédito de prueba, conectada a Claude, y un asistente de voz de prueba creado por prompt con el que hablaste desde el navegador.
---

Vapi arma agentes que **hablan por teléfono**: atienden, preguntan, responden y anotan el resultado. Vos le describís a Claude qué tiene que hacer el agente y Claude lo crea en Vapi.
Ejemplo (inventado): Denvet llama el día anterior a cada turno de vacunación para confirmar y anota quién confirma, quién reprograma y quién pide una persona.

**Caso real nuestro (Brujería, oct 2026):** dos agentes con la voz de Mati, uno para confirmar asistencia y otro que hizo sonar todos los celulares de la sala. Lo que aprendimos: los números gratis de Vapi son de EE. UU.; para llamar a celulares argentinos hay que **importar un número** (Twilio o Telnyx), y la lista se armó con **consentimiento explícito**.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude y la pestaña **Code** andando ([Claude Code](#s2-claude-code)).
- [ ] Una tarjeta que acepte pagos en dólares (para cuando se termine el saldo de prueba).
- [ ] Leíste el método para conectar ([Conectá cualquier herramienta](#s10-conectar-todo)).
- [ ] Un guion simple de lo que hace tu agente (una tarea, no diez).

> **Datos:** **solo llamá a quien te dio permiso**, decí al principio que es una IA y de parte de quién, y ofrecé hablar con una persona. En Argentina rige el **Registro "No Llame"** (Ley 26.951): no lo uses para vender en frío. Hoy **solo hablamos desde el navegador**.

> **Costo:** plataforma **USD 0,05/min** + modelo, voz, transcripción y telefonía aparte. Según terceros, **USD 0,10 a 0,30 por minuto** en total. Cuentas nuevas: **USD 5 de prueba**. Plan Core **USD 29/mes** (nov 2026, [vapi.ai/pricing](https://vapi.ai/pricing)).

## Paso 1 · Creá tu cuenta de Vapi
1. Entrá a **[dashboard.vapi.ai](https://dashboard.vapi.ai)** y registrate (Google o mail).
2. Poné el nombre de tu empresa y mirá tu saldo en **Billing**.

**Tenés que ver:** el panel con **Assistants**, **Phone Numbers** y **Calls**.

## Paso 2 · Conectá Vapi a Claude
Se conecta con inicio de sesión: **no copies ninguna clave de Vapi**.

1. En la app de Claude: **Customize › Connectors** › **+** › **Add custom connector** › **Name:** `Vapi` › **URL:** `https://mcp.vapi.ai/mcp` › opciones avanzadas vacías › **Add** › **Connect** › iniciá sesión y elegí tu organización.
2. Abrí la pestaña **Code** (elegí la carpeta de tu cerebro) y escribí `/mcp` en el cuadro. Vapi aparece solo, porque es la misma cuenta.

Si preferís agregarlo solo en la pestaña Code, pedíselo:

```prompt
Agregá el MCP de Vapi con esta dirección: https://mcp.vapi.ai/mcp (para todas mis carpetas). Avisame cuando esté y después decime cómo inicio sesión.
```

> **Ojo:** Vapi tiene una herramienta que **hace una llamada real** (`create_call`) y otra que **cobra** simulaciones (`run_simulations`). Cuando Claude pida permiso para usarlas, leé a quién llama antes de aceptar.

**Tenés que ver:** en `/mcp`, **vapi** conectado.

## Paso 3 · Creá un asistente de prueba con un prompt
En la pestaña **Code**. Los datos son **inventados**:

```prompt
Con el MCP de Vapi, creá un asistente de prueba llamado "Prueba · Confirmación de turnos".
Negocio (inventado): Veterinaria Patitas Córdoba. Tarea: llamar a un cliente para confirmar un turno de vacunación mañana a las 10:30.
Reglas:
- Español rioplatense, voseo, frases cortas, tono amable.
- Primera frase: saludá, decí que sos un asistente de inteligencia artificial de Veterinaria Patitas y preguntá si es buen momento.
- Pedí que confirme, reprograme o cancele. Si reprograma, preguntá día y franja preferida, sin prometer horario.
- Si pregunta precios o diagnósticos, decí que lo llama una persona del equipo.
- Si pide que no lo llamen más, disculpate, anotalo y cortá.
- Máximo 2 minutos.
Al terminar, guardá un resumen y: resultado (confirma / reprograma / cancela / no_contactado), preferencia_de_horario, requiere_humano (sí/no), no_llamar_mas (sí/no).
Voz en español latino natural y transcripción en español.
NO hagas ninguna llamada. Pasame el ID del asistente y un resumen de cómo quedó.
```

**Tenés que ver:** en Vapi › **Assistants**, "Prueba · Confirmación de turnos".

## Paso 4 · Hablá con el asistente desde el navegador
1. En **[dashboard.vapi.ai](https://dashboard.vapi.ai)** › **Assistants** › tu asistente.
2. Tocá el botón para hablarle (suele decir **Talk to Assistant**) y aceptá el micrófono.
3. Hacé de cliente: confirmá, reprogramá, preguntá un precio, pedí que no te llamen más.

> **Ojo:** el nombre del botón puede variar según la versión del panel.

Después, en la pestaña **Code**:

```prompt
Con el MCP de Vapi, traé la última llamada de "Prueba · Confirmación de turnos": transcripción, resumen, datos guardados y costo. Decime qué cambiarías del prompt para que suene más natural.
```

**Tenés que ver:** la transcripción, el resultado guardado y el costo.

## Paso 5 · Entendé los números de teléfono
| Opción | Qué permite | Costo |
|---|---|---|
| **Número gratis de Vapi** | Uno por cuenta, de **EE. UU.**, solo **recibe** | Gratis |
| **Número importado** (Twilio, Telnyx) | Llamar a celulares argentinos | Lo que cobre ese proveedor |
| **Llamada web** (Paso 4) | Probar sin teléfono | Solo los minutos |

Hoy alcanza con la llamada web. Importar un número argentino (**Phone Numbers** › **Import**) es un paso aparte, con costo y verificación de identidad: después del taller.

**Tenés que ver:** sabés si tenés número y de qué tipo.

## Cómo sé que funcionó
Creaste el asistente por prompt, hablaste con él y Claude te trajo la transcripción. Prueba final en la pestaña **Code**:

```prompt
Mejorá el asistente "Prueba · Confirmación de turnos": que confirme el nombre de la mascota (inventado: "Toby"), que repita día y hora antes de cortar y que si hay más de 10 segundos de silencio pregunte "¿seguís ahí?". Actualizalo y no hagas llamadas.
```

**Tenés que ver:** Claude te confirma el cambio y, al volver a hablarle desde el navegador, pregunta por Toby.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `/mcp` muestra vapi con error | Elegilo › **Authenticate**. Si sigue, pedile a Claude: "Sacá el MCP de Vapi y agregalo de nuevo". |
| Habla en inglés o con acento raro | Pedile a Claude transcripción en español y voz en español latino. Probá dos o tres voces. |
| Corta antes de que la persona hable | Pedile que suba el silencio permitido (por ejemplo, 30 segundos). Nos pasó en Brujería. |
| No puedo llamar a un celular argentino | El número gratis es de EE. UU. y solo recibe. Importá uno argentino (Paso 5). |
| Se terminó el saldo | Cargá en **Billing**. No actives recargas automáticas sin tope. |

## Para seguir solo
- Mandá el resultado de cada llamada a n8n para que se anote solo en tu planilla o en dlastcrm ([n8n](#s6-n8n)).
- Armá un asistente que **atienda** consultas fuera de horario con las respuestas de `ventas/` de tu cerebro.
- Antes de llamar a clientes reales: consentimiento, horario razonable, opción de persona y registro de quién pidió no ser llamado.

## Fuentes
Consultadas el 18/11/2026.
- Vapi MCP: https://docs.vapi.ai/sdk/mcp-server · precios: https://vapi.ai/pricing
- Números e importación: https://docs.vapi.ai/phone-calling · https://docs.vapi.ai/phone-numbers/import-twilio
- Costo real por minuto (terceros): https://www.activepieces.com/blog/vapi-pricing-2026-the-real-cost-per-minute
- Registro "No Llame": https://www.argentina.gob.ar/justicia/derechofacil/leysimple/registro-no-llame
