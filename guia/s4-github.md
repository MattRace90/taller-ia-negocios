---
titulo: GitHub y GitHub Desktop
bloque: Setup
tiempo: 20 min
para: Todos
necesitas: s3-herramientas-base
resultado: Cuenta de GitHub (gratis), GitHub Desktop con tu sesión iniciada, Git configurado con tu nombre y un repositorio privado de prueba publicado.
---

GitHub es el lugar donde vas a guardar tu cerebro en la nube, con el historial de cada cambio. Es como un Google Drive con memoria: podés ver qué cambió, cuándo y volver atrás.
Ejemplo: si en Viajes TDH alguien cambia la respuesta a "¿es seguro pagar por transferencia?", queda registrado quién la cambió y podés recuperar la versión anterior.
Para no usar la terminal, vamos con **GitHub Desktop**, la app oficial de GitHub con botones.

Tres palabras que vas a ver: un **repositorio** (o **repo**) es una carpeta que Git vigila y que tiene su copia en GitHub. Un **commit** es una "foto" guardada de tus archivos con una frase que dice qué cambiaste. **Push** es subir esas fotos a GitHub. Más en el [glosario](#t2-piezas).

## Antes de empezar
- [ ] Git instalado ([Herramientas base](#s3-herramientas-base), Paso 2).
- [ ] Un mail al que tengas acceso (GitHub te manda un código).

## Privado o público: la única decisión importante
| | Privado | Público |
|---|---|---|
| Quién lo ve | Solo vos y quienes invites | Cualquier persona en internet |
| Para qué sirve | Tu cerebro, tus procesos, tu código | Proyectos abiertos, plantillas para compartir |
| Hoy | **Siempre este** | Nunca para el cerebro |

> **Datos:** aunque sea privado, en GitHub **nunca** van contraseñas, claves de API, tokens ni datos personales de tus clientes. Las claves van en el lugar que corresponde (lo vemos en [Cuentas en la nube](#s5-cuentas-nube)).

## Paso 1 · Creá tu cuenta de GitHub
1. Entrá a **[github.com/signup](https://github.com/signup)**.
2. Poné tu mail, una contraseña y un nombre de usuario. El usuario aparece en tus links (`github.com/[TU-USUARIO]`): usá algo profesional, por ejemplo el nombre de tu empresa.
3. Si GitHub te muestra un rompecabezas para comprobar que sos una persona, resolvelo.
4. Confirmá el código que te llega por mail.
5. Si te ofrece planes, quedate con **Free**. Si te hace preguntas sobre cómo vas a usar GitHub, podés saltearlas (**Skip**).

> **Costo:** el plan **Free** incluye repositorios **privados ilimitados**. No hace falta tarjeta. El plan Team (USD 4 por usuario por mes) no lo necesitás para arrancar.

**Tenés que ver:** tu panel de GitHub con tu foto o inicial arriba a la derecha.

## Paso 2 · Instalá GitHub Desktop
1. Entrá a **[desktop.github.com](https://desktop.github.com)** y bajá la app.

<div data-os="mac">

2. Abrí el `.zip` (o `.dmg`) y arrastrá **GitHub Desktop** a **Aplicaciones**. Pide macOS 12 o superior.

</div>
<div data-os="win">

2. Abrí el instalador `.exe`. Se instala solo. Pide Windows 10 de 64 bits o superior.

</div>

**Tenés que ver:** la app abierta con la pantalla de bienvenida.

## Paso 3 · Iniciá sesión en GitHub Desktop

<div data-os="mac">

1. En la barra de menú: **GitHub Desktop › Settings**.
2. Pestaña **Accounts** › **Sign Into [GitHub.com](https://GitHub.com)**.
3. Tocá **Continue With Browser**. Se abre el navegador: iniciá sesión y aceptá volver a la app.

</div>
<div data-os="win">

1. Menú **File › Options**.
2. Pestaña **Accounts** › **Sign Into [GitHub.com](https://GitHub.com)**.
3. Tocá **Continue With Browser**. Se abre el navegador: iniciá sesión y aceptá volver a la app.

</div>

> **Ojo:** la contraseña de GitHub la escribís **solo en [github.com](https://github.com)**, en tu navegador. Nunca en un chat con Claude ni en un archivo.

**Tenés que ver:** en **Accounts**, tu usuario de GitHub con tu foto o inicial.

## Paso 4 · Poné tu nombre y tu mail en Git
Git firma cada cambio con un nombre y un mail. Lo configurás una sola vez, con la app o con la terminal (elegí una).

**Con GitHub Desktop (recomendado):**

<div data-os="mac">

1. **GitHub Desktop › Settings** › pestaña **Git**.

</div>
<div data-os="win">

1. **File › Options** › pestaña **Git**.

</div>

2. Completá **Name** con tu nombre y elegí tu mail de GitHub en **Email**.
3. Tocá **Save**.

**Con la terminal (alternativa):**

```bash
git config --global user.name "[TU NOMBRE Y APELLIDO]"
git config --global user.email "[EL MAIL DE TU CUENTA DE GITHUB]"
```

Verificá:

```bash
git config --global --list
```

**Tenés que ver:** tu nombre y tu mail (en la app, guardados en **Git**; en la terminal, en las líneas `user.name` y `user.email`).

## Paso 5 · Publicá un repositorio privado de prueba
Practicamos con uno vacío. Tu cerebro lo publicás en [Tu cerebro](#p1-cerebro), con los mismos botones.

1. En GitHub Desktop: **File › New repository** (si es la primera vez, también aparece el botón **Create a New Repository on your Hard Drive…**).
2. Completá:
   - **Name:** `prueba-github`
   - **Local path:** tocá **Choose…** y elegí tu carpeta **Documentos**
   - Tildá **Initialize this repository with a README**.
3. Tocá **Create repository**.
4. Arriba, tocá **Publish repository**.
5. Dejá tildado **Keep this code private** y tocá **Publish Repository**.

**Tenés que ver:** en **github.com/[TU-USUARIO]**, el repositorio `prueba-github` con la etiqueta **Private**.

## Cómo sé que funcionó
- GitHub Desktop muestra tu cuenta en **Accounts**.
- `git config --global --list` muestra tu nombre y tu mail.
- En [github.com](https://github.com) ves `prueba-github` marcado como **Private**.

Y en Claude Code, dentro de `Documentos/prueba-github`. Abrí la terminal y entrá a la carpeta:

<div data-os="mac">

```bash
cd ~/Documents/prueba-github && claude
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\prueba-github; claude
```

</div>

Después pegá:

```prompt
Fijate si esta carpeta es un repositorio de Git, a qué repositorio de GitHub está conectada y si es privado o público. Después agregá una línea al README con la fecha de hoy y decime qué tengo que tocar en GitHub Desktop para subir ese cambio.
```

**Tenés que ver:** Claude confirma el repo, hace el cambio y te indica **Commit to main** y después **Push origin**. Hacelo en GitHub Desktop: abajo a la izquierda escribí un resumen (por ejemplo "Prueba"), tocá **Commit to main** y arriba **Push origin**. En [github.com](https://github.com) vas a ver la línea nueva en el README.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No aparece **Keep this code private** | Publicalo igual y cambialo en [github.com](https://github.com) › tu repo › **Settings › General › Danger Zone › Change visibility** › **Private**. |
| El navegador no vuelve a GitHub Desktop después de iniciar sesión | Cerrá la pestaña, volvé a la app y repetí **Sign Into [GitHub.com](https://GitHub.com)**. |
| Publicaste algo como **público** por error | Cambialo a privado ya (fila de arriba). Si subiste una clave, borrala de su servicio y creá una nueva: aunque lo pongas privado, pudo haberse copiado. |
| GitHub Desktop no ve una carpeta como repositorio | Usá **File › Add local repository**; si dice que no es un repositorio, ofrece crearlo: aceptá. |
| `git: command not found` | Volvé a [Herramientas base](#s3-herramientas-base), Paso 2. |

## Para seguir solo
- Invitá a tu equipo al repo del cerebro: [github.com](https://github.com) › tu repo › **Settings › Collaborators**.
- Antes de subir cosas, pedile a Claude: "Revisá que no haya claves, contraseñas ni datos de clientes en lo que voy a subir".
- Pedile a Claude que te arme un `.gitignore` con `.env` y carpetas con datos sensibles adentro: lo que esté ahí nunca se sube.

## Fuentes
Consultadas el 18/11/2026.
- Planes de GitHub: https://github.com/pricing
- Instalar GitHub Desktop: https://docs.github.com/en/desktop/installing-and-authenticating-to-github-desktop/installing-github-desktop
- Iniciar sesión en GitHub Desktop: https://docs.github.com/en/desktop/installing-and-authenticating-to-github-desktop/authenticating-to-github-in-github-desktop
- Configurar Git en GitHub Desktop: https://docs.github.com/en/desktop/configuring-and-customizing-github-desktop/configuring-git-for-github-desktop
- Crear y publicar un repositorio: https://docs.github.com/en/desktop/overview/creating-your-first-repository-using-github-desktop
- Agregar un repositorio local: https://docs.github.com/en/desktop/adding-and-cloning-repositories/adding-a-repository-from-your-local-computer-to-github-desktop
