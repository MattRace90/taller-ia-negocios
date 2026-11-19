---
titulo: Herramientas base
bloque: Setup
tiempo: 15 min solo Git · 45 min todo (ffmpeg tarda; mientras se instala, seguí leyendo)
para: Todos
necesitas: s2-claude-code
resultado: Git instalado y verificado por Claude (y, si tu desafío lo pide, Node, Python, ffmpeg y Obsidian).
---

Son los programas que Claude usa por detrás para armar tu web, editar tus videos y correr tus bots. Los instalás una vez y Claude hace el resto.
Ejemplo: cuando Manuel Martínez le pida a Claude "cortá los silencios de este video", Claude va a usar ffmpeg. Si no está instalado, no puede.

> **Ojo:** lo **obligatorio para todos es Git** (Paso 1). **Node** lo necesitás para D2, D3 y D4; **Python y ffmpeg**, para D4 (video). Si no elegiste esos desafíos, instalá solo Git y seguí.

| Programa | Para qué |
|---|---|
| **Git** | Guardar el historial de tu cerebro y subirlo a GitHub. **Obligatorio.** |
| **Node.js** | Correr la web, el editor de video y los bots. |
| **Python** | Scripts chicos: datos, planillas, audio. |
| **ffmpeg** | Cortar, convertir y unir video y audio. |
| **Obsidian** | Leer y editar tu cerebro como un cuaderno. |

## Antes de empezar
- [ ] La pestaña **Code** abierta en **Local** con tu carpeta `prueba-claude` ([Claude Code](#s2-claude-code)).
- [ ] La contraseña de tu compu a mano (los instaladores la piden).

> **Tip:** cuando instalás algo con un instalador, Claude a veces no lo "ve" enseguida. Si te dice que no está, cerrá la app de Claude, volvé a abrirla y abrí una sesión nueva en Code.

## Paso 1 · Instalá Git (obligatorio)

<div data-os="mac">

Pedíselo a Claude:

```prompt
Fijate si tengo Git instalado. Si no está, corré xcode-select --install para instalar las herramientas de desarrollo de Apple y avisame cuando aparezca el cartel.
```

Si aparece un cartel de macOS, tocá **Instalar** y aceptá la licencia. Tarda de 5 a 15 minutos. Si Claude dice que ya está, mejor: seguí.

</div>
<div data-os="win">

1. Entrá a **[git-scm.com/install/windows](https://git-scm.com/install/windows)** y bajá el instalador de 64 bits.
2. Abrilo con doble clic. Son muchas pantallas: dejá todo como viene y tocá **Next** hasta **Install**, y al final **Finish**.
3. Cerrá la app de Claude y volvé a abrirla.

</div>

**Tenés que ver:** pedile "decime qué versión de Git tengo" y Claude responde algo como `git version 2.x.x`.

## Paso 2 · Instalá Node.js (D2, D3, D4)
1. Entrá a **[nodejs.org/en/download](https://nodejs.org/en/download)** y bajá el instalador de la versión **LTS** (la estable): `.pkg` en Mac, `.msi` en Windows.
2. Abrilo con doble clic y seguí los pasos dejando todo por defecto. Te pide la contraseña de la compu.

> **Ojo:** instalá Node de **una sola forma**. Si ya lo tenías (nvm, Homebrew), no lo instales de nuevo.

**Tenés que ver:** pedile "decime qué versión de node y npm tengo" y Claude responde dos números (por ejemplo `v26.x`).

## Paso 3 · Instalá Python (D4)

<div data-os="mac">

Entrá a **[python.org/downloads](https://python.org/downloads)**, bajá el instalador de macOS, abrí el `.pkg` y seguí los pasos.

</div>
<div data-os="win">

Pedíselo a Claude:

```prompt
Instalá Python en mi compu con el instalador oficial nuevo para Windows (Python install manager) y después instalá la última versión estable. Verificá que funcione y decime qué versión quedó.
```

Si no le sale, buscá **Python install manager** en la **Microsoft Store**, instalalo y repetí el pedido.

</div>

**Tenés que ver:** Claude te dice la versión, por ejemplo `Python 3.15.x`.

## Paso 4 · Instalá ffmpeg (D4)

<div data-os="mac">

En Mac, ffmpeg se instala con **Homebrew** (un instalador de programas). Homebrew pide la contraseña de la Mac, así que **este paso es en la terminal, una sola vez**.

> **Ojo:** Homebrew pide macOS 15 (Sequoia) o superior. Si tu Mac es más vieja o es Intel, avisá en la mesa de ayuda antes de empezar.


1. Apretá **Cmd+Espacio**, escribí **Terminal** y apretá **Enter**.
2. Pegá esto y apretá **Enter**:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

3. Escribí la contraseña de la Mac (no se ve mientras la escribís: es normal) y apretá **Enter**. Cuando te lo pida, otra vez **Enter**. Tarda unos minutos.
4. Cerrá la Terminal. El resto lo hace Claude. Volvé a la pestaña Code y pegá:

```prompt
Terminé de instalar Homebrew. Hacé los "Next steps" que pide Homebrew para que el comando brew funcione, verificá brew --version y después instalá ffmpeg con brew. Avisame cuando termine.
```

</div>
<div data-os="win">

Pedíselo a Claude:

```prompt
Instalá ffmpeg con winget usando el paquete oficial Gyan.FFmpeg, aceptando los acuerdos. Después verificá que funciona y decime qué versión quedó.
```

> **Ojo:** en compus de empresa, `winget` a veces está bloqueado. Si da error, no bajes ffmpeg de cualquier página: pedí ayuda a la mesa.

</div>

**Tenés que ver:** Claude te confirma una línea que empieza con `ffmpeg version`.

## Paso 5 · Instalá Obsidian
1. Entrá a **[obsidian.md/download](https://obsidian.md/download)** y bajá el instalador.
2. Abrilo con doble clic (en Mac, arrastrá **Obsidian** a **Aplicaciones**).
3. Abrilo. Todavía no crees nada: tu cerebro lo abrís en [Tu cerebro](#p1-cerebro).

> **Costo:** Obsidian es gratis, también para uso comercial. **Sync** es pago y hoy no lo necesitás.

**Tenés que ver:** la pantalla de bienvenida de Obsidian.

## Cómo sé que funcionó
En la pestaña Code, pegá:

```prompt
Revisá qué herramientas tengo instaladas: git, node, npm, python, ffmpeg y, si es Mac, brew. Armame una tabla con herramienta, ¿está instalada? y versión. Si falta algo, decime cómo instalarlo, pero no instales nada sin preguntarme.
```

**Tenés que ver:** una tabla con Git en "sí" (y lo demás según tu desafío).

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude dice que no encuentra algo que acabás de instalar | Cerrá la app de Claude, abrila de nuevo y abrí una sesión nueva en Code. En Windows, si sigue, reiniciá la compu. |
| Mac: Claude dice `brew: command not found` | Pedile: "Hacé los Next steps de Homebrew para que brew funcione". |
| Mac: Homebrew dice que tu macOS no tiene soporte | Avisá en la mesa de ayuda: hay otras formas de conseguir ffmpeg. |
| Windows: `npm` da "running scripts is disabled" | Decile a Claude: "usá npm.cmd y npx.cmd". Si sigue, mesa de ayuda. |
| Un instalador pide una clave de administrador que no tenés | Es una compu de la empresa: pedí ayuda a la mesa. |

## Para seguir solo
- Una vez por mes, pedile a Claude: "Actualizá los programas que instalé con Homebrew (o winget)".
- Si Claude te dice "no tengo X", pedile: "Decime cómo instalar X en mi sistema y verificá que quedó andando".
- Abrí tu cerebro en Obsidian y probá la **vista de grafo**.

## Fuentes
Consultadas el 18/11/2026.
- Git: https://git-scm.com/install/mac · https://git-scm.com/install/windows
- Node.js: https://nodejs.org/en/download
- Python: https://www.python.org/downloads/ · https://docs.python.org/3/using/windows.html
- Homebrew: https://brew.sh/
- ffmpeg: https://ffmpeg.org/download.html · https://www.gyan.dev/ffmpeg/builds/
- Obsidian: https://obsidian.md/download · https://obsidian.md/pricing
