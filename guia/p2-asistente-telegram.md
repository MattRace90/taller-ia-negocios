---
titulo: "Tu asistente en Telegram: propuestas y gastos"
bloque: Tutorial
tiempo: 60 a 90 min
para: Todos (sobre todo Manuel Martínez Oratoria, Viajes TDH, Celve y Denvet)
necesitas: p1-cerebro, s6-n8n, s7-telegram, s9-api-anthropic
resultado: Un bot de Telegram tuyo que con /propuesta te devuelve una propuesta con tu marca en PDF y con /gasto carga el comprobante en tu planilla.
---

Un solo bot, dos trabajos que hoy te comen tiempo. Con **/propuesta** le pasás lo que se habló en una llamada de venta y te devuelve la propuesta armada, con tu logo y tus precios, lista para revisar y mandar. Con **/gasto** le mandás la foto del ticket o "gasté 12.000 en nafta" y queda anotado en tu planilla.
Ejemplos del taller: Manuel arma la propuesta In Company apenas corta con la empresa; TDH, un presupuesto prolijo; Celve y Denvet cargan los comprobantes desde el celular sin abrir la planilla.

> **Tip:** palabras que vas a ver en esta página:
> - **n8n:** un programa en la nube que une apps sin programar. Cada automatización se llama **workflow** y cada cajita del workflow es un **nodo**.
> - **Credencial:** la llave guardada en n8n para entrar a otra app (Telegram, Google, Anthropic).
> - **Token del bot:** la clave larga que te dio BotFather al crear tu bot. Se cuida como una contraseña.
> - **Chat ID:** el número de tu chat de Telegram. Sirve para que el bot solo te conteste a vos.
> - **ID de un archivo de Google:** el código largo que aparece en la dirección del archivo.
> - **Skill:** una receta escrita que Claude sigue siempre igual.
> - **MCP:** el enchufe para que Claude maneje otra app, acá n8n ([Las piezas](#t2-piezas)).
> - **JSON:** un formato de texto ordenado (campo: valor) que los programas leen fácil.

## Antes de empezar
- [ ] Tu cerebro armado, con `negocio/oferta-y-precios.md` y `marca/voz.md` ([Armá el cerebro](#p1-cerebro)).
- [ ] Cuenta de n8n en la nube (con la prueba gratis alcanza) ([n8n](#s6-n8n)).
- [ ] Un bot de Telegram creado con BotFather: su **token** y **tu chat ID** ([Telegram](#s7-telegram)).
- [ ] Clave de API de Anthropic con crédito cargado ([API de Anthropic](#s9-api-anthropic)).
- [ ] Una cuenta de Google (Drive, Docs y Sheets).
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)) y saber qué es un conector ([Conectores y MCP](#s8-conectores-y-mcp)).
- [ ] Opcional, para mandar audios: una clave de API de OpenAI (la usamos solo para pasar el audio a texto).

> **Costo:** n8n Cloud arranca en €20 por mes con pago anual (hay prueba gratis, sin tarjeta); Telegram es gratis; cada propuesta y cada gasto consumen centavos de la API de Anthropic. Detalle en [Stack y costos](#r-stack-y-costos).

> **Datos:** el bot lee transcripciones de llamadas y comprobantes. No le mandes DNI, números de tarjeta ni datos de salud de tus clientes. Para probar hoy, usá la llamada y los tickets de ejemplo de esta página (son inventados).

## Paso 1 · Prepará Google: planilla, carpeta y plantilla
Vas a crear tres cosas. De cada una necesitás su **ID**: es el pedazo largo de la dirección entre `/d/` y `/edit` (en carpetas, lo que va después de `/folders/`).

1. **Planilla de gastos.** En Google Sheets creá una planilla nueva, llamala `Gastos [TU-EMPRESA]` y a la hoja ponele `Gastos`. En la fila 1 escribí estos títulos, uno por columna:

```text
Fecha	Monto	Moneda	Categoría	Concepto	Proveedor	Origen	Cargado
```

2. **Carpeta de propuestas.** En Google Drive creá la carpeta `Propuestas`.
3. **Plantilla de propuesta.** En Google Docs creá un documento `Plantilla propuesta`. Poné tu logo arriba, tus colores en los títulos y tu pie de página (web, teléfono). Después pegá este texto con los marcadores tal cual, con las llaves dobles:

```text
{{TITULO}}
Fecha: {{FECHA}} · Para: {{CLIENTE}}

Contexto
{{CONTEXTO}}

El problema
{{PROBLEMA}}

Nuestra propuesta
{{SOLUCION}}

Alcance
{{ALCANCE}}

Inversión
{{INVERSION}}

Próximos pasos
{{PROXIMOS_PASOS}}
```

4. Anotá en un bloc de notas los tres IDs: planilla, carpeta y plantilla.

**Tenés que ver:** la planilla con los 8 títulos, la carpeta vacía y la plantilla con tu logo y los marcadores.

## Paso 2 · Cargá las credenciales en n8n
Una credencial es la llave que n8n usa para entrar a cada servicio. Las cargás vos: Claude nunca ve tus claves.

1. Entrá a tu n8n y creá un workflow vacío (solo para cargar las llaves).
2. Agregá un nodo **Telegram**. En **Credential to connect with › Create new credential** pegá el token del bot y guardá. Ponele de nombre `Telegram [TU-EMPRESA]`.
3. Repetí con un nodo **Anthropic**: pegá tu clave de API. Nombre: `Anthropic`.
4. Repetí con **Google Sheets**, **Google Drive** y **Google Docs**: en cada uno tocá **Sign in with Google** y aceptá los permisos.
5. Opcional: nodo **OpenAI** con tu clave de OpenAI, para los audios.
6. Borrá ese workflow de prueba (las credenciales quedan guardadas).

**Tenés que ver:** en la lista de credenciales de n8n, las 5 (o 6) que creaste.

> **Ojo:** en n8n instalado en tu compu (self-hosted), **Sign in with Google** no aparece y hay que crear un cliente OAuth en Google Cloud. Para el taller usá n8n Cloud.

## Paso 3 · Instalá la skill "propuesta-comercial"
La skill es el manual de cómo se arma una propuesta: estructura fija y la regla de oro, **nunca inventar precios**. La vas a usar sola en Claude Code y también dentro del bot.

1. Abrí la terminal (en Mac, **Terminal**; en Windows, **PowerShell**; si no sabés cómo, mirá el Paso 1 de [Instalá Claude Code](#s2-claude-code)) y abrí Claude Code en la carpeta de tu cerebro:

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

**Tenés que ver:** Claude Code abierto y, arriba, el nombre de tu carpeta del cerebro.

2. Abrí el [Kit del taller](#r-kit) en otra pestaña, tocá **Copiar** en la skill `propuesta-comercial` y pegala debajo de este prompt. En Windows, `[MI-USUARIO]` es el nombre de tu usuario de Windows; si no lo sabés, dejalo así: Claude Code lo averigua solo.

```prompt
Creá una skill personal llamada propuesta-comercial. Guardá el texto que pego abajo, exacto y sin cambios, en el archivo SKILL.md de la carpeta de skills de mi usuario (~/.claude/skills/propuesta-comercial/SKILL.md; en Windows es C:\Users\[MI-USUARIO]\.claude\skills\propuesta-comercial\SKILL.md). Cuando termines, decime la ruta exacta donde quedó.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

3. Cerrá Claude Code con `/exit` y abrilo de nuevo con `claude`. Si escribís `/`, tiene que aparecer `propuesta-comercial` en la lista.
4. Probala sin bot, con esta llamada inventada:

```prompt
/propuesta-comercial Transcripción de ejemplo (inventada): "Hola, soy Laura, de RRHH de una empresa de logística de Córdoba. Tenemos 12 jefes de depósito que tienen que presentar resultados todos los lunes y se traban, leen las filminas, no los escucha nadie. Queremos algo en la empresa, en marzo, ideal dos o tres encuentros. Pasame una propuesta y la vemos con gerencia."
```

**Tenés que ver:** una propuesta con contexto, problema, solución, alcance, inversión y próximos pasos. Si tu precio no está en el cerebro, la inversión dice `PENDIENTE`. Eso está bien: no inventó.

## Paso 4 · Conectá n8n a Claude Code (MCP)
n8n tiene un servidor MCP propio: le permite a Claude buscar, crear, editar y probar workflows en tu cuenta. ([Fuente: doc de n8n](https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server/))

1. En n8n andá a **Settings › Instance-level MCP** y tocá **Enable MCP access** (tenés que ser dueño o admin de la cuenta).
2. En **Connect a client**, copiá la **Server URL**. Termina en `/mcp-server/http`.
3. Salí de Claude Code (`/exit`) y, en la terminal, agregá el conector:

```bash
claude mcp add --transport http n8n [PEGÁ-ACÁ-LA-SERVER-URL]
```

4. Abrí `claude` y escribí `/mcp`. Elegí **n8n** y autenticá: se abre el navegador, entrás a n8n y aprobás el acceso.

**Tenés que ver:** en `/mcp`, el servidor `n8n` como conectado.

> **Tip:** si preferís usar Claude en la web o en la app, el mismo servidor se agrega en **Customize › Connectors › Add › Add custom connector** con nombre `n8n` y la Server URL. Pero para este tutorial conviene Claude Code: lee los archivos de tu cerebro y arma el workflow en el mismo paso.

> **Ojo:** si la autenticación por navegador falla, en n8n abrí **Connect a client** › pestaña **API key**, copiá el token (se muestra una sola vez) y usá `claude mcp add --transport http n8n [SERVER-URL] --header "Authorization: Bearer [TU-TOKEN]"`. Ese comando va **en la terminal, con Claude Code cerrado**. Nunca pegues el token en el chat de Claude.

## Paso 5 · Que Claude arme el workflow
En Claude Code, dentro de la carpeta del cerebro, pegá este prompt. Antes de mandarlo, reemplazá lo que está entre corchetes:
- `[TU-EMPRESA]`: el nombre que le pusiste a las credenciales en el Paso 2.
- `[TU-CHAT-ID]`: tu chat ID ([Telegram](#s7-telegram)).
- `[TUS-CATEGORÍAS]`: tus categorías de gasto (o dejá las del ejemplo).
- `[ID-DE-LA-PLANILLA]`, `[ID-DE-LA-PLANTILLA]` y `[ID-DE-LA-CARPETA]`: los tres IDs que anotaste en el Paso 1.

```prompt
Usá el conector de n8n para armar un workflow nuevo llamado "Asistente Telegram [TU-EMPRESA]". Antes de crear nada, leé de esta carpeta CLAUDE.md, negocio/oferta-y-precios.md, negocio/cliente-ideal.md, marca/voz.md y datos/reglas.md, y la skill ~/.claude/skills/propuesta-comercial/SKILL.md.

Lo que tiene que hacer el workflow:

1. Telegram Trigger con la credencial "Telegram [TU-EMPRESA]", que escuche mensajes, con "Download Images/Files" activado y "Restrict to Chat IDs" = [TU-CHAT-ID]. Zona horaria del workflow: America/Argentina/Cordoba.

2. Un Switch que separe:
   - mensaje con foto, o texto que empieza con /gasto → rama GASTO
   - mensaje de voz, o texto que empieza con /propuesta → rama PROPUESTA
   - cualquier otra cosa → responder por Telegram: "Mandame /gasto con el detalle o una foto del comprobante, o /propuesta con lo que se habló en la llamada."

3. Rama GASTO:
   - Si es foto: nodo Anthropic › Analyze Image (Input Type: Binary File(s), campo data). Si es texto: Anthropic › Message a Model. Modelo: claude-haiku-5-5.
   - Las dos tienen que devolver SOLO un JSON con: fecha (AAAA-MM-DD; si no figura, la de hoy), monto (número, sin símbolos ni puntos de miles; null si no se lee), moneda (ARS o USD), categoria (una de estas: [TUS-CATEGORÍAS, POR EJEMPLO: Combustible, Insumos, Servicios, Sueldos, Impuestos, Software, Otros]), concepto (máximo 8 palabras), proveedor (o "sin dato").
   - Un nodo Code que lea ese JSON aunque venga envuelto en un bloque de código.
   - Si monto es null: responder "No pude leer el monto. Escribímelo así: /gasto 12000 nafta" y cortar.
   - Google Sheets › Append Row en la planilla [ID-DE-LA-PLANILLA], hoja "Gastos", columnas Fecha, Monto, Moneda, Categoría, Concepto, Proveedor, Origen (foto o texto) y Cargado (fecha y hora de carga).
   - Responder por Telegram: "Anotado: {fecha} · {moneda} {monto} · {categoria} · {concepto}. Si algo está mal, corregilo en la planilla."

4. Rama PROPUESTA:
   - Si es un mensaje de voz y existe una credencial de OpenAI: OpenAI › Transcribe a Recording. Si no hay credencial de OpenAI, responder "Por ahora mandame la transcripción como texto, después de /propuesta" y cortar.
   - Anthropic › Message a Model, modelo claude-sonnet-5-5. En System Message poné el texto completo de la skill propuesta-comercial y, debajo, bajo el título "CEREBRO DE LA EMPRESA", el contenido de los archivos que leíste. El mensaje del usuario es la transcripción (sin el /propuesta). Pedí la salida en JSON, como dice la skill.
   - Code que lea el JSON.
   - Google Drive › Copy del documento [ID-DE-LA-PLANTILLA] a la carpeta [ID-DE-LA-CARPETA], con el nombre "Propuesta - {cliente} - {fecha de hoy}".
   - Google Docs › Update › Find and Replace Text sobre la copia, para cada marcador: {{TITULO}}, {{FECHA}}, {{CLIENTE}}, {{CONTEXTO}}, {{PROBLEMA}}, {{SOLUCION}}, {{ALCANCE}}, {{INVERSION}}, {{PROXIMOS_PASOS}}.
   - Google Drive › Download de la copia, con Google File Conversion a PDF.
   - Telegram › Send Document con el PDF, y después un mensaje con el link al Google Doc y "Antes de mandarla, revisá: {pendientes}".

5. Antes de crear, buscá mis credenciales en n8n y decime cuáles vas a usar en cada nodo. Si falta alguna, frená y decime cuál tengo que crear.
6. Creá el workflow, validalo y corregí los errores que encuentres. NO lo publiques. Cuando esté listo, dame el link para abrirlo.
```

Claude te va a ir mostrando lo que hace y pidiendo permiso para usar las herramientas de n8n: aceptá.

**Tenés que ver:** el link al workflow. Al abrirlo en n8n, un disparador de Telegram, un Switch con tres salidas y dos ramas de nodos.

> **Tip:** si Claude pregunta algo que no sabés (por ejemplo, el formato de una fecha), contestá "elegí lo más simple y avisame qué elegiste".

## Paso 6 · Probalo y publicalo
1. En n8n, abrí el workflow y tocá **Publish** (arriba a la derecha). Confirmá con **Publish**.
2. En Telegram, abrí tu bot y probá estos tres mensajes (datos inventados):

```text
/gasto gasté 12.000 en nafta para el reparto
```

```text
/propuesta Llamada con Laura, RRHH de una logística de Córdoba. 12 jefes de depósito que presentan resultados los lunes y se traban. Quieren algo en la empresa en marzo, dos o tres encuentros. Lo ve gerencia.
```

3. Sacale una foto a un ticket cualquiera (de un café, por ejemplo) y mandásela al bot.
4. Si algo no anda, pedile a Claude Code:

```prompt
Revisá la última ejecución con error del workflow "Asistente Telegram [TU-EMPRESA]" en n8n, decime qué falló en una línea y corregilo. Después avisame para que lo vuelva a probar.
```

**Tenés que ver:** una fila nueva en la planilla por cada gasto, el mensaje "Anotado:" en Telegram y un PDF con tu logo en el chat y en la carpeta `Propuestas`.

## Camino alternativo · Armalo a mano, nodo por nodo
Si el conector no anda o querés entender cada pieza, armalo vos. En n8n: **Create workflow**, y agregá estos nodos en orden. Las expresiones (lo que va entre `{{ }}`) se pegan con el campo en modo **Expression**.

| # | Nodo | Configuración |
|---|---|---|
| 1 | **Telegram Trigger** | Trigger On: Message. Additional Fields: **Download Images/Files** = activado; **Restrict to Chat IDs** = tu chat ID. |
| 2 | **Switch** | Salida "gasto": `{{ !!$json.message.photo \|\| ($json.message.text \|\| '').startsWith('/gasto') }}` es verdadero. Salida "propuesta": `{{ !!$json.message.voice \|\| ($json.message.text \|\| '').startsWith('/propuesta') }}` es verdadero. **Fallback Output**: Extra Output, conectada a un **Telegram › Send Message** con el texto de ayuda. |
| 3a | **Anthropic › Analyze Image** (si hay foto) | Model: `claude-haiku-5-5`. Input Type: Binary File(s), campo `data`. Text Input: el pedido de JSON del paso 5 (fecha, monto, moneda, categoría, concepto, proveedor). Para separar foto de texto, poné antes un **If** con `{{ !!$json.message.photo }}`. |
| 3b | **Anthropic › Message a Model** (si es texto) | Mismo modelo y mismo pedido, con el mensaje: `{{ $json.message.text }}`. |
| 4 | **Code** | Lee el JSON: `const t = $input.first().json.content?.[0]?.text ?? JSON.stringify($input.first().json); return [{ json: JSON.parse(t.replace(/```json\|```/g, '').trim()) }];` (si falla, mirá la salida del nodo anterior y pedile a Claude que ajuste la ruta). |
| 5 | **Google Sheets › Append Row** | Tu planilla, hoja `Gastos`. Mapeá cada columna con `{{ $json.fecha }}`, `{{ $json.monto }}`, etc. Cargado: `{{ $now.toFormat('yyyy-MM-dd HH:mm') }}`. |
| 6 | **Telegram › Send Message** | Chat ID: `{{ $('Telegram Trigger').item.json.message.chat.id }}`. Texto: `Anotado: {{ $json.fecha }} · {{ $json.monto }} · {{ $json.categoria }}`. |
| 7 | **OpenAI › Transcribe a Recording** (opcional, si es audio) | Campo binario `data`. |
| 8 | **Anthropic › Message a Model** (propuesta) | Model: `claude-sonnet-5-5`. **Options › System Message**: el texto de la skill `propuesta-comercial` + tu `oferta-y-precios.md` + tu `voz.md` pegados abajo. Mensaje: la transcripción (`{{ $json.text }}` si vino del audio, o el texto del mensaje). |
| 9 | **Code** | Igual que el 4. |
| 10 | **Google Drive › Copy** | File: tu plantilla. Parent folder: `Propuestas`. Name: `Propuesta - {{ $json.cliente }}`. |
| 11 | **Google Docs › Update** | Document: el ID que devolvió el Copy. Una acción **Find and Replace Text** por cada marcador (`{{TITULO}}` → `{{ $('Code1').item.json.titulo }}`, y así). Ojo con el nombre del nodo Code en tu workflow. |
| 12 | **Google Drive › Download** | El mismo ID. Options › **Google File Conversion** › Google Docs: **PDF**. |
| 13 | **Telegram › Send Document** | **Binary File** activado, campo `data`. |

Cuando termines, **Publish** y probá como en el paso 6.

**Tenés que ver:** los mismos resultados del paso 6: la fila en la planilla, el "Anotado:" en Telegram y el PDF de la propuesta.

## Cómo sé que funcionó
Desde el celular, con la compu cerrada:

```text
/propuesta Me llamó una empresa que quiere [LO QUE VENDÉS] para [CANTIDAD] personas en [MES]. Les preocupa [PROBLEMA QUE CONTARON].
```

Te tiene que llegar un PDF con tu logo, con tu oferta real y con `PENDIENTE` donde falta un dato. Y un `/gasto` tiene que aparecer en la planilla en menos de un minuto.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El bot no responde nada | Revisá que el workflow esté publicado (**Publish**). Si hay otro workflow u otro programa usando el mismo bot, despublicalo: un bot de Telegram manda sus mensajes a un solo lugar. |
| El bot no responde, y en n8n no aparece ninguna ejecución | Revisá que tu chat ID en **Restrict to Chat IDs** sea el correcto ([Telegram](#s7-telegram)). |
| La propuesta inventa un precio | Revisá que `oferta-y-precios.md` esté en el System Message y pedile a Claude Code: "Reforzá en el System Message la regla de no inventar precios y volvé a probar". |
| Los marcadores `{{CONTEXTO}}` quedan sin reemplazar | El texto de la plantilla tiene que ser idéntico al marcador, sin espacios ni negritas a la mitad. Volvé a escribirlo de corrido. |
| Error de formato en el audio (OpenAI) | Telegram manda los audios como `.oga`. Pedile a Claude Code: "Agregá antes de la transcripción un paso que renombre el archivo de audio a .ogg". |
| El gasto se carga con el monto mal (12 en vez de 12.000) | Agregá al pedido de JSON: "En Argentina el punto separa miles y la coma, decimales". |

## Para seguir solo
- **Comprobantes en PDF:** pedile a Claude que sume a la rama GASTO el nodo **Anthropic › Analyze Document**, para las facturas que llegan por mail en PDF.
- **Resumen del mes:** un segundo workflow que el día 1 lea la planilla y te mande por Telegram el total por categoría y el gasto más alto (útil para un informe de rentabilidad).
- **Sumá a tu equipo:** agregá sus chat IDs en **Restrict to Chat IDs** (separados por coma) y una columna "Cargado por" con `{{ $('Telegram Trigger').item.json.message.from.first_name }}`.
