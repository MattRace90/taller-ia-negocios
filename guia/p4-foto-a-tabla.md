---
titulo: "De foto o PDF a planilla, con revisión humana"
bloque: Tutorial
tiempo: 45 a 60 min
para: Celve, Denvet, Fondus (sirve para cualquiera que cargue datos a mano)
necesitas: s2-claude-code
resultado: Una carpeta que convierte fotos y PDF en una planilla limpia, con lo dudoso separado para que una persona lo apruebe.
---

Es la versión completa del [D1](#d1-automatiza): hoy hacé primero la MVP (3 fotos en un chat); esto es para si te sobra tiempo. Acá procesás una **carpeta entera** con la skill `extraer-a-tabla`: cartas a platos con su marca "sin TACC" (Celve), remitos a filas de venta (Denvet), solicitudes a campos del sistema (Fondus). La regla: **la IA propone, una persona aprueba**.

## Antes de empezar
- [ ] La app de escritorio de Claude con la pestaña **Code** ([S2 · Claude Code en la pestaña Code](#s2-claude-code)).
- [ ] Una cuenta de Google (para Google Sheets).
- [ ] De 2 a 5 documentos de prueba: fotos (JPG o PNG) o PDF. Si no trajiste, sacale una foto a un ticket o hacé una captura de la carta de un local en Instagram (es pública).

> **Datos:** usá documentos sin datos personales. Una carta o un remito comercial, sí. Una solicitud con DNI, ingresos o salud, **no**: completá un formulario en blanco con datos inventados.

## Paso 1 · Armá la carpeta y abrila en Code
1. En **Documentos**, creá la carpeta `foto-a-tabla` y, adentro, `entrada` y `salida`. Copiá tus documentos en `entrada`.
2. En la app de Claude: **Code** › **Local** › **Open folder…** › `foto-a-tabla`.

**Tenés que ver:** el cuadro de mensaje de Code con `foto-a-tabla` como carpeta.

<div data-os="mac">

> **Ojo:** las fotos de iPhone suelen ser `.HEIC`. Pedile a Claude: "Pasá a JPG las fotos .HEIC de entrada/", o configurá el iPhone en **Ajustes › Cámara › Formatos › Más compatible**.

</div>

## Paso 2 · Instalá la skill "extraer-a-tabla"
En el [Kit del taller](#r-kit), tocá **Copiar** en la skill `extraer-a-tabla` y pegala debajo de este pedido:

```prompt
Creá una skill personal llamada extraer-a-tabla con el texto que pego abajo, exacto y sin cambios, en la carpeta de skills de mi usuario (~/.claude/skills/extraer-a-tabla/SKILL.md). Decime dónde quedó.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

Aprobá el permiso. Si al escribir `/` no aparece, abrí una sesión nueva en la misma carpeta.

**Tenés que ver:** `extraer-a-tabla` al escribir `/`.

> **Ojo:** el nombre de los botones puede variar según la versión de la app.

## Paso 3 · Definí las columnas con un ejemplo
La IA copia mejor un ejemplo que una explicación (ejemplos inventados):

| Negocio | Una fila por… | Columnas | Campos críticos |
|---|---|---|---|
| Gastronomía | plato | categoria, nombre, precio, sin_tacc, vegetariano, vegano | sin_tacc, vegano |
| Producción y reparto | renglón del remito | numero_remito, fecha, cliente, producto, cantidad, total_renglon, total_remito | cantidades y totales |
| Venta consultiva | solicitud | los campos de tu sistema, con el mismo nombre | los obligatorios |

```prompt
/extraer-a-tabla
Los documentos de entrada/ son [QUÉ SON]. Quiero una fila por [QUÉ].
Columnas, con una fila de ejemplo: [COLUMNAS Y UNA FILA].
Campos críticos (ante la mínima duda, a revisión): [CAMPOS].
Regla extra: [EJ: ANTE LA DUDA, NO SE MARCA APTO].
```

Claude suma columnas de control (`archivo`, `confianza`, `a_revisar`, `motivo`, `revisado_por`) y te pide el OK antes de leer todo.

**Tenés que ver:** un archivo `columnas.md` con la definición de cada columna.

## Paso 4 · Extraé y mirá el reporte
Contestá **"sí, extraé"**. Claude escribe en `salida/`:
- `tabla.csv`: todas las filas, con su confianza (un **CSV** es una planilla guardada como texto).
- `a-revisar.csv`: solo lo que necesita un humano: confianza baja, todo lo de salud o plata, lo ilegible (`[ILEGIBLE]`, nunca adivinado) y lo que no cierra (renglones que no suman el total).
- `reporte.md`: cuántos archivos, cuántas filas y por qué mandó cada una a revisión.

> **Ojo:** en salud, **ante la duda, no se marca apto**. Un alfajor de maicena sin la leyenda "sin TACC" queda **no apto**, con confianza baja y a revisión.

**Tenés que ver:** los tres archivos y, en el chat, el resumen con los conteos.

## Paso 5 · Revisá en Google Sheets
1. Abrí [sheets.new](https://sheets.new) › **Archivo › Importar › Subir** › `salida/tabla.csv` › reemplazar la hoja › **Importar datos**.
2. Filtrá `a_revisar` por "sí". Compará cada fila con el documento original, corregí y poné tus iniciales en `revisado_por`.

> **Tip:** si conectaste Google Drive en Claude ([Conectores](#s8-conectores-y-mcp)), pedile: "Creá una planilla de Google con salida/tabla.csv".

**Tenés que ver:** todas las filas a revisar con iniciales.

## Cómo sé que funcionó
Poné un documento nuevo en `entrada/` y pedí:

```prompt
/extraer-a-tabla Procesá solo los archivos nuevos de entrada/ con las columnas de columnas.md. Sumalos a salida/ y mostrame el reporte.
```

Funciona si no te pregunta las columnas de nuevo, nada ilegible aparece completado y cada fila a revisar tiene un motivo que entendés.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No puede leer una imagen | Pasala a JPG o PNG. Si está borrosa, sacala de nuevo, de frente y con luz. |
| Con un PDF largo se corta | "Procesá de a un archivo y guardá después de cada uno". |
| Inventó un precio o una marca | "No completes nada que no se lea: [ILEGIBLE] y a revisión." Sumalo a `columnas.md`. |
| Manda todo a revisión | Revisá qué marcaste como crítico. |
| En Sheets todo queda en una columna | Al importar, separador **Coma**. |

## Para seguir solo
- **Medí el ahorro:** cronometrá 10 remitos a mano y con la skill (contando la revisión).
- **Cargarlo a Supabase:** exportá la planilla revisada como CSV, pedile a Claude "armá para-cargar.csv con las filas revisadas y las columnas de mi tabla [NOMBRE]" y subilo vos en Supabase, **Table Editor › Insert › Import data from CSV**. Nunca le pases a Claude la clave service role.
- **Que corra solo:** un flujo de [n8n](#s6-n8n) que tome las fotos de una carpeta de Drive y te avise por [Telegram](#s7-telegram) cuando hay filas para revisar.
