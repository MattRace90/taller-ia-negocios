---
titulo: Armá el cerebro de tu empresa
bloque: Práctica
tiempo: 60 min
para: Todos
necesitas: s1-claude, s2-claude-code, s4-github
resultado: Una carpeta con tu negocio escrito en archivos .md, que Claude lee solo y que queda guardada en GitHub.
---

La IA no conoce tu negocio: trabaja con lo que le das para leer. Hoy vas a dejar escrito, en archivos simples, lo que hoy está en tu cabeza: qué vendés, a quién, cómo respondés a "¿es una estafa?" o "es caro", cómo hablás.
Es el manual del empleado nuevo, pero el empleado es Claude. Todo lo que hagamos después del almuerzo (bots, propuestas, contenido) va a leer de acá.

## Antes de empezar
- [ ] Claude Code instalado y con tu sesión iniciada ([Instalá Claude Code](#s2-claude-code)).
- [ ] Cuenta de GitHub, GitHub Desktop instalado y tu nombre y mail cargados en Git ([GitHub](#s4-github), Pasos 1 a 4).
- [ ] Tu archivo **CONTEXTO-borrador.md**: lo armamos con tu formulario y el material que compartiste. Descargalo de [Usá tu borrador](#c2-tu-borrador) o de la página de tu empresa: va a quedar en tu carpeta **Descargas**. Si no lo tenés, igual podés hacer esta práctica: Claude te entrevista desde cero.


### Traé (o tené a mano en tu compu) · recomendado, no obligatorio
Ya te lo pedimos en el formulario y mucho está en tu borrador. Igual, tenelo a mano: Claude te lo va a pedir para completar el cerebro. Si lo subiste a una carpeta de Drive en el formulario, el link está en la página de tu empresa (sección **Empresas**).
- **Tu marca:** manual de marca si lo tenés, logo, colores, tipografías y 3 piezas que te gusten de las tuyas.
- **Tu competencia:** 3 a 5 competidores con su web e Instagram, y una marca de tu rubro que admires.
- **Lo que vendés:** lista de productos o servicios con precios, promos y condiciones.
- **Cómo hablás:** 2 o 3 mensajes reales (un WhatsApp, un posteo, un audio transcripto).
- **Lo que más te preguntan:** las 10 preguntas frecuentes con su respuesta oficial.
- **Cómo trabajás:** los procesos clave (cómo se vende, cómo se atiende, quién hace qué).
- **A dónde vas:** el objetivo de los próximos 90 días, en un número.

> **Datos:** en el cerebro va cómo funciona tu negocio, no los datos de tus clientes. Nada de nombres, DNI, teléfonos ni deudas de clientes, contraseñas o claves.

## Paso 1 · Creá la carpeta del cerebro y guardá el borrador
Vas a tener una carpeta por empresa, siempre en **Documentos** y siempre con el mismo nombre: `cerebro-[TU-EMPRESA]`, en minúsculas, sin espacios ni tildes. Por ejemplo `cerebro-fondus` o `cerebro-celve`. Adentro va una subcarpeta `fuentes`, donde vive el borrador.

La ruta del borrador queda así:

<div data-os="mac">

```text
~/Documents/cerebro-[TU-EMPRESA]/fuentes/CONTEXTO-borrador.md
```

1. Abrí **Finder** y entrá a **Documentos**.
2. Clic derecho en un lugar vacío › **Nueva carpeta**. Escribí `cerebro-[TU-EMPRESA]` y apretá **Enter**.
3. Entrá a esa carpeta (doble clic) y creá otra carpeta adentro llamada `fuentes`.
4. Abrí **Descargas** en otra ventana y arrastrá `CONTEXTO-borrador.md` adentro de `fuentes`.
5. Abrí la **Terminal** y entrá a la carpeta del cerebro:

```bash
cd ~/Documents/cerebro-[TU-EMPRESA]
```

</div>
<div data-os="win">

```text
C:\Users\[TU-USUARIO]\Documents\cerebro-[TU-EMPRESA]\fuentes\CONTEXTO-borrador.md
```

1. Abrí el **Explorador de archivos** y entrá a **Documentos**.
2. Clic derecho en un lugar vacío › **Nuevo › Carpeta**. Escribí `cerebro-[TU-EMPRESA]` y apretá **Enter**.
3. Entrá a esa carpeta (doble clic) y creá otra carpeta adentro llamada `fuentes`.
4. Abrí **Descargas** en otra ventana y arrastrá `CONTEXTO-borrador.md` adentro de `fuentes`.
5. Abrí **PowerShell** y entrá a la carpeta del cerebro:

```powershell
cd $HOME\Documents\cerebro-[TU-EMPRESA]
```

> **Ojo:** si tu Windows guarda Documentos en OneDrive, ese comando da error "no se encuentra la ruta". Usá el truco de abajo. Y conviene que el cerebro **no** quede sincronizado con OneDrive y GitHub a la vez: si dudás, preguntá en la mesa.

</div>

> **Tip:** si el comando `cd` da error, escribí `cd ` (con un espacio al final), arrastrá la carpeta `cerebro-[TU-EMPRESA]` desde Finder o el Explorador hasta la ventana de la terminal y apretá **Enter**. La ruta se escribe sola.

**Tenés que ver:** la terminal muestra `cerebro-[TU-EMPRESA]` al final de la línea, y adentro de la carpeta está `fuentes/CONTEXTO-borrador.md`.

## Paso 2 · Instalá la skill "armar-mi-cerebro"
Una skill es un proceso escrito que Claude sigue solo cada vez que se lo pedís. Esta la escribimos para el taller: entrevista, ordena y escribe tu cerebro.

Lo hacés en **dos mensajes**: primero le avisás a Claude qué va a recibir, después le pegás la skill.

1. En la terminal, dentro de la carpeta, abrí Claude Code:

```bash
claude
```

Si te pregunta si confiás en la carpeta, elegí **Yes**.

2. Copiá este primer mensaje, pegalo en Claude Code y apretá **Enter**:

```prompt
En mi próximo mensaje te voy a pegar el texto de una skill. Guardalo exacto y sin cambios en el archivo SKILL.md de una skill personal llamada armar-mi-cerebro, en la carpeta de skills de mi usuario: ~/.claude/skills/armar-mi-cerebro/SKILL.md (si estoy en Windows, es la misma carpeta .claude dentro de mi usuario). Cuando termines, decime la ruta exacta donde quedó. Ahora solo respondé "Listo, pegala".
```

**Tenés que ver:** Claude responde "Listo, pegala" (o parecido).

3. Abrí la página [Kit del taller](#r-kit) en otra pestaña, tocá **Copiar** en la skill `armar-mi-cerebro`, volvé a Claude Code, pegala y apretá **Enter**. Si es largo, Claude Code lo muestra como `[Pasted text …]`: es normal.
4. Claude te va a pedir permiso para crear el archivo: leé la ruta y aceptá.
5. Cerrá Claude Code (escribí `/exit` y **Enter**) y volvé a abrirlo con `claude`, así carga la skill nueva.

**Tenés que ver:** si escribís `/` aparece `armar-mi-cerebro` en la lista.

## Paso 3 · Que Claude arme tu cerebro
Escribí:

```prompt
/armar-mi-cerebro
```

Claude va a leer tu borrador (en `fuentes/`), contarte qué entendió y crear las carpetas (`negocio/`, `marca/`, `ventas/`, `equipo/`, `operacion/`, `datos/`, `objetivos/`). Después te va a hacer preguntas **de a 5**.

Cómo contestar para que salga bien:
- Contestá como le hablarías a un empleado nuevo. Corto y concreto.
- Si la sugerencia está bien, escribí **"sí"**. Si no sabés, **"pendiente"**.
- Para la voz de la marca, pegá 2 o 3 mensajes reales tuyos (un WhatsApp a un cliente, un posteo, la transcripción de un audio). Sirve más que describirte.
- Respuestas largas: podés dictarlas con el micrófono de tu compu y pegar el texto.

**Tenés que ver:** Claude te cuenta qué entendió de tu negocio, crea las carpetas y te hace la primera tanda de preguntas numeradas.

> **Tip:** no hace falta resolver todos los pendientes hoy. Con 30 minutos de preguntas ya tenés un cerebro que funciona. El resto lo completás en la semana: abrís Claude Code en la carpeta y escribís `/armar-mi-cerebro` de nuevo.

## Paso 4 · Mirá lo que quedó
1. En Claude Code, pedí:

```prompt
Mostrame el árbol de archivos del cerebro y cuántos pendientes quedan en objetivos/pendientes.md.
```

2. Opcional: abrí la carpeta en **Obsidian** (**Abrir carpeta como bóveda**) para leerla y editarla como un cuaderno ([Obsidian](#s11-obsidian)).

**Tenés que ver:** un `CLAUDE.md` corto (menos de 80 líneas) y las carpetas con archivos adentro.

## Paso 5 · Probalo
Cerrá Claude Code (`/exit`), volvé a abrirlo en la carpeta (`claude`) y preguntá, sin explicarle nada:

```prompt
Sin que te cuente nada: ¿quién es nuestro cliente ideal, qué es lo que más nos preguntan y cómo respondemos la objeción más común? Después escribí un mensaje de bienvenida para un cliente nuevo con nuestra voz.
```

**Tenés que ver:** respuestas sobre tu empresa, con tus palabras, sin que le hayas explicado nada.

Si algo está mal, corregilo ahí mismo: "Eso no es así, es [LO CORRECTO]. Guardalo en el archivo que corresponda."

## Paso 6 · Subilo a GitHub (privado)
GitHub guarda tu cerebro en la nube, con historial de cada cambio. Si mañana usás otra IA o cambiás de compu, tu cerebro sigue siendo tuyo.

1. En Claude Code:

```prompt
Prepará esta carpeta para Git: creá un .gitignore que excluya .env, *.key, .DS_Store y cualquier archivo de fuentes/ que tenga datos personales de clientes (el CONTEXTO-borrador.md no se excluye: va al repo privado). Inicializá el repositorio y hacé el primer commit con el mensaje "Cerebro inicial".
```

2. Abrí **GitHub Desktop › File › Add local repository**, tocá **Choose…**, elegí tu carpeta `cerebro-[TU-EMPRESA]` (en **Documentos**) y tocá **Add repository**.
3. Arriba, tocá **Publish repository**, dejá tildado **Keep this code private** y tocá **Publish Repository**.

**Tenés que ver:** en [github.com](https://github.com), en tu perfil, el repositorio `cerebro-[TU-EMPRESA]` con el candado de privado.

> **Ojo:** el repositorio tiene que ser **privado**. Si GitHub Desktop no muestra la casilla, revisalo después en [github.com](https://github.com) › tu repo › **Settings › General › Danger Zone › Change visibility**.

## Cómo sé que funcionó
- Abrís Claude Code en la carpeta, preguntás algo de tu negocio y responde bien sin que le expliques nada.
- El repo aparece en GitHub como privado.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `/armar-mi-cerebro` no aparece | Cerrá Claude Code con `/exit` y abrilo de nuevo. Si sigue sin aparecer, pedí: "¿Dónde están mis skills personales? Fijate si existe armar-mi-cerebro". |
| Claude pregunta demasiado de golpe | Escribile: "De a 3 preguntas, por favor". |
| Claude inventa algo | "Eso no está en mi negocio, sacalo y dejalo como PENDIENTE". |
| No encuentra el borrador | Revisá que el archivo esté en `cerebro-[TU-EMPRESA]/fuentes/` y que abriste `claude` parado en `cerebro-[TU-EMPRESA]` (no adentro de `fuentes`). Si lo dejaste suelto en la carpeta principal, también funciona: la skill lo mueve sola a `fuentes/`. |
| GitHub Desktop no ve la carpeta como repositorio | Te faltó el paso 6.1: pedile a Claude que inicialice Git. O en GitHub Desktop tocá **create a repository** cuando te lo ofrezca. |
| El commit falla con "Please tell me who you are" | Git no tiene tu nombre y mail: hacé [GitHub](#s4-github), Paso 4, y pedile a Claude que repita el commit. |

## Para seguir solo
- **Una vez por semana**, 15 minutos: `/armar-mi-cerebro` para resolver pendientes. Cada respuesta que agregás mejora todo lo que la IA hace por vos.
- **Usalo desde el celular**: en [claude.ai](https://claude.ai) creá un **Proyecto**, subí los archivos del cerebro como conocimiento y usalo desde la app.
- **Sumá a tu equipo**: invitalos al repo de GitHub. Si alguien cambia una respuesta de precios, todos (y la IA) usan la versión nueva.
