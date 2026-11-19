---
titulo: "'Extras: placas en tu voz y el reporte que llega solo'"
bloque: Tutorial
tiempo: 50 min (2 tutoriales de 25 min)
para: La Consejera del Éxito (placas) · Denvet, Fondus y Celve (reporte) · sirven para todos
necesitas: s2-claude-code, p1-cerebro, s8-conectores-y-mcp
resultado: Un carrusel armado con tu voz y tu estilo, listo para pulir; y un resumen semanal que se arma solo cada lunes a partir de una planilla.
---

Dos tutoriales cortos e independientes. Hacé el que más te sirva o los dos.
**Parte A · Placas en tu voz (pasos 1 a 3):** Claude escribe el carrusel con tu forma de hablar, lo diseña con tu estilo y vos pulís.
**Parte B · El reporte que llega solo (pasos 4 a 7):** cada lunes, sin que nadie lo pida, Claude lee una planilla y te arma el resumen.

## Antes de empezar
- [ ] La app de escritorio de Claude: pestaña **Code** › **Local** › **Open folder…** › tu carpeta `cerebro-[TU-EMPRESA]` ([Instalá Claude Code](#s2-claude-code)).
- [ ] Tu cerebro con `marca/voz.md` y, para la parte A, `marca/identidad-visual.md` ([Armá el cerebro](#p1-cerebro)).
- [ ] Parte A: una cuenta de Canva y 3 placas tuyas que te gusten, guardadas en `referencias/` dentro del cerebro.
- [ ] Parte B: una planilla de Google con al menos 4 semanas de datos (o armamos una inventada en el Paso 4).
- [ ] Parte B: Google Drive conectado en **Customize › Connectors** ([Conectores](#s8-conectores-y-mcp)). Opcional: Gmail.

> **Datos:** las placas no necesitan datos de clientes; no uses fotos ni testimonios sin permiso. La planilla del reporte lleva números del negocio, no datos personales.

## Paso 1 · Escribí el guion del carrusel (parte A)
En la pestaña **Code**, en tu cerebro:

```prompt
Leé marca/voz.md y marca/identidad-visual.md y mirá las placas de referencias/. Escribí un carrusel de Instagram de [CANTIDAD, ej. 6] placas sobre [TEMA]. Para cada placa: el texto exacto (máximo 20 palabras, con mi forma de hablar), qué va en la imagen y dónde va el texto. La primera frena el scroll; la última invita a [ACCIÓN: ESCRIBIR POR WHATSAPP, COMENTAR, ENTRAR AL LINK]. Guardalo en contenido/carruseles/[TEMA].md.
```

Corregí hasta que suene a vos ("esto no lo diría nunca", "más corto"). Lo que vale para siempre: "guardalo en marca/voz.md".

**Tenés que ver:** el texto de cada placa, en tu voz.

## Paso 2 · Diseñalo (parte A)
**Camino 1 · Con el conector de Canva.** Conectalo en **Customize › Connectors** › **Canva** › **Connect**. Después, en la misma sesión:

```prompt
Con Canva, diseñá un carrusel de Instagram con el guion de contenido/carruseles/[TEMA].md: una placa por parte, con el texto exacto, sin cambiar ni una palabra. Usá mi kit de marca de Canva si tengo; si no, los colores y la tipografía de marca/identidad-visual.md. Mostrame las opciones antes de elegir.
```

Abrí la opción que te guste en Canva para pulir. Para bajarla: "Exportá ese diseño en PNG".

> **Ojo:** si Canva devuelve una sola placa, pedí las siguientes de a una: "Ahora la placa 2, mismo estilo". Si Claude no ve Canva en la pestaña Code, hacelo en un **chat** nuevo: adjuntá el archivo del guion con el **+** y pegá el mismo pedido. Fuente: [Ayuda de Canva](https://www.canva.com/help/connect-claude-to-canva/) (18/11/2026).

**Camino 2 · Como página web que Claude pasa a PNG.** Control total del texto:

```prompt
Con el guion de contenido/carruseles/[TEMA].md, armá el carrusel como HTML: una placa de 1080 x 1350 por parte, con mis colores, tipografías y logo de marca/identidad-visual.md y el texto exacto. Abrilo para que lo vea. Cuando te diga que está bien, exportá cada placa a PNG en contenido/carruseles/[TEMA]/. Si hace falta instalar algo, decime qué y esperá mi OK.
```

**Tenés que ver:** las placas como imágenes, listas para pulir y publicar.

## Paso 3 · Generá imágenes coherentes (parte A)

```prompt
Escribí un "estilo fijo" de 3 líneas para mis imágenes (paleta, luz, encuadre, textura, qué evitar) según marca/identidad-visual.md y referencias/, y guardalo ahí. Después, para cada placa de contenido/carruseles/[TEMA].md que necesite imagen, escribí un prompt que empiece con ese estilo y termine con: "sin texto, sin logos, sin caras de personas reales".
```

Pegá esos prompts en tu herramienta de imágenes (Canva, ChatGPT, Gemini o, pago, **Higgsfield**: [Stack y costos](#r-stack-y-costos)). El texto va en Canva o en el HTML, nunca dentro de la imagen.

**Tenés que ver:** imágenes que juntas parecen de la misma marca.

## Paso 4 · Prepará la planilla (parte B)
Una fila por día o semana, una columna por dato. Ejemplos:

| Tipo de negocio | Reporte | Columnas (ejemplo) |
|---|---|---|
| Producción y reparto | Rentabilidad del mes | fecha, producto, unidades vendidas, ventas en pesos, costo de insumos, otros costos |
| Venta consultiva | Cómo vinieron los leads | fecha, fuente, leads, contactados, reuniones, ventas, horas hasta el primer contacto |
| Startup o marketplace | Qué sigue esta semana | tarea, área, responsable (rol), estado, fecha límite |

¿No tenés planilla? Armá una de práctica:

```prompt
Creá ejemplo-datos.csv con datos inventados de 8 semanas para este reporte: [TIPO DE REPORTE]. Columnas: [COLUMNAS]. Números creíbles, una semana mala y un dato faltante. Aclará en una nota que son inventados.
```

Subila: [sheets.new](https://sheets.new) › **Archivo › Importar › Subir** (**File › Import › Upload**). Nombre: `Reporte semanal [TU EMPRESA]`.

**Tenés que ver:** la planilla en tu Drive, con los datos en la primera pestaña.

## Paso 5 · Instalá la skill y armá el primer reporte (parte B)
Va **dentro de tu cerebro**, así viaja con tu repositorio de GitHub. En el [Kit del taller](#r-kit) copiá `reporte-semanal` y pegala debajo de:

```prompt
Creá una skill de este proyecto llamada reporte-semanal: guardá el texto que pego abajo, exacto y sin cambios, en .claude/skills/reporte-semanal/SKILL.md. Sumá reportes/ al .gitignore. Decime la ruta.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

Abrí una sesión nueva en la misma carpeta y escribí:

```prompt
/reporte-semanal
Quiero un reporte de [RENTABILIDAD DEL MES / CÓMO VINIERON LOS LEADS / QUÉ SIGUE ESTA SEMANA]. Los datos están en la planilla de Google "[NOMBRE DE LA PLANILLA]".
```

La primera vez te pregunta qué mirar y contra qué comparar, y lo guarda en `operacion/reporte-semanal.md`.

**Tenés que ver:** un resumen de menos de una pantalla. Controlá 2 números a mano contra la planilla.

## Paso 6 · Programalo para cada lunes (parte B)
**Opción A · En tu compu.** Corre con la app abierta y la compu despierta (activá **Keep computer awake** en la configuración de la app; cerrar la tapa la duerme igual). En la pestaña **Code**, en tu cerebro:

```prompt
Creá una tarea programada local llamada reporte-semanal, todos los lunes a las [HORA, ej. 8:00], en esta carpeta, con estas instrucciones: "Usá la skill reporte-semanal con la configuración de operacion/reporte-semanal.md. Corré sin hacer preguntas: si falta algo, decilo en el reporte."
```

**Opción B · En la nube** (corre con la compu apagada; plan Pro o superior; *research preview*). Necesita tu cerebro en GitHub ([GitHub](#s4-github)):
1. En **GitHub Desktop**: mensaje "Skill de reporte" › **Commit to main** › **Push origin**.
2. En la pestaña **Code**:

```prompt
/schedule todos los lunes a las [HORA] usá la skill reporte-semanal con la configuración de operacion/reporte-semanal.md, sin hacer preguntas, y mandame el resultado por Gmail a [TU MAIL]. No hagas commits ni cambies archivos del repositorio.
```

3. En los conectores de la tarea, dejá solo Google Drive y Gmail.

> **Ojo:** la tarea en la nube no ve tu compu: solo el repositorio y los conectores. Por eso la skill va a GitHub y los datos a Google Sheets.

**Tenés que ver:** la tarea en **Scheduled** (local) o en [claude.ai/code/routines](https://claude.ai/code/routines) (nube).

## Paso 7 · Probalo (parte B)
Tocá **Run now** en la tarea. Cambiá un número en la planilla y corrélo otra vez.

**Tenés que ver:** el reporte con el número nuevo (y el mail, si configuraste Gmail).

## Cómo sé que funcionó
- **Parte A:** un carrusel en PNG que suena a vos y solo necesitó retoques.
- **Parte B:** el lunes, sin tocar nada, el reporte aparece en el historial de la tarea. Prueba:

```prompt
Leé el último reporte y la planilla "[NOMBRE DE LA PLANILLA]". Decime si algún número no sale de la planilla y mostrame la cuenta de los 3 principales.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude no ve Canva | Sesión nueva. Si sigue, desconectalo y conectalo en **Customize › Connectors**. |
| Canva cambia el texto | Pedí "texto exacto". Si insiste, usá el camino 2 (HTML). |
| El reporte lee la pestaña equivocada | Poné los datos en la primera pestaña. |
| La tarea local no corrió | App abierta y compu despierta. El historial de la tarea dice por qué se salteó. |
| La tarea en la nube no encuentra la skill | Faltó subirla a GitHub (Paso 6, opción B). |
| No llega el mail | Claude pide aprobación antes de mandar. Abrí la corrida y aprobalo, o dejá el reporte en el historial. |

## Para seguir solo
- **Una tanda por semana:** 4 carruseles de una vez a partir de tu calendario.
- **Que el reporte decida algo:** sumá a `operacion/reporte-semanal.md` "si [DATO] baja más de [X]%, ponelo primero como alerta y proponé una acción".
- **Al celular:** un flujo de [n8n](#s6-n8n) que reenvíe el mail del reporte por [Telegram](#s7-telegram).
