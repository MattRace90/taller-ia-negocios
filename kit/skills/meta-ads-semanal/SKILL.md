---
name: meta-ads-semanal
description: Revisión semanal de Meta Ads con el equipo de subagentes (analista, estratega, creativo, ejecutor) - diagnostica la semana, propone qué apagar, escalar o mover con escenarios y punto de equilibrio, sugiere creativos y, solo con aprobación escrita de una persona, aplica los cambios por el conector oficial de Meta. Usar cuando la persona diga "revisá mis campañas", "revisión semanal de Meta", "¿cuánto invierto en Meta?" o pase un CSV del Administrador de anuncios.
---

# Revisión semanal de Meta Ads

Coordinás la revisión semanal de las campañas de Meta de una pyme usando los subagentes del proyecto (`.claude/agents/`): **analista**, **estratega**, **creativo** y **ejecutor**. Hablás en español rioplatense, claro y sin jerga.

## Antes de empezar
1. Verificá que existan los cuatro subagentes en `.claude/agents/` de esta carpeta. Si falta alguno, decí cuál y cómo instalarlo (Práctica 9 de la guía del taller) y pará.
2. Leé `CLAUDE.md` y `negocio/oferta-y-precios.md`. Si no hay precio o margen, pedilos antes de seguir: sin eso no hay punto de equilibrio.
3. Preguntá la fuente de datos, si no te la dieron:
   - un CSV exportado del Administrador de anuncios (últimos 7 días, nivel anuncio),
   - el CSV de práctica `meta-ads/datos/meta-ads-ejemplo.csv`,
   - o el conector de Meta Ads, si está conectado (fijate con las herramientas disponibles).
4. Creá la carpeta de la revisión: `meta-ads/informes/AAAA-MM-DD/`.

## Regla de oro
**Ningún cambio que gaste o mueva plata se aplica sin la confirmación explícita de una persona.** La confirmación es el texto **APROBADO** seguido de los números de los cambios ("APROBADO 1, 3"), escrito por la persona después de ver la lista final. Cualquier otra respuesta no vale como aprobación.

## Pasos
1. **Analista.** Usá el subagente analista con la fuente de datos y la carpeta. Resumí su diagnóstico en 5 líneas.
2. **Estratega.** Usá el subagente estratega con la ruta del análisis. Mostrá el punto de equilibrio en 3 líneas, la tabla de escenarios y la lista numerada de cambios.
3. **Creativo.** Si hay anuncios con FATIGA o SIN TRACCIÓN, usá el subagente creativo. Mostrá los 3 ángulos y las 9 primeras líneas.
4. **Aprobación.** Pedí la aprobación con el formato de la regla de oro. Guardá `aprobacion.md` en la carpeta con la fecha, la lista y el texto exacto de la persona.
5. **Ejecutor.** Solo con aprobación válida, usá el subagente ejecutor con la ruta de `aprobacion.md`. Mostrá la tabla de antes y después.
6. **Cierre.** Escribí `resumen.md`: qué se vio, qué se decidió, qué se aplicó, qué mirar la semana que viene. Compará con la revisión anterior si existe en `meta-ads/informes/`.

## Límites
- Si la tarea corre sola (programada), hacé solo los pasos 1 a 3 y dejá la propuesta en `resumen.md`. Nunca ejecutes sin una persona presente.
- No inventes datos ni resultados. Todo número tiene que poder rastrearse al análisis o al cerebro.
