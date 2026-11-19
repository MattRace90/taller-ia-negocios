---
titulo: Armá el cerebro de tu empresa
bloque: Práctica
tiempo: 60 min (de 12 a 13, todos juntos)
para: Todos
necesitas: s1-claude, s2-claude-code, s4-github
resultado: Una carpeta con tu negocio escrito en archivos .md, que Claude lee solo desde la pestaña Code y que queda guardada en GitHub privado.
---

La IA no conoce tu negocio: trabaja con lo que le das para leer. Hoy vas a dejar escrito, en archivos simples, lo que está en tu cabeza: qué vendés, a quién, cómo respondés a "¿es una estafa?" o "es caro", cómo hablás.
Es el manual del empleado nuevo, pero el empleado es Claude. Todo lo que hagamos a la tarde (bots, propuestas, contenido) lee de acá. Todo se hace desde la **pestaña Code** de la app de Claude, sin terminal.

## Antes de empezar
- [ ] La app de escritorio de Claude abierta, con tu cuenta, y la pestaña **Code** visible arriba de la barra lateral ([Instalá Claude Code](#s2-claude-code)).
- [ ] GitHub Desktop instalado y con tu cuenta de GitHub iniciada ([GitHub](#s4-github)).
- [ ] Tu archivo **CONTEXTO-borrador.md**, descargado de la tabla de [Usá tu borrador](#c2-tu-borrador) (queda en **Descargas**). Si no lo tenés, igual podés hacer esta práctica: Claude te entrevista desde cero.

### Traé (o tené a mano en tu compu) · recomendado, no obligatorio
Ya te lo pedimos en el formulario y mucho está en tu borrador. Igual, tenelo a mano: Claude te lo va a pedir para completar el cerebro. Si lo subiste a una carpeta de Drive en el formulario, el link está en la página de tu empresa (sección **Empresas**).
- **Tu marca:** manual de marca si lo tenés, logo, colores, tipografías y 3 piezas tuyas que te gusten.
- **Tu competencia:** 3 a 5 competidores con su web e Instagram, y una marca de tu rubro que admires.
- **Lo que vendés:** lista de productos o servicios con precios, promos y condiciones.
- **Cómo hablás:** 2 o 3 mensajes reales (un WhatsApp, un posteo, un audio transcripto).
- **Lo que más te preguntan:** las 10 preguntas frecuentes con su respuesta oficial.
- **Cómo trabajás:** los procesos clave (cómo se vende, cómo se atiende, quién hace qué).
- **A dónde vas:** el objetivo de los próximos 90 días, en un número.

> **Datos:** en el cerebro va cómo funciona tu negocio, no los datos de tus clientes. Nada de nombres, DNI, teléfonos ni deudas de clientes, contraseñas o claves.

## Paso 1 · Creá la carpeta del cerebro
Una carpeta por empresa, en **Documentos**, siempre con el mismo nombre: `cerebro-[TU-EMPRESA]`, en minúsculas, sin espacios ni tildes (por ejemplo `cerebro-fondus`). Adentro, una subcarpeta `fuentes` con el borrador.

**Opción A · con el Finder o el Explorador:**

<div data-os="mac">

1. **Finder › Documentos**. Clic derecho en un lugar vacío › **Nueva carpeta** › `cerebro-[TU-EMPRESA]`.
2. Entrá (doble clic) y creá adentro la carpeta `fuentes`.
3. Arrastrá `CONTEXTO-borrador.md` desde **Descargas** a `fuentes`.

</div>
<div data-os="win">

1. **Explorador de archivos › Documentos**. Clic derecho en un lugar vacío › **Nuevo › Carpeta** › `cerebro-[TU-EMPRESA]`.
2. Entrá (doble clic) y creá adentro la carpeta `fuentes`.
3. Arrastrá `CONTEXTO-borrador.md` desde **Descargas** a `fuentes`.

> **Ojo:** si tu Windows guarda Documentos en OneDrive, conviene que el cerebro **no** quede sincronizado con OneDrive y GitHub a la vez. Si dudás, preguntá en la mesa.

</div>

**Opción B · pidiéndoselo a Claude:** en la app tocá **Code**, en el selector de entorno elegí **Local**, tocá **Open folder…** y elegí tu carpeta **Documentos**. Después escribí:

```prompt
Creá en esta carpeta la carpeta cerebro-[TU-EMPRESA] con una subcarpeta fuentes adentro. Buscá CONTEXTO-borrador.md en mi carpeta Descargas y movelo a cerebro-[TU-EMPRESA]/fuentes. Decime cómo quedó.
```

Claude te muestra un pedido de permiso con botones: leé qué va a hacer y tocá **Permitir**.

**Tenés que ver:** `Documentos/cerebro-[TU-EMPRESA]/fuentes/CONTEXTO-borrador.md`.

## Paso 2 · Abrí la carpeta en la pestaña Code
1. En la app, tocá **Code** (arriba de la barra lateral) y empezá una sesión nueva (**+ New**).
2. En el selector de entorno (debajo del cuadro de mensaje) elegí **Local**.
3. Tocá **Open folder…** (o el botón para elegir la carpeta) y elegí `cerebro-[TU-EMPRESA]`. No elijas `fuentes`: la de arriba.
4. Si te pregunta si confiás en la carpeta, aceptá.

> **Ojo:** el nombre del botón para elegir la carpeta puede variar según la versión de la app.

Escribí en el cuadro:

```prompt
¿Qué archivos hay en esta carpeta?
```

**Tenés que ver:** Claude nombra `fuentes/CONTEXTO-borrador.md`.

## Paso 3 · Instalá la skill "armar-mi-cerebro"
Una skill es un proceso escrito que Claude sigue cada vez que se lo pedís. Esta la escribimos para el taller: entrevista, ordena y escribe tu cerebro. Se la pedís a Claude y él la instala.

1. Abrí [Kit del taller](#r-kit) en otra pestaña y tocá **Copiar** en la skill `armar-mi-cerebro`.
2. Volvé a la pestaña Code, pegá este pedido y, **abajo, en el mismo mensaje**, pegá lo que copiaste:

```prompt
Instalá esta skill personal llamada armar-mi-cerebro: guardá el texto que pego abajo, exacto y sin cambios, en ~/.claude/skills/armar-mi-cerebro/SKILL.md (en Windows, la misma carpeta .claude dentro de mi usuario). Cuando termines, decime la ruta exacta donde quedó.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

3. Aparece el pedido de permiso para crear el archivo: leé la ruta y tocá **Permitir**.

> **Tip:** en vez de pegar el contenido, podés escribir: "Instalá como skill personal armar-mi-cerebro desde este link: https://mattrace90.github.io/taller-ia-negocios/kit/skills/armar-mi-cerebro/SKILL.md". Claude la baja y la guarda.

**Tenés que ver:** al escribir `/` en el cuadro aparece `armar-mi-cerebro` en la lista. Si no aparece, abrí una sesión nueva (**+ New**) en la misma carpeta.

## Paso 4 · Que Claude arme tu cerebro
Escribí:

```prompt
/armar-mi-cerebro
```

Claude lee tu borrador, te cuenta qué entendió, crea las carpetas (`negocio/`, `marca/`, `ventas/`, `equipo/`, `operacion/`, `datos/`, `objetivos/`) y te hace preguntas **de a 5**. Aprobá los permisos para crear archivos.

Cómo contestar:
- Como le hablarías a un empleado nuevo. Corto y concreto.
- Si la sugerencia está bien, **"sí"**. Si no sabés, **"pendiente"**.
- Para la voz de la marca, pegá 2 o 3 mensajes reales tuyos. Sirve más que describirte.
- Respuestas largas: dictalas con el micrófono de tu compu y pegá el texto.

**Tenés que ver:** el resumen de tu negocio, las carpetas nuevas y la primera tanda de preguntas numeradas.

> **Tip:** con 30 minutos de preguntas ya tenés un cerebro que funciona. El resto lo completás en la semana: abrís la carpeta en la pestaña Code y escribís `/armar-mi-cerebro` de nuevo.

## Paso 5 · Probalo
Abrí una sesión nueva (**+ New**) en la misma carpeta y preguntá, sin explicarle nada:

```prompt
Sin que te cuente nada: ¿quién es nuestro cliente ideal, qué es lo que más nos preguntan y cómo respondemos la objeción más común? Después escribí un mensaje de bienvenida para un cliente nuevo con nuestra voz.
```

**Tenés que ver:** respuestas sobre tu empresa, con tus palabras. Si algo está mal: "Eso no es así, es [LO CORRECTO]. Guardalo en el archivo que corresponda."

> **Tip:** si querés leerlo como un cuaderno, abrí la carpeta en **Obsidian** ([Obsidian](#s11-obsidian)).

## Paso 6 · Subilo a GitHub (privado)
GitHub guarda tu cerebro en la nube, con historial de cada cambio. Si cambiás de compu o de IA, tu cerebro sigue siendo tuyo.

1. En la pestaña Code:

```prompt
Creá un .gitignore en esta carpeta que excluya .env, *.key, .DS_Store y cualquier archivo de fuentes/ con datos personales de clientes (el CONTEXTO-borrador.md sí va: el repo es privado).
```

2. En **GitHub Desktop › File › Add local repository**, tocá **Choose…**, elegí `cerebro-[TU-EMPRESA]` y tocá **Add repository**. Si dice que no es un repositorio, tocá **create a repository** y después **Create repository**.
3. Arriba, tocá **Publish repository**, dejá tildado **Keep this code private** y tocá **Publish Repository**.

**Tenés que ver:** en [github.com](https://github.com), en tu perfil, el repo `cerebro-[TU-EMPRESA]` con el candado de privado.

> **Ojo:** el repo tiene que ser **privado**. Si no viste la casilla, revisalo en [github.com](https://github.com) › tu repo › **Settings › General › Danger Zone › Change visibility**.

## Cómo sé que funcionó
- Abrís la carpeta en la pestaña Code, preguntás algo de tu negocio y responde bien sin que le expliques nada.
- El repo aparece en GitHub como privado.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `/armar-mi-cerebro` no aparece | Abrí una sesión nueva. Si sigue, pedí: "¿Dónde están mis skills personales? Fijate si existe armar-mi-cerebro". |
| No encuentra el borrador | Revisá que abriste `cerebro-[TU-EMPRESA]` (no `fuentes`). Si el borrador quedó suelto en la carpeta principal, también sirve: la skill lo mueve a `fuentes/`. |
| Claude pregunta demasiado de golpe | "De a 3 preguntas, por favor". |
| Claude inventa algo | "Eso no está en mi negocio, sacalo y dejalo como PENDIENTE". |
| No me deja elegir **Local** o no veo **Code** | Actualizá la app de Claude y revisá que tu plan sea Pro o superior ([Instalá Claude Code](#s2-claude-code)). |
| GitHub Desktop no publica | Revisá que iniciaste sesión en **GitHub Desktop › Settings › Accounts** ([GitHub](#s4-github)). |

## Para seguir solo
- **Una vez por semana**, 15 minutos: `/armar-mi-cerebro` para resolver pendientes. Después, en GitHub Desktop: **Commit to main** y **Push origin**.
- **Usalo desde el celular**: creá un **Proyecto** en [claude.ai](https://claude.ai) con los archivos del cerebro ([Usá tu borrador](#c2-tu-borrador), Paso 4).
- **Sumá a tu equipo**: invitalos al repo privado. Si alguien cambia un precio, todos (y la IA) usan la versión nueva.
