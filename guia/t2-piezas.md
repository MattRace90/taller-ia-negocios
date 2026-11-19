---
titulo: 'Las piezas: prompt, cerebro, skills, agentes, conectores, MCP y API'
bloque: Teoría
tiempo: 20 min de lectura
para: Todos
necesitas: t1-modelos
resultado: Sabés qué es cada pieza, para qué sirve y dónde se instala, y tenés a mano el glosario de palabras técnicas para leer cualquier tutorial del día sin perderte.
---

Hoy vas a escuchar muchas palabras nuevas: skill, agente, MCP, conector, hook. Son todas piezas alrededor del mismo modelo.
Pensalo así: **Claude es un empleado nuevo muy capaz**. Cada pieza es algo que le das para que trabaje como si llevara años en tu empresa.
Ejemplo: en Denvet, el mismo Claude puede contestar dudas de stock (con el cerebro), armar el pedido semanal (con una skill), leer el Drive (con un conector) y avisarte por Telegram (con la API).

> **Tip:** los **Probalo** de esta página se hacen en **Claude Code**, parado en la carpeta de tu cerebro. Si todavía no instalaste Claude Code ni armaste el cerebro, leé ahora y probá después de [Instalá Claude Code](#s2-claude-code) y [Tu cerebro](#p1-cerebro). Al final de la página está el **glosario** con todas las palabras técnicas del día.

## El mapa en una tabla
| Pieza | Analogía | Qué es | Ejemplo del taller | Dónde se instala |
|---|---|---|---|---|
| **Prompt** | La orden que le das en el momento | Lo que escribís en el chat | "Armá 3 respuestas para alguien que dice que es caro" | En el chat, cada vez |
| **Cerebro / contexto** (`CLAUDE.md`) | El manual del empleado nuevo | Archivos de texto con quién sos, qué vendés, cómo hablás y tus reglas | `CLAUDE.md` + las carpetas `negocio/`, `marca/`, `ventas/` de tu empresa | La carpeta `cerebro-[TU-EMPRESA]` en tu compu (y en GitHub). En la web: un Proyecto |
| **Skill** | Una receta del manual de procesos | Un proceso escrito una vez que Claude sigue cada vez que hace falta | `/propuesta-comercial`, "responder reseñas" | `.claude/skills/` en tu carpeta, o **Customize › Skills** en la app |
| **Agente** | El empleado que trabaja solo | Modelo + instrucciones + datos + herramientas, que decide el siguiente paso hasta terminar | El agente que responde y filtra consultas de Fondus | Claude Code, Cowork, n8n o un bot |
| **Subagente** | El gerente que reparte trabajo a su equipo | Un agente que otro agente llama para una parte de la tarea, con su propia "mochila" | Un "investigador" que lee reseñas y le pasa el resumen al "redactor" | `.claude/agents/` en tu carpeta |
| **Conector** | Las llaves de la oficina | Una conexión lista para usar con una app (Drive, Gmail, Calendar, Canva) | Claude lee tu Google Drive | **Customize › Connectors** en la app de Claude |
| **MCP** | El enchufe universal (el USB-C de la IA) | El estándar con el que cualquier app se conecta a Claude. Un conector es un MCP ya empaquetado | El MCP de n8n, de Metricool, de Supabase | `claude mcp add …` en Claude Code, o **Add custom connector** en la app |
| **API** | El teléfono interno de la empresa | La puerta para que **tus programas** (un bot, n8n) le hablen a Claude sin vos | El bot de Telegram que responde solo | Clave de la consola de Anthropic ([Clave de API](#s9-api-anthropic)), se paga por uso |
| **Hook** | El timbre automático | Un comando que Claude Code corre solo en un momento fijo | Notificación en la compu cuando Claude te necesita | `/hooks` o `.claude/settings.json` |
| **Plugin** | La caja de herramientas armada | Un paquete que trae skills, agentes, hooks y MCP juntos | Instalar `skill-creator` para que Claude te ayude a crear skills | `/plugin` en Claude Code |

## Cómo se combinan

```text
              TU PEDIDO (prompt)
                     │
                     ▼
   ┌─────────────────────────────────────┐
   │  MODELO (Opus / Sonnet / Haiku)      │
   │   + CEREBRO  → sabe quién sos        │
   │   + SKILLS   → sabe cómo lo hacés    │
   │   + CONECTORES / MCP → puede tocar   │
   │       Drive, Gmail, n8n, Supabase    │
   └─────────────────────────────────────┘
          │                    │
   lo usás vos            lo usa un programa
   (chat, Cowork,         (bot, n8n, tarea
    Claude Code)           programada) → API
          │
   si la tarea es grande, reparte en SUBAGENTES
   y los HOOKS avisan o controlan en el camino
```

La regla: **el modelo es el motor; el cerebro y las skills lo hacen tuyo; los conectores le dan manos.**

## Cada pieza, de a una

### Prompt: el pedido
Un buen prompt es un brief de trabajo, no una pregunta suelta. Tiene objetivo, contexto, límites y cómo te das cuenta de que está bien.
**Antes:** "Escribí un post sobre créditos."
**Después:** "Leé `marca/voz.md`. Escribí un post para Instagram de Fondus para alguien que ya fue rechazado por un banco. Tono cercano, sin prometer aprobación. Si te falta un dato, PENDIENTE."

**Probalo:**

```prompt
Objetivo: [QUÉ QUERÉS LOGRAR].
Contexto: [PARA QUIÉN ES Y QUÉ TENÉS QUE SABER].
No hagas: [LÍMITES, por ejemplo no inventes precios].
Antes de empezar, haceme las preguntas que necesites para hacerlo bien.
```

### Cerebro: el manual del empleado nuevo
Claude no tiene memoria entre chats ([por qué](#t1-modelos)). El cerebro es la solución: archivos de texto que lee **antes** de trabajar.
- `CLAUDE.md`: tus reglas y el mapa de la carpeta. Claude Code lo lee **siempre** al abrir esa carpeta. Corto: menos de 200 líneas.
- Los archivos de `negocio/`, `marca/` y `ventas/`: qué vendés, a quién, precios, voz, preguntas frecuentes. Claude los lee cuando la tarea los pide.
- `fuentes/`: los documentos de origen, por ejemplo el borrador `CONTEXTO-borrador.md` que te preparamos.
- En la web y el celular, lo mismo se logra con un **Proyecto** que tiene esos archivos cargados.

Cómo armarlo: [Tu cerebro](#p1-cerebro) y [Usá tu borrador](#c2-tu-borrador).

**Probalo** (en Claude Code, en la carpeta de tu cerebro):

```prompt
Leé mi CLAUDE.md y decime en 5 líneas qué sabés de mi empresa. Después decime las 3 cosas que te faltan saber para ayudarme mejor.
```

### Skill: la receta que se escribe una vez
Un prompt lo escribís cada vez. **Una skill la escribís una vez y se ejecuta mil.**
Es una carpeta con un archivo `SKILL.md`: un nombre, una descripción ("cuándo usarme") y los pasos. Claude la usa sola cuando tu pedido coincide con la descripción, o la llamás con `/nombre`.
Ejemplo: La Consejera del Éxito tiene una skill "placa en mi voz" que siempre lee su estilo, arma 3 opciones y espera el OK.

- En Claude Code: `.claude/skills/<nombre>/SKILL.md` (de la carpeta) o `~/.claude/skills/<nombre>/SKILL.md` (para todas tus carpetas). `/skills` las lista.
- En la app: **Customize › Skills** (subís un ZIP). Requiere **Settings › Capabilities › Code execution and file creation** activado.

**Probalo:**

```prompt
Revisá lo que hicimos en esta conversación y convertilo en una skill llamada [NOMBRE-EN-MINUSCULAS] en .claude/skills/. Que la descripción diga claramente cuándo usarla. Mostrámela antes de guardarla.
```

### Agente: el empleado que trabaja solo
Un chat responde una vez. Un agente **trabaja en ciclo**: mira, decide el siguiente paso, usa una herramienta, revisa el resultado y sigue hasta terminar.
**Agente = modelo + instrucciones + datos + herramientas.**

| | Bot de menú | Automatización (n8n) | Agente |
|---|---|---|---|
| Cómo funciona | "Marcá 1 para ventas" | Siempre los mismos pasos: si pasa A, hacé B | Decide qué hacer según el caso |
| Bueno para | Opciones fijas | Tareas repetidas y predecibles | Casos distintos cada vez |
| Ejemplo | Menú de WhatsApp | Cada formulario nuevo va a una planilla | Lee la consulta, busca en tus preguntas frecuentes, responde o deriva a una persona |

Claude Code y Cowork **ya son agentes**. Lo que vas a armar hoy son agentes con un objetivo propio: [Agente que responde y filtra](#p3-agente-preguntas), [Asistente en Telegram](#p2-asistente-telegram).

> **Ojo:** nunca le des autonomía a algo que no viste funcionar. Antes de dejarlo solo, pasá el [checklist del agente seguro](#t6-datos-y-seguridad).

### Subagente: el gerente con equipo
Cuando la tarea es grande, Claude puede repartirla en subagentes. Cada uno trabaja con su propia ventana de contexto y le devuelve solo el resultado al principal. Así la conversación principal no se llena.
Ejemplo: "investigador" lee 200 reseñas de agencias de viaje y le pasa a "redactor" los 5 dolores más repetidos.
- Se guardan en `.claude/agents/<nombre>.md` con `name`, `description` y las instrucciones.
- Se crean pidiéndoselo a Claude. `/agents` hoy solo te recuerda eso: no es un gestor con botones.

**Probalo:**

```prompt
Creá un subagente en .claude/agents/ llamado investigador-resenas. Su trabajo: leer los archivos de la carpeta [CARPETA CON RESEÑAS, por ejemplo fuentes/resenas] y devolver los 5 dolores más repetidos, con una cita textual de cada uno. Solo lectura: que no edite nada.
```

### Conector y MCP: las llaves y el enchufe
**MCP** (Model Context Protocol) es el estándar para conectar apps a una IA: como el USB-C, el mismo enchufe sirve para todo. **Un conector es un MCP ya armado** que activás con un click.

| | Conector | MCP "a mano" | API |
|---|---|---|---|
| Para quién | Vos, desde la app | Vos, desde Claude Code | Tus programas |
| Cómo se instala | **Customize › Connectors** › **Connect** | `claude mcp add …` | Clave + código o n8n |
| Ejemplo | Gmail, Drive, Calendar, Canva | n8n, Supabase, Metricool | Bot de Telegram, flujo de n8n |

- Los conectores de [claude.ai](https://claude.ai) también aparecen en Claude Code si entrás con la misma cuenta.
- `/mcp` en Claude Code muestra el estado de tus conexiones.

Paso a paso: [Conectores y MCP](#s8-conectores-y-mcp) y [Conectá todo](#s10-conectar-todo).

**Probalo** (con Google Drive conectado):

```prompt
Buscá en mi Google Drive el último archivo con la palabra "precios" y resumime qué cambió respecto del anterior. No modifiques nada.
```

### API: el teléfono interno
La suscripción (Pro, Max) es para que **vos** uses Claude. La **API** es para que **un programa** lo use sin vos: el bot que responde de noche, el flujo de n8n que clasifica mails.
- Se paga aparte, por consumo, con créditos prepagos en la consola de Anthropic.
- Funciona con una **clave** (empieza con `sk-ant-`) que es como la llave de tu casa: nunca en el chat, nunca en GitHub ([Datos y seguridad](#t6-datos-y-seguridad)).

Cómo sacar la clave: [Clave de API](#s9-api-anthropic). Precios: [Stack y costos](#r-stack-y-costos).

### Hook: el timbre automático
Un hook es un comando que Claude Code corre solo en un momento definido: antes de usar una herramienta, al terminar, cuando necesita tu atención.
Ejemplo útil para empezar: que la compu te avise cuando Claude está esperando tu OK, así no te quedás mirando la pantalla.
Se configura con `/hooks` o en `.claude/settings.json`.

**Probalo:**

```prompt
Configurá un hook de notificación para que mi compu me avise con un mensaje "Claude Code te necesita" cada vez que estés esperando mi respuesta. Explicame qué archivo vas a tocar antes de hacerlo.
```

### Plugin: la caja de herramientas armada
Un plugin junta varias piezas (skills, subagentes, hooks, MCP) en un solo paquete que se instala de una. Se manejan con `/plugin` en Claude Code.
Ejemplo: `/plugin install skill-creator@claude-plugins-official` instala una skill que te ayuda a crear skills.

> **Ojo:** instalá plugins y MCP solo de fuentes que conocés (el marketplace oficial, la empresa dueña de la app). Un plugin puede correr comandos en tu compu.

## Glosario: palabras técnicas en una línea
Cuando una página use una de estas palabras sin explicarla, volvé acá.

| Palabra | Qué es, en simple |
|---|---|
| **Terminal** (en Windows, **PowerShell**) | Una ventana donde le das órdenes a la compu escribiendo. Copiás el comando, lo pegás y apretás **Enter**. |
| **Comando** | Una orden que se escribe en la terminal. Por ejemplo, `claude` abre Claude Code. |
| **Carpeta y ruta** | La ruta es la "dirección" de un archivo: `Documentos/cerebro-fondus/CLAUDE.md`. |
| **`cd`** | El comando para "entrar" a una carpeta en la terminal: `cd Documents`. Truco: escribí `cd ` (con espacio), arrastrá la carpeta a la ventana y apretá **Enter**. |
| **Archivo `.md` (Markdown)** | Un archivo de texto común, con títulos (`#`) y listas (`-`). Se abre con cualquier editor; Obsidian lo muestra prolijo. |
| **Git** | Un programa que guarda el historial de cambios de una carpeta. |
| **GitHub** | La web donde guardás una copia de esa carpeta en la nube, privada. |
| **Repositorio (repo)** | Una carpeta que Git vigila, y su copia en GitHub. Tu cerebro va a ser un repo. |
| **Commit** | Una "foto" guardada de cómo están tus archivos, con una frase que dice qué cambiaste. |
| **Push / Pull** | Push = subir tus commits a GitHub. Pull (o Fetch) = bajar lo nuevo que hay en GitHub. |
| **Rama (branch) y pull request (PR)** | La rama es una copia aparte para probar cambios. El PR es el pedido para sumarlos a la versión principal: vos lo revisás y lo aceptás. |
| **Token (en IA)** | Un pedacito de palabra. Es lo que mide cuánto lee y escribe Claude, y lo que se paga en la API. |
| **Token (en apps)** | Una contraseña larga para que un programa entre a tu cuenta (por ejemplo, el token de tu bot de Telegram). **Es secreto.** |
| **API key (clave de API)** | Una contraseña para que un programa use un servicio y te cobre a vos. **Es secreta.** |
| **Variable de entorno** | Un dato con nombre (`NOMBRE=valor`) que un programa lee al arrancar. Así se le pasan las claves sin escribirlas en el código. |
| **`.env`** | Un archivo de texto con esas variables, una por línea. Vive solo en tu compu y nunca se sube a GitHub. Cómo crearlo: [Datos y seguridad](#t6-datos-y-seguridad). |
| **`.gitignore`** | La lista de archivos que Git **no** tiene que subir nunca. Ahí va el `.env`. |
| **OAuth ("Iniciar sesión con…")** | Cuando una app te manda a Google, GitHub o Facebook para que digas "sí, le doy permiso". La app nunca ve tu contraseña. |
| **Cron** | Una forma de escribir horarios para tareas automáticas. `7 9 * * 1` = minuto 7, hora 9, todos los lunes. |
| **Webhook** | Una dirección web que recibe un aviso cuando pasa algo ("llegó un mensaje") y dispara otra cosa. |
| **Deploy** | Publicar una versión nueva de tu web o tu bot. |
| **Bóveda (vault)** | En Obsidian, la carpeta que abrís como cuaderno. |
| **Localhost** | Tu propia compu haciendo de servidor. `http://localhost:3000` solo lo ves vos. |
| **Node, npm y npx** | Node corre programas escritos en JavaScript. npm los instala. npx los corre sin instalarlos. |
| **CLI** | Un programa que se usa desde la terminal (Claude Code, `wrangler`, `higgsfield`). |
| **JSON** | Un formato de texto para datos: `{"nombre": "Toby"}`. |
| **Self-hosted** | Instalado en tu compu o en tu servidor, en vez de en la nube del proveedor. |

## Para seguir solo
- Dibujá tu empresa con estas piezas: qué va en el cerebro, qué 3 procesos se vuelven skills, qué apps conectás.
- Cada vez que repitas el mismo prompt por tercera vez, convertilo en skill.
- Mirá [Dónde trabajar](#t3-donde-trabajar) para saber en qué lugar usar cada pieza.
