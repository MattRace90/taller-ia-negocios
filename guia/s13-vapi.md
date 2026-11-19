---
titulo: Vapi, agentes de voz por teléfono
bloque: Setup
tiempo: 40 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude, s2-claude-code, s10-conectar-todo
resultado: Cuenta de Vapi con crédito de prueba, conectada a Claude, y un asistente de voz de prueba creado por prompt con el que hablaste desde el navegador.
---

Vapi arma agentes que **hablan por teléfono**: atienden, preguntan, responden y anotan el resultado. Vos le describís a Claude qué tiene que hacer el agente y Claude lo crea en Vapi.
Ejemplo (inventado): Denvet podría llamar el día anterior a cada turno de vacunación para confirmar, y anotar quién confirma, quién reprograma y quién pide hablar con una persona.

**Caso real nuestro:** para el evento Brujería (oct 2026) armamos dos agentes con la voz de Mati: uno que llamaba a quienes compraron entrada para confirmar asistencia, y otro que hizo sonar todos los celulares de la sala a la vez. Aprendizajes que te ahorramos: los números gratis de Vapi son de EE. UU., para llamar a celulares argentinos hay que **importar un número** (Twilio o Telnyx), y la lista de la sala se armó con un formulario que pedía **consentimiento explícito** para recibir la llamada.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude y Claude Code instalado.
- [ ] Una tarjeta que acepte pagos en dólares (para cargar saldo cuando se termine el de prueba).
- [ ] Leíste el método para conectar ([Conectá cualquier herramienta](#s10-conectar-todo)).
- [ ] Un guion simple de lo que tiene que hacer tu agente (una tarea, no diez).

> **Datos:** un agente de voz habla con personas reales. **Solo llamá a quien te dio permiso** para recibir esa llamada, decí al principio que es una IA y de parte de quién, y ofrecé hablar con una persona. En Argentina existe el **Registro Nacional "No Llame"** (Ley 26.951) para llamadas de publicidad: no uses el agente para vender en frío. Para el taller, **solo hablamos desde el navegador** o llamamos a tu propio celular.

> **Costo:** Vapi cobra **por minuto**. Su tarifa de plataforma es **USD 0,05/min**, y se suman el modelo de IA, la voz, la transcripción y la telefonía, que se cobran aparte. Según terceros, el total real queda entre **USD 0,10 y 0,30 por minuto**. Las cuentas nuevas traen **USD 5 de crédito** de prueba. El plan Core cuesta **USD 29/mes** (5 números, 10 llamadas simultáneas) y las líneas extra, **USD 10/mes** cada una (nov 2026, [vapi.ai/pricing](https://vapi.ai/pricing)).

## Paso 1 · Creá tu cuenta de Vapi
1. Entrá a **[dashboard.vapi.ai](https://dashboard.vapi.ai)** y registrate (Google o mail).
2. Completá el nombre de tu organización (tu empresa).
3. Fijate tu saldo de prueba en la sección de facturación (**Billing**).

**Tenés que ver:** el panel de Vapi, con el menú de **Assistants**, **Phone Numbers** y **Calls**.

## Paso 2 · Conectá Vapi a Claude
Vapi tiene MCP oficial, con inicio de sesión (no hace falta copiar ninguna clave).

**En Claude Code** (en una terminal, no adentro de Claude Code; en Windows, PowerShell, con el mismo comando):

```bash
claude mcp add --transport http --scope user vapi https://mcp.vapi.ai/mcp
```

Abrí Claude Code, escribí `/mcp` › **vapi** › **Authenticate** › iniciá sesión y elegí tu organización.

**En la app de Claude:** **Customize › Connectors** › **+** › **Add custom connector** › **Name:** `Vapi` › **URL:** `https://mcp.vapi.ai/mcp` › dejá vacías las opciones avanzadas › **Add** › **Connect**.

> **Ojo:** el MCP de Vapi tiene una herramienta (`create_call`) que **hace una llamada real** y otra (`run_simulations`) que **cobra** simulaciones. Cuando Claude pida permiso para usarlas, leé a quién llama antes de aceptar.

> **Tip:** guías viejas dicen que hay que pegar tu API key en un header. Ya no: el MCP actual usa inicio de sesión. No pongas tu clave de Vapi en ningún comando ni chat.

**Tenés que ver:** en `/mcp`, **vapi** conectado con su lista de herramientas (asistentes, llamadas, números).

## Paso 3 · Creá un asistente de prueba con un prompt
Pegá esto en Claude Code. Los datos son **inventados**:

```prompt
Con el MCP de Vapi, creá un asistente de prueba llamado "Prueba · Confirmación de turnos".
Negocio (inventado): Veterinaria Patitas Córdoba. Tarea: llamar a un cliente para confirmar un turno de vacunación de su mascota mañana a las 10:30.
Reglas:
- Hablá en español rioplatense, con voseo, frases cortas y tono amable.
- Primera frase: saludá, decí que sos un asistente de inteligencia artificial de Veterinaria Patitas y preguntá si es buen momento.
- Pedí que confirme, reprograme o cancele. Si reprograma, preguntá día y franja horaria preferida, sin prometer un horario.
- Si pregunta algo que no sabés (precios, diagnósticos), decí que lo va a llamar una persona del equipo.
- Si pide que no lo llamen más, disculpate, anotalo y cortá.
- Máximo 2 minutos de llamada.
Al terminar la llamada, guardá un resumen y estos datos: resultado (confirma / reprograma / cancela / no_contactado), preferencia_de_horario, requiere_humano (sí/no), no_llamar_mas (sí/no).
Usá una voz en español latino que suene natural y la transcripción en español.
NO hagas ninguna llamada. Cuando termines, pasame el ID del asistente y un resumen de cómo quedó configurado.
```

**Tenés que ver:** en el panel de Vapi, **Assistants**, el asistente "Prueba · Confirmación de turnos".

## Paso 4 · Hablá con el asistente desde el navegador
Antes de cualquier teléfono, probalo vos.

1. En **[dashboard.vapi.ai](https://dashboard.vapi.ai)** › **Assistants** › elegí tu asistente.
2. Tocá el botón para hablar con el asistente (arriba a la derecha; suele decir **Talk to Assistant**) y aceptá el permiso del micrófono.
3. Hacé de cliente: confirmá, después probá reprogramar, preguntá un precio y pedí que no te llamen más.

> **Ojo:** el nombre exacto del botón puede variar con las versiones del panel. Si no lo encontrás, pedile a Claude: "¿cómo pruebo este asistente desde el navegador en Vapi?".

Después, en Claude Code:

```prompt
Con el MCP de Vapi, traé la última llamada del asistente "Prueba · Confirmación de turnos": mostrame la transcripción, el resumen, los datos que guardó y cuánto costó. Decime qué cambiarías del prompt para que suene más natural.
```

**Tenés que ver:** la transcripción de tu conversación, el resultado guardado y el costo de la llamada.

## Paso 5 · Entendé los números de teléfono
| Opción | Qué permite | Costo |
|---|---|---|
| **Número gratis de Vapi** | Uno por cuenta, con código de área de **EE. UU.**, solo para **recibir** llamadas | Gratis |
| **Número importado** (Twilio, Telnyx, DIDWW o SIP) | Llamadas salientes e internacionales, número argentino | Lo que cobre ese proveedor |
| **Llamada web** (Paso 4) | Probar sin teléfono | Solo los minutos |

Para el taller alcanza con la llamada web. Si querés que tu agente **llame** a celulares argentinos, necesitás comprar un número argentino en Twilio o Telnyx e importarlo en Vapi (**Phone Numbers** › **Import**). Es un paso aparte, con su propio costo y verificación de identidad: hacelo después del taller.

> **Ojo:** los planes de Vapi limitan cuántas llamadas pueden sonar **a la vez** (4 en la cuenta inicial, 10 en Core). Si vas a llamar a una lista, Claude tiene que hacerlo en tandas.

**Tenés que ver:** en **Phone Numbers**, sabés si tenés un número y de qué tipo.

## Cómo sé que funcionó
- El asistente existe en Vapi y lo creaste por prompt, sin tocar el panel.
- Hablaste con él desde el navegador y Claude te trajo la transcripción y el costo.
- Sabés qué te falta para llamar a un número real (número importado + lista con consentimiento).

Prueba final en Claude Code:

```prompt
Con lo que viste de la llamada de prueba, mejorá el asistente "Prueba · Confirmación de turnos": que confirme el nombre de la mascota (dato inventado: "Toby"), que repita el día y la hora antes de cortar y que si hay silencio de más de 10 segundos pregunte "¿seguís ahí?". Actualizalo y no hagas llamadas.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `/mcp` muestra vapi con error o "timeout" | Revisá tu conexión y reintentá **Authenticate**. Si sigue: `claude mcp remove vapi` y agregalo de nuevo. |
| El asistente habla en inglés o con acento raro | Pedile a Claude que ponga la transcripción en español y elija una voz en español latino. Probá dos o tres voces. |
| Corta antes de que la persona hable | Subí el tiempo de silencio permitido (por ejemplo, 30 segundos). Nos pasó en Brujería. |
| No puedo llamar a un celular argentino | El número gratis de Vapi es de EE. UU. y solo recibe. Importá un número argentino (Paso 5). |
| Se terminó el saldo | Cargá crédito en **Billing**. Poné un tope y no actives recargas automáticas sin límite. |
| La llamada cuesta más de lo esperado | Bajá la duración máxima, usá un modelo más chico y revisá el costo por llamada en **Calls**. |

## Para seguir solo
- Conectá el final de cada llamada a n8n (con un webhook: una dirección que recibe el aviso de "terminó la llamada") para que el resultado se anote solo en tu planilla o en dlastcrm ([n8n](#s6-n8n)).
- Armá un asistente que **atienda** (en vez de llamar) para las consultas fuera de horario, con las respuestas de `ventas/` de tu cerebro.
- Antes de llamar a clientes reales: formulario con consentimiento, horario razonable, opción de hablar con una persona y registro de quién pidió no ser llamado.

## Fuentes
Consultadas el 18/11/2026.
- Vapi MCP (URL, OAuth, comando para Claude Code, herramientas): https://docs.vapi.ai/sdk/mcp-server
- Vapi, precios y llamadas simultáneas: https://vapi.ai/pricing
- Vapi, números gratis (EE. UU., solo entrantes) e importación: https://docs.vapi.ai/phone-calling · https://docs.vapi.ai/phone-numbers/import-twilio · https://docs.vapi.ai/telnyx
- Costo total por minuto (terceros): https://www.activepieces.com/blog/vapi-pricing-2026-the-real-cost-per-minute · https://www.retellai.com/blog/revealing-vapi-ai-pricing
- Registro Nacional "No Llame" (Ley 26.951): https://www.argentina.gob.ar/justicia/derechofacil/leysimple/registro-no-llame · https://nollame.aaip.gob.ar
- Caso propio: agentes de confirmación y "llamada en sala" del evento Brujería (oct 2026).
