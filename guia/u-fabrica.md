---
titulo: "Fábrica de contenidos: plan del mes, imágenes y video"
bloque: Tutorial
tiempo: 90 min (más 20 a 30 min de instalación)
para: Todos (ejemplos con Celve y Viajes TDH Docta; sirve para cualquier rubro)
necesitas: s2-claude-code, p1-cerebro
resultado: Tres skills instaladas (plan de contenidos, imágenes para redes y video para redes) que leen la marca desde tu cerebro y te entregan el PDF del mes, placas en PNG y un reel editado.
---

La fábrica son tres skills (recetas que Claude sigue siempre igual): una arma **qué se publica en el mes**, otra hace **las placas y carruseles** y la tercera **edita el video que grabás con el celular**. Las tres leen la ficha de tu marca: todo sale con tu voz, tus colores y tu logo. Nada se genera ni se publica sin tu aprobación.
Ejemplo inventado: Celve le pasa "lanzamos una caja navideña" y recibe el calendario de diciembre, 8 placas y el guion del reel.

Se instala **una vez** con doble clic. Después, todo se usa desde la pestaña **Code** de la app de Claude.

## Antes de empezar
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)). Plan Pro o superior.
- [ ] Tu cerebro en `Documentos/cerebro-[TU-EMPRESA]` con `marca/` completa ([Armá el cerebro](#p1-cerebro)).
- [ ] Tu logo en PNG sin fondo, si lo tenés (Canva: **Descargar › PNG › Fondo transparente**).
- [ ] Unos 3 GB libres y buena conexión: el instalador baja programas y un modelo de voz de ~500 MB.
- [ ] Google Chrome o Microsoft Edge (para los PDF).
- [ ] Opcional: Higgsfield, para escenas fotorrealistas ([Herramientas creativas](#s12-creativas)).

> **Ojo:** si podés, instalá **antes** del taller o en el almuerzo. Con 20 personas bajando 500 MB, el wifi se arrastra.

> **Costo:** la fábrica es gratis y usa tu plan de Claude. Higgsfield es pago (desde USD 15/mes, plan Starter, nov 2026; [precios oficiales](https://higgsfield.ai/pricing), [Stack y costos](#r-stack-y-costos)).

> **Datos:** la ficha de la marca guarda cómo hablás y qué vendés. Nada de contraseñas, DNI, teléfonos de clientes ni datos bancarios.

**Qué instala:** Node.js (PDF), ffmpeg (video), uv + Python 3.12 (scripts), el modelo de voz Whisper "small" (pasar a texto lo que grabaste), las 3 skills en tu carpeta de skills (`.claude/skills/`) y, solo en Mac y si no lo tenés, Homebrew (te pide la contraseña de la Mac). Si ya tenías una versión anterior, la guarda en `.claude/skills-anteriores/`. Se puede correr más de una vez.

## Paso 1 · Descargá y descomprimí la fábrica
[Descargá la fábrica](kit/descargas/fabrica-de-contenidos.zip) (1 MB).

<div data-os="mac">

En **Descargas**, doble clic en `fabrica-de-contenidos.zip`. Si bajaste con Safari, puede que ya esté descomprimida: si ves la carpeta, seguí.

</div>
<div data-os="win">

En **Descargas**, clic derecho en `fabrica-de-contenidos.zip` › **Extraer todo…** › **Extraer**. No lo abras desde adentro del ZIP sin extraer: el instalador no encuentra las skills.

</div>

**Tenés que ver:** la carpeta `fabrica-de-contenidos` con `GUIA.pdf`, `INSTALAR-Mac.command`, `INSTALAR-Windows.bat`, `LEEME-PRIMERO.txt` y las carpetas `instalador` y `skills`.

## Paso 2 · Corré el instalador (doble clic, una sola vez)

<div data-os="mac">

1. Doble clic en **INSTALAR-Mac.command**. Se abre una ventana de Terminal: es el instalador trabajando, no tenés que escribir comandos.
2. Si aparece **"no se puede abrir porque es de un desarrollador no identificado"** (Gatekeeper, el control de seguridad de la Mac): cerrá el aviso y hacé **clic derecho** › **Abrir** › **Abrir**. Si no hay botón **Abrir**: **Configuración del Sistema › Privacidad y seguridad** › al final, **Abrir igualmente**, y confirmá con tu contraseña o Touch ID.
3. Si te pide la **contraseña de la Mac** (para Homebrew): escribila y Enter. No se ve mientras la escribís: es normal.
4. Si pregunta si instala Google Chrome: `s` y Enter (o `n` si usás Edge).
5. Esperá los pasos del 1 al 7. El 6 (modelo de voz) es el más lento.

> **Ojo:** el texto exacto del aviso y del botón cambia según la versión de macOS.

</div>
<div data-os="win">

1. Doble clic en **INSTALAR-Windows.bat**.
2. Si aparece **"Windows protegió su PC"** (SmartScreen): **Más información** › **Ejecutar de todas formas**.
3. Cuando Windows pregunte si permitís cambios, tocá **Sí** (al instalar Node.js, ffmpeg o uv).
4. Esperá los pasos del 1 al 7. El 6 (modelo de voz) es el más lento.

Si dice que no encuentra **winget**, instalá **Instalador de aplicaciones** (App Installer) desde Microsoft Store y volvé a abrir el `.bat`.

> **Ojo:** en compus de empresa, el antivirus puede bloquear el `.bat` o pedir una clave de administrador. No lo desactives: pedí ayuda a la mesa y, mientras, usá el **Plan B** (al final).

</div>

Cuando termine, **cerrá la app de Claude y volvé a abrirla**. Si no, no ve lo instalado.

**Tenés que ver:** el verificador del instalador dice que está todo listo.

## Paso 3 · Abrí tu cerebro en la pestaña Code y comprobá
App de Claude › **Code** › **Local** › **Open folder…** › elegí `cerebro-[TU-EMPRESA]`.

```prompt
Verificá que las skills de contenido estén bien instaladas.
```

**Tenés que ver:** que está todo listo, y al escribir `/` aparecen `plan-de-contenidos`, `imagenes-para-redes` y `video-para-redes`. Si falta algo, te dice qué hacer (casi siempre: instalador de nuevo y reabrir Claude).

## Paso 4 · Conectá la fábrica con tu cerebro
La fábrica trabaja en una carpeta `contenidos/` **dentro** de tu cerebro. Copiá antes tu logo a `marca/logo.png`.

```prompt
Creá mi carpeta de contenido en contenidos/ de este proyecto, para una sola marca, la mía. Los PDF salen con el nombre "[NOMBRE-DE-TU-EMPRESA]", los colores de marca/identidad-visual.md y el logo de marca/logo.png.
Después cargá mi marca en la fábrica desde mi cerebro: leé CLAUDE.md y las carpetas negocio/, marca/ y ventas/ (no leas datos/ ni nada con datos de clientes). Armá el Cerebro de la marca [NOMBRE-DE-TU-MARCA] en contenidos/marcas/ con el formato de la skill. Lo que falte, dejalo como [COMPLETAR] y mostrame un resumen corto.
```

Corregí el resumen con tus palabras ("tratamos de usted", "publicamos lunes, miércoles y viernes") y completá **cuántas piezas por mes** y **cómo te contactan**.

> **Tip:** tu cerebro sigue siendo la fuente de verdad. Si cambiás `marca/`, pedí: "Actualizá el Cerebro de la marca en contenidos/ con lo nuevo de marca/".

**Tenés que ver:** `contenidos/marcas/[tu-marca]/cerebro.md` (secciones A a I), tu logo al lado y `contenidos/identidad.json`.

## Paso 5 · Ejercicio 1: el plan del mes

```prompt
Armame el plan de contenidos de [MES] de [NOMBRE-DE-TU-MARCA]. Publicamos [N] posteos ([N] carruseles), [N] reels y [N] historias. Objetivo del mes: [QUÉ QUERÉS LOGRAR]. Novedades: [LANZAMIENTOS, PROMOS CON PRECIO Y VIGENCIA]. Eventos: [FECHA Y QUÉ, o "ninguno": no inventes].
```

Claude pregunta lo que falte y te muestra **la tabla del mes** (P = posteo, H = historia, R = reel). Corregí: "Todo bien menos el P3, que se parece al P1. Pasá la H2 al viernes". Cuando apruebes, desarrolla cada pieza y te ofrece el PDF: decí que sí.

**Tenés que ver:** en `contenidos/entregas/[AAAA-MM]/[tu-marca]/` el `plantilla.pdf` (qué grabar y hasta cuándo, el detalle y el calendario) y `calendario.csv`.

> **Tip:** "Esto vale para adelante: nunca usamos la palabra barato". Lo guarda en la ficha y no lo repite.

## Paso 6 · Ejercicio 2: placas y carrusel

```prompt
Haceme un carrusel de 5 placas para [NOMBRE-DE-TU-MARCA] sobre [TEMA, ej. 4 ERRORES AL ARMAR LA VALIJA]. Formato 4:5. Imagen: Claude (gratis). Método: desde cero.
```

O las del plan: "Hacé las imágenes del plan de [MES]".

Primero te muestra los textos y la idea visual (**freno**): aprobá o corregí. Después arma las placas y las revisa. Pedí cambios ("titular más grande", "otro fondo"); cada uno sale como v2, v3. Para historia: "Pasala a historia 9:16".

**Tenés que ver:** los PNG en `contenidos/entregas/[AAAA-MM]/[tu-marca]/imagenes/[CÓDIGO]/` y una hoja de contacto con todas juntas.

> **Tip:** con Higgsfield conectado, elegí "Imagen: Higgsfield (pago)" para una escena fotorrealista. ¿Viste una placa que te gusta? Adjuntala: "Copiá el estilo de esta imagen con mi marca".

## Paso 7 · Ejercicio 3: video para redes
La skill **no genera video con IA**: arma el guion, vos grabás y ella edita (cortes, subtítulos con tu marca, tomas de apoyo, cierre con logo y portada). Video 100% IA: [Herramientas creativas](#s12-creativas).

```prompt
Armame un reel para esta semana de [NOMBRE-DE-TU-MARCA] sobre [TEMA]. Lo graba [QUIÉN]. Duración 20 a 30 segundos.
```

(Si nadie quiere aparecer: "Quiero un reel sin hablar ni mostrar la cara".)

Aprobá el guion. Grabá con el celular: vertical y apoyado, luz de frente, **cada frase en una toma** (si te trabás, repetí la frase entera), 2 o 3 tomas sin hablar (manos, producto, lugar) y pasá los **originales** (sin filtros ni reenviar por WhatsApp). Pasalos a la compu (AirDrop, cable o Google Drive) y:

```prompt
Ya grabé, los videos están en [CARPETA, ej. Descargas/reel-diciembre]. Editalo.
```

Te muestra el **storyboard** y te pregunta estilo, tomas de apoyo y música. Aprobá y pedí cambios: "en el segundo 5 que se vea el producto".

**Tenés que ver:** el video en `contenidos/entregas/[AAAA-MM]/[tu-marca]/videos/[CÓDIGO]/entrega/`, con portada y subtítulos `.srt`. Miralo y escuchalo antes de publicar: Claude no escucha el audio.

> **Ojo:** la primera edición tarda más (pasa la voz a texto). La música sumala al publicar, desde Instagram o TikTok.

## Cómo sé que funcionó

```prompt
Mostrame qué hay en contenidos/entregas/ de este mes: cuántas piezas del plan están aprobadas, cuáles tienen imágenes o video y qué quedó como [COMPLETAR].
```

**Tenés que ver:** el PDF del mes, un carrusel en PNG y un reel editado, con su estado.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude no encuentra las skills | Cerrá y abrí la app de Claude. Si sigue, corré el instalador de nuevo. |
| Mac: "desarrollador no identificado" | Clic derecho › **Abrir** › **Abrir**, o **Privacidad y seguridad › Abrir igualmente**. |
| Mac: "no tenés permisos" al abrir el instalador | Este paso es **en la terminal, una sola vez**: abrí **Terminal**, escribí `bash ` (con espacio), arrastrá `INSTALAR-Mac.command` a la ventana y Enter. |
| Windows: el instalador se cierra enseguida | Fijate que hayas extraído el ZIP. Clic derecho en el `.bat` › **Ejecutar como administrador**. |
| "No encuentro ffmpeg" o "uv" | Cerrá y abrí la app de Claude. |
| El PDF no se genera | Pedí "Verificá la instalación". Hace falta Chrome o Edge. |
| Las piezas salen genéricas | Sumá 2 o 3 textos reales tuyos a `marca/` y pedí que actualice el Cerebro de la marca. |
| El logo sale con recuadro blanco | Pasalo en PNG sin fondo. |

## Para seguir solo
- Cada mes: "Armame el plan de contenidos de [MES]". O como [tarea programada](#t4-tareas-programadas) el primer lunes del mes.
- Varias marcas o líneas: una ficha por marca en `contenidos/marcas/`.
- Programá lo aprobado en Metricool ([Herramientas creativas](#s12-creativas)) y contale a Claude qué funcionó: "Esto vale para adelante: …".

## Plan B: las skills de la agencia
Si la fábrica no se instala, o querés ir más allá, estas son skills que usamos en la agencia, limpias para el taller (sin datos de clientes). Se instalan solas.

| Skill | Para qué sirve | Necesita |
|---|---|---|
| [creador-angulos-publicitarios](kit/plan-b/creador-angulos-publicitarios.zip) | Arma con vos un **ángulo de venta**: a quién, qué dolor, qué promesa. | Nada |
| [nomenclador-ads](kit/plan-b/nomenclador-ads.zip) | Le pone **nombre ordenado** a cada anuncio para saber cuál rinde y por qué. | Nada |
| [rediseno-9x16](kit/plan-b/rediseno-9x16.zip) | Pasa una placa cuadrada a **historia o reel vertical**, sin estirarla. | Nada |
| [static-remix](kit/plan-b/static-remix.zip) | Recrea **anuncios ganadores de la competencia** con tu producto y tu marca. | Higgsfield conectado (pago; muestra el costo y pide OK antes de generar) y Python con PyMuPDF |
| [estrategia-benchmark](kit/plan-b/estrategia-benchmark.zip) | Analiza anuncios de tu competencia en la Biblioteca de anuncios de Meta y arma una **presentación de estrategia**. | Navegador; mejor con el conector de Meta ([Meta y Google](#s14-meta-y-google)) |
| [product-bible](kit/plan-b/product-bible.zip) | Una **carpeta por producto** con ficha, colores, mensajes e imágenes. | Python con Pillow (Claude lo instala si se lo pedís) |
| [frontend-design](kit/plan-b/frontend-design.zip) | Para que una **web** no parezca de plantilla. De Anthropic (Apache 2.0). | Nada |
| [animaciones](kit/plan-b/animaciones.zip) | 20 estilos de **animación en código** para un video corto sin grabar. | Node.js. Usa Remotion: gratis hasta 3 personas ([Stack y costos](#r-stack-y-costos)) |

### Cómo instalar una skill del Plan B
1. Descargá el ZIP de la tabla.
2. En la pestaña **Code** (cualquier carpeta), pegá:

```prompt
Instalá la skill del archivo [NOMBRE-DE-LA-SKILL].zip que está en mi carpeta Descargas, en la carpeta de skills de mi usuario (.claude/skills/ dentro de mi carpeta de usuario). Si ya está descomprimido, usá la carpeta. Si la skill necesita instalar algo para funcionar, decime qué y esperá mi OK.
```

**Tenés que ver:** la skill al escribir `/`, por ejemplo `/creador-angulos-publicitarios`. Si no aparece, abrí una sesión nueva.

> **Tip:** para usarla también en el chat de Claude: **Settings › Capabilities** › activá **Code execution and file creation**, y en **Customize › Skills** subí el ZIP tal cual. Más en el [Kit del taller](#r-kit).
