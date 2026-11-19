---
titulo: Tu editor de video y dónde conviene trabajar
bloque: Tutorial
tiempo: 60 a 75 min (más las descargas, si no las hiciste antes)
para: Manuel Martínez Oratoria, La Consejera del Éxito (y cualquiera que grabe videos)
necesitas: p1-cerebro, s2-claude-code, s3-herramientas-base
resultado: Tu propio editor de video que corta silencios, subtitula y agrega tu placa final; un script que manda cada video de alumno a su carpeta de Drive; y claro cuándo usar el chat, Cowork, Claude Code o Claude Code en la web.
---

Grabar no es el problema. Lo que cansa es lo que viene después: cortar los silencios, poner subtítulos, la placa final, renombrar 20 archivos y subirlos a la carpeta de cada uno.
Hoy armás un editor de video propio, de cero, que hace eso solo con tu marca. Y resolvemos un cuello de botella típico de las escuelas: que cada video de alumno llegue a su carpeta sin tocarlo a mano.

> **Ojo:** este editor **trabaja sobre video que ya grabaste**: corta, subtitula y le pone tu placa. No inventa un video desde cero. Para video generado 100% con IA (escenas, o un presentador virtual que habla por vos) se usan Higgsfield o HeyGen: mirá [Herramientas creativas](#s12-creativas).

## Antes de empezar
- [ ] Claude Code instalado y saber abrir la terminal: en Mac, **Terminal**; en Windows, **PowerShell** ([Instalá Claude Code](#s2-claude-code), Paso 1).
- [ ] Node y ffmpeg instalados ([Herramientas base](#s3-herramientas-base)). Probalo: `node --version` y `ffmpeg -version` tienen que responder.
- [ ] Tu cerebro con `marca/identidad-visual.md` (colores en hex, tipografía, logo) ([Tu cerebro](#p1-cerebro)).
- [ ] Un video **tuyo** hablando a cámara, de 30 a 90 segundos, grabado con el celular. Que tenga pausas: así se nota el corte de silencios.
- [ ] Parte 2: Google Drive para escritorio instalado y con tu sesión iniciada.
- [ ] Unos 3 GB libres en el disco (el editor y el modelo de transcripción).

> **Datos:** todo lo de este tutorial corre **en tu compu**: el video y la transcripción no se suben a ninguna IA en la nube. Igual, para practicar usá un video tuyo, no de un cliente o alumno.

## Parte 1 · Tu editor de video con Remotion (30 min)
Remotion es una herramienta para hacer videos con código. Vos no escribís el código: lo escribe Claude Code, y vos le pedís cambios en castellano.

## Paso 1 · Creá el proyecto del editor
Abrí la terminal y escribí estas dos líneas (la segunda descarga Remotion y tarda un par de minutos):

> **Ojo:** Remotion y, más adelante, el modelo de transcripción bajan bastante (cientos de MB). Si el wifi está lento, hacé estos dos pasos en el almuerzo o con los datos del celular, y mientras tanto mirá la Parte 3. En Windows: si `npx` o `npm` salen en rojo con "running scripts is disabled", escribí `npx.cmd` y `npm.cmd`; si `cd $HOME\Documents` da error de ruta (pasa con OneDrive), usá el truco de arrastrar la carpeta de [Tu cerebro](#p1-cerebro), Paso 1.

<div data-os="mac">

```bash
cd ~/Documents
npx create-video@latest
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents
npx create-video@latest
```

</div>

El asistente te hace preguntas en la terminal. Te movés con las flechas y confirmás con Enter. Respondé así:
1. Nombre de la carpeta: `editor-video`.
2. Plantilla: **Blank** (en blanco).
3. Si pregunta por **Agent Skills** (instrucciones para que Claude Code sepa usar Remotion): **sí**.
4. Si pregunta por gestor de paquetes: **npm**.

Después entrá a la carpeta y abrí la vista previa:

<div data-os="mac">

```bash
cd editor-video
npm install
npm run dev
```

</div>
<div data-os="win">

```powershell
cd editor-video
npm install
npm run dev
```

</div>

**Tenés que ver:** el **Remotion Studio** abierto en el navegador, con una composición vacía. Dejá esa terminal abierta.

> **Costo:** Remotion es gratis para personas y para empresas de **hasta 3 personas**, incluso para uso comercial. Si tu empresa tiene más gente, necesitás una licencia de empresa. Ver [Stack y costos](#r-stack-y-costos).

## Paso 2 · Instalá la skill editar-video y abrí Claude Code
1. Abrí **otra** terminal y entrá a la carpeta del editor:

<div data-os="mac">

```bash
cd ~/Documents/editor-video
claude
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\editor-video
claude
```

</div>

2. Instalá la skill `editar-video`: en el [Kit del taller](#r-kit) (abrilo en otra pestaña) tocá **Copiar** en `editar-video` y pegala debajo de este prompt:

```prompt
Creá una skill personal llamada editar-video. Guardá el texto que pego abajo, exacto y sin cambios, en el archivo SKILL.md de la carpeta de skills de mi usuario (~/.claude/skills/editar-video/SKILL.md; en Windows es C:\Users\[MI-USUARIO]\.claude\skills\editar-video\SKILL.md). Cuando termines, decime la ruta exacta donde quedó.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

3. Salí con `/exit` y volvé a entrar con `claude`.
4. Contale dónde está tu cerebro, una sola vez. Cambiá `[RUTA-DE-TU-CARPETA-CEREBRO]` por la ruta de tu carpeta: en Mac, `~/Documents/cerebro-[TU-EMPRESA]`; en Windows, `C:\Users\[MI-USUARIO]\Documents\cerebro-[TU-EMPRESA]`. También podés arrastrar la carpeta a la ventana y se pega sola.

```prompt
Mi cerebro está en [RUTA-DE-TU-CARPETA-CEREBRO]. Guardá esa ruta en el CLAUDE.md de este proyecto, para que la skill editar-video sepa dónde leer marca/identidad-visual.md.
```

**Tenés que ver:** `editar-video` aparece al escribir `/`.

## Paso 3 · Editá tu primer video
En Claude Code escribí `/editar-video ` (con un espacio al final). Después arrastrá tu video desde Finder o el Explorador a la ventana: se pega su ruta. Abajo, escribí la línea de la placa final, cambiando lo que está entre corchetes por tu frase y tu usuario o web. Queda así:

```prompt
/editar-video [ARRASTRÁ-ACÁ-TU-VIDEO]
Placa final: "[TU-LLAMADO-A-LA-ACCIÓN]" y [TU-USUARIO-O-WEB].
```

Claude va a:
1. Copiar el video (nunca toca el original).
2. Mostrarte cuántos silencios va a cortar y cuántos segundos ahorra. Respondé **"dale"**.
3. Instalar Whisper (el programa que transcribe) y el modelo en español. La primera vez tarda unos minutos.
4. Mostrarte las palabras dudosas de los subtítulos para que las corrijas.
5. Armar la composición en el Studio para que la mires.
6. Renderizar (generar el archivo de video final) en `salida/`.

**Tenés que ver:** en el Studio, tu video vertical con subtítulos y la placa con tus colores al final. Después, el archivo `salida/[nombre]-final.mp4`.

> **Tip:** pedí cambios como se los pedirías a un editor: "Subtítulos más grandes", "Resaltá en amarillo la palabra que digo", "La placa final 2 segundos más". Cuando te guste el estilo: "Guardá este estilo como el default".

> **Tip:** si das clases o hacés vivos, el mismo editor sirve para cortar clips de lo que ya grabaste. Pedí: "De este video de 40 minutos, proponeme los 3 mejores fragmentos de 30 a 60 segundos para reels, con el minuto exacto y por qué".

## Parte 2 · Cada video de alumno a su carpeta (20 min)
El caso de una escuela de oratoria: después de cada encuentro hay un video por alumno, y alguien los renombra y los sube uno por uno a la carpeta de cada alumno. La idea:

1. **Al empezar cada grabación, el docente dice el nombre del alumno en voz alta.** "Juan Pérez, encuentro 3."
2. Los videos del día se copian a una carpeta de entrada.
3. Un script (un programita que hace una tarea fija) transcribe **solo los primeros segundos** de cada video, encuentra el nombre, lo renombra (`2026-11-19_Juan-Perez_encuentro-3.mp4`) y lo copia a la carpeta del alumno.
4. Las carpetas de alumnos están en **Google Drive para escritorio**, que sincroniza solo. Por eso no hace falta conectarse a la API de Drive: el script copia a una carpeta de tu compu y Drive lo sube.

> **Datos:** el video de un alumno es un dato personal. Antes de procesarlo hace falta su **consentimiento por escrito** (por ejemplo, una línea en la inscripción: "Autorizo que se grabe mi exposición y se guarde en mi carpeta privada"). Las carpetas se comparten solo con cada alumno. La transcripción se hace en la compu, no en la nube.

## Paso 4 · Encontrá la ruta de tu Drive
<div data-os="mac">

1. Abrí **Finder**. En la barra lateral, en **Ubicaciones**, está **Google Drive**.
2. Entrá a la carpeta donde están (o van a estar) las carpetas de los alumnos.
3. Arrastrá esa carpeta a la Terminal: se pega la ruta. Va a ser parecida a `/Users/[TU-USUARIO]/Library/CloudStorage/GoogleDrive-[TU-EMAIL]/Mi unidad/Alumnos`.

</div>
<div data-os="win">

1. Abrí el **Explorador de archivos**. Google Drive aparece como una unidad, normalmente **G:**.
2. Entrá a la carpeta donde están (o van a estar) las carpetas de los alumnos.
3. Hacé clic en la barra de direcciones y copiá la ruta. Va a ser parecida a `G:\Mi unidad\Alumnos`.

</div>

**Tenés que ver:** la ruta copiada. Guardala, la usás en el paso siguiente.

## Paso 5 · Que Claude Code arme el script
En Claude Code, dentro de `editor-video` (ya tiene Whisper instalado de la Parte 1):

```prompt
Armá un script para ordenar los videos de mis alumnos. Escribilo en la carpeta alumnos/ de este proyecto.

Cómo funciona:
1. Lee los videos (.mp4 y .mov) de la carpeta alumnos/entrada/.
2. De cada video, extrae con ffmpeg los primeros 12 segundos de audio y los transcribe en español con el Whisper.cpp que ya instalamos (modelo multilingüe, idioma es).
3. Busca en la transcripción el nombre de un alumno de la lista alumnos/lista.csv (columnas: nombre, apellido, carpeta). La coincidencia tiene que tolerar errores chicos de transcripción y tildes. Si dice "encuentro" y un número, lo toma.
4. Si encuentra al alumno con seguridad: copia el video a [RUTA-DE-TU-DRIVE]/[carpeta del alumno]/ con el nombre AAAA-MM-DD_Nombre-Apellido_encuentro-N.mp4 (la fecha es la de grabación del archivo).
5. Si no lo encuentra o hay duda entre dos alumnos: lo copia a alumnos/revisar/ y no lo manda a ningún lado.
6. COPIA, no mueve: el original queda en entrada/ hasta que yo lo borre.
7. Deja un registro en alumnos/registro.csv: archivo original, lo que transcribió, alumno elegido, confianza, destino.
8. Tiene un modo prueba (--prueba) que muestra qué haría sin copiar nada.

Creá alumnos/lista.csv con 3 alumnos INVENTADOS de ejemplo y las carpetas de entrada y revisar. Explicame en 5 líneas cómo lo corro.
```

**Tenés que ver:** la carpeta `alumnos/` con el script, `lista.csv` de ejemplo y las instrucciones para correrlo.

## Paso 6 · Probalo con videos tuyos
1. Grabá 2 videos cortos con el celular. Al empezar decí: "[NOMBRE-INVENTADO-DE-LA-LISTA], encuentro 1". Pasalos a `alumnos/entrada/`.
2. Pedile a Claude:

```prompt
Corré el script de alumnos en modo prueba y mostrame qué haría con cada video.
```

3. Si está bien: "Correlo de verdad".

**Tenés que ver:** los videos renombrados en las carpetas de Drive y, a los pocos minutos, sincronizados en [drive.google.com](https://drive.google.com). El registro en `alumnos/registro.csv`.

> **Tip:** para usarlo de verdad, reemplazá `lista.csv` por la lista real de alumnos y el link de carpeta de cada uno. Esa lista queda en tu compu: no la subas a GitHub (pedile a Claude que la agregue al `.gitignore`).

## Parte 3 · Dónde conviene trabajar (10 min)
Claude tiene cuatro lugares de trabajo. No compiten: cada uno sirve para algo. Para verlo, el **mismo problema resuelto de las cuatro formas**: "tengo 20 videos del encuentro y quiero cada uno renombrado y en la carpeta de su alumno".

| Dónde | Qué es | Cómo resuelve el ejemplo | Usalo para |
|---|---|---|---|
| **Claude (web o app)**: chat y **Proyectos** | Conversás. No toca tus archivos. Los Proyectos guardan conocimiento fijo para todos los chats. | Te ayuda a definir la convención de nombres y te arma la lista de pasos. Vos hacés el trabajo. | Pensar, escribir, analizar un documento que subís. Desde el celular. |
| **Cowork** (app de escritorio) | Un agente que lee y escribe archivos de una carpeta de tu compu. Sin código. | Le das la carpeta y le pedís: "renombrá estos videos según esta lista y movelos a estas carpetas". Lo hace una vez, mirando nombres y fechas. No puede escuchar el nombre dicho en el video. | Ordenar, renombrar y clasificar archivos; armar documentos, planillas y presentaciones con lo que tenés en la compu. |
| **Claude Code local** (terminal o pestaña **Code**) | Trabaja en tu compu con tus archivos **y tus programas** (ffmpeg, Whisper, Node). | Escribe el script de la Parte 2: escucha los primeros segundos, renombra y copia. Queda para siempre y se repite con un comando. | Instalar cosas, automatizar algo que se repite, armar apps, webs y editores. |
| **Claude Code en la web** (claude.ai/code) | Corre en la nube sobre un repositorio de GitHub. Funciona desde el celular. | Si el script está en GitHub, desde el celular le pedís: "que también acepte archivos .m4v". Hace el cambio y lo deja en el repo; en la compu lo bajás con GitHub Desktop. No ve los videos de tu compu. | Cambios en código o en tu web cuando no estás en la compu. |

**Demo corta (la hace Mati):** el mismo pedido en Cowork con una carpeta de archivos de prueba, y el mismo cambio en Claude Code en la web desde el celular.

> **Tip:** regla rápida. ¿Solo pensar o escribir? Chat. ¿Ordenar archivos una vez? Cowork. ¿Algo que se repite o que necesita programas? Claude Code. ¿Lejos de la compu y el proyecto está en GitHub? Claude Code en la web.

## Cómo sé que funcionó
- Tenés `salida/[nombre]-final.mp4`: vertical, sin silencios, con subtítulos y tu placa final.
- En tu Drive, el video de prueba quedó en la carpeta del alumno inventado, con el nombre correcto.
- Prueba final, en Claude Code dentro de `editor-video`:

```prompt
Editá este otro video con el mismo estilo de siempre y sin preguntarme nada salvo las palabras dudosas: [ARRASTRÁ-ACÁ-OTRO-VIDEO]
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `npx` o `node` no se reconoce | Node no está instalado o abriste la terminal antes de instalarlo. Cerrala, abrila de nuevo y revisá [Herramientas base](#s3-herramientas-base). |
| `ffmpeg` no se reconoce | Mismo caso: instalalo desde [Herramientas base](#s3-herramientas-base) y abrí una terminal nueva. |
| Whisper no se instala en Mac (error de `make` o de compilador) | Corré `xcode-select --install`, aceptá, esperá que termine y pedile a Claude que reintente. |
| Whisper no se instala en Windows | Pedile a Claude: "Usá @remotion/whisper-webgpu para transcribir en el navegador". |
| Los subtítulos salen en inglés | El modelo termina en `.en`. Pedí: "Usá el modelo small multilingüe con idioma es". |
| El script manda todo a `revisar/` | Revisá que el nombre se diga claro al principio y que esté igual en `lista.csv`. Mirá en `registro.csv` qué transcribió. |
| Drive no sube los archivos | Fijate que Google Drive para escritorio esté abierto y con tu sesión. Los archivos grandes tardan. |

## Para seguir solo
- **Plantillas por formato:** pedile al editor un estilo para reels, otro para historias y otro horizontal para YouTube, y guardalos con nombre.
- **El resumen del encuentro:** con la misma transcripción, Claude puede escribir el resumen para el grupo y un borrador de feedback para cada alumno, que el docente revisa antes de enviar.
- **Automático al terminar el encuentro:** programá el script para que corra solo cada día de encuentro a la noche (pestaña **Code › Scheduled** de la app de escritorio, con la compu prendida).

## Fuentes
- Remotion, crear un proyecto (`npx create-video@latest`): https://www.remotion.dev/docs/cli/create-video
- Remotion, uso con Claude Code (plantilla Blank, Agent Skills, `npm run dev`): https://www.remotion.dev/docs/ai/claude-code
- Remotion, transcribir audio (opciones oficiales: Whisper.cpp local, WebGPU, OpenAI, ElevenLabs): https://www.remotion.dev/docs/captions/transcribing
- Remotion, `@remotion/install-whisper-cpp` y `transcribe()` (WAV 16 kHz, `language`, modelos): https://www.remotion.dev/docs/install-whisper-cpp/ · https://www.remotion.dev/docs/install-whisper-cpp/transcribe
- Remotion, render por línea de comando: https://www.remotion.dev/docs/cli/render
- Remotion, licencia (gratis hasta 3 personas): https://www.remotion.dev/docs/license/pricing
- Google, Drive para escritorio en Mac (CloudStorage) y Windows (unidad G:): https://support.google.com/drive/answer/12178485 · https://support.google.com/a/answer/7644837
- Dónde trabajar y tareas programadas: `investigacion/claude-code-datos.md`.
- Verificado el 18/11/2026.
