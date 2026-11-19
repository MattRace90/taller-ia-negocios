---
titulo: Atajos de Claude Code
bloque: Teoría
tiempo: 15 min
para: Todos
necesitas: s2-claude-code
resultado: Manejás la pestaña Code con los comandos y las teclas que más se usan, y sabés armar un buen pedido.
---

Claude Code se maneja escribiendo en español y con unos pocos comandos que empiezan con `/`. Este es el machete para tener abierto durante el día y después.
**Todo lo que escribís en el cuadro de la pestaña Code funciona igual que en la terminal**: los comandos `/`, tus skills y los `@archivo`. Lo que cambia son algunas teclas: abajo te marcamos cuáles son **solo en la terminal**.
¿Dudás si usar el chat, Cowork o Claude Code? Está en [Dónde trabajar](#t3-donde-trabajar).

> **Datos:** verificado en la documentación oficial (code.claude.com/docs) el 18 y 19/11/2026.

## Antes de empezar
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).
- [ ] Una sesión abierta en una carpeta: **Code › + New › Local › Open folder…**. Para practicar sin miedo, usá una carpeta de prueba.

## Qué son los comandos de barra
Un **comando de barra** es una palabra que empieza con `/` y le da una orden **a Claude Code** (no un pedido de trabajo): "resumí la charla", "cambiá de modelo", "mostrame cuánto llevo usado". Son como los botones de un control remoto, pero escritos.
- Se escriben en el cuadro de la pestaña Code (o en la terminal, si la usás) y se mandan con **Enter**.
- Escribí `/` y aparece **la lista completa**; seguí tipeando para filtrar. En la app también: botón **+** › **Slash commands**.
- Tienen que ir **al principio del mensaje**. Lo que escribís después es el detalle: `/compact quedate con los precios`.
- **Tus skills también son comandos:** aparecen en la misma lista y las usás con `/nombre-de-la-skill`.
- Podés mandarlos mientras Claude trabaja: la mayoría espera a que termine el paso; algunos (como `/usage` o `/tasks`) responden al toque.
- **Algunos existen solo en la terminal** (por ejemplo `/resume` o `/teleport`). Otros, en la app, te contestan `isn't available in this environment` (por ejemplo `/permissions`): ahí usá los botones o los ajustes de la app.

**Probalo:**

```prompt
/
```

**Tenés que ver:** una lista de comandos y, entre ellos, tus skills. Escribí `/co` y queda filtrada (`/compact`, `/context`…).

> **Ojo:** la documentación no tiene una lista cerrada de qué comandos faltan en la pestaña Code. Regla simple: si no aparece al escribir `/`, en la app no está.

## Tareas en segundo plano
Una **tarea en segundo plano** es algo que Claude deja corriendo "atrás" mientras sigue charlando con vos: por ejemplo, tu web de prueba prendida, una descarga larga o un **subagente** (un ayudante) investigando.

**Mandar algo a segundo plano:**
- Pedíselo:

```prompt
Prendé la web de prueba en segundo plano y seguí conmigo. Avisame la dirección para abrirla.
```

- Si un comando tarda más de la cuenta, Claude lo pasa solo a segundo plano en vez de cortarlo.
- **Solo en la terminal:** **Ctrl+B** manda al fondo lo que está corriendo.

**Ver y frenar tareas en la app:**
1. En la barra de arriba de la sesión, abrí el menú **⋮** › **Background tasks**. Aparece cuando la sesión tiene algo corriendo atrás.
2. Ves los subagentes, los comandos y los procesos que están andando.
3. Tocá uno para ver qué está mostrando, o para **frenarlo**.

**Tenés que ver:** en la lista, la tarea que pediste (por ejemplo, la web de prueba).

También podés pedírselo en palabras: "¿qué tenés corriendo en segundo plano?" o "frená la web de prueba".

**En la terminal:** `/tasks` muestra y administra todo lo que corre atrás (también `/bashes`). **Ctrl+T** no es lo mismo: muestra la lista de pasos que Claude se armó para la tarea.

> **Ojo:** en una sesión **Local** de la app, lo que dejás en segundo plano sigue mientras la sesión esté abierta; al cerrar Claude Code se limpia. En la **nube** tiene un tiempo máximo. No confirmamos en la documentación que **Ctrl+B** o `/tasks` funcionen en el cuadro de la app: usá el panel **Background tasks**.

## Los que más vas a usar hoy
| Escribís | Para qué sirve | Ejemplo |
|---|---|---|
| `/nombre-de-la-skill` | Usa una skill a mano. Igual, Claude las usa solo cuando tu pedido coincide | `/armar-mi-cerebro` · `/propuesta-comercial` |
| `/btw [pregunta]` | Una pregunta al costado, **sin cortar lo que Claude está haciendo** | `/btw ¿cómo se llamaba el archivo de precios?` |
| `/compact` | Resume la conversación para liberar lugar sin perder el hilo. Podés decirle qué conservar | `/compact quedate con las decisiones de precios` |
| `/clear` | Conversación nueva, vacía. Conserva el `CLAUDE.md`. Una tarea = una conversación | Cuando terminás un desafío y arrancás otro |
| `/context` | Muestra cuánto de la "memoria de trabajo" está ocupada y con qué | Cuando Claude empieza a olvidarse cosas |
| `/rewind` | Vuelve atrás la conversación y los cambios en archivos | Cuando Claude rompió algo |
| `@archivo` | Le pasa un archivo puntual (te sugiere a medida que escribís) | `Leé @ventas/objeciones.md y armá 3 respuestas` |

> **Tip:** antes de `/clear`, pedile "guardá en `inbox/` lo que decidimos hoy". La próxima vez lo lee y no repetís todo.

## Tu cerebro y tus procesos
| Comando | Qué hace |
|---|---|
| `/init` | Crea un `CLAUDE.md` en una carpeta que no tiene cerebro |
| `/memory` | Abre lo que Claude recuerda (tus `CLAUDE.md`). También sirve decirle "recordá que…" |
| `/skills` | Lista tus skills instaladas |
| `/agents` | Para crear subagentes ([Las piezas](#t2-piezas)) |
| `/plugin` | Instala plugins (paquetes de skills, agentes y MCP). En la app, desde el administrador de plugins |
| `/export` | Guarda la conversación como texto |

## Modelo, uso y conexiones
| Comando | Qué hace | En la app, también |
|---|---|---|
| `/model` | Cambia el modelo (Opus, Sonnet, Haiku, Fable) ([Modelos](#t1-modelos)) | El selector de modelo debajo del cuadro |
| `/effort` | Cuánto piensa: `low`, `medium`, `high`, `xhigh`, `max` | El menú de esfuerzo |
| `/usage` | Cuánto usaste y cuánto te queda | |
| `/insights` | Informe de cómo venís usando Claude Code y qué conviene automatizar | |
| `/mcp` | Tus conexiones MCP y su estado | |
| `/permissions` | Qué puede hacer Claude sin preguntarte (en la terminal; en la app responde que no está disponible) | **Permitir siempre** en el pedido de permiso |
| `/schedule` | Programa una tarea que corre sola en la nube | **Scheduled** en la barra lateral ([Tareas programadas](#t4-tareas-programadas)) |
| `/remote-control` | Seguís esta sesión desde el celular ([Dónde trabajar](#t3-donde-trabajar)) | El interruptor **Remote Control** de la sesión |

> **Ojo:** si un comando no aparece al escribir `/`, actualizá la app de Claude. Lo de modelo y modo también lo tenés con botones debajo del cuadro.

## Teclas en la pestaña Code
En Windows, donde dice **Cmd** es **Ctrl**.

| Tecla | Qué hace |
|---|---|
| **Enter** | Manda el pedido. Mientras Claude trabaja, podés escribir una corrección y mandarla: la lee después del paso que está haciendo |
| **Esc** | Frena a Claude en el momento |
| **Cmd+Shift+M** | Cambia el modo de permisos (**Manual**, **Accept edits**, **Plan**, **Auto**) |
| **Cmd+N** | Sesión nueva |
| **Cmd+;** | Pregunta al costado (igual que `/btw`) |
| **Cmd+Shift+I** | Menú de modelo |
| **Cmd+Shift+E** | Menú de esfuerzo |
| **Cmd+Shift+D** | Panel de cambios (qué archivos tocó) |
| **Cmd+/** | Muestra todos los atajos |

Imágenes y capturas: arrastralas al cuadro o usá el botón **+**.

> **Ojo:** en la pestaña Code, **Shift+Tab no cambia el modo** (en la terminal sí). Usá **Cmd+Shift+M** o el selector de modo.

### Solo en la terminal
Si algún día usás Claude Code en la terminal, estas teclas son de ahí: **Shift+Tab** (cambia el modo), **Esc Esc** (menú para volver atrás), **Ctrl+C** dos veces (sale), **Ctrl+R** (busca pedidos anteriores), **Ctrl+G** (escribe el pedido en un editor), **Ctrl+B** (manda la tarea al fondo), **Ctrl+T** (muestra la lista de pasos de Claude), `/tasks` (tareas en segundo plano), y el símbolo `!` al principio para correr un comando.

## Modo plan: primero pensá, después hacé
Para tareas grandes, elegí **Plan** en el selector de modo (o **Cmd+Shift+M**). Claude lee, investiga y te propone qué va a hacer, **sin tocar nada**. Lo corregís, y recién cuando estás de acuerdo pasás a **Manual** o **Accept edits** para que lo haga.

> **Ojo:** el modo que salta todos los permisos (**Bypass permissions**) no lo uses en el taller. Ver [Datos y seguridad](#t6-datos-y-seguridad).

## Un buen pedido
Un buen prompt es un brief de trabajo: objetivo, contexto, límites y cómo te das cuenta de que está bien.

```prompt
Objetivo: [QUÉ QUERÉS LOGRAR].
Usá: [ARCHIVOS O DATOS, por ejemplo @ventas/preguntas-frecuentes.md].
No hagas: [LÍMITES, por ejemplo no cambies precios, no mandes nada].
Antes de empezar, proponeme un plan de 5 pasos y esperá mi OK.
Al final, mostrame cómo verificaste que funciona.
```

Tres trucos que cambian el resultado:
- **"Haceme preguntas antes de empezar."** Te ahorra la primera versión mala.
- **"Si no está en mis archivos, escribí PENDIENTE."** Evita que invente.
- **Dividí:** primero el plan, después la parte 1, revisás, después la parte 2.

**Probalo:**

```prompt
/context
```

Después probá `/compact quedate solo con lo que decidimos` y volvé a mirar `/context`.

**Tenés que ver:** el detalle de cuánto ocupa cada cosa. Después del `/compact`, ocupa menos.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude "se olvida" de lo que hablaron | `/context`. Si está lleno, `/compact` o `/clear` y empezá con un pedido claro. |
| Te pide permiso todo el tiempo | En el pedido de permiso tocá **Permitir siempre** para ese tipo de acción, o pedile a Claude que te muestre y ajuste los permisos de esta carpeta. |
| Hizo un cambio que no querías | `/rewind`. |
| Se quedó trabado | **Esc** y pedile que te cuente en qué estaba. |
| Quedó algo corriendo que no querés | Menú **⋮** › **Background tasks** › tocá la tarea y frenala. |
| Te quedaste sin uso | `/usage` para ver cuándo se renueva. Pasá a Sonnet en el selector de modelo. |
| Un comando no existe | Actualizá la app de Claude y abrí una sesión nueva. |

## Para seguir solo
- `/insights` cada viernes: mirá qué pedidos te salieron mejor y copialos.
- Cada prompt que repetís por tercera vez, convertilo en skill ([Las piezas](#t2-piezas) y [Kit del taller](#r-kit)).
- **Avanzado, en la terminal:** `claude` abre Claude Code en la carpeta donde estás, `claude -c` sigue la última conversación, `claude -p "[PEDIDO]"` hace un pedido único y sale (sirve para scripts), `claude --permission-mode plan` arranca en modo plan, y `claude doctor` revisa la instalación.
