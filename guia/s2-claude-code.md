---
titulo: Instalá Claude Code
bloque: Setup
tiempo: 20 min
para: Todos
necesitas: s1-claude
resultado: Claude Code abierto en una carpeta de tu compu, con tu sesión iniciada y respondiendo.
---

Claude Code es Claude trabajando en tu compu: lee y escribe archivos, instala programas, arma bots y webs. Es la herramienta principal del taller.
Hay dos formas de usarlo: desde la **pestaña Code** de la app (sin terminal, ideal si nunca abriste una) o desde la **terminal**: una ventana donde le das órdenes a la compu escribiendo. La pestaña Code ya viene con la app. Acá instalás la versión de terminal, porque algunas prácticas la usan.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude ([Tu cuenta](#s1-claude)). El plan gratis no incluye Claude Code.
- [ ] La app de escritorio de Claude instalada.
- [ ] Mac con **macOS 13 (Ventura) o superior**, o Windows 10 actualizado o Windows 11. Se fija en **menú Apple › Acerca de esta Mac** o en **Configuración › Sistema › Información**.

> **Ojo:** si tu Mac es más vieja, o la compu es de la empresa y el antivirus bloquea el instalador (o te pide una clave de administrador que no tenés), no pierdas tiempo: avisá en la mesa de ayuda. Mientras tanto podés seguir con el chat y Cowork en la app.

## Paso 1 · Abrí la terminal

<div data-os="mac">

Apretá **Cmd+Espacio** (se abre el buscador Spotlight), escribí **Terminal** y apretá **Enter**.

</div>
<div data-os="win">

1. Antes que nada, instalá **Git for Windows**. Entrá a **[git-scm.com/install/windows](https://git-scm.com/install/windows)** (si no carga, a **[git-scm.com](https://git-scm.com)** › **Download**), bajá el instalador de 64 bits y abrilo. Son muchas pantallas: dejá todo como viene y tocá **Next** hasta **Install**, y al final **Finish**. Claude Code funciona sin Git, pero con Git anda mejor y lo vas a necesitar para GitHub.
2. Apretá la tecla **Windows**, escribí **PowerShell** y abrí **Windows PowerShell**. No hace falta abrirlo como administrador.

</div>

**Tenés que ver:** una ventana con texto y un cursor esperando que escribas.

## Paso 2 · Instalá Claude Code

> **Ojo:** si el wifi está lento, el instalador puede tardar más o cortarse con un error. Esperá un minuto y pegá el mismo comando otra vez: no rompe nada repetirlo.

Copiá el comando con el botón **Copiar**, hacé clic en la terminal, pegalo (**Cmd+V** en Mac; **Ctrl+V** o clic derecho en Windows) y apretá **Enter**. Tarda uno o dos minutos.

<div data-os="mac">

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

</div>
<div data-os="win">

```powershell
irm https://claude.ai/install.ps1 | iex
```

</div>

Cuando termine, **cerrá la terminal y abrí una nueva** (así reconoce el comando nuevo) y verificá:

```bash
claude --version
```

**Tenés que ver:** un número de versión, por ejemplo `2.1.211 (Claude Code)`.

<div data-os="mac">

> **Ojo:** si dice `command not found: claude`, mirá lo último que escribió el instalador: a veces pide agregar una carpeta al PATH (la lista de lugares donde la compu busca programas). Pegá el comando de abajo, cerrá la Terminal, abrí una nueva y repetí `claude --version`.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
```

</div>

## Paso 3 · Iniciá sesión
1. Creá una carpeta de prueba en **Documentos** y entrá a ella con este comando:

<div data-os="mac">

```bash
mkdir -p ~/Documents/prueba-claude && cd ~/Documents/prueba-claude
```

</div>
<div data-os="win">

```powershell
mkdir $HOME\Documents\prueba-claude; cd $HOME\Documents\prueba-claude
```

En el Explorador, la carpeta `Documents` se ve como **Documentos**: es la misma.

> **Ojo:** si tu Windows guarda Documentos en OneDrive, la carpeta queda en `C:\Users\[TU-USUARIO]\Documents`, que no es la que el Explorador muestra como **Documentos**. Para abrir en el Explorador la carpeta donde estás parado, escribí `explorer .` (con el punto) y apretá **Enter**.

</div>

**Tenés que ver:** la línea de la terminal termina en `prueba-claude`.

2. Abrí Claude Code:

```bash
claude
```

3. La primera vez te pregunta el tema de colores: elegí cualquiera con las flechas y apretá **Enter**.
4. Te pregunta cómo iniciar sesión: elegí la cuenta de Claude (**Claude account with subscription**) y apretá **Enter**. Se abre el navegador: tocá el botón para autorizar y volvé a la terminal.
5. Te pregunta si confiás en la carpeta: elegí **Yes** y **Enter**.

**Tenés que ver:** un cuadro para escribir con el cursor titilando.

## Paso 4 · Tu primer pedido

```prompt
Creá un archivo hola.md con 3 ideas para usar IA en un negocio como el mío: [DESCRIBÍ TU NEGOCIO EN UNA LÍNEA]. Después mostrame qué archivos hay en esta carpeta.
```

Claude te va a pedir permiso para crear el archivo. Leé qué va a hacer y aceptá.

**Tenés que ver:** Claude te lista los archivos y aparece `hola.md`. Para verlo vos: abrí **Finder** (Mac) o el **Explorador de archivos** (Windows) › **Documentos** › **prueba-claude**.

## Paso 5 · La pestaña Code de la app (sin terminal)
1. En la app de Claude, tocá **Code** arriba de la barra lateral.
2. En el selector de entorno elegí **Local › Open folder…** y abrí `Documentos/prueba-claude`.
3. Pedí lo mismo que en la terminal: es el mismo Claude Code, con botones.

**Tenés que ver:** el cuadro de mensaje de Code con el nombre de la carpeta `prueba-claude` arriba o al costado.

> **Tip:** los comandos de la [machete de atajos](#t5-atajos) (`/context`, `/compact`, `/rewind`…) funcionan en los dos lados.

## Cómo sé que funcionó
`claude --version` muestra una versión, `claude` abre la sesión con tu cuenta y creó `hola.md`.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `claude: command not found` o "no se reconoce" | Cerrá la terminal y abrí una nueva. En Mac, si sigue, hacé lo del **Ojo** del Paso 2. Si sigue, corré el instalador otra vez. |
| No sé si estoy en la carpeta correcta | Escribí `pwd` y apretá **Enter**: te muestra dónde estás. Para abrir esa carpeta en la ventana de archivos: `open .` (Mac) o `explorer .` (Windows). |
| En Windows: "The token '&&' is not a valid statement separator" | Estás en PowerShell con un comando de CMD. Usá el comando de PowerShell de arriba. |
| En Windows: "'irm' is not recognized" | Estás en CMD. Abrí **PowerShell** y repetí. |
| Dice que tu plan no incluye Claude Code | Revisá que la cuenta tenga Pro y escribí `/login` para volver a entrar. |
| Algo raro con la instalación | Corré `claude doctor`: revisa todo y te dice qué arreglar. |

## Para seguir solo
- `claude update` actualiza Claude Code (igual se actualiza solo).
- Abrí siempre Claude Code **parado en la carpeta del proyecto**: así lee el `CLAUDE.md` de esa carpeta.
- Mirá la [machete de atajos](#t5-atajos) y probá **Shift+Tab** hasta el modo plan.
