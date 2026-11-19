---
titulo: De foto o PDF a planilla, con revisión humana
bloque: Tutorial
tiempo: 45 a 60 min
para: Celve, Denvet, Fondus (sirve para cualquiera que cargue datos a mano)
necesitas: s2-claude-code
resultado: Una carpeta que convierte fotos y PDF en una planilla limpia, con lo dudoso separado para que una persona lo apruebe.
---

Cargar datos a mano es lento y se cuelan errores. Hoy vas a pasar documentos desordenados a una tabla: cartas de restaurantes a platos con su marca "sin TACC" (Celve), remitos a filas de venta (Denvet), solicitudes y anexos a los campos del sistema (Fondus).
La regla de oro: **la IA propone, una persona aprueba**. Claude marca qué tan seguro está de cada fila y separa lo dudoso. Nada se carga sin que alguien lo mire.

## Antes de empezar
- [ ] Claude Code instalado y con tu sesión iniciada ([Instalá Claude Code](#s2-claude-code)).
- [ ] Una cuenta de Google para usar Google Sheets.
- [ ] De 2 a 5 documentos de prueba: fotos (JPG o PNG) o PDF. Una carta, un remito, un formulario. Si no trajiste, sacale una foto a un ticket o hacé una captura de la carta de un local en Instagram (es información pública).
- [ ] Opcional, para los más técnicos: acceso al **Table Editor** de tu proyecto de Supabase.

> **Datos:** usá documentos sin datos personales o con datos de prueba. Una carta de restaurante o un remito con nombre comercial está bien. Una solicitud con DNI, ingresos o datos de salud de una persona, **no**: para practicar, usá un formulario en blanco completado con datos inventados. Antes de pasar documentos reales a cualquier IA, acordá la regla en tu empresa y escribila en `datos/reglas.md` de tu cerebro.

## Paso 1 · Armá la carpeta de trabajo
Una carpeta con dos subcarpetas: `entrada/` (lo que llega) y `salida/` (lo que sale).

<div data-os="mac">

1. Abrí **Finder › Documentos** y creá la carpeta `foto-a-tabla`. Adentro, creá `entrada` y `salida`.
2. Copiá tus fotos y PDF en `entrada`.
3. Abrí la **Terminal** (apretá **Cmd + Espacio**, escribí `Terminal` y Enter) y entrá a la carpeta:

```bash
cd ~/Documents/foto-a-tabla
```

> **Ojo:** las fotos de iPhone suelen ser `.HEIC` y no siempre se leen bien. Pasalas a JPG: mandátelas por WhatsApp a vos mismo y descargalas, o configurá el iPhone en **Ajustes › Cámara › Formatos › Más compatible**.

</div>
<div data-os="win">

1. Abrí el **Explorador de archivos › Documentos** y creá la carpeta `foto-a-tabla`. Adentro, creá `entrada` y `salida`.
2. Copiá tus fotos y PDF en `entrada`.
3. Abrí **PowerShell** (apretá la tecla **Windows**, escribí `PowerShell` y Enter) y entrá a la carpeta:

```powershell
cd $HOME\Documents\foto-a-tabla
```

</div>

**Tenés que ver:** la terminal muestra `foto-a-tabla` al final de la línea.

> **Tip:** ¿preferís no usar la terminal? En la app de escritorio de Claude, pestaña **Code**, elegí **Local › Open folder…** y abrí `foto-a-tabla`. El resto del tutorial es igual.

## Paso 2 · Instalá la skill "extraer-a-tabla"
La skill tiene las reglas escritas: cómo definir las columnas, cómo marcar la confianza, qué separar para revisar y que **nunca** complete un dato que no se lee.

1. Abrí Claude Code en la carpeta:

```bash
claude
```

**Tenés que ver:** Claude Code abierto en `foto-a-tabla`.

2. En [Kit del taller](#r-kit) (abrilo en otra pestaña) tocá **Copiar** en la skill `extraer-a-tabla` y pegala debajo de este prompt. En Windows, `[MI-USUARIO]` es tu usuario de Windows; si no lo sabés, dejalo así: Claude Code lo averigua.

```prompt
Creá una skill personal llamada extraer-a-tabla. Guardá el texto que pego abajo, exacto y sin cambios, en el archivo SKILL.md de la carpeta de skills de mi usuario (~/.claude/skills/extraer-a-tabla/SKILL.md; en Windows es C:\Users\[MI-USUARIO]\.claude\skills\extraer-a-tabla\SKILL.md). Cuando termines, decime la ruta exacta donde quedó.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

3. Aceptá el permiso para crear el archivo. Salí con `/exit` y volvé a entrar con `claude`.

**Tenés que ver:** si escribís `/` aparece `extraer-a-tabla` en la lista.

## Paso 3 · Definí las columnas con un ejemplo
La IA copia mejor un ejemplo que una explicación. Elegí la fila que más se parece a tu caso y adaptala (son ejemplos inventados):

| Tipo de negocio | Una fila por… | Columnas de ejemplo | Campos críticos |
|---|---|---|---|
| Directorio o marketplace de gastronomía | plato | categoria, nombre, descripcion, precio, sin_tacc, vegetariano, vegano, disponible | sin_tacc, vegetariano, vegano |
| Producción y reparto | renglón del remito | numero_remito, fecha, cliente, producto, cantidad, precio_unitario, total_renglon, total_remito | cantidades y totales |
| Venta consultiva (planes, seguros) | solicitud | los nombres de los campos tal cual aparecen en tu sistema | todos los obligatorios |

Escribí en Claude Code. Antes de mandarlo, cambiá cada `[CORCHETE]` por lo tuyo:

```prompt
/extraer-a-tabla
Los documentos de entrada/ son [QUÉ SON, POR EJEMPLO: CARTAS DE RESTAURANTES]. Quiero una fila por [UNA FILA POR QUÉ, POR EJEMPLO: PLATO].
Estas son las columnas, con una fila de ejemplo:
[PEGÁ LOS NOMBRES DE LAS COLUMNAS Y UNA FILA DE EJEMPLO]
Campos críticos (si hay la mínima duda, van a revisión): [CAMPOS CRÍTICOS].
Regla extra: [UNA REGLA DE TU NEGOCIO, POR EJEMPLO: ANTE LA DUDA, NO SE MARCA APTO].
```

Claude te va a mostrar las columnas que entendió, con las columnas de control que suma siempre (`archivo`, `marca_en_documento`, `confianza`, `a_revisar`, `motivo` y `revisado_por`, que queda vacía para quien revisa), y te pide el OK antes de leer todo.

**Tenés que ver:** un archivo `columnas.md` en la carpeta con la definición de cada columna.

## Paso 4 · Extraé y mirá el reporte
Contestá **"sí, extraé"**. Claude lee cada archivo y escribe:
- `salida/tabla.csv`: todas las filas, con su confianza (alta, media o baja). Un **CSV** es una planilla guardada como texto: se abre con Google Sheets o Excel.
- `salida/a-revisar.csv`: solo las filas que necesitan un humano.
- `salida/reporte.md`: cuántos archivos leyó, cuántas filas, cuántas por nivel de confianza y por qué mandó cada una a revisión.

Qué va a revisión siempre:
- Todo lo de confianza **baja**.
- Todo lo crítico para la salud o la plata: una marca "sin TACC", un total, un campo obligatorio.
- Lo que no se lee. Claude escribe `[ILEGIBLE]` y **no adivina**.
- Lo que no cierra: los renglones de un remito no suman el total, falta un número en la numeración.

> **Ojo:** para todo lo que toca la salud, la regla es **"ante la duda, no se marca apto"**. Si la carta no dice "sin TACC" pero el plato parece apto (por ejemplo, un alfajor de maicena), la IA lo deja como **no apto**, con confianza baja, y lo manda a revisión con el motivo. Una persona decide.

**Tenés que ver:** los tres archivos en `salida/` y, en el chat, un resumen con los conteos.

### Ejemplo (los datos son inventados)
**Foto 1, `pizarron-cafe.jpg`:** el pizarrón de una cafetería. Dice "Tostado de jamón y queso $6.500", "Budín de limón SIN TACC $3.200", "Wrap veggie $7.?00" (el segundo número está borroneado) y "Alfajor de maicena $2.800".
**Foto 2, `carta-restaurante.pdf`:** una carta impresa. Abajo tiene una leyenda: un ícono de espiga tachada = sin TACC y "(V)" = vegano. Platos: "Risotto de hongos [ícono] $11.900", "Ensalada de quinoa (V) $9.400" y "Pollo grillé con puré $10.500".

La tabla que tendría que salir (`salida/tabla.csv`, resumida):

| archivo | nombre | precio | sin_tacc | vegetariano | vegano | marca_en_documento | confianza | a_revisar | motivo |
|---|---|---|---|---|---|---|---|---|---|
| pizarron-cafe.jpg | Tostado de jamón y queso | 6500 | no | no | no | — | alta | no | — |
| pizarron-cafe.jpg | Budín de limón | 3200 | sí | no | no | "SIN TACC" | alta | sí | Marca de salud: confirmar con el local |
| pizarron-cafe.jpg | Wrap veggie | [ILEGIBLE] | no | sí | no | "veggie" | baja | sí | Precio borroneado ("7.?00"). "Veggie" no aclara si es vegano |
| pizarron-cafe.jpg | Alfajor de maicena | 2800 | no | no | no | — | baja | sí | Podría ser apto, pero el pizarrón no lo dice. Ante la duda, no se marca apto |
| carta-restaurante.pdf | Risotto de hongos | 11900 | sí | no | no | ícono de espiga tachada (leyenda: sin TACC) | alta | sí | Marca de salud: confirmar con el local |
| carta-restaurante.pdf | Ensalada de quinoa | 9400 | no | sí | sí | "(V)" (leyenda: vegano) | media | no | Vegetariano deducido de "vegano" |
| carta-restaurante.pdf | Pollo grillé con puré | 10500 | no | no | no | — | alta | no | — |

`salida/a-revisar.csv` tiene 4 de las 7 filas. El reporte dice: "2 archivos · 7 filas · alta 4 · media 1 · baja 2 · a revisar 4 (2 marcas sin TACC, 1 precio ilegible, 1 posible apto no marcado)".

## Paso 5 · Revisá en Google Sheets
1. Abrí [sheets.new](https://sheets.new) para crear una planilla nueva.
2. **Archivo › Importar › Subir** (en inglés: **File › Import › Upload**) y elegí `salida/tabla.csv`.
3. En la ubicación de importación elegí reemplazar la hoja actual y tocá **Importar datos**.
4. Filtrá la columna `a_revisar` por "sí". Revisá fila por fila contra la foto original: corregí lo que haga falta y poné tus iniciales en `revisado_por`.

> **Tip:** si ya conectaste Google Drive y Sheets en Claude ([Conectores](#s8-conectores-y-mcp)), podés pedirle a Claude en el chat: "Creá una planilla de Google llamada [NOMBRE] con el contenido de este CSV" y adjuntar el archivo. Si el conector no está, el camino de arriba siempre funciona.

**Tenés que ver:** todas las filas a revisar con iniciales en `revisado_por`.

## Paso 6 · Cargalo a Supabase (para los más técnicos)
Supabase es una base de datos en la nube. Si tu app la usa, la forma segura de cargar datos es por CSV desde el **Table Editor** (la vista de tablas de Supabase), nunca desde la app.

1. En Google Sheets: **Archivo › Descargar › Valores separados por comas (.csv)** (en inglés: **File › Download › Comma-separated values**). Guardalo en `salida/` como `revisado.csv`.
2. En Claude Code:

```prompt
Leé salida/revisado.csv. Armá salida/para-cargar.csv solo con las filas que tienen revisado_por completo y sin [ILEGIBLE]. Dejá únicamente estas columnas, con estos nombres exactos y en este orden: [COLUMNAS DE TU TABLA EN SUPABASE]. Pasá sí/no a true/false y los precios a números enteros sin puntos. Decime cuántas filas quedaron afuera y por qué.
```

3. En Supabase: **Table Editor** › tu tabla (por ejemplo `platos`) › **Insert › Import data from CSV** y subí `para-cargar.csv`.

> **Ojo:** nunca le pegues a Claude la clave **service role** de Supabase ni datos de usuarios. Para esta carga no hace falta: subís el CSV vos, desde el navegador. Si una sola celda no coincide con el tipo de la columna, Supabase puede rechazar toda la importación: revisá que los nombres y tipos coincidan.

**Tenés que ver:** las filas nuevas en la tabla, con la misma cantidad que te dijo Claude.

## Cómo sé que funcionó
Poné un documento nuevo en `entrada/` y escribí:

```prompt
/extraer-a-tabla
Procesá solo los archivos nuevos de entrada/ con las mismas columnas de columnas.md. Sumalos a salida/tabla.csv y a salida/a-revisar.csv y mostrame el reporte.
```

Funciona si: no te pregunta las columnas de nuevo, nada ilegible aparece "completado" y cada fila a revisar tiene un motivo que entendés.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude dice que no puede leer una imagen | Pasala a JPG o PNG (las `.HEIC` del iPhone suelen fallar). Si está borrosa, sacala de nuevo, de frente y con luz. |
| Con un PDF largo se queda a mitad de camino | Pedile: "Procesá de a un archivo y guardá después de cada uno". |
| Inventó un precio o una marca | "No completes nada que no se lea. Poné [ILEGIBLE], confianza baja y mandalo a revisión." Si se repite, agregá esa regla en `columnas.md`. |
| Manda todo a revisión | Revisá qué marcaste como crítico. Con remitos, por ejemplo, alcanza con revisar los que tienen un total que no cierra. |
| En Google Sheets todo queda en una sola columna | Al importar, en el tipo de separador elegí **Coma**. |
| Supabase rechaza el CSV | Los nombres de las columnas tienen que ser idénticos a los de la tabla y los tipos tienen que coincidir (true/false, números sin puntos). |

## Para seguir solo
- **Medí el ahorro.** Tomá el tiempo de cargar 3 cartas o 10 remitos a mano y con la skill (contando la revisión). Un buen objetivo: bajar al menos a la mitad el tiempo de carga.
- **Más documentos, misma skill.** Comprobantes de gastos (fecha, proveedor, monto, categoría): copiá la carpeta, cambiá el ejemplo en `columnas.md` y listo.
- **Que corra solo.** Más adelante, un flujo de [n8n](#s6-n8n) puede tomar las fotos que caen en una carpeta de Google Drive y avisarte por [Telegram](#s7-telegram) cuando hay filas para revisar. La revisión humana sigue igual.
