---
titulo: 'Extras: placas en tu voz y el reporte que llega solo'
bloque: Tutorial
tiempo: 50 a 60 min (2 tutoriales de 25 a 30 min)
para: La Consejera del Éxito (placas) · Denvet, Fondus y Celve (reporte) · sirven para todos
necesitas: s2-claude-code, p1-cerebro, s8-conectores-y-mcp
resultado: Un carrusel armado con tu voz y tu estilo, listo para pulir; y un resumen semanal que se arma solo cada lunes a partir de una planilla.
---

Dos tutoriales cortos, independientes. Hacé la que más te sirva o las dos.
**Parte A · Placas en tu voz (pasos 1 a 3):** la IA escribe el carrusel con tu forma de hablar, lo diseña con tu estilo y vos solo pulís detalles.
**Parte B · El reporte que llega solo (pasos 4 a 7):** cada lunes, sin que nadie lo pida, Claude lee una planilla y te manda un resumen: la rentabilidad del mes, cómo vinieron los leads o "qué sigue esta semana".

## Antes de empezar
- [ ] Claude Code instalado y abierto en tu carpeta del cerebro: en la Terminal (Mac) o PowerShell (Windows), `cd` a tu carpeta y `claude` ([Instalá Claude Code](#s2-claude-code)).
- [ ] Tu cerebro con `marca/voz.md` y, para la parte A, `marca/identidad-visual.md` (logo, colores, tipografías) ([Armá el cerebro](#p1-cerebro)).
- [ ] Parte A: una cuenta de Canva y 3 placas tuyas que te gusten, como referencia. Guardá las capturas en una carpeta `referencias/` dentro de tu carpeta del cerebro.
- [ ] Parte B: una planilla de Google con datos de al menos 4 semanas. Si todavía no la tenés, en el paso 4 armamos una de ejemplo con datos inventados.
- [ ] Parte B: Google Drive conectado en Claude (**Customize › Connectors**, ver [Conectores](#s8-conectores-y-mcp)). Opcional: Gmail, para que el reporte te llegue por mail.

> **Datos:** para las placas no hace falta ningún dato de clientes. No uses fotos ni testimonios de alumnos o clientes sin su permiso. Para el reporte, la planilla tiene que tener números del negocio, no datos personales: el reporte trabaja con totales.

## Paso 1 · Escribí el guion del carrusel (parte A)
En Claude Code, parado en la carpeta del cerebro. Cambiá `[CANTIDAD]` (por ejemplo, 6), `[TEMA]` y `[ACCIÓN…]` por lo tuyo:

```prompt
Leé marca/voz.md y marca/identidad-visual.md. Mirá las placas de referencias/ para entender mi estilo. Escribí un carrusel de Instagram de [CANTIDAD] placas sobre [TEMA]. Para cada placa: el texto exacto (máximo 20 palabras, con mis palabras y mi forma de hablar), qué va en la imagen y dónde va el texto. La primera placa tiene que frenar el scroll y la última invita a [ACCIÓN: ESCRIBIR POR WHATSAPP, COMENTAR, ENTRAR AL LINK]. Guardalo en contenido/carruseles/[TEMA].md.
```

Corregilo hasta que suene a vos: "esto no lo diría nunca", "más corto", "usá 'vos'". Cada corrección que vale para siempre, pedile que la guarde en `marca/voz.md`.

**Tenés que ver:** un archivo con el texto de cada placa, en tu voz.

## Paso 2 · Diseñalo (parte A)
Elegí un camino.

### Camino 1 · Con el conector de Canva
El conector de Canva le permite a Claude crear diseños en tu cuenta, usar tu kit de marca (con las plantillas de marca compartidas con vos), buscar tus diseños y exportarlos, por ejemplo a PNG. Según la ayuda de Canva, el conector está en todos sus planes; algunas funciones, como buscar plantillas de marca, piden un plan pago.
Fuentes: [Ayuda de Canva: conectar Claude](https://www.canva.com/help/connect-claude-to-canva/) y [Conector de Canva en Claude](https://claude.com/connectors/canva), consultadas el 18/11/2026.

1. En Claude: **Customize › Connectors**, buscá **Canva**, tocá **Connect** e iniciá sesión en Canva.
2. Abrí un chat nuevo en la app de Claude y fijate que Canva esté activado en los conectores de ese chat. Adjuntá el archivo del guion del paso 1: tocá el **+** del cuadro de texto, elegí subir un archivo y buscá `contenido/carruseles/[TEMA].md` en tu carpeta del cerebro. Después escribí esto. Los colores en hex son los códigos tipo `#1A2B3C`: están en `marca/identidad-visual.md`.

```prompt
Con Canva, diseñá un carrusel de Instagram con el guion que te adjunto: una placa por cada parte, con el texto exacto, sin cambiar ni una palabra. Usá mi kit de marca de Canva si tengo uno; si no, usá estos colores: [COLORES EN HEX] y esta tipografía: [TIPOGRAFÍA]. Mostrame las opciones que te dé Canva antes de elegir.
```

3. Elegí la opción que más te guste y abrila en Canva para pulir: cambiá una imagen, mové un texto, ajustá un color.
4. Para bajarla: en Canva, o pedile a Claude "Exportá ese diseño en PNG".

**Tenés que ver:** el carrusel en tu cuenta de Canva, con el texto exacto del guion.

> **Ojo:** no verificamos cuántas placas arma Canva en un solo pedido. Si te devuelve una sola, pedí las siguientes de a una: "Ahora la placa 2, con el mismo estilo que la anterior". Si Claude no ve Canva, abrí un chat nuevo y revisá que el conector esté activado.

### Camino 2 · Como página web que Claude pasa a PNG
Control total del texto y del diseño, sin depender de otra app. En Claude Code:

```prompt
Con el guion de contenido/carruseles/[TEMA].md, armá el carrusel como un archivo HTML: una placa de 1080 x 1350 píxeles por cada parte, con mis colores, tipografías y logo de marca/identidad-visual.md, y el texto exacto del guion. Abrilo para que lo vea. Cuando te diga que está bien, exportá cada placa a PNG en contenido/carruseles/[TEMA]/ usando Google Chrome en modo headless si lo tengo instalado; si hace falta instalar algo, decime qué y esperá mi OK.
```

**Tenés que ver:** las placas como imágenes, listas para pulir y publicar.

## Paso 3 · Generá imágenes coherentes (parte A)
Para que todas las imágenes parezcan de la misma marca, se escribe un **estilo fijo** una vez y se repite al principio de cada prompt.

```prompt
Leé marca/identidad-visual.md y mirá las placas de referencias/. Escribí un "estilo fijo" de 3 líneas para mis imágenes: paleta, luz, encuadre, textura y qué evitar. Guardalo en marca/identidad-visual.md. Después, para cada placa de contenido/carruseles/[TEMA].md que necesite imagen, escribí un prompt de imagen que empiece con ese estilo fijo, describa la escena en una frase y termine con: "sin texto en la imagen, sin logos, sin caras de personas reales".
```

Pegá esos prompts en la herramienta de imágenes que uses (la de Canva, ChatGPT o Gemini). Si querés más calidad y control, **Higgsfield** es una opción paga: mirá planes en [Stack y costos](#r-stack-y-costos).

> **Tip:** el texto lo ponés en Canva o en el HTML, nunca dentro de la imagen generada: la IA de imágenes todavía se equivoca con las letras.

**Tenés que ver:** imágenes que, puestas juntas, parecen de la misma marca.

## Paso 4 · Prepará la planilla (parte B)
El reporte lee una planilla de Google. Una fila por día o por semana y una columna por dato. Ejemplos de columnas:

| Tipo de negocio | Reporte | Columnas de la planilla (ejemplo) |
|---|---|---|
| Producción y reparto | Rentabilidad del mes | fecha, producto, unidades producidas, unidades vendidas, ventas en pesos, costo de insumos, costo de envases, otros costos |
| Venta consultiva | Cómo vinieron los leads | fecha, fuente del anuncio, equipo, leads, contactados, reuniones pactadas, ventas, horas hasta el primer contacto |
| Startup o marketplace | Qué sigue esta semana | tarea, área, responsable (rol), estado, fecha límite, objetivo de la semana |

¿No tenés la planilla todavía? Armá una de práctica. En el prompt, cambiá `[TIPO DE REPORTE]` y `[COLUMNAS]` por una fila de la tabla de arriba:

```prompt
Creá ejemplo-datos.csv con datos inventados de 8 semanas para este reporte: [TIPO DE REPORTE]. Usá estas columnas: [COLUMNAS]. Que los números sean creíbles, que haya una semana mala y un dato faltante, y aclarale en la primera fila de notas que son datos inventados.
```

Subilo a Google Sheets: [sheets.new](https://sheets.new) › **Archivo › Importar › Subir** (en inglés: **File › Import › Upload**). Ponele un nombre fácil, por ejemplo `Reporte semanal [TU EMPRESA]`.

**Tenés que ver:** la planilla en tu Google Drive, con los datos en la primera pestaña.

## Paso 5 · Instalá la skill y armá el primer reporte (parte B)
Esta skill se guarda **dentro de tu cerebro** (no en tu usuario), así viaja con tu repositorio de GitHub (privado) y la puede usar una tarea en la nube. En [Kit del taller](#r-kit) copiá `reporte-semanal` y pegala debajo de:

```prompt
Creá una skill de este proyecto llamada reporte-semanal: guardá el texto que pego abajo, exacto y sin cambios, en .claude/skills/reporte-semanal/SKILL.md dentro de esta carpeta. Sumá la línea reportes/ al .gitignore. Cuando termines, decime la ruta exacta.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

Salí con `/exit`, volvé a entrar con `claude` y escribí:

```prompt
/reporte-semanal
Quiero un reporte de [TIPO: RENTABILIDAD DEL MES / CÓMO VINIERON LOS LEADS / QUÉ SIGUE ESTA SEMANA]. Los datos están en la planilla de Google "[NOMBRE DE LA PLANILLA]".
```

La primera vez te hace unas preguntas (qué números mirar, contra qué comparar, a quién mandarlo) y guarda las respuestas en `operacion/reporte-semanal.md`. Después arma el primer reporte.

**Tenés que ver:** un resumen de menos de una pantalla. Controlá 2 números a mano contra la planilla antes de seguir.

## Paso 6 · Programalo para cada lunes (parte B)
Elegí dónde corre.

<div data-os="mac">

> **Tip:** en la tarea local, la Mac tiene que estar despierta a esa hora. Para que no se duerma sola, en Claude activá **Keep computer awake** (en **Settings › Desktop app** o **Settings › This computer › System**). Cerrar la tapa la duerme igual.

</div>
<div data-os="win">

> **Tip:** en la tarea local, la PC tiene que estar despierta a esa hora. Para que no se suspenda sola, en Claude activá **Keep computer awake** (en **Settings › Desktop app** o **Settings › This computer › System**).

</div>

### Opción A · En tu compu (app de escritorio)
Corre solo con la app de Claude abierta y la compu despierta. Si estaba dormida, corre una vez cuando se despierta.
1. En la app de escritorio, pestaña **Code**, abrí una sesión en tu carpeta del cerebro y pegá:

```prompt
Creá una tarea programada local llamada reporte-semanal, que corra todos los lunes a las [HORA, POR EJEMPLO 8:00], en esta carpeta, con estas instrucciones: "Usá la skill reporte-semanal con la configuración de operacion/reporte-semanal.md. Corré sin hacer preguntas: si falta algo, decilo en el reporte."
```

2. También se puede a mano: **Code › Scheduled › New task** (si aparece un menú, **Set up manually** o **Local**), con la frecuencia **Weekly**.
3. Abrí la tarea y tocá **Run now**. Si pide permisos, permitilos siempre, así los lunes no se frena.

### Opción B · En la nube (corre aunque la compu esté apagada)
Necesita tu cerebro en GitHub ([GitHub](#s4-github)) y un plan Pro o superior. Está en *research preview*: puede cambiar.
1. Subí la skill y la configuración al repositorio: en **GitHub Desktop**, escribí un mensaje (por ejemplo "Skill de reporte"), tocá **Commit to main** y después **Push origin**.
2. En Claude Code, en la carpeta del cerebro:

```prompt
/schedule todos los lunes a las [HORA] usá la skill reporte-semanal con la configuración de operacion/reporte-semanal.md, sin hacer preguntas, y mandame el resultado por Gmail a [TU MAIL]. No hagas commits ni cambies archivos del repositorio.
```

3. Claude te pregunta lo que falte (horario, repositorio) y la guarda. También podés crearla desde [claude.ai/code/routines](https://claude.ai/code/routines) › **New task**.
4. Revisá los conectores de la tarea: vienen todos los que tenés conectados. Dejá solo Google Drive y Gmail.

> **Ojo:** las tareas en la nube no ven tu compu: solo el repositorio y los conectores. Por eso la skill tiene que estar subida a GitHub y los datos tienen que estar en Google Sheets, no en un archivo local.

**Tenés que ver:** la tarea en la lista de **Scheduled** (local) o en [claude.ai/code/routines](https://claude.ai/code/routines) (nube), y una corrida de prueba con el reporte.

## Paso 7 · Probalo (parte B)
Tocá **Run now** en la tarea (o, en la nube, pedí `/schedule run`). Después cambiá un número en la planilla y corrélo otra vez.

**Tenés que ver:** el reporte con el número nuevo. Si configuraste Gmail, el mail en tu bandeja.

## Cómo sé que funcionó
- **Parte A:** tenés un carrusel en PNG que suena a vos y que solo necesitó retoques.
- **Parte B:** el lunes, sin tocar nada, el reporte aparece en el historial de la tarea (y en tu mail, si lo configuraste), con los números de la planilla.

Prueba del reporte, en Claude Code:

```prompt
Leé el último reporte y la planilla "[NOMBRE DE LA PLANILLA]". Decime si algún número del reporte no sale de la planilla y mostrame la cuenta de los 3 números principales.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude no ve Canva | Chat nuevo y revisá que Canva esté activado en los conectores de ese chat. Si sigue, desconectalo y conectalo de nuevo en **Customize › Connectors**. |
| Canva o la IA cambian el texto | Pedí "texto exacto, sin cambiar ni una palabra". Si insiste, usá el camino 2 (HTML): ahí el texto queda fijo. |
| Las imágenes no se parecen entre sí | Usá el mismo estilo fijo al principio de cada prompt y la misma herramienta para todas. |
| El reporte lee la pestaña equivocada | Poné los datos en la primera pestaña. El conector de Google Drive lee las planillas como CSV; no verificamos cómo maneja varias pestañas. |
| La tarea local no corrió el lunes | La app tiene que estar abierta y la compu despierta. En el historial de la tarea, al pasar el mouse por una corrida salteada, dice por qué. |
| La tarea en la nube no encuentra la skill | Te faltó subirla a GitHub (paso 6, opción B, punto 1). |
| No llega el mail | Fuera del modo automático, Claude pide aprobación antes de mandar. Abrí la corrida y aprobalo, o dejá el reporte solo en el historial. |

## Para seguir solo
- **Una tanda por semana.** Pedile 4 carruseles de una vez a partir de tu calendario de contenido y diseñalos en una sola sesión.
- **Que el reporte decida algo.** Sumá a `operacion/reporte-semanal.md` una regla: "si [DATO] baja más de [X]% contra la semana anterior, ponelo primero, como alerta, y proponé una acción".
- **Al celular.** Si preferís Telegram en vez de mail, armá en [n8n](#s6-n8n) un flujo que, cuando llega el mail del reporte, te lo reenvíe por [Telegram](#s7-telegram).
