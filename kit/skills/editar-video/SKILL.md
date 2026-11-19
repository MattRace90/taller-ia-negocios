---
name: editar-video
description: Edita un video hablado (persona a cámara) con el proyecto de Remotion de la carpeta actual - corta los silencios con ffmpeg, transcribe en español con Whisper local, agrega subtítulos y una placa final con la marca (lee marca/identidad-visual.md del cerebro) y renderiza en vertical 9:16. Usar cuando la persona diga "editá este video", "cortá los silencios", "subtitulá este video", "agregale la placa final" o pase un archivo .mp4 o .mov para editar.
---

# Editar video

Editás videos hablados cortos (reels, historias, clases cortadas) para una pyme. Hablás en español rioplatense, claro y sin jerga. La persona no es técnica: explicale lo que hacés en una línea por paso.

## Qué necesitás
- Estar parado en la carpeta de un proyecto de Remotion (tiene `package.json` con `remotion`). Si no lo estás, avisá y pedí que abran Claude Code en la carpeta del editor.
- `ffmpeg` instalado (`ffmpeg -version`). Si no está, avisá y no sigas.
- El video a editar. Si no te lo pasaron, preguntá la ruta.
- La identidad visual: buscá `marca/identidad-visual.md` en la carpeta del cerebro. Si no sabés dónde está el cerebro, preguntá la ruta una vez y guardala en el `CLAUDE.md` del proyecto del editor.

## Reglas
1. **Nunca tocás el original.** Copiás el video a `entrada/` y trabajás sobre la copia.
2. **Una pasada de prueba antes de renderizar todo:** mostrá qué cortes vas a hacer (cuántos, cuántos segundos se ahorran) antes de cortar.
3. **Subtítulos fieles:** no corregís lo que dijo la persona salvo errores de transcripción evidentes. Las palabras dudosas las listás para que la persona las revise.
4. **Marca:** colores, tipografía y logo salen de `marca/identidad-visual.md`. Si falta algo, usá blanco y negro y anotalo como pendiente. No inventes un logo.
5. **Datos:** todo se procesa en la compu. No subas el video ni la transcripción a ningún servicio externo sin preguntar.

## Paso 1 · Preparar
1. Copiá el video a `entrada/` con un nombre sin espacios.
2. Leé `marca/identidad-visual.md` y anotá: color principal (hex), color secundario, tipografía, ruta del logo, texto de la placa final (CTA y usuario o web). Si no hay CTA, preguntá cuál usar.
3. Mirá duración, resolución y orientación con `ffprobe`.

## Paso 2 · Cortar silencios
1. Detectá silencios con el filtro `silencedetect` de ffmpeg (punto de partida: `noise=-35dB`, `d=0.6`).
2. Dejá 0,15 s de aire antes y después de cada parte hablada para que no suene cortado.
3. Mostrá: cantidad de cortes, duración antes y después. Esperá un "dale".
4. Generá `trabajo/sin-silencios.mp4`. Si el audio queda cortado o hay saltos raros, ajustá el umbral (más negativo = corta menos) y repetí.

## Paso 3 · Transcribir y subtitular
1. Si el proyecto no tiene `@remotion/install-whisper-cpp`, instalalo con `npx remotion add @remotion/install-whisper-cpp`.
2. Instalá Whisper.cpp y un modelo **multilingüe** (no los `.en`): `small` para ir rápido, `medium` para más calidad. Idioma: `es`.
3. Convertí el audio a WAV de 16 kHz, 16 bits, mono con ffmpeg (es el formato que pide `transcribe()`).
4. Transcribí con marcas de tiempo por palabra y convertí el resultado a subtítulos con `toCaptions()`. Guardalos en `trabajo/subtitulos.json`.
5. Listá las palabras con baja confianza o nombres propios para que la persona las revise. Aplicá sus correcciones.

## Paso 4 · Componer en Remotion
Creá o actualizá una composición `VideoEditado`:
- 1080 × 1920 (9:16), 30 fps.
- El video sin silencios llenando la pantalla (recortado al centro si es horizontal).
- Subtítulos de 2 a 4 palabras por vez, grandes, en el tercio inferior, con la tipografía de la marca y la palabra que se está diciendo resaltada con el color principal. Siempre legibles (borde o fondo semitransparente).
- Placa final de 3 segundos: fondo con el color principal, logo, CTA y usuario o web.

Abrí la vista previa (`npm run dev`) y pedile a la persona que la mire antes de renderizar.

## Paso 5 · Renderizar
1. Renderizá con `npx remotion render VideoEditado salida/[nombre]-final.mp4` (H.264).
2. Decí dónde quedó, cuánto dura y cuánto pesa.
3. Proponé el texto del posteo en la voz de `marca/voz.md` si existe.

## Si algo falla
- Whisper no se instala en Mac: probablemente faltan las herramientas de desarrollo. Indicá correr `xcode-select --install` y reintentar.
- Whisper no se instala en Windows: ofrecé la alternativa `@remotion/whisper-webgpu` (corre en el navegador) y explicá la diferencia.
- La transcripción sale en inglés o rara: confirmá que el modelo no termine en `.en` y que el idioma sea `es`.
- El render es muy lento: renderizá primero 10 segundos de prueba con `--frames=0-299`.
