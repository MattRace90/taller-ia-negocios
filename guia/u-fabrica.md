---
titulo: "Fábrica de contenidos: plan del mes, imágenes y video"
bloque: Tutorial
tiempo: 90 min (más 20 a 30 min de instalación)
para: Todos (ejemplos con Celve y Viajes TDH Docta; sirve para cualquier rubro)
necesitas: s2-claude-code, p1-cerebro
resultado: Tres skills instaladas (plan de contenidos, imágenes para redes y video para redes) que leen la marca desde tu cerebro y te entregan el PDF del mes, placas en PNG y un reel editado.
---

La fábrica son tres skills (recetas escritas que Claude sigue siempre igual) que se suman a Claude: uno arma **qué se publica en el mes**, otro hace **las placas y los carruseles** y el tercero **edita el video que grabás con el celular**. Los tres leen la misma ficha de tu marca, así que todo sale con tu voz, tus colores y tu logo. Nada se genera ni se publica sin que lo apruebes.
Ejemplo: Celve le pasa las novedades de diciembre (inventadas para este ejemplo: "lanzamos una caja navideña") y recibe el calendario del mes, las 8 placas listas y el guion del reel para grabar en la planta.

## Antes de empezar
- [ ] Claude Code instalado, o la app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)). Pide plan Pro o superior.
- [ ] El cerebro de tu empresa armado en `Documentos/cerebro-[TU-EMPRESA]` ([Armá el cerebro](#p1-cerebro)), con `marca/` completa.
- [ ] Tu logo en PNG sin fondo (si lo tenés). En Canva: **Descargar › PNG › Fondo transparente**.
- [ ] Unos 3 GB libres en el disco y buena conexión: el instalador baja programas y un modelo de voz de unos 500 MB.
- [ ] Google Chrome o Microsoft Edge (para los PDF).
- [ ] Opcional: cuenta de Higgsfield, solo si querés escenas fotorrealistas en las placas ([Herramientas creativas](#s12-creativas)).

> **Ojo:** si podés, instalá la fábrica **antes** del taller o en el almuerzo. Con 20 personas bajando 500 MB a la vez, el wifi del salón se arrastra.

> **Costo:** la fábrica es gratis. Usa tu plan de Claude. Las placas "Claude (gratis)" y la edición de video no gastan nada extra. Higgsfield es pago (desde USD 15/mes en el plan Starter, nov 2026; [precios oficiales](https://higgsfield.ai/pricing) y detalle en [Stack y costos](#r-stack-y-costos)).

> **Datos:** la ficha de la marca guarda cómo hablás y qué vendés. No le pases contraseñas, DNI, teléfonos de clientes ni datos bancarios. La skill tiene prohibido guardarlos.

## Qué instala (para que sepas qué pasa en tu compu)

| Qué | Para qué |
|---|---|
| Node.js | Generar los PDF y correr el verificador |
| ffmpeg | Leer y editar video |
| uv + Python 3.12 | Correr los scripts de placas y video sin instalar nada a mano |
| Modelo de voz Whisper "small" (~500 MB) | Pasar a texto lo que grabaste |
| Las 3 skills | Se copian a la carpeta de skills de tu usuario (`~/.claude/skills/`) |
| Homebrew (solo Mac, si no lo tenés) | El instalador de programas de Mac. Te pide la contraseña de la Mac |

Si ya tenías una versión anterior de estas skills, el instalador la guarda en `~/.claude/skills-anteriores/` antes de copiar la nueva. Se puede correr más de una vez sin problema.

## Paso 1 · Descargá y descomprimí la fábrica
1. [Descargá la fábrica](kit/descargas/fabrica-de-contenidos.zip) (pesa 1 MB).

<div data-os="mac">

2. Andá a **Descargas** y hacé doble clic en `fabrica-de-contenidos.zip`. Se crea la carpeta `fabrica-de-contenidos`. Si bajaste con Safari, puede que ya la haya descomprimido sola: si ves la carpeta y no el ZIP, está bien, seguí.
3. Abrila. Adentro tenés `GUIA.pdf`, `INSTALAR-Mac.command`, `INSTALAR-Windows.bat`, `LEEME-PRIMERO.txt` y las carpetas `instalador` y `skills`.

</div>
<div data-os="win">

2. Andá a **Descargas**, hacé clic derecho en `fabrica-de-contenidos.zip` › **Extraer todo…** › **Extraer**.
3. Abrí la carpeta que se creó. Adentro tenés `GUIA.pdf`, `INSTALAR-Mac.command`, `INSTALAR-Windows.bat`, `LEEME-PRIMERO.txt` y las carpetas `instalador` y `skills`.

> **Ojo:** no lo abras con doble clic "desde adentro" del ZIP sin extraer: el instalador no encuentra la carpeta `skills` y no copia nada.

</div>

**Tenés que ver:** la carpeta `fabrica-de-contenidos` con los archivos de arriba.

## Paso 2 · Corré el instalador

<div data-os="mac">

1. Hacé doble clic en **INSTALAR-Mac.command**.
2. Si aparece **"no se puede abrir porque es de un desarrollador no identificado"** (es Gatekeeper, el control de seguridad de la Mac):
   - Cerrá el aviso. Hacé **clic derecho** sobre `INSTALAR-Mac.command` › **Abrir** › **Abrir**.
   - Si el aviso no trae el botón **Abrir**: andá a **Configuración del Sistema › Privacidad y seguridad**, bajá hasta el final y tocá **Abrir igualmente** al lado del nombre del archivo. Confirmá con tu contraseña o Touch ID.
3. Si dice que **no tenés permisos** para abrirlo: abrí la app **Terminal**, escribí `bash ` (con un espacio al final), arrastrá `INSTALAR-Mac.command` adentro de la ventana y apretá Enter.
4. Si no tenés Homebrew, te pide la **contraseña de la Mac**. Al escribirla no se ve nada: es normal. Escribila y Enter.
5. Si no encuentra Google Chrome, te pregunta si lo instala: respondé `s` y Enter (o `n` si usás Edge).
6. Esperá. Muestra los pasos del 1 al 7. El paso 6 (modelo de voz) es el más lento.

> **Ojo:** verificá en tu Mac el texto exacto del aviso y del botón: cambia un poco según la versión de macOS.

</div>
<div data-os="win">

> **Ojo:** en compus de empresa, el antivirus puede bloquear o borrar el `.bat`, o Windows te pide una clave de administrador que no tenés. No lo desactives por tu cuenta: pedí ayuda a la mesa. Mientras tanto, las skills del **Plan B** (al final de esta página) se instalan sin instalador.

1. Hacé doble clic en **INSTALAR-Windows.bat**.
2. Si aparece **"Windows protegió su PC"** (es SmartScreen): tocá **Más información** › **Ejecutar de todas formas**.
3. Cuando Windows pregunte si permitís que la app haga cambios, tocá **Sí** (lo pide al instalar Node.js, ffmpeg o uv).
4. Esperá. Muestra los pasos del 1 al 7. El paso 6 (modelo de voz) es el más lento.

Necesita **winget** (el instalador de apps de Windows). Si dice que no lo encuentra, instalá **Instalador de aplicaciones** (App Installer) desde Microsoft Store y volvé a abrir `INSTALAR-Windows.bat`.

> **Datos:** en Windows el instalador deja guardadas dos variables de tu usuario: `UV_PYTHON_INSTALL_DIR` (para que Python funcione dentro de la app de Claude) y `HF_HUB_DISABLE_SYMLINKS_WARNING` (para que no salga un aviso al bajar el modelo de voz). No toca nada más del sistema.

</div>

7. Cuando termine, **cerrá Claude y volvé a abrirlo** (si lo usás en la terminal: `/exit` y otra vez `claude`). Si no, no ve lo que se instaló.

**Tenés que ver:** al final de la ventana del instalador, el verificador dice que está todo listo. En Claude Code, al escribir `/` aparecen `plan-de-contenidos`, `imagenes-para-redes` y `video-para-redes`.

## Paso 3 · Comprobá la instalación
Abrí Claude Code en la carpeta de tu cerebro:

<div data-os="mac">

```bash
cd ~/Documents/cerebro-[TU-EMPRESA]
claude
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\cerebro-[TU-EMPRESA]
claude
```

</div>

En la app de escritorio: pestaña **Code** › selector de entorno › **Local** › **Open folder…** › elegí `cerebro-[TU-EMPRESA]`.

```prompt
Verificá que las skills de contenido estén bien instaladas.
```

**Tenés que ver:** que está todo listo. Si falta algo, te dice qué y cómo resolverlo (casi siempre: correr el instalador de nuevo y reabrir Claude).

## Paso 4 · Conectá la fábrica con el cerebro de tu empresa
La fábrica guarda todo en una **carpeta de trabajo** y lee la ficha de cada marca desde `marcas/<marca>/cerebro.md`. La vas a crear **dentro** de la carpeta de tu cerebro, así tenés un solo lugar para todo y la skill la encuentra sola.

1. Antes, copiá tu logo a la carpeta `marca/` de tu cerebro (por ejemplo, `marca/logo.png`). Creá la carpeta de trabajo con este prompt. Cambiá `[NOMBRE-DE-TU-EMPRESA]`, los colores (los códigos tipo `#1A2B3C` de `marca/identidad-visual.md`) y `[RUTA-AL-LOGO.png]` por `marca/logo.png`:

```prompt
Creá mi carpeta de contenido en la carpeta contenidos/ de este proyecto. Es para una sola marca, la mía (uso propio). Los PDF tienen que salir con el nombre "[NOMBRE-DE-TU-EMPRESA]", estos colores: [#COLOR1], [#COLOR2], y el logo que está en [RUTA-AL-LOGO.png].
```

**Tenés que ver:** la carpeta `contenidos/` creada dentro de tu carpeta del cerebro.

2. Cargá tu marca desde el cerebro (no la escribas de nuevo). Cambiá `[NOMBRE-DE-TU-MARCA]` y la ruta del logo como antes:

```prompt
Cargá mi marca en la fábrica de contenidos. La fuente es el cerebro de mi empresa que está en esta carpeta: leé CLAUDE.md y las carpetas negocio/, marca/ y ventas/. No leas datos/ ni nada con datos de clientes. Con eso armá el Cerebro de la marca [NOMBRE-DE-TU-MARCA] en contenidos/marcas/ con el formato de la skill. Copiá el logo de [RUTA-AL-LOGO.png]. Lo que no esté en mi cerebro dejalo como [COMPLETAR] y mostrame un resumen corto para confirmar.
```

3. Leé el resumen. Corregí lo que esté mal con tus palabras ("el tono es más formal, tratamos de usted", "publicamos lunes, miércoles y viernes"). Completá lo que falte: sobre todo **cuántas piezas por mes** (posteos, reels, historias) y **cómo te contactan** (WhatsApp, mensaje de Instagram, link).

> **Tip:** tu cerebro sigue siendo la fuente de verdad. Si cambiás algo en `marca/`, pedí: "Actualizá el Cerebro de la marca en contenidos/ con lo nuevo de marca/". Así no tenés dos versiones distintas.

**Tenés que ver:** `contenidos/marcas/[tu-marca]/cerebro.md` con las secciones A a I (la marca, productos, público, voz, identidad visual, objetivos, restricciones, material y aprendizaje), tu logo al lado y `contenidos/identidad.json`.

## Paso 5 · Ejercicio 1: el plan de contenidos del mes
1. Pasale las novedades y los eventos del mes (si no hay, decilo):

```prompt
Novedades de [MES]: [LANZAMIENTOS, PROMOS CON PRECIO Y VIGENCIA, CAMBIOS DE HORARIO]. Eventos: [FECHA Y QUÉ: TALLER, CHARLA, FERIA]. Si no hay eventos, no inventes ninguno.
```

2. Pedí el plan:

```prompt
Armame el plan de contenidos de [MES] de [NOMBRE-DE-TU-MARCA]. Publicamos [N] posteos (de los cuales [N] son carruseles), [N] reels y [N] historias. El objetivo del mes es [QUÉ QUERÉS LOGRAR, EJ: QUE NOS ESCRIBAN POR WHATSAPP PARA LA CAJA NAVIDEÑA].
```

3. Claude te pregunta lo que falte (todo junto) y te muestra **la tabla del mes**: código, fecha, formato, tema, etapa, idea y la primera frase de cada pieza. P1, P2… son posteos; H1… historias; R1… reels.
4. Aprobá o cambiá con tus palabras. Rehace solo lo que pediste:

```prompt
Todo bien menos el P3, que se parece al P1. Y pasá la H2 al viernes.
```

5. Cuando esté todo aprobado, desarrolla cada pieza (texto de cada placa, texto de la publicación con hashtags y qué hay que grabar o fotografiar, con fecha límite) y te pregunta si genera el PDF. Decí que sí.

**Tenés que ver:** en `contenidos/entregas/[AAAA-MM]/[tu-marca]/` los archivos `plantilla.pdf` (qué grabar y hasta cuándo, el detalle de cada pieza y el calendario) y `calendario.csv` (para pegar en una planilla).

> **Tip:** si algo vale para siempre, decilo así: "Esto vale para adelante: nunca usamos la palabra barato". Lo guarda en la ficha de la marca y no lo repite.

## Paso 6 · Ejercicio 2: imágenes y carrusel para redes
Podés hacer las placas del plan o una pieza suelta.

1. Un carrusel suelto (ejemplo con Viajes TDH Docta, datos inventados):

```prompt
Haceme un carrusel de 5 placas para [NOMBRE-DE-TU-MARCA] con [TEMA, EJ: 4 ERRORES AL ARMAR LA VALIJA PARA UN VIAJE LARGO]. Formato 4:5. Imagen: Claude (gratis). Método: desde cero.
```

   O las placas del plan que aprobaste:

```prompt
Hacé las imágenes del plan de [MES].
```

2. **Freno:** primero te muestra el texto de cada placa (titular, texto y la invitación final) y la idea visual. Aprobá o corregí. No diseña nada hasta que digas que sí.
3. Arma el fondo con tus colores (y tus fotos, si están en la carpeta de la marca), pone los textos con un programa (así no salen letras deformes) y revisa cada placa antes de mostrártela.
4. Pedí cambios con tus palabras: "el titular más grande", "otro fondo", "sin el logo arriba". Cada cambio sale como versión nueva (v2, v3).
5. Pasalo a historia sin estirarlo:

```prompt
Pasala a historia 9:16.
```

**Tenés que ver:** los PNG en `contenidos/entregas/[AAAA-MM]/[tu-marca]/imagenes/[CÓDIGO]/` y una hoja de contacto con todas las placas juntas. Abrí los PNG con doble clic para verlos en grande.

> **Tip:** si tenés Higgsfield conectado, elegí "Imagen: Higgsfield (pago)" para una escena fotorrealista. La IA hace solo el fondo, sin letras; el texto y tu producto real los pone el programa. Si no está conectado, te da el prompt listo para pegar en Higgsfield y te pide la imagen.

> **Tip:** ¿viste una placa que te gusta? "Copiá el estilo de esta imagen con mi marca" y adjuntala. Copia la estructura, no los textos, el logo ni las personas.

## Paso 7 · Ejercicio 3: video para redes
La skill **no genera video con IA**: arma el guion, vos grabás con el celular y ella edita sola (cortes, subtítulos con tu letra y tus colores, tomas de apoyo, cierre con logo y portada). Si querés un video hecho 100% con IA (escenas generadas o un presentador virtual), eso es con Higgsfield o HeyGen: mirá [Herramientas creativas](#s12-creativas).

1. Pedí el guion:

```prompt
Armame un reel para esta semana de [NOMBRE-DE-TU-MARCA] sobre [TEMA]. Lo graba [QUIÉN]. Duración 20 a 30 segundos.
```

   Si nadie quiere aparecer: "Quiero un reel sin hablar ni mostrar la cara".

2. **Freno:** te muestra el plan del video, el guion palabra por palabra y cómo grabarlo. Aprobá o cambiá.
3. Grabá con el celular siguiendo estas reglas:
   - Vertical y apoyado, a la altura de los ojos. Luz de ventana de frente.
   - **Cada frase en una toma aparte** (o todo seguido con una pausa entre frases). Si te trabás, repetí la frase entera.
   - 2 o 3 tomas cortas **sin hablar** (manos, producto, lugar) de 5 a 8 segundos.
   - Pasá los videos **originales**: sin filtros, sin música y sin reenviarlos por WhatsApp.
4. Pasá los videos a la compu (AirDrop en Mac; cable o Google Drive en Mac y Windows) y decí dónde están:

```prompt
Ya grabé, los videos están en [RUTA, EJ: Descargas/reel-diciembre]. Editalo.
```

5. **Freno:** te muestra el **storyboard** (qué se escucha y qué se ve en cada momento) y te pregunta el estilo (sobrio, cálido, moderno o enérgico), las tomas de apoyo y la música. Aprobá.
6. Edita solo. Pedí cambios con tus palabras: "en el segundo 5 que se vea el producto", "hacelo más corto".

**Tenés que ver:** el video en `contenidos/entregas/[AAAA-MM]/[tu-marca]/videos/[CÓDIGO]/entrega/`, con su portada y el archivo de subtítulos `.srt`. Miralo y escuchalo vos antes de publicar: Claude no escucha el audio.

> **Ojo:** la primera edición tarda más porque pasa la voz a texto con el modelo que bajó el instalador. Después es rápido. La música se la sumás al publicar, desde la biblioteca de Instagram o TikTok (o una de Pixabay Music que la skill te sugiere buscar).

## Cómo sé que funcionó
Con los tres ejercicios hechos tenés: el PDF del mes, un carrusel en PNG y un reel editado, todo con tu marca. La prueba final:

```prompt
Mostrame qué hay en contenidos/entregas/ de este mes: cuántas piezas del plan están aprobadas, cuáles ya tienen imágenes o video y qué quedó marcado como [COMPLETAR].
```

**Tenés que ver:** la lista de piezas con su estado y lo que falta completar.

## Si algo falla

| Te pasa | Hacé esto |
|---|---|
| Claude no encuentra las skills | Cerrá y abrí Claude. Si sigue igual, corré el instalador de nuevo. |
| Mac: "desarrollador no identificado" | Clic derecho › **Abrir** › **Abrir**, o **Configuración del Sistema › Privacidad y seguridad › Abrir igualmente**. |
| Mac: "no tenés permisos" al abrir el instalador | Terminal › escribí `bash ` › arrastrá `INSTALAR-Mac.command` › Enter. |
| Windows: el instalador se cierra enseguida | Clic derecho en `INSTALAR-Windows.bat` › **Ejecutar como administrador**. Fijate que hayas extraído el ZIP. |
| "No encuentro ffmpeg" o "uv" | Cerrá y abrí Claude: se instalaron pero todavía no los ve. |
| El PDF no se genera | Pedí "Verificá la instalación". Hace falta Chrome o Edge. |
| Las piezas salen genéricas | Completá la voz en tu cerebro (`marca/`) con 2 o 3 textos reales tuyos y pedí que actualice el Cerebro de la marca. |
| El logo sale con un recuadro blanco | Pasalo en PNG sin fondo. |

## Para seguir solo
- Cada mes: "Novedades de [MES]: …" y "Armame el plan de contenidos de [MES]". Podés dejarlo como [tarea programada](#t4-tareas-programadas) para que el primer lunes del mes te arme el borrador.
- Si manejás varias marcas o líneas de producto, cargá una ficha por marca en `contenidos/marcas/` y pedí el plan de cada una por su nombre.
- Programá lo aprobado en Metricool ([Herramientas creativas](#s12-creativas)) y, al mes siguiente, contale a Claude qué funcionó: "Esto vale para adelante: …".

## Plan B: las skills de la agencia
Si la fábrica no se instala en tu compu, o querés ir más allá (anuncios para Meta, nombres ordenados para tus creativos, estrategia de competencia), estas son skills que usamos en la agencia. Las limpiamos para el taller: no traen datos de clientes. No dependen de la fábrica: se instalan solas.

| Skill | Para qué sirve | Cuándo usarla | Necesita |
|---|---|---|---|
| [creador-angulos-publicitarios](kit/plan-b/creador-angulos-publicitarios.zip) | Arma con vos, paso a paso, un **ángulo de venta**: a quién le hablás, qué dolor, qué parte de tu producto lo resuelve y qué promesa hacés. | Antes de hacer anuncios o un plan de contenido de venta. | Nada |
| [nomenclador-ads](kit/plan-b/nomenclador-ads.zip) | Le pone **nombre ordenado** a cada anuncio (formato, persona, tono, ángulo, gancho, palanca, estructura) analizándolo. | Cuando tenés muchos anuncios y querés saber cuál rinde y por qué. | Nada |
| [rediseno-9x16](kit/plan-b/rediseno-9x16.zip) | Rediseña una placa cuadrada como **historia o reel vertical**, sin estirarla. | Cuando tenés el 1:1 aprobado y necesitás el 9:16. | Nada |
| [static-remix](kit/plan-b/static-remix.zip) | Toma un PDF con **anuncios ganadores de la competencia** y los recrea con tu producto y tu marca. | Cuando querés probar anuncios estáticos nuevos rápido. | Higgsfield conectado (pago) y Python con PyMuPDF |
| [estrategia-benchmark](kit/plan-b/estrategia-benchmark.zip) | Analiza los anuncios de tu competencia en la Biblioteca de anuncios de Meta, los puntúa y arma una **presentación de estrategia**. | Para planificar campañas o presentar una estrategia. | Navegador; mejor con el conector de Meta ([Meta y Google](#s14-meta-y-google)) |
| [product-bible](kit/plan-b/product-bible.zip) | Arma una **carpeta por producto** con ficha, colores, mensajes, reseñas e imágenes ordenadas. | Si tenés catálogo (alimentos, productos, paquetes) y querés una fuente única para hacer anuncios. | Python con Pillow |
| [frontend-design](kit/plan-b/frontend-design.zip) | Guía de diseño para que una **web o landing** no parezca hecha con plantilla. Es de Anthropic (licencia Apache 2.0). | Con el [desafío de web](#d3-web-app). | Nada |
| [animaciones](kit/plan-b/animaciones.zip) | 20 estilos de **animación en código** (neón, papel, pizarra, pixel art…) para animar una escena de tu producto o tu negocio. | Para un video corto distinto, sin grabar. | Node.js. Usa Remotion: gratis para empresas de hasta 3 personas ([Stack y costos](#r-stack-y-costos)) |

### Cómo instalar una skill del Plan B
1. Descargá el ZIP de la tabla.
2. Descomprimilo en tu carpeta de skills:

<div data-os="mac">

```bash
mkdir -p ~/.claude/skills
unzip ~/Downloads/[NOMBRE-DE-LA-SKILL].zip -d ~/.claude/skills/
```

> **Ojo:** si bajaste con Safari, puede que ya lo haya descomprimido y el `.zip` no esté. En ese caso, en vez de `unzip` usá `mv ~/Downloads/[NOMBRE-DE-LA-SKILL] ~/.claude/skills/`.

</div>
<div data-os="win">

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Expand-Archive -Path "$HOME\Downloads\[NOMBRE-DE-LA-SKILL].zip" -DestinationPath "$HOME\.claude\skills\"
```

</div>

3. Cerrá y abrí Claude Code. Escribí `/` y buscala.

**Tenés que ver:** la skill en la lista, por ejemplo `/creador-angulos-publicitarios`.

Para usarla en la app de Claude (web o escritorio): **Settings › Capabilities** › activá **Code execution and file creation**. Después **Customize › Skills** y subí el ZIP tal cual lo descargaste (adentro ya trae la carpeta de la skill). Más detalle en el [Kit del taller](#r-kit).

> **Ojo:** `animaciones` necesita además correr `npm install` dentro de su carpeta la primera vez (la skill se lo pide a Claude sola). `static-remix` gasta créditos de Higgsfield por cada imagen: siempre te muestra el costo y pide confirmación antes de generar.
