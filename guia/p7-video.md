---
titulo: Tu editor de video y dónde conviene trabajar
bloque: Tutorial
tiempo: 45 a 60 min (más las descargas, si no las hiciste antes)
para: Manuel Martínez Oratoria, La Consejera del Éxito (y cualquiera que grabe videos)
necesitas: p1-cerebro, s2-claude-code, s3-herramientas-base
resultado: Tu propio editor de video que corta silencios, subtitula y agrega tu placa final; un script que manda cada video de alumno a su carpeta de Drive; y claro cuándo usar el chat, Cowork, Claude Code o Claude Code en la web.
---

Grabar no es el problema. Lo que cansa es lo que viene después: cortar silencios, subtitular, la placa final, renombrar 20 archivos y subirlos a la carpeta de cada uno.
Hoy armás un editor de video propio que hace eso con tu marca, y un script para que cada video de alumno llegue solo a su carpeta. Todo pidiéndoselo a Claude en la pestaña **Code**.

> **Ojo:** este editor **trabaja sobre video que ya grabaste**. No inventa video desde cero. Para video 100% con IA: [Herramientas creativas](#s12-creativas).

## Antes de empezar
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).
- [ ] Node y ffmpeg instalados ([Herramientas base](#s3-herramientas-base)).
- [ ] Tu cerebro con `marca/identidad-visual.md` (colores, tipografía, logo) ([Tu cerebro](#p1-cerebro)).
- [ ] Un video **tuyo** hablando a cámara, de 30 a 90 segundos, con pausas.
- [ ] Parte 2: Google Drive para escritorio instalado y con tu sesión iniciada.
- [ ] Unos 3 GB libres en el disco.

> **Datos:** todo corre **en tu compu**: el video y la transcripción no se suben a la nube. Igual, practicá con un video tuyo, no de un cliente o alumno.

## Parte 1 · Tu editor de video con Remotion (30 min)
Remotion hace videos con código. El código lo escribe Claude; vos pedís cambios en castellano.

> **Ojo:** Remotion y el modelo de transcripción bajan cientos de MB. Si el wifi está lento, hacé la Parte 1 en el almuerzo y mientras tanto mirá la Parte 3.

## Paso 1 · Pedile a Claude que cree el editor
App de Claude › **Code** › selector de entorno **Local** › **Open folder…** › elegí **Documentos**. Pegá:

```prompt
Fijate si tengo Node y ffmpeg instalados. Si están, creá en esta carpeta un proyecto de Remotion llamado editor-video, con la plantilla Blank y las Agent Skills de Remotion (para que sepas usarlo). Instalá las dependencias y abrime el Remotion Studio en el navegador, dejándolo corriendo. Si falta algo, decime qué y esperá.
```

Aprobá los permisos que pide (**Permitir**). Tarda un par de minutos.

**Tenés que ver:** el **Remotion Studio** abierto en el navegador, con una composición vacía.

> **Costo:** Remotion es gratis para personas y empresas de **hasta 3 personas**, incluso uso comercial. Si son más, hace falta licencia. Ver [Stack y costos](#r-stack-y-costos).

## Paso 2 · Instalá la skill editar-video
1. Abrí una **sesión nueva** en la pestaña Code con **Open folder…** › `Documentos/editor-video`.
2. En el [Kit del taller](#r-kit) tocá **Copiar** en `editar-video` y pegala debajo de este prompt:

```prompt
Creá una skill personal llamada editar-video. Guardá el texto que pego abajo, exacto y sin cambios, en la carpeta de skills de mi usuario (.claude/skills/editar-video/SKILL.md dentro de mi carpeta de usuario). Después buscá mi carpeta cerebro-[TU-EMPRESA] en Documentos y guardá su ruta en el CLAUDE.md de este proyecto, para que la skill lea marca/identidad-visual.md. Decime las dos rutas.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

**Tenés que ver:** `editar-video` aparece al escribir `/`. Si no, abrí otra sesión nueva en la misma carpeta.

## Paso 3 · Editá tu primer video
Copiá tu video adentro de la carpeta `editor-video` (con Finder o el Explorador de archivos). Después escribí:

```prompt
/editar-video [NOMBRE-DE-TU-VIDEO.mp4]
Placa final: "[TU-LLAMADO-A-LA-ACCIÓN]" y [TU-USUARIO-O-WEB].
```

Claude copia el video (nunca toca el original), te dice cuántos silencios corta (respondé **"dale"**), instala Whisper (el programa que transcribe) la primera vez, te muestra las palabras dudosas para corregir y renderiza.

**Tenés que ver:** en el Studio, tu video vertical con subtítulos y tu placa al final. Después, `salida/[nombre]-final.mp4`.

> **Tip:** pedí cambios como a un editor: "Subtítulos más grandes", "Resaltá en amarillo la palabra que digo", "Guardá este estilo como el default". Y para clases largas: "De este video de 40 minutos, proponeme los 3 mejores fragmentos para reels, con el minuto exacto".

## Parte 2 · Cada video de alumno a su carpeta (20 min)
El caso de una escuela de oratoria: un video por alumno después de cada encuentro. La idea:
1. Al empezar cada grabación, el docente dice el nombre: "Juan Pérez, encuentro 3".
2. Un script (un programita con una tarea fija) transcribe **los primeros segundos**, encuentra el nombre, renombra el video y lo copia a la carpeta del alumno.
3. Las carpetas están en **Google Drive para escritorio**, que sincroniza solo. No hace falta conectarse a Drive.

> **Datos:** el video de un alumno es un dato personal. Hace falta su **consentimiento por escrito** (por ejemplo, en la inscripción). Las carpetas se comparten solo con cada alumno. La transcripción se hace en la compu.

## Paso 4 · Que Claude arme el script
En la sesión de `editor-video` (ya tiene Whisper de la Parte 1):

```prompt
Buscá en mi compu la carpeta de Google Drive para escritorio y, adentro, la carpeta [NOMBRE-DE-LA-CARPETA-DE-ALUMNOS]. Decime la ruta.
Después armá un script en la carpeta alumnos/ de este proyecto que:
1. Lea los videos (.mp4 y .mov) de alumnos/entrada/.
2. Transcriba en español los primeros 12 segundos de cada uno con el Whisper que ya instalamos.
3. Busque el nombre en alumnos/lista.csv (nombre, apellido, carpeta), tolerando errores chicos y tildes. Si dice "encuentro" y un número, lo toma.
4. Si está seguro: copie el video a la carpeta del alumno en Drive como AAAA-MM-DD_Nombre-Apellido_encuentro-N.mp4.
5. Si duda: lo copie a alumnos/revisar/.
6. COPIE, no mueva. Deje un registro en alumnos/registro.csv.
7. Tenga un modo prueba que muestre qué haría sin copiar nada.
Creá lista.csv con 3 alumnos INVENTADOS y las carpetas entrada y revisar.
```

**Tenés que ver:** la ruta de tu Drive y la carpeta `alumnos/` con el script y `lista.csv` de ejemplo.

## Paso 5 · Probalo con videos tuyos
1. Grabá 2 videos cortos diciendo al principio "[NOMBRE-INVENTADO-DE-LA-LISTA], encuentro 1" y copialos a `alumnos/entrada/`.
2. Pedí:

```prompt
Corré el script de alumnos en modo prueba y mostrame qué haría con cada video. Si está bien, correlo de verdad.
```

**Tenés que ver:** los videos renombrados en las carpetas de Drive y, a los pocos minutos, en [drive.google.com](https://drive.google.com).

> **Tip:** para usarlo de verdad, reemplazá `lista.csv` por la lista real. Esa lista queda en tu compu: pedile a Claude que la sume al `.gitignore` para que nunca vaya a GitHub.

## Parte 3 · Dónde conviene trabajar (10 min)
El mismo problema ("20 videos del encuentro, cada uno a la carpeta de su alumno") en los cuatro lugares:

| Dónde | Cómo lo resuelve |
|---|---|
| **Chat** (web o app) | Te ayuda a definir los nombres y los pasos. El trabajo lo hacés vos. |
| **Cowork** | Renombra y mueve los archivos de una carpeta, una vez. No escucha el nombre dicho en el video. |
| **Pestaña Code** (Claude Code en tu compu) | Escribe el script de la Parte 2, que usa tus programas y se repite siempre. |
| **Claude Code en la web** | Cambia el script desde el celular si está en GitHub. No ve los videos de tu compu. |

Más detalle: [Dónde trabajar](#t3-donde-trabajar).

## Cómo sé que funcionó
- Tenés `salida/[nombre]-final.mp4`: vertical, sin silencios, con subtítulos y tu placa.
- El video de prueba quedó en la carpeta del alumno inventado, con el nombre correcto.
- Prueba final, en la sesión de `editor-video`:

```prompt
Editá [NOMBRE-DE-OTRO-VIDEO.mp4] con el mismo estilo de siempre, sin preguntarme nada salvo las palabras dudosas.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude dice que no tiene Node o ffmpeg | Instalalos desde [Herramientas base](#s3-herramientas-base), cerrá la app de Claude y abrila de nuevo. |
| Whisper no se instala en Mac (error de compilador) | Pedí: "Instalá las herramientas de línea de comandos de Xcode". Aceptá la ventana que aparece y, al terminar, "reintentá". |
| Whisper no se instala en Windows | Pedí: "Usá @remotion/whisper-webgpu para transcribir en el navegador". |
| Los subtítulos salen en inglés | Pedí: "Usá el modelo small multilingüe con idioma es". |
| El script manda todo a `revisar/` | Que el nombre se diga claro al principio y esté igual en `lista.csv`. Mirá `registro.csv`. |
| Drive no sube los archivos | Google Drive para escritorio tiene que estar abierto y con tu sesión. |

## Para seguir solo
- **Plantillas por formato:** un estilo para reels, otro para historias y otro horizontal, guardados con nombre.
- **El resumen del encuentro:** con la misma transcripción, un resumen para el grupo y un borrador de feedback por alumno, que el docente revisa.
- **Automático:** programá el script para cada día de encuentro a la noche (**Code › Scheduled**, con la compu prendida). Ver [Tareas programadas](#t4-tareas-programadas).

## Fuentes
- Remotion con Claude Code (Blank, Agent Skills): https://www.remotion.dev/docs/ai/claude-code · crear proyecto: https://www.remotion.dev/docs/cli/create-video
- Remotion, transcribir (Whisper.cpp, WebGPU): https://www.remotion.dev/docs/captions/transcribing
- Remotion, licencia: https://www.remotion.dev/docs/license/pricing
- Google Drive para escritorio: https://support.google.com/drive/answer/12178485
- Claude Code en la app de escritorio: https://code.claude.com/docs/en/desktop
- Verificado el 18/11/2026.
