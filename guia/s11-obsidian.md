---
titulo: Obsidian, tu segundo cerebro (opcional)
bloque: Setup
tiempo: 10 min
para: Opcional (todos)
necesitas: p1-cerebro
resultado: Obsidian abierto sobre la carpeta de tu cerebro, para leer y editar lo que escribe Claude.
---

> **Opcional:** para el taller **no hace falta**. Claude trabaja igual sobre tu carpeta desde la pestaña Code. Obsidian solo es una forma linda de **leer y editar** esa misma carpeta, con links entre notas. Si estás corto de tiempo, salteá esta página.

Claude escribe tu cerebro en archivos `.md`. Obsidian es el cuaderno donde **vos** los leés y ves cómo se conectan. Es la misma carpeta: lo que cambia uno, lo ve el otro al instante.
Ejemplo: Claude guarda en `ventas/objeciones.md` la respuesta nueva a "no tengo tiempo". La dueña de La Consejera del Éxito la abre en Obsidian, le ajusta una frase y listo.

## Antes de empezar
- [ ] La carpeta de tu cerebro creada ([Armá el cerebro](#p1-cerebro)).
- [ ] (Recomendado) La carpeta guardada en GitHub ([GitHub](#s4-github)).

> **Costo:** Obsidian es **gratis, también para uso comercial**. **Obsidian Sync** (para el celular) cuesta USD 4-5/mes (nov 2026, [obsidian.md/pricing](https://obsidian.md/pricing)). No lo necesitás.

## Paso 1 · Instalá Obsidian
Se instala con doble clic desde **[obsidian.md/download](https://obsidian.md/download)**.

<div data-os="mac">

Bajá la versión para macOS, abrí el `.dmg` y arrastrá **Obsidian** a **Aplicaciones**. Si pregunta si abrir una app de internet, tocá **Abrir**.

</div>
<div data-os="win">

Bajá el instalador `.exe` y abrilo. Después abrí **Obsidian** desde el menú Inicio.

</div>

**Tenés que ver:** la bienvenida de Obsidian.

## Paso 2 · Abrí tu cerebro como bóveda
1. Tocá **Abrir carpeta como bóveda** (**Open folder as vault**).
2. Elegí la carpeta de tu cerebro (la misma que abrís en la pestaña Code). Si pregunta si confiás en el autor, **Confiar**.

> **Ojo:** no crees una bóveda nueva vacía: abrí **la carpeta que ya existe**.

**Tenés que ver:** a la izquierda, tus carpetas (`negocio/`, `marca/`, `ventas/`…) y tu `CLAUDE.md`.

## Paso 3 · Pedile a Claude que enlace las notas
En la pestaña **Code**, con la carpeta del cerebro elegida:

```prompt
Creá la carpeta inbox/ si no existe. Agregá al CLAUDE.md esta regla: "Cuando escribas o actualices una nota, enlazá las notas relacionadas con [[nombre-de-la-nota]] y dejá lo nuevo sin clasificar en inbox/". Agregá también .obsidian/workspace.json al .gitignore. No borres nada.
```

**Tenés que ver:** en Obsidian aparece `inbox/` sin que hagas nada.

## Cómo sé que funcionó
1. En Obsidian, nota nueva en `inbox/` con una idea (por ejemplo: "Probar promo 2x1 los martes").
2. En la pestaña Code:

```prompt
Leé lo que hay en inbox/, archivalo en la carpeta correcta y enlazalo con las notas relacionadas usando [[...]]. Mostrame qué cambiaste.
```

**Tenés que ver:** la nota movida y con links, en Obsidian. Con **Cmd/Ctrl + G** la ves conectada en el grafo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Obsidian no muestra lo que creó Claude | Abriste otra carpeta. Cerrá la bóveda y abrí la del cerebro. |
| Aparecen archivos duplicados o "conflicted" | La carpeta está en iCloud/OneDrive/Drive **y** en GitHub. Dejá solo GitHub. |
| Un link `[[...]]` no abre nada | La nota no existe con ese nombre. Hacé clic y Obsidian la crea. |

## Para seguir solo
- Atajos y grafo con colores: [Usá Obsidian como un pro](#s11b-obsidian-atajos).
- Rutina semanal: pedile a Claude "Ordená inbox/, enlazá notas y avisame si ves datos personales de clientes". Podés programarla ([Tareas programadas](#t4-tareas-programadas)).
- No edites el mismo archivo en Obsidian mientras Claude lo está escribiendo.

## Fuentes
Consultadas el 18/11/2026.
- Obsidian, descarga y precios: https://obsidian.md/download · https://obsidian.md/pricing
