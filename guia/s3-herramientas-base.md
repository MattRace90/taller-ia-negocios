---
titulo: Herramientas base
bloque: Setup
tiempo: 45 min (Homebrew y ffmpeg tardan; mientras se instalan, seguí leyendo)
para: Todos
necesitas: s2-claude-code
resultado: Node, Git, Python, ffmpeg y Obsidian instalados y respondiendo en la terminal.
---

> **Ojo:** de esta página, lo **obligatorio para todos es Git** (lo necesitás para guardar tu cerebro en GitHub). **Node** lo necesitás para D2, D3 y D4; **Python y ffmpeg**, para D4 (video). Si no elegiste esos desafíos, instalá solo Git y seguí: el resto queda acá para después.

Son los programas que Claude Code usa por detrás para armar tu web, editar tus videos y correr tus bots. No los vas a usar a mano: los instalás una vez y Claude hace el resto.
Ejemplo: cuando Manuel Martínez le pida a Claude "cortá los silencios de este video", Claude va a usar ffmpeg. Si no está instalado, no puede.

| Programa | Para qué lo vamos a usar hoy |
|---|---|
| **Node.js** | Correr la web, el editor de video (Remotion) y los bots. Claude Code ya **no** lo necesita para instalarse, pero lo demás sí. |
| **Git** | Guardar el historial de cambios de tu cerebro y subirlo a GitHub. |
| **Python** | Scripts chicos: procesar datos, planillas o audio. |
| **ffmpeg** | Cortar, convertir y unir video y audio. |
| **Obsidian** | Leer y editar tu cerebro como si fuera un cuaderno. |
| **Homebrew** (solo Mac) | Un instalador de programas por terminal. Lo usamos para ffmpeg. |

## Antes de empezar
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] La contraseña de tu compu a mano (algunos instaladores la piden).
- [ ] Mac: fijate tu versión en **menú Apple › Acerca de esta Mac**. Homebrew pide **macOS Sequoia 15 o superior** (y en Mac con procesador Intel no garantiza que ande). Si tenés una versión anterior o una Mac Intel, avisá en la mesa de ayuda antes del Paso 4.
- [ ] Windows: Git for Windows ya instalado (lo hiciste en [Instalá Claude Code](#s2-claude-code), Paso 1). Mejor si tenés permisos de administrador.

> **Tip:** cada vez que instalás algo, **cerrá la terminal y abrí una nueva** antes de verificar. Si no, la terminal vieja no "ve" el programa nuevo.

Todos los comandos de esta página se pegan en la terminal: **Terminal** en Mac, **PowerShell** en Windows (cómo abrirla: [Instalá Claude Code](#s2-claude-code), Paso 1). Copiá, pegá y apretá **Enter**.

## Paso 1 · Instalá Node.js

1. Entrá a **[nodejs.org/en/download](https://nodejs.org/en/download)** y bajá el instalador de la versión **LTS** (la estable; al 18/11/2026 es la **v26.13.1**). Si la página te muestra comandos, buscá más abajo el botón del instalador (`.pkg` en Mac, `.msi` en Windows).

<div data-os="mac">

2. Abrí el archivo `.pkg` y seguí los pasos (**Continuar**, **Instalar**). Te pide la contraseña de la Mac.

</div>
<div data-os="win">

2. Bajá el **Windows Installer (.msi)**, abrilo y dejá todas las opciones por defecto (**Next** hasta **Install**).

</div>

3. En una terminal nueva:

```bash
node -v
npm -v
```

<div data-os="win">

> **Ojo:** si `npm -v` sale en rojo con "running scripts is disabled on this system", no está roto: es una traba de seguridad de PowerShell. Escribí `npm.cmd -v` (y en el resto del taller, `npm.cmd` y `npx.cmd` en vez de `npm` y `npx`). Si no te sale, pedí ayuda a la mesa.

</div>

**Tenés que ver:** dos números de versión, por ejemplo `v26.13.1` y otro para npm.

> **Ojo:** instalá Node de **una sola forma**. Si ya lo tenías por otro lado (nvm, Homebrew), no lo instales de nuevo: quedan dos y se pisan.

## Paso 2 · Instalá Git

<div data-os="mac">

En la Mac, Git viene con las herramientas de desarrollo de Apple. Pegá esto en la Terminal:

```bash
xcode-select --install
```

Se abre un cartel: tocá **Instalar**, aceptá la licencia y esperá. Pesa varios cientos de MB, así que puede tardar 5 a 15 minutos. Si dice que ya están instaladas, mejor: seguí.

</div>
<div data-os="win">

Ya lo instalaste en [Instalá Claude Code](#s2-claude-code). Si no lo hiciste, bajá **Git for Windows** desde **[git-scm.com/install/windows](https://git-scm.com/install/windows)**, abrilo y aceptá todas las opciones por defecto.

</div>

Verificá en una terminal nueva:

```bash
git --version
```

**Tenés que ver:** algo como `git version 2.x.x`.

## Paso 3 · Instalá Python

<div data-os="mac">

1. Entrá a **[python.org/downloads](https://python.org/downloads)** y bajá el instalador de macOS (al 18/11/2026, **Python 3.15.2**).
2. Abrí el `.pkg` y seguí los pasos.
3. Verificá en una terminal nueva:

```bash
python3 --version
```

En Mac se escribe `python3` (con el 3), no `python`.

</div>
<div data-os="win">

Python cambió su instalador para Windows: el clásico (el del casillero "Add python.exe to PATH") está **deprecado desde la versión 3.14**. Usá el nuevo **Python install manager**.

1. En PowerShell:

```powershell
winget install 9NQ7512CXL7T -e --accept-package-agreements --disable-interactivity
```

`winget` es el instalador de programas que trae Windows. Si `winget` no anda, buscá **Python install manager** en la **Microsoft Store** e instalalo desde ahí. Es el mismo programa.

**Tenés que ver:** un mensaje que termina en `Successfully installed` (o "Instalado correctamente").

2. Cerrá PowerShell, abrí uno nuevo e instalá Python:

```powershell
py install 3.15
```

Si te pregunta si querés agregar una carpeta al PATH, respondé que sí.

3. Verificá:

```powershell
py list
python --version
```

</div>

**Tenés que ver:** `Python 3.15.x` (o la versión que hayas instalado).

## Paso 4 · Instalá ffmpeg

<div data-os="mac">

En Mac lo instalamos con **Homebrew**. Primero Homebrew, después ffmpeg.

1. Pegá el instalador oficial de Homebrew (lo sacamos de **brew.sh**):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Te pide la contraseña de la Mac (no se ve mientras la escribís, ni siquiera con asteriscos: es normal; escribila y apretá **Enter**). Después te pide que apretes **Enter** para seguir. Tarda unos minutos.

2. **Importante:** al terminar, el instalador muestra un bloque **Next steps** con dos o tres comandos. Copialos y pegalos tal cual. Si no lo hacés, `brew` no funciona. En las Mac con chip Apple (M1 o posterior) suelen ser estos:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

3. Verificá Homebrew:

```bash
brew --version
```

4. Instalá ffmpeg (tarda varios minutos, baja muchas piezas):

```bash
brew install ffmpeg
```

</div>
<div data-os="win">

> **Ojo:** en compus de empresa, `winget` a veces está bloqueado o el antivirus frena la descarga. Si da error, no bajes ffmpeg de cualquier página: pedí ayuda a la mesa. Solo lo necesitás para el desafío de video (D4).

En PowerShell:

```powershell
winget install --id Gyan.FFmpeg -e
```

Si te pregunta si aceptás los términos, escribí `Y` y apretá **Enter**.

Es la versión que publica **[gyan.dev](https://gyan.dev)**, el sitio que recomienda **[ffmpeg.org](https://ffmpeg.org)** para Windows. No bajes ffmpeg de otras páginas.

</div>

Cerrá la terminal, abrí una nueva y verificá:

```bash
ffmpeg -version
```

**Tenés que ver:** un texto largo que empieza con `ffmpeg version`.

## Paso 5 · Instalá Obsidian
1. Entrá a **[obsidian.md/download](https://obsidian.md/download)** y bajá el instalador.

<div data-os="mac">

2. Abrí el `.dmg` y arrastrá **Obsidian** a **Aplicaciones**.

</div>
<div data-os="win">

2. Abrí el `.exe` y seguí los pasos.

</div>

3. Abrí Obsidian. Todavía no crees nada: en [Tu cerebro](#p1-cerebro) vas a abrir tu carpeta del cerebro con **Open folder as vault** (en español, **Abrir carpeta como bóveda**).

> **Costo:** Obsidian es gratis, también para uso comercial. **Sync** (sincronizar entre dispositivos) es opcional y pago. Hoy no lo necesitás: tu cerebro se guarda en GitHub.

**Tenés que ver:** la pantalla de bienvenida de Obsidian.

## Cómo sé que funcionó
Abrí Claude Code en tu carpeta de prueba (`claude`) y pegá:

```prompt
Revisá qué herramientas tengo instaladas en esta compu. Corré los comandos de versión de: node, npm, git, python (python3 en Mac, py y python en Windows), ffmpeg y, solo si es Mac, brew. Armame una tabla con: herramienta, ¿está instalada?, versión. Si falta algo, decime cómo instalarlo en mi sistema operativo, pero no instales nada sin preguntarme.
```

**Tenés que ver:** una tabla con todo en "sí". Si algo falta, Claude te dice cómo resolverlo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `command not found` o "no se reconoce" justo después de instalar | Cerrá la terminal y abrí una nueva. En Windows, si sigue, reiniciá la compu. |
| Mac: `brew: command not found` después de instalar Homebrew | Te faltaron los comandos de **Next steps** (Paso 4.2). Pegalos y abrí una terminal nueva. |
| Mac: Homebrew dice que tu macOS no tiene soporte | Homebrew pide macOS 15 o superior. En 11 a 14 a veces anda, pero sin garantía. Avisá en la mesa de ayuda: hay otras formas de conseguir ffmpeg para Mac (los enlaces están en **[ffmpeg.org/download.html](https://ffmpeg.org/download.html)**). |
| Windows: escribís `python` y se abre la Microsoft Store | No tenés Python instalado todavía. Hacé el Paso 3 completo y usá `py`. |
| Windows: `npm` o `npx` dan un error de "running scripts is disabled" | Probá con `npm.cmd -v`. Si sigue, pedí ayuda en la mesa: es una configuración de seguridad de PowerShell. Si estás solo, el arreglo que documenta Microsoft para tu usuario es `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` (respondé `S` o `Y`). |
| Mac: `xcode-select` dice "command line tools are already installed" | Está todo bien: seguí con el paso siguiente. |

## Para seguir solo
- Una vez por mes: en Mac, `brew upgrade` actualiza todo lo instalado con Homebrew. En Windows, `winget upgrade --all`.
- Si Claude te dice "no tengo X instalado", pedile: "Decime cómo instalar X en mi sistema y verificá que quedó andando".
- Abrí tu cerebro en Obsidian y probá la **vista de grafo**: muestra cómo se conectan tus archivos.

## Fuentes
Consultadas el 18/11/2026.
- Node.js: https://nodejs.org/en/download
- Git: https://git-scm.com/install/mac · https://git-scm.com/install/windows
- Python: https://www.python.org/downloads/ · https://docs.python.org/3/using/windows.html
- Homebrew: https://brew.sh/ · https://docs.brew.sh/Installation
- ffmpeg: https://ffmpeg.org/download.html · https://www.gyan.dev/ffmpeg/builds/
- Obsidian: https://obsidian.md/download · https://obsidian.md/pricing
- Claude Code (no requiere Node): https://code.claude.com/docs/en/setup
