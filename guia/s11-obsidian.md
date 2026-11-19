---
titulo: Obsidian, tu segundo cerebro
bloque: Setup
tiempo: 30 min
para: Todos
necesitas: p1-cerebro, s4-github
resultado: Obsidian abierto sobre la carpeta de tu cerebro, con links entre notas, sincronizado con GitHub y una rutina semanal para mantenerlo ordenado.
---

Claude Code escribe tu cerebro en archivos `.md`. Obsidian es el cuaderno donde **vos** los leés, los editás y ves cómo se conectan. Es la misma carpeta: lo que cambia uno, lo ve el otro al instante.
Ejemplo: en La Consejera del Éxito, Claude guarda en `ventas/objeciones.md` la respuesta nueva a "no tengo tiempo". La dueña la abre en Obsidian, le ajusta una frase y la próxima propuesta ya sale con la versión corregida.

## Antes de empezar
- [ ] La carpeta de tu cerebro creada (por ejemplo `cerebro-[TU-EMPRESA]` en **Documentos**) ([Armá el cerebro](#p1-cerebro)).
- [ ] La carpeta subida a GitHub como repositorio **privado** ([GitHub](#s4-github)).
- [ ] GitHub Desktop instalado y con tu sesión iniciada.

> **Datos:** Obsidian guarda todo **en tu compu**, en archivos comunes. No sube nada a ningún lado salvo que actives Sync o Git. En el cerebro va cómo funciona tu negocio, no datos personales de tus clientes.

> **Costo:** Obsidian es **gratis, también para uso comercial** (la licencia comercial de USD 50 por usuario por año es opcional). **Obsidian Sync** cuesta **USD 4/mes con pago anual o USD 5/mes mensual** (nov 2026, [obsidian.md/pricing](https://obsidian.md/pricing)). No lo necesitás para empezar.

## Paso 1 · Instalá Obsidian
Si ya lo instalaste en [Herramientas base](#s3-herramientas-base), Paso 5, saltá al Paso 2.

1. Entrá a **[obsidian.md/download](https://obsidian.md/download)**.

<div data-os="mac">

2. Bajá la versión para macOS, abrí el `.dmg` y arrastrá **Obsidian** a **Aplicaciones**.
3. Abrilo desde **Aplicaciones**. Si macOS pregunta si querés abrir una app descargada de internet, tocá **Abrir**.

</div>
<div data-os="win">

2. Bajá el instalador para Windows (`.exe`) y abrilo. Se instala solo.
3. Abrí **Obsidian** desde el menú Inicio.

</div>

**Tenés que ver:** la pantalla de bienvenida de Obsidian, con las opciones para crear o abrir una bóveda.

## Paso 2 · Abrí tu cerebro como bóveda
Una **bóveda** (vault) es solo una carpeta que Obsidian muestra como cuaderno.

1. En la bienvenida, tocá **Abrir carpeta como bóveda** (en inglés, **Open folder as vault**).
2. Elegí tu carpeta `cerebro-[TU-EMPRESA]` (la misma que subiste a GitHub).
3. Si pregunta si confiás en el autor de la bóveda, tocá **Confiar** (es tu carpeta).

> **Ojo:** no crees una bóveda nueva vacía: abrí **la carpeta que ya existe**. Si no, vas a tener dos cerebros que no se hablan.

**Tenés que ver:** a la izquierda, las carpetas `negocio/`, `marca/`, `ventas/`… y tu `CLAUDE.md`.

> **Tip:** dejá abierta en otra pestaña [Usá Obsidian como un pro](#s11b-obsidian-atajos): las 10 teclas de todos los días, el grafo con colores y cómo capturar al inbox.

## Paso 3 · Sumá las carpetas que faltan
La estructura sugerida para todo el taller:

| Carpeta | Qué va |
|---|---|
| `inbox/` | Todo lo que entra sin ordenar: notas rápidas, audios transcritos, ideas. Claude lo archiva una vez por semana |
| `negocio/` | Qué vendés, a quién, precios, diferencial |
| `marca/` | Voz, palabras que usás y que nunca usás, ejemplos reales |
| `ventas/` | Preguntas frecuentes, objeciones y cómo las respondés, guiones |
| `equipo/` | Quién hace qué, cómo se deriva una consulta |
| `operacion/` | Procesos paso a paso (cómo se arma un pedido, cómo se agenda un turno) |
| `datos/` | `reglas.md` (qué datos se le pasan a la IA y cuáles no) y números del negocio que sí se pueden compartir (ventas por mes, ticket promedio). Nunca datos de clientes |
| `objetivos/` | Metas del trimestre y `pendientes.md` |
| `fuentes/` | Material de origen: tu `CONTEXTO-borrador.md`, PDFs, presentaciones. Si algo tiene datos de clientes, va al `.gitignore` |

Las carpetas que creó la skill `armar-mi-cerebro` ya están. Solo falta `inbox/`. En Claude Code, parado en la carpeta del cerebro:

```prompt
Revisá la estructura de este cerebro. Creá las carpetas que falten de esta lista: inbox, negocio, marca, ventas, equipo, operacion, datos, objetivos, fuentes. En cada carpeta nueva dejá un README.md de 2 líneas que diga qué va ahí. No muevas ni borres nada de lo que ya existe.
Después agregá al CLAUDE.md esta regla: "Cuando escribas o actualices una nota, enlazá las notas relacionadas con [[nombre-de-la-nota]] y dejá todo lo nuevo sin clasificar en inbox/".
```

**Tenés que ver:** en Obsidian aparecen las carpetas nuevas sin que hagas nada.

## Paso 4 · Usá links entre notas
En Obsidian, escribir `[[` abre un buscador de notas. Elegís una y queda un link: `[[objeciones]]`. Así el cerebro se vuelve una red y no una pila de archivos sueltos.

1. Abrí `negocio/empresa.md` (o el archivo principal de tu negocio).
2. Donde nombres un producto o una objeción, escribí `[[` y elegí la nota correspondiente.
3. Abrí la **vista de grafo** (ícono de red en la barra izquierda, o **Ctrl/Cmd + G**) para ver cómo se conectan.

Claude Code entiende estos links: cuando lee `[[objeciones]]`, sabe que tiene que ir a buscar esa nota.

> **Tip:** usá nombres de archivo cortos, en minúsculas y sin tildes (`objeciones.md`, `precios.md`). Los links quedan más limpios y Claude los encuentra mejor.

**Tenés que ver:** en el grafo, tus notas conectadas por líneas.

## Paso 5 · Cómo conviven Claude Code y Obsidian
| Lo hace Claude Code | Lo hacés vos en Obsidian |
|---|---|
| Escribe y actualiza notas largas | Leés, corregís una frase, agregás un dato |
| Archiva el `inbox/` y crea links | Tirás ideas rápidas en `inbox/` |
| Hace el commit en Git | Revisás el grafo y los pendientes |

Una sola regla: **no edites el mismo archivo en los dos al mismo tiempo**. Si Claude está escribiendo una nota, esperá a que termine antes de tocarla en Obsidian.

**Tenés que ver:** pedile a Claude que cambie una línea de una nota y mirá cómo se actualiza en Obsidian en segundos.

## Paso 6 · Sincronizá con GitHub
Tenés dos caminos. Elegí uno.

**Opción A · GitHub Desktop (la más simple):** cuando terminás de trabajar, abrís GitHub Desktop, escribís un resumen del cambio, **Commit to main** y **Push origin**. Es lo mismo que ya usaste en [GitHub](#s4-github).

**Opción B · Plugin Git de Obsidian (automático):**
1. **Settings** (engranaje abajo a la izquierda) › **Community plugins** › **Turn on community plugins**.
2. **Browse** › buscá **Git** (de Vinzent) › **Install** › **Enable**.
3. En las opciones del plugin, poné un intervalo de guardado y sincronización automática (por ejemplo, cada 30 minutos) y activá que traiga los cambios al abrir Obsidian.

> **Ojo:** el plugin usa el Git instalado en tu compu ([Herramientas base](#s3-herramientas-base)). Los nombres de las opciones cambian entre versiones: verificá en la pantalla del plugin cuál es el intervalo de **commit-and-sync** y cuál el de **pull**.

Agregá esto al `.gitignore` para no subir la configuración de pantalla de Obsidian:

```prompt
Agregá al .gitignore de esta carpeta las líneas .obsidian/workspace.json y .obsidian/workspace-mobile.json, y hacé commit con el mensaje "Ignorar layout de Obsidian".
```

> **Ojo:** no pongas la carpeta del cerebro adentro de iCloud Drive, OneDrive o Google Drive **y además** en Git. Dos sincronizadores sobre la misma carpeta terminan en archivos duplicados o rotos. Elegí uno: para el taller, GitHub.

**Tenés que ver:** en [github.com](https://github.com), tu repo con el último cambio de hace minutos.

## Paso 7 · Llevalo al celular
| Opción | Costo | Cómo | Para quién |
|---|---|---|---|
| **Obsidian Sync** | USD 4-5/mes | En la compu: **Settings › Sync**. En el celu: app Obsidian, misma cuenta | El que edita mucho desde el celular |
| **App de GitHub** | Gratis | Bajá **GitHub** en el celu y abrí tu repo privado | Solo leer (consultar un precio, una respuesta) |
| **Plugin Git en el celu** | Gratis | App Obsidian + plugin Git con un token de GitHub | Quien se anima: sus autores avisan que en el celu es **inestable** |
| **Proyecto en [claude.ai](https://claude.ai)** | Incluido en Pro | Subís los archivos del cerebro a un **Proyecto** | Preguntarle al cerebro desde el celu |

> **Tip:** para la mayoría alcanza con la **app de GitHub** para leer y un **Proyecto en [claude.ai](https://claude.ai)** para preguntar. Si en 30 días ves que editás seguido desde el celu, pagá Sync.

**Tenés que ver:** tu cerebro abierto en el celular por el camino que elegiste.

## Paso 8 · Armá la rutina semanal
15 minutos, una vez por semana (por ejemplo, el lunes a primera hora). Las carpetas que creó la skill `armar-mi-cerebro` ya están. Solo falta `inbox/`. En Claude Code, parado en la carpeta del cerebro:

```prompt
Hacé el mantenimiento semanal del cerebro:
1. Revisá inbox/ y archivá cada nota en la carpeta correcta (negocio, marca, ventas, equipo, operacion, datos, objetivos o fuentes). Si una nota completa algo que ya existe, sumala a ese archivo en vez de crear uno nuevo.
2. Agregá links [[...]] entre las notas relacionadas.
3. Si encontrás datos personales de clientes (nombres, teléfonos, DNI, deudas), no los muevas: avisame cuáles son.
4. Actualizá objetivos/pendientes.md con lo que quedó sin resolver.
5. Mostrame un resumen de lo que moviste y hacé commit con el mensaje "Mantenimiento semanal [FECHA]".
No borres nada sin preguntarme.
```

> **Tip:** podés dejar esta rutina como tarea programada para que Claude la corra solo cada lunes ([Tareas programadas](#t4-tareas-programadas)).

**Tenés que ver:** `inbox/` vacío o casi, y un commit nuevo en GitHub.

## Cómo sé que funcionó
1. Escribí en Obsidian una nota nueva en `inbox/` con una idea suelta (por ejemplo: "Probar promo 2x1 los martes").
2. En Claude Code:

```prompt
Leé lo que hay en inbox/, decime en qué carpeta lo archivarías y con qué notas lo enlazarías. Después hacelo.
```

**Tenés que ver:** la nota movida, con links `[[...]]`, visible en Obsidian y en el grafo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Obsidian no muestra los archivos que creó Claude | Fijate que abriste la carpeta correcta como bóveda: **Settings › About** (o el nombre arriba a la izquierda) muestra la ruta. |
| No encuentro **Community plugins** | Está en **Settings**, abajo de **Core plugins**. Primero activá **Turn on community plugins**. |
| El plugin Git dice que no encuentra Git | Instalá Git ([Herramientas base](#s3-herramientas-base)) y reiniciá Obsidian. Mientras tanto, usá GitHub Desktop. |
| Aparecen archivos "conflicted" o duplicados | Tenés dos sincronizadores. Sacá la carpeta de iCloud/OneDrive/Drive y dejá solo GitHub. |
| Un link `[[...]]` sale en otro color y no abre nada | La nota no existe con ese nombre. Hacé clic y Obsidian la crea, o corregí el nombre. |
| GitHub Desktop no ve cambios hechos en Obsidian | Guardá la nota (se guarda sola al dejar de escribir) y tocá **Fetch origin** o reabrí GitHub Desktop. |

## Para seguir solo
- Sumá una nota diaria: **Settings › Core plugins › Daily notes** y que vaya a `inbox/`. Volcá ahí lo que pase en el día y dejá que la rutina semanal lo ordene.
- Invitá a tu equipo al repo privado. Cada uno abre la misma carpeta en su Obsidian y todos (y Claude) leen la misma versión.
- Cuando el cerebro crezca, pedile a Claude que arme un `INDICE.md` con links a las notas más importantes.

## Fuentes
Consultadas el 18/11/2026.
- Obsidian, descarga y precios (uso comercial, Sync, Publish): https://obsidian.md/download · https://obsidian.md/pricing
- Plugin Git para Obsidian (soporte en el celular "muy inestable"): https://github.com/Vinzent03/obsidian-git · https://publish.obsidian.md/git-doc
- Estructura y checklist de cerebro reutilizada del kit de Brujería (oct 2026).
