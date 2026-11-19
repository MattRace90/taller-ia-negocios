---
name: reporte-semanal
description: Arma un resumen semanal corto a partir de una planilla de Google (o un CSV) y el cerebro de la empresa — rentabilidad del mes, cómo vinieron los leads o "qué sigue esta semana" — y lo entrega por el canal configurado. La primera vez pregunta qué medir y guarda la configuración en operacion/reporte-semanal.md; después corre sin preguntar, ideal para una tarea programada de los lunes. Nunca inventa números ni modifica la planilla. Usar cuando digan "reporte semanal", "resumen del lunes", "cómo venimos", "rentabilidad del mes", "cómo vinieron los leads", "qué sigue esta semana" o desde una tarea programada.
---

# Reporte semanal

Armás un resumen que el dueño de una pyme lee en 2 minutos el lunes a la mañana. Español rioplatense, con voseo, oraciones cortas, sin jerga.
Vos leés, calculás y explicás. **No inventás números ni tocás la planilla.**

## Reglas
1. **Cada número sale de la planilla.** Si un dato falta, lo decís ("falta cargar la semana del 10/11") y no lo estimás. Si estimás algo porque te lo pidieron en la configuración, lo marcás "(estimado)".
2. **Las cuentas se hacen con código, no de cabeza.** Usá una herramienta de cálculo (un script corto) para sumas, promedios y porcentajes, y guardá cómo calculaste cada número clave.
3. **Solo lectura.** No modificás la planilla, ni las fórmulas, ni el formato.
4. **Totales, no personas.** Si la planilla trae nombres, teléfonos o mails de clientes, no los ponés en el reporte. Trabajás con totales por categoría, fuente o equipo.
5. **Corto.** El reporte entra en una pantalla de celular: menos de 20 líneas.
6. **Modo sin nadie mirando.** Si corrés desde una tarea programada o te dicen "sin preguntar", no hacés preguntas: si algo falla, lo decís en la primera línea del reporte y seguís con lo que se pueda.
7. **Sin commits.** No hacés commits ni cambiás archivos del repositorio, salvo `operacion/reporte-semanal.md` en la configuración inicial y los reportes en `reportes/` cuando corrés en la compu.

## Paso 1 · Configuración (solo la primera vez)
Si no existe `operacion/reporte-semanal.md` y hay alguien mirando, preguntá en una sola tanda (máximo 5 preguntas, con sugerencia):
1. **Qué reporte:** rentabilidad del mes, cómo vinieron los leads, qué sigue esta semana u otro.
2. **De dónde salen los datos:** nombre exacto de la planilla de Google (o ruta del CSV) y qué columnas usar.
3. **Qué números importan:** sugerí los de la plantilla que corresponda (abajo).
4. **Contra qué se compara:** semana anterior, mes anterior, un objetivo (cuál).
5. **Cómo se entrega:** solo en el chat o historial de la tarea, guardado en `reportes/` o por Gmail a un mail.

Guardá las respuestas en `operacion/reporte-semanal.md` con este formato: tipo de reporte, fuente, columnas, métricas con su fórmula en palabras, comparación, alertas (reglas tipo "si X baja más de Y%"), entrega. Mostralo y pedí el OK.
Si no existe la configuración y nadie está mirando: armá el mejor reporte posible con lo que encuentres y en la primera línea decí "Falta configurar: corré /reporte-semanal con alguien mirando".

## Paso 2 · Leer los datos
- Leé `operacion/reporte-semanal.md` y, si existen, `CLAUDE.md` y `objetivos/` (para "qué sigue" y para comparar contra objetivos).
- Abrí la planilla con el conector de Google Drive (las planillas llegan como CSV) o el archivo local.
- Chequeá antes de calcular: que estén las columnas esperadas, qué semanas o meses hay, celdas vacías, valores raros (negativos donde no van, un número 10 veces más grande que el resto). Anotá todo para la sección "Datos que faltan".
- Usá la fecha de hoy: "esta semana" es la semana anterior completa (lunes a domingo); "el mes" es el mes en curso hasta ayer, salvo que la configuración diga otra cosa.

## Paso 3 · Calcular
Usá las métricas de la configuración. Si no hay, usá la plantilla:

**Rentabilidad del mes** (ejemplo: una granja que vende maples)
- Ventas del mes y del mes anterior.
- Costos del mes por rubro (alimento, packaging, sanidad, otros) y total.
- Resultado = ventas − costos. Margen = resultado / ventas.
- Costo por unidad (por maple) = costos totales / unidades producidas.
- Producción vs. ventas: unidades producidas, vendidas y sin vender.
- Alerta si el costo por unidad sube o el margen baja contra el mes anterior.

**Cómo vinieron los leads** (ejemplo: una agencia que vende por anuncios)
- Leads de la semana, por fuente y por equipo.
- Embudo: leads → contactados → entrevistas → ventas, con el porcentaje de cada paso.
- Tiempo hasta el primer contacto (promedio y cuántos esperaron más de 24 h).
- Comparación con la semana anterior. Fuente que más ventas trajo y fuente que más leads trajo sin ventas.

**Qué sigue esta semana** (ejemplo: una startup con dos fundadores)
- Qué se terminó la semana pasada y qué quedó pendiente (de la planilla de tareas).
- Números de tracción de la semana (locales prospectados, respuestas, locales en prueba, publicaciones) contra el objetivo.
- **3 prioridades para esta semana por rol**, justificadas con un dato o con un objetivo de `objetivos/`. Nada de tareas nuevas que no salgan de los datos o los objetivos: si proponés algo nuevo, aclaralo como "sugerencia".

## Paso 4 · Escribir el reporte
Formato fijo:

```
Reporte semanal · [EMPRESA] · semana del [FECHA] al [FECHA]

Lo importante: [2 o 3 líneas en lenguaje simple: qué pasó y qué significa]

Números clave
- [Métrica]: [valor] ([+/− % contra el período anterior])
- … (de 3 a 6 líneas)

Alertas
- [Solo si alguna regla de la configuración se cumplió. Si no, "Sin alertas."]

Qué sigue
1. …
2. …
3. …

Datos que faltan
- [Semanas sin cargar, columnas vacías, valores raros. Si no falta nada, "Nada."]
```

- Números redondeados y con separador de miles argentino (`1.234.567`). Porcentajes sin decimales salvo que sean menores a 1%.
- Sin tablas largas ni jerga ("margen" sí, "EBITDA" no, salvo que la configuración lo use).

## Paso 5 · Entregar
Según la configuración:
- **Chat o historial:** mostralo y listo.
- **Archivo:** si corrés en la compu, guardalo en `reportes/AAAA-MM-DD.md` (esa carpeta tiene que estar en `.gitignore`; si no está, avisá). En la nube no guardes archivos.
- **Gmail:** mandalo con el asunto "Reporte semanal · [EMPRESA] · [FECHA]" al mail configurado. Si el envío necesita una aprobación que nadie va a dar, dejá el reporte en el historial y decí en la primera línea que el mail no salió.

## Cierre
Si hay alguien mirando, terminá con una línea: de dónde salieron los datos y cuándo es la próxima corrida (si sabés que es una tarea programada). Ofrecé ajustar métricas o alertas en `operacion/reporte-semanal.md`.
