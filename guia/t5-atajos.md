---
titulo: Atajos de Claude Code
bloque: Teoría
tiempo: 15 min
para: Todos
necesitas: s2-claude-code
resultado: Manejás Claude Code con los comandos y las teclas que más se usan, y sabés armar un buen pedido.
---

Claude Code se maneja escribiendo en español y con unos pocos comandos que empiezan con `/`. Este es el machete para tener abierto durante el día y después.
Datos verificados en la documentación oficial el 18/11/2026. Si un comando no te aparece, actualizá con `claude update`.
¿Dudás si usar el chat, Cowork, Claude Code o la nube? Está en [Dónde trabajar](#t3-donde-trabajar).

## Antes de empezar
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] Claude Code abierto en una carpeta de trabajo: en la terminal (la ventana donde escribís comandos; en Windows, **PowerShell**) escribiste `claude`, o abriste la pestaña **Code** de la app. Para practicar sin miedo, usá la carpeta `prueba-claude` de [Instalá Claude Code](#s2-claude-code).

Los comandos `/` y las teclas funcionan en la terminal y en la pestaña **Code**. Escribí `/` y aparece la lista completa con buscador. Para usar uno, escribilo y apretá **Enter**.

**Tenés que ver:** al escribir `/`, una lista de comandos que se filtra a medida que tipeás.

## La memoria de trabajo (que no se "olvide")
| Comando | Qué hace | Cuándo usarlo |
|---|---|---|
| `/context` | Muestra cuánto de la "memoria de trabajo" (la ventana de contexto) está ocupada y con qué | Cuando Claude empieza a olvidarse cosas o a andar lento |
| `/compact` | Resume la conversación y libera lugar | En medio de una tarea larga. Podés guiarlo: `/compact quedate con las decisiones de precios` |
| `/clear` | Empieza una conversación nueva, vacía. Conserva el `CLAUDE.md` | Cuando cambiás de tema. Una tarea = una conversación |
| `/resume` | Retoma una conversación anterior de esta compu | Al otro día, para seguir donde quedaste |
| `/rewind` | Vuelve atrás la conversación y los cambios en archivos (también `/undo`) | Cuando Claude rompió algo |
| `/export` | Guarda la conversación como texto | Para compartir lo que hiciste o guardarlo en tu cerebro |

> **Tip:** antes de `/clear`, pedile "guardá en `inbox/` lo que decidimos hoy" (si la carpeta no existe, la crea). La próxima vez lo lee y no repetís todo.

## Tu cerebro y tus procesos
| Comando | Qué hace | Cuándo usarlo |
|---|---|---|
| `/init` | Crea un `CLAUDE.md` para la carpeta | En una carpeta nueva que no tiene cerebro |
| `/memory` | Abre y edita lo que Claude recuerda (tus `CLAUDE.md`) | Para corregir o sumar una regla permanente. También sirve decirle "recordá que…" |
| `/skills` | Lista tus skills | Para ver qué procesos tenés instalados |
| `/agents` | Te recuerda cómo crear subagentes: pidiéndoselo a Claude o en `.claude/agents/` | Cuando querés repartir una tarea grande ([Las piezas](#t2-piezas)) |
| `/plugin` | Instala y maneja plugins (paquetes de skills, agentes y MCP) | Por ejemplo: `/plugin install skill-creator@claude-plugins-official` |

## Modelo, uso y conexiones
| Comando | Qué hace | Cuándo usarlo |
|---|---|---|
| `/model` | Cambia el modelo (Opus, Sonnet, Haiku, Fable). Con flechas izquierda/derecha cambiás el esfuerzo | Tareas difíciles: Opus. Simples: Sonnet o Haiku ([Modelos](#t1-modelos)) |
| `/effort` | Cuánto piensa antes de responder: `low`, `medium`, `high`, `xhigh`, `max` | `/effort high` para diseñar algo; `low` para ordenar archivos |
| `/usage` | Cuánto usaste y cuánto te queda del plan (también `/cost`) | Para no quedarte sin uso en medio del taller |
| `/insights` | Arma un reporte de cómo venís usando Claude Code | Una vez por semana, para mejorar tus pedidos |
| `/mcp` | Muestra tus conexiones MCP (n8n, Supabase, Metricool…) y su estado | Cuando una herramienta no responde |
| `/permissions` | Qué puede hacer Claude sin preguntarte | Para dejar de aprobar siempre lo mismo |
| `/hooks` | Configura acciones automáticas (por ejemplo, un aviso cuando Claude te necesita) | Una vez, para que te avise |

## Nube, celular y tareas que corren solas
| Comando | Qué hace | Más info |
|---|---|---|
| `/schedule` | Programa una tarea que corre sola en la nube (también `/routines`). `/schedule list` las muestra | [Tareas programadas](#t4-tareas-programadas) |
| `/loop 5m [TAREA]` | Repite un pedido cada cierto tiempo mientras la sesión está abierta | [Tareas programadas](#t4-tareas-programadas) |
| `/remote-control` | Conecta esta sesión para seguirla desde el celular o el navegador (también `/rc`) | [Dónde trabajar](#t3-donde-trabajar) |
| `/teleport` | Trae a tu compu una sesión que estaba corriendo en la nube (también `/tp`) | [Dónde trabajar](#t3-donde-trabajar) |
| `/tasks` | Muestra las tareas que corren en segundo plano | |

## Cuando algo anda mal
| Comando | Qué hace |
|---|---|
| `/doctor` | Revisa que la instalación esté bien y te dice qué arreglar. Desde afuera: `claude doctor` |
| `/login` | Volvés a entrar con tu cuenta (si dice que tu plan no incluye Claude Code) |
| `/feedback` | Le avisás a Anthropic de un error |

## Teclas
| Tecla | Qué hace |
|---|---|
| **Shift+Tab** (en Windows puede ser **Alt+M**) | Cambia el modo: **manual** (pregunta todo) → **aceptar cambios** → **plan** (solo propone, no toca nada) |
| **Esc** | Frena a Claude en el momento |
| **Esc Esc** (con el cuadro vacío) | Abre el menú para volver atrás (igual que `/rewind`) |
| **Ctrl+C** dos veces | Sale de Claude Code |
| **Flecha arriba** | Repite tus pedidos anteriores |
| **Ctrl+R** | Busca en tus pedidos anteriores |
| **Ctrl+V** (Mac) · **Alt+V** (Windows) | Pega una imagen o captura de pantalla. En iTerm2 (Mac): **Cmd+V** |
| **Option+P** (Mac) · **Alt+P** (Windows) | Cambia de modelo sin escribir `/model` |
| **Ctrl+G** | Abre tu pedido en un editor de texto, para escribir uno largo cómodo |
| **Ctrl+B** | Manda la tarea que está corriendo al fondo y te deja seguir escribiendo |

## Símbolos al principio del pedido
| Escribís | Qué hace | Ejemplo |
|---|---|---|
| `/` | Abre los comandos y tus skills | `/propuesta-comercial` |
| `@` | Adjunta un archivo o carpeta (te sugiere a medida que escribís) | `Leé @ventas/objeciones.md y armá 3 respuestas` |
| `!` | Corre un comando de terminal sin salir de Claude Code | `!ls` (Mac) · `!dir` (Windows) |

## Modo plan: primero pensá, después hacé
Para tareas grandes, apretá **Shift+Tab** hasta que diga **plan**. Claude lee, investiga y te propone qué va a hacer, **sin tocar nada**. Lo corregís, y recién cuando estás de acuerdo lo dejás hacer.
También podés arrancar directo en modo plan (en Windows, el mismo comando en PowerShell):

```bash
claude --permission-mode plan
```

En la pestaña **Code** de la app, el modo se elige en el selector de permisos: **Manual**, **Accept edits**, **Plan**, **Auto**.

> **Ojo:** el modo que salta todos los permisos (**Bypass permissions**) no lo uses en el taller. Ver [Datos y seguridad](#t6-datos-y-seguridad).

## Comandos para abrir Claude Code desde la terminal
Estos se escriben **en la terminal**, antes de entrar a Claude Code (no adentro). Son iguales en Mac y en Windows.

| Comando | Qué hace |
|---|---|
| `claude` | Abre Claude Code en la carpeta donde estás |
| `claude -c` | Sigue la última conversación de esta carpeta |
| `claude -r` | Te muestra la lista de conversaciones anteriores para elegir una (o `claude -r "[NOMBRE]"`) |
| `claude -p "[PEDIDO]"` | Hace un pedido único, imprime la respuesta y sale. Sirve para scripts y tareas programadas |
| `claude --model sonnet` | Abre con un modelo elegido |
| `claude --cloud "[TAREA]"` | Arranca una sesión nueva en la nube con esa tarea |
| `claude --teleport` | Trae a la compu una sesión de la nube |
| `claude --remote-control` | Abre una sesión ya conectada para seguirla desde el celular |
| `claude update` | Actualiza Claude Code (igual se actualiza solo) |
| `claude doctor` | Revisa la instalación |

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

Mirá qué está ocupando la ventana. Después probá `/compact quedate solo con lo que decidimos` y volvé a mirar `/context`.

**Tenés que ver:** una cuadrícula de colores con cuánto ocupa cada cosa. Después del `/compact`, ocupa menos.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude "se olvida" de lo que hablaron | `/context`. Si está lleno, `/compact` o `/clear` y empezá con un pedido claro. |
| Te pide permiso todo el tiempo | Elegí "permitir siempre" para ese tipo de acción, o revisá `/permissions`. |
| Hizo un cambio que no querías | `/rewind` o **Esc Esc**. |
| Se quedó trabado | **Esc** y pedile que te cuente en qué estaba. |
| Te quedaste sin uso | `/usage` para ver cuándo se renueva. Pasá a Sonnet con `/model sonnet`. |
| Un comando no existe | Actualizá con `claude update` y volvé a abrir. |

## Para seguir solo
- `/insights` cada viernes: mirá qué pedidos te salieron mejor y copialos.
- Cada prompt que repetís por tercera vez, convertilo en skill ([Las piezas](#t2-piezas) y [Kit del taller](#r-kit)).
- Probá `/schedule` con algo simple: "todos los lunes a las 9:07, resumime los pendientes de mi cerebro" ([Tareas programadas](#t4-tareas-programadas)).
