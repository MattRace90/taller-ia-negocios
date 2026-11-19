---
titulo: GitHub y GitHub Desktop
bloque: Setup
tiempo: 20 min
para: Todos
necesitas: s3-herramientas-base
resultado: Cuenta de GitHub (gratis), GitHub Desktop con tu sesión iniciada y tu nombre configurado, y un repositorio privado de prueba publicado.
---

GitHub es donde guardás tu cerebro en la nube, con el historial de cada cambio: un Google Drive con memoria. Todo se hace con botones, desde **GitHub Desktop** (la app oficial), sin terminal.
Ejemplo: si en Viajes TDH alguien cambia la respuesta a "¿es seguro pagar por transferencia?", queda registrado quién la cambió y podés volver a la versión anterior.

Tres palabras: un **repositorio** (o **repo**) es una carpeta que Git vigila y que tiene su copia en GitHub. Un **commit** es una "foto" de tus archivos con una frase que dice qué cambiaste. **Push** es subir esas fotos a GitHub. Más en el [glosario](#t2-piezas).

## Antes de empezar
- [ ] Git instalado ([Herramientas base](#s3-herramientas-base), Paso 1).
- [ ] Un mail al que tengas acceso (GitHub te manda un código).

## Privado o público
| | Privado | Público |
|---|---|---|
| Quién lo ve | Solo vos y quienes invites | Cualquiera en internet |
| Hoy | **Siempre este** | Nunca para el cerebro |

> **Datos:** aunque sea privado, en GitHub **nunca** van contraseñas, claves, tokens ni datos personales de tus clientes.

## Paso 1 · Creá tu cuenta de GitHub
1. Entrá a **[github.com/signup](https://github.com/signup)**.
2. Poné tu mail, una contraseña y un nombre de usuario profesional (aparece en tus links: `github.com/[TU-USUARIO]`).
3. Si aparece un rompecabezas para comprobar que sos una persona, resolvelo vos. Confirmá el código del mail.
4. Quedate con el plan **Free** (podés saltear las preguntas con **Skip**).

> **Costo:** **Free** incluye repositorios **privados ilimitados** y no pide tarjeta.

**Tenés que ver:** tu panel de GitHub con tu foto o inicial arriba a la derecha.

## Paso 2 · Instalá GitHub Desktop
1. Entrá a **[desktop.github.com](https://desktop.github.com)** y bajá la app.

<div data-os="mac">

2. Abrí el archivo descargado y arrastrá **GitHub Desktop** a **Aplicaciones**. Pide macOS 12 o superior.

</div>
<div data-os="win">

2. Abrí el instalador `.exe` con doble clic: se instala solo. Pide Windows 10 de 64 bits o superior.

</div>

**Tenés que ver:** la app abierta con la pantalla de bienvenida.

## Paso 3 · Iniciá sesión y poné tu nombre

<div data-os="mac">

1. **GitHub Desktop › Settings** › pestaña **Accounts** › **Sign Into GitHub.com** › **Continue With Browser**. Iniciá sesión en el navegador y aceptá volver a la app.
2. En la misma ventana, pestaña **Git**: completá **Name** y elegí tu mail de GitHub en **Email**. Tocá **Save**.

</div>
<div data-os="win">

1. **File › Options** › pestaña **Accounts** › **Sign Into GitHub.com** › **Continue With Browser**. Iniciá sesión en el navegador y aceptá volver a la app.
2. En la misma ventana, pestaña **Git**: completá **Name** y elegí tu mail de GitHub en **Email**. Tocá **Save**.

</div>

> **Ojo:** la contraseña de GitHub la escribís **solo en github.com**, en tu navegador. Nunca en un chat con Claude.

**Tenés que ver:** en **Accounts**, tu usuario; en **Git**, tu nombre y tu mail.

## Paso 4 · Publicá un repositorio privado de prueba
1. **File › New repository**.
2. **Name:** `prueba-github` · **Local path:** **Choose…** › **Documentos** · tildá **Initialize this repository with a README**.
3. **Create repository** › arriba, **Publish repository**.
4. Dejá tildado **Keep this code private** y tocá **Publish Repository**.

**Tenés que ver:** en **github.com/[TU-USUARIO]**, el repo `prueba-github` con la etiqueta **Private**.

## Cómo sé que funcionó
En la app de Claude, abrí **Code** › **Local** › elegí la carpeta `Documentos/prueba-github` ([cómo](#s2-claude-code)) y pegá:

```prompt
Fijate si esta carpeta es un repositorio de Git, a qué repositorio de GitHub está conectada, si es privado y con qué nombre y mail está configurado Git. Después agregá una línea al README con la fecha de hoy y decime qué tengo que tocar en GitHub Desktop para subir ese cambio.
```

Después, en GitHub Desktop: abajo a la izquierda escribí un resumen (por ejemplo "Prueba"), tocá **Commit to main** y arriba **Push origin**.

**Tenés que ver:** en [github.com](https://github.com), la línea nueva en el README.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No aparece **Keep this code private** | Publicalo y cambialo en github.com › tu repo › **Settings › General › Danger Zone › Change visibility** › **Private**. |
| El navegador no vuelve a GitHub Desktop | Cerrá la pestaña y repetí **Sign Into GitHub.com**. |
| Publicaste algo **público** por error | Pasalo a privado ya. Si subiste una clave, borrala en su servicio y creá una nueva. |
| GitHub Desktop no ve una carpeta como repositorio | **File › Add local repository**; si ofrece crearlo, aceptá. |
| Claude dice que Git no está instalado | Volvé a [Herramientas base](#s3-herramientas-base), Paso 1. |

## Para seguir solo
- Invitá a tu equipo: github.com › tu repo › **Settings › Collaborators**.
- Antes de subir, pedile a Claude: "Revisá que no haya claves, contraseñas ni datos de clientes en lo que voy a subir".
- Pedile a Claude que arme un `.gitignore` con `.env` y las carpetas sensibles: lo que esté ahí nunca se sube.

## Fuentes
Consultadas el 18/11/2026.
- Planes de GitHub: https://github.com/pricing
- GitHub Desktop (instalar, iniciar sesión, configurar Git, primer repo): https://docs.github.com/en/desktop
