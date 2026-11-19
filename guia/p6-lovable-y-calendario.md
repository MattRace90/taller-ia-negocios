---
titulo: Una app en Lovable + tu calendario de contenido
bloque: Tutorial
tiempo: 50 a 60 min (Parte A 30 min, Parte B 20 a 30 min)
para: Denvet, Fondus, Manuel Martínez Oratoria, Celve (y cualquiera que quiera una app o programar contenido)
necesitas: p1-cerebro, s1-claude, s2-claude-code, s8-conectores-y-mcp
resultado: Una app interna tuya funcionando en un link de Lovable, y dos semanas de publicaciones escritas por Claude con tu voz y cargadas en Metricool para que las revises.
---

Este tutorial tiene dos partes que se hacen por separado. En la primera armás una **app simple que te queda para usar y explorar**: el control diario de maples de Denvet, un mini CRM de leads para Fondus o un portal de alumnos para Manuel. Se arma escribiendo, sin programar.
En la segunda, Claude lee tu cerebro, arma el calendario de contenido y lo deja **programado en Metricool** para que vos lo revises y apruebes.

## Antes de empezar
- [ ] Tu cerebro armado ([Tu cerebro](#p1-cerebro)).
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)) o la app de Claude ([Claude](#s1-claude)).
- [ ] Parte A: cuenta en [lovable.dev](https://lovable.dev) (alcanza con la gratis para probar; ver [Stack y costos](#r-stack-y-costos)).
- [ ] Parte B: cuenta en [metricool.com](https://metricool.com) con tu marca creada y tus redes conectadas (Instagram, Facebook y las que uses).
- [ ] Parte B: saber cómo se conecta un conector a Claude ([Conectores y MCP](#s8-conectores-y-mcp)).

> **Datos:** en la app de práctica usá datos inventados. Si después cargás leads o alumnos reales, son datos personales: la app tiene que tener login (Paso A4) y nadie de afuera tiene que poder verlos.

## Parte A · Tu app en Lovable (30 min)

## Paso A1 · Elegí qué app vas a hacer
Una app chica, que resuelva **una** tarea que hoy hacés en papel, en WhatsApp o en una planilla desordenada. Ejemplos del taller:

| Empresa | App | Qué resuelve |
|---|---|---|
| Denvet | Control diario de maples | Cada día la granja carga producción, roturas y conteo; la app calcula el stock y los maples sin vender. |
| Fondus | Mini CRM de leads | Cada lead con su estado (nuevo, contactado, entrevista pactada, descartado), quién lo tiene y cuándo hay que volver a escribirle. |
| Manuel | Portal de alumnos | Cada alumno ve su grupo, sus encuentros, el link a su carpeta de videos y su feedback. |

**Tenés que ver:** una sola frase que diga quién usa la app, qué carga y qué quiere ver. Ejemplo: "El encargado de la granja carga cada tarde la producción por categoría y el dueño ve el stock del día".

## Paso A2 · Que Claude escriba el prompt para Lovable desde tu cerebro
Lovable trabaja mejor si el primer mensaje es completo. Ese mensaje lo escribe Claude, leyendo tu cerebro. Abrí la terminal (en Mac, **Terminal**; en Windows, **PowerShell**) y abrí Claude Code en la carpeta del cerebro:

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

> **Tip:** ¿no usás Claude Code? Hacelo en la app de Claude, dentro de un Proyecto con los archivos de tu cerebro subidos. Cambiá "Guardá el prompt en…" por "Devolveme el prompt".

Pegá esto (cambiá `[TU-FRASE-DEL-PASO-A1]` por tu frase y `[NOMBRE-DE-LA-APP]` por un nombre corto, sin espacios):

```prompt
Quiero hacer una app interna en Lovable: [TU-FRASE-DEL-PASO-A1].

Leé mi cerebro (CLAUDE.md, operacion/procesos.md, operacion/donde-se-va-el-tiempo.md, equipo/organizacion.md y marca/identidad-visual.md; si alguno no existe, seguí con lo que haya en operacion/, equipo/ y marca/) y escribí UN solo prompt para pegar en Lovable, en español, con este orden:
1. Qué es la app y para quién (2 líneas).
2. Quiénes la usan y qué puede hacer cada uno (roles).
3. Las pantallas, una por una, con qué se ve y qué se puede tocar.
4. Los datos: cada tabla con sus campos (nombre, tipo, si es obligatorio) y cómo se relacionan.
5. Cálculos automáticos, si hay.
6. Reglas: que pida login con email, que se use bien desde el celular, que esté en español.
7. Estilo visual con mis colores y tipografías.
8. 10 registros de ejemplo INVENTADOS para probar.

Nada de datos reales de clientes ni de personas. Lo que no sepas de mi operación, preguntámelo antes de escribir el prompt (máximo 5 preguntas).
Guardá el prompt en apps/[NOMBRE-DE-LA-APP]/prompt-lovable.md.
```

**Tenés que ver:** el archivo `prompt-lovable.md` con las 8 partes.

Si preferís arrancar con un ejemplo armado, este es para una granja (los datos son inventados). Copialo y cambiá lo que no sea tuyo:

```prompt
Creá una app web interna llamada "Stock de maples" para una granja de huevos.

Para quién: el encargado de la granja carga los datos cada tarde desde el celular. El dueño mira el stock y el resumen desde el celular o la compu.

Roles:
- Encargado: carga la planilla del día y ve el historial.
- Dueño: ve todo, edita categorías y corrige cargas.

Pantallas:
1. Inicio: tarjetas con el stock actual de maples por categoría, los maples sin vender del día y una alerta si el conteo físico no coincide con el stock calculado.
2. Carga del día: un formulario con fecha (hoy por defecto) y, por categoría, producción del día, roturas, salidas (ventas) y conteo físico. Botones grandes, pensados para usar con una mano.
3. Historial: tabla por día y categoría, con filtro por fecha y exportar a CSV.
4. Categorías: lista editable (por ejemplo: Blanco grande, Blanco mediano, Color grande, Color mediano).

Datos:
- categorias: id, nombre (obligatorio), activa (sí/no).
- cargas_diarias: id, fecha, categoria_id, produccion_maples, roturas_maples, salidas_maples, conteo_fisico_maples, cargado_por, creado_en.

Cálculos:
- Stock calculado del día = stock del día anterior + producción − roturas − salidas.
- Diferencia = conteo físico − stock calculado. Si la diferencia es distinta de cero, mostrarla en rojo.
- Maples sin vender del día = producción − salidas.

Reglas:
- Login con email. Solo usuarios invitados pueden entrar.
- Todo en español de Argentina. Fechas en formato día/mes/año.
- Pensada primero para celular.

Estilo: simple y claro, fondo blanco, color principal verde campo, números grandes.

Cargá 10 días de datos de ejemplo inventados para 4 categorías, con dos días donde el conteo no coincide.
```

Variantes cortas para adaptar con el prompt de arriba:
- **Mini CRM de leads (Fondus):** tablas `leads` (nombre, teléfono, origen, organizador asignado, estado, próximo contacto, notas) y `vendedores`. Pantallas: tablero por estado, ficha del lead, "a quién le escribo hoy".
- **Portal de alumnos (Manuel):** tablas `grupos`, `alumnos`, `encuentros` y `feedback`. Cada alumno entra con su email y ve solo lo suyo: sus encuentros, el link a su carpeta de videos y su feedback.

## Paso A3 · Creá la app en Lovable
1. Entrá a [lovable.dev](https://lovable.dev) con tu cuenta.
2. Pegá el prompt en la caja de la pantalla principal y envialo.
3. Esperá a que termine (1 a 3 minutos). Lovable muestra el chat a la izquierda y la vista previa a la derecha.

**Tenés que ver:** la app funcionando en la vista previa, con los datos de ejemplo.

> **Tip:** Lovable trae su propio backend (**Lovable Cloud**: base de datos, login y archivos, sobre la base de Supabase). Cuando tu app necesite guardar datos o tener login, Lovable lo activa solo o te pide aprobarlo en el chat. Aprobalo. No hace falta crear nada en Supabase para este tutorial.

## Paso A4 · Iterá de a un cambio por mensaje
Lovable gasta créditos por mensaje. Un pedido claro por vez rinde más que cinco cambios juntos.

Probá la app como si fueras el encargado y pedí cambios cortos:

```prompt
En la pantalla de carga, después de guardar, mostrá un resumen del día con el stock calculado y la diferencia contra el conteo, y un botón "Copiar resumen para WhatsApp".
```

```prompt
Revisá la seguridad: que sin login no se pueda ver ninguna pantalla ni leer ningún dato, y que solo el dueño pueda editar categorías. Explicame en 3 líneas cómo quedó.
```

**Tenés que ver:** cada cambio aplicado en la vista previa. Si algo se rompe, pedí: "Volvé a como estaba antes del último cambio".

## Paso A5 · Publicala y compartí el link
1. Tocá **Publish**, arriba a la derecha.
2. La app queda en una dirección `*.lovable.app` (podés cambiar el nombre).
3. Si hacés cambios después, se publican cuando tocás **Publish changes** en el mismo menú.

**Tenés que ver:** la app abierta desde tu celular, en el link público, pidiendo login.

> **Ojo:** el link público lo puede abrir cualquiera que lo tenga. Por eso la app pide login (Paso A4). En el menú de **Publish** también podés restringir el acceso a personas invitadas; revisá qué permite tu plan.

## Parte B · Tu calendario de contenido con Metricool (20 min)

## Paso B1 · Conectá Metricool a Claude

> **Ojo:** para conectar Instagram dentro de Metricool, la cuenta tiene que ser **profesional** (empresa o creador) y Meta te puede pedir un código por SMS o de tu app de autenticación. Hacelo antes del taller si podés. Si hoy no se conecta, igual podés hacer el Paso B2: Claude arma el calendario sin los horarios de tu cuenta.
Metricool tiene un conector oficial para Claude. Funciona con cualquier plan de Metricool, incluido el gratis (con los límites de tu plan).

**Opción 1, en la app de Claude (web o escritorio):**
1. **Customize › Connectors**, buscá **Metricool** en el directorio y tocá **Connect**.
2. Iniciá sesión en Metricool y tocá **Grant access**.

**Opción 2, en Claude Code:**

<div data-os="mac">

```bash
claude mcp add --transport http metricool https://ai.metricool.com/mcp
```

</div>
<div data-os="win">

```powershell
claude mcp add --transport http metricool https://ai.metricool.com/mcp
```

</div>

Después abrí `claude`, escribí `/mcp`, elegí **metricool**, tocá **Authenticate**, autorizá en el navegador y tocá **Grant access**.

**Tenés que ver:** Metricool como **Connected** (en la app) o con estado conectado en `/mcp` (en Claude Code).

> **Tip:** si conectaste Metricool en la app de Claude con la misma cuenta, también aparece en Claude Code. No hace falta hacer las dos opciones.

> **Ojo:** el conector puede ver tus métricas y **crear y editar publicaciones programadas**. No maneja mensajes, comentarios ni campañas pagas. Si alguna vez querés cortarlo: **Customize › Connectors**, los tres puntos al lado de Metricool, **Disconnect**.

> **Costo:** el plan gratis de Metricool permite 20 publicaciones programadas por mes y no incluye LinkedIn ni X. Para dos semanas a 3 o 4 publicaciones por semana alcanza. Detalle en [Stack y costos](#r-stack-y-costos).

## Paso B2 · Que Claude arme el calendario con tu cerebro
En Claude Code, parado en la carpeta del cerebro (como en el Paso A2). Cambiá `[FECHA-DE-INICIO]` (por ejemplo, 24/11) y `[CANTIDAD]` (por ejemplo, 3):

```prompt
Armá el calendario de contenido de las próximas 2 semanas, desde el [FECHA-DE-INICIO].

1. Leé marca/voz.md, negocio/cliente-ideal.md, ventas/objeciones.md y ventas/preguntas-frecuentes.md.
2. Usá Metricool para ver cuáles son los mejores días y horarios para publicar en mi cuenta de Instagram, y qué publicaciones ya tengo programadas, para no pisarlas.
3. Proponé [CANTIDAD] publicaciones por semana, mezclando: responder una objeción, mostrar cómo trabajamos, una prueba (caso o testimonio que YA esté en mi cerebro, nada inventado) y una invitación a escribirnos.
4. Para cada una: fecha y hora, red, formato (carrusel, reel, imagen), el texto completo del posteo en mi voz, y qué imagen o video hace falta.
5. Guardá todo en contenido/calendario-[AAAA-MM].md como una tabla y mostramelo. Todavía no cargues nada en Metricool.
```

**Tenés que ver:** la tabla del calendario en pantalla y en `contenido/calendario-[AAAA-MM].md`. Corregí lo que no suene a vos: "El del martes está muy formal, decilo como en marca/voz.md".

## Paso B3 · Cargalo en Metricool para revisión
Cuando el calendario te guste:

```prompt
Cargá en Metricool las publicaciones del calendario que aprobé, como publicaciones para revisión (no publicadas directo), en las fechas y horarios de la tabla. Si alguna necesita imagen o video, cargala igual con el texto y anotá en el calendario "falta subir el archivo". Al final, listame qué quedó cargado y con qué fecha.
```

**Tenés que ver:** en [metricool.com](https://metricool.com), en el **Planificador**, las publicaciones en sus fechas, pendientes de tu revisión.

> **Tip:** lo más simple es que la imagen o el video los subas vos en Metricool cuando revisás cada publicación. Las placas las podés hacer con el tutorial [Placas en tu voz](#p10-extras).

## Cómo sé que funcionó
- La app de la Parte A abre desde tu celular, pide login y guarda lo que cargás.
- En Metricool ves las publicaciones de las próximas dos semanas, con tus textos.
- Prueba final, en Claude Code:

```prompt
Usando Metricool, decime qué tengo programado para la semana que viene, en qué horario, y si alguno de los textos usa palabras que mi cerebro dice que no usamos.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Lovable armó algo distinto a lo que pediste | No pidas todo de nuevo. Señalá una cosa: "La pantalla de carga tiene que tener una fila por categoría, no un campo por día". |
| Se te terminaron los créditos de Lovable | Los créditos gratis se renuevan por día y por mes. Mientras, seguí ajustando el prompt en Claude para que el próximo mensaje sea más preciso. |
| La app pide aprobar **Cloud** | Es la base de datos y el login. Aprobalo. |
| Metricool no aparece en el directorio de conectores | Agregalo a mano: **Customize › Connectors › Add › Add custom connector**, nombre `Metricool`, URL `https://ai.metricool.com/mcp`. En el plan gratis de Claude solo podés tener un conector personalizado. |
| Claude no ve tu cuenta de Instagram en Metricool | La red tiene que estar conectada dentro de Metricool, en esa marca. Revisalo en [metricool.com](https://metricool.com). |
| Claude publicó en vez de dejar para revisión | Borrá o editá la publicación en Metricool. La próxima vez pedí "como borrador para revisión" y que te muestre el listado antes de cargar. |

## Para cuando quieras ir más allá: publicar con tu propia app de Meta
Metricool es el camino recomendado: ya está aprobado por Meta, no requiere programar y se conecta en dos minutos. Si algún día querés publicar en Instagram o Facebook **sin intermediarios**, con tu propio sistema, esto es lo que hace falta (no lo hacemos en vivo):

- **Cuenta profesional de Instagram** (de empresa o de creador). Según el tipo de inicio de sesión, vinculada a una página de Facebook.
- **Una app en Meta for Developers** (developers.facebook.com), dentro de tu portfolio comercial.
- **Permisos:** con inicio de sesión de Instagram, `instagram_business_basic` e `instagram_business_content_publish`. Con inicio de sesión de Facebook, `instagram_basic`, `instagram_content_publish` y `pages_read_engagement`.
- **Acceso y revisión:** la app necesita acceso Standard o Advanced a esos permisos. Para publicar en cuentas de otros (por ejemplo, si sos agencia) Meta revisa la app.
- **Cómo se publica:** primero se crea un "contenedor" con la imagen o el video (tiene que estar en una URL pública) y después se publica. Acepta imágenes JPEG, reels, carruseles de hasta 20 piezas e historias.
- **Límite:** hay un tope de publicaciones por API cada 24 horas (la doc indica 100; revisalo antes de planificar volumen).

Con eso, Claude Code puede escribirte un pequeño programa que lea tu calendario y publique. Es más control, pero también más mantenimiento: tokens que vencen, cambios de la API y revisión de Meta.

## Para seguir solo
- **Una app por mes:** cuando una tarea vive en una planilla que nadie entiende, es candidata a app en Lovable. Arrancá siempre por el Paso A2: el prompt desde el cerebro.
- **Rutina de contenido del lunes:** convertí la Parte B en una tarea programada que cada lunes arme el calendario de la semana y te lo deje para revisar ([Tareas programadas](#t4-tareas-programadas)).
- **Medí qué funciona:** cada fin de mes pedile a Claude: "Con las métricas de Metricool del último mes, decime qué tipo de publicación funcionó mejor y ajustá el calendario que viene".

## Fuentes
- Lovable, backend integrado (Lovable Cloud): https://docs.lovable.dev/integrations/cloud
- Lovable, publicar y compartir (**Publish**, `lovable.app`, visibilidad): https://docs.lovable.dev/features/hosting
- Lovable, planes y créditos: https://docs.lovable.dev/introduction/plans-and-credits
- Metricool, cómo conectar su MCP con Claude (URL, pasos, herramientas, planes): https://help.metricool.com/how-to-connect-metricools-mcp-with-claude-0l84v
- Meta, publicación de contenido en Instagram (cuenta profesional, permisos, contenedores, límites): https://developers.facebook.com/docs/instagram-platform/content-publishing
- Claude, conectores: ver `investigacion/claude-code-datos.md` (**Customize › Connectors**).
- Verificado el 18/11/2026.
