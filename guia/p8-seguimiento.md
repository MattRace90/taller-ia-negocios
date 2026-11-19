---
titulo: Seguimiento a quien no compró
bloque: Tutorial
tiempo: 45 min
para: La Consejera del Éxito, Viajes TDH, Manuel Martínez Oratoria, Fondus
necesitas: s2-claude-code, p1-cerebro
resultado: Una planilla con cada persona que consultó y no compró, su segmento, 3 mensajes en tu voz y un aviso cada mañana con a quién escribirle hoy.
---

La mayoría de las consultas no compra en el primer contacto, y casi nadie las vuelve a llamar. Falta tiempo y falta saber qué decir.
Hoy Claude separa a cada persona según dónde quedó ("es caro", "lo pienso", preguntó el precio y no contestó), escribe 3 mensajes por grupo con tu voz y cada mañana te dice "hoy recontactá a estos 8". **Vos mandás los mensajes.**

## Antes de empezar
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).
- [ ] Tu cerebro con `marca/voz.md` y `ventas/objeciones.md` ([Armá el cerebro](#p1-cerebro)). Si están flojos, la skill te pregunta.
- [ ] La lista de quienes consultaron y no compraron (Paso 1). Con 20 o 30 alcanza.
- [ ] Una cuenta de Google para la planilla.

> **Datos:** los datos de tus clientes quedan en la planilla de Google y en una carpeta de trabajo **aparte**. **No** van al cerebro ni a GitHub. Pasale a Claude lo mínimo: nombre de pila, canal, contacto, qué consultó, fecha y cómo quedó. Nunca DNI, deudas, salud ni tarjetas.

## Paso 1 · Exportá a quienes no compraron
Juntalos en un archivo (CSV, Excel o texto; un **CSV** es una planilla guardada como texto). Idealmente con nombre, contacto, canal, qué consultó, fecha y cómo quedó.

| Dónde están | Cómo sacarlos |
|---|---|
| Google Sheets o Excel | **Archivo › Descargar › Valores separados por comas (.csv)** o **Guardar como** › CSV. |
| WhatsApp Business | No exporta la lista. Armala a mano en una planilla mirando chats y etiquetas (unos 20 min para 30 contactos). |
| Un CRM (dlastcrm u otro) | **Exportar** en la lista de contactos u oportunidades, filtrando "perdida" o "sin respuesta". |
| MailerLite o Contactos de Google | Usá su opción de exportar y sumá a mano una columna con cómo quedó cada uno. |

**Tenés que ver:** un archivo con al menos 20 personas en tu carpeta **Descargas**.

## Paso 2 · Armá la carpeta de trabajo
Va **fuera** del cerebro, para que los datos de clientes nunca terminen en GitHub.
1. En **Documentos**, creá la carpeta `seguimiento-[TU-EMPRESA]` (con Finder o el Explorador de archivos).
2. App de Claude › **Code** › **Local** › **Open folder…** › elegí `seguimiento-[TU-EMPRESA]`.
3. Pegá:

```prompt
Creá las carpetas entrada y salida. Mové a entrada/ el archivo [NOMBRE-DEL-ARCHIVO] que está en mi carpeta Descargas.
```

**Tenés que ver:** `entrada/` con tu archivo adentro.

## Paso 3 · Instalá la skill "seguimiento"
En el [Kit del taller](#r-kit) tocá **Copiar** en `seguimiento` y pegala debajo de:

```prompt
Creá una skill personal llamada seguimiento. Guardá el texto que pego abajo, exacto y sin cambios, en la carpeta de skills de mi usuario (.claude/skills/seguimiento/SKILL.md dentro de mi carpeta de usuario). Decime la ruta.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

Tocá **Permitir** cuando pida permiso.

**Tenés que ver:** al escribir `/` aparece `seguimiento`. Si no, abrí una sesión nueva en la misma carpeta.

## Paso 4 · Segmentá por dónde quedó cada persona

```prompt
/seguimiento
Mi cerebro es la carpeta cerebro-[TU-EMPRESA] en Documentos. Los contactos están en entrada/. Segmentalos según dónde quedó cada persona y mostrame cuántos hay por grupo antes de escribir mensajes.
```

Claude lee tu voz y tus objeciones (si pide permiso para leer fuera de la carpeta, aceptá) y propone grupos: preguntó el precio y no respondió · tuvo una objeción (una por cada objeción de tu cerebro) · pidió info y desapareció · compró una vez y no volvió · sin datos.

Si alguien está mal ubicado: "[NOMBRE] no dijo que es caro, viaja el año que viene. Movelo a [SEGMENTO]".

**Tenés que ver:** una tabla con los segmentos y cuántas personas hay en cada uno.

## Paso 5 · Escribí 3 mensajes por segmento
Contestá **"ok, escribí los mensajes"**. Para cada segmento: día 1, día 3 y día 7, con tu voz.

Ejemplo inventado, segmento "es caro":
- **Día 1:** "Hola {nombre}, me quedé pensando en lo del precio. ¿Te sirve si te paso cómo queda en cuotas?"
- **Día 3:** "{nombre}, te comparto lo que nos dijo alguien que también dudaba: [TESTIMONIO REAL]."
- **Día 7:** "{nombre}, no te escribo más por esto. Si querés retomarlo, respondeme 'sí'."

Corregilo como a un vendedor nuevo: "más corto", "no digas 'estimado'".

> **Ojo:** la skill no inventa testimonios, descuentos ni fechas límite: deja un hueco entre corchetes. Tampoco promete lo que tu cerebro prohíbe.

**Tenés que ver:** `mensajes.md` con 3 mensajes por segmento. Si te ofrece copiar los modelos (sin datos de nadie) a `ventas/seguimiento.md` de tu cerebro, decile que sí.

## Paso 6 · Armá la planilla
Claude te pregunta **cuántas personas podés recontactar por día** y reparte las fechas. Escribe `salida/planilla-seguimiento.csv` con: nombre, canal, contacto, segmento, las 3 fechas de envío (`envio_1` a `envio_3`), las 3 columnas `enviado_` vacías (las completás vos), `estado` y los 3 mensajes con el nombre puesto.

Subila a Google Sheets: [sheets.new](https://sheets.new) › **Archivo › Importar › Subir** (en inglés: **File › Import › Upload**) › elegí el CSV › **Importar datos**. Nombre: `Seguimiento [TU EMPRESA]`.

**Tenés que ver:** una fila por persona con las fechas completas.

> **Datos:** con la planilla en Google Sheets, pedile a Claude "Borrá los archivos de entrada/". No conviene tener copias sueltas.

## Paso 7 · El aviso de cada mañana
Corre en tu compu: con la app de Claude **abierta** y la compu **despierta**. Si estaba dormida, corre una vez al despertar.
1. Conectá **Google Drive** en **Customize › Connectors** ([Conectores](#s8-conectores-y-mcp)).
2. En la pestaña **Code**, en `seguimiento-[TU-EMPRESA]`, pegá:

```prompt
Creá una tarea programada local llamada recontactar-hoy, de lunes a viernes a las [HORA, ej. 8:30], en esta carpeta, con estas instrucciones: "Abrí con el conector de Google Drive la planilla [NOMBRE DE TU PLANILLA]. Buscá las filas con estado 'en seguimiento' que tengan una fecha de envío de hoy o anterior y el enviado correspondiente vacío. Ordenalas de la más atrasada a la más nueva. Mostrá como máximo [CANTIDAD]: nombre, canal, contacto, qué mensaje toca y el texto listo para copiar. Empezá con 'Hoy recontactá a estas N personas'. No mandes mensajes ni modifiques la planilla."
```

3. Abrí la tarea en **Scheduled** y tocá **Run now**. Si pide permisos, elegí permitir siempre.

**Tenés que ver:** la tarea `recontactar-hoy` en **Scheduled** y una corrida con la lista de hoy.

> **Tip:** ¿lo querés en el celular aunque la compu esté apagada? Armalo en [n8n](#s6-n8n) + [Telegram](#s7-telegram): Schedule Trigger › Google Sheets › Filter › Telegram.

## Paso 8 · Mandá y anotá
El envío es **manual**: copiás el mensaje, lo mandás desde tu WhatsApp o mail y ponés la fecha en `enviado_`. Si responde: `estado` = "respondió". Si compra: "compró". Si pide que no le escriban: "no molestar", y se respeta.

**Tenés que ver:** la fecha en `enviado_1` de cada persona a la que le escribiste hoy.

> **Ojo:** mandar mensajes automáticos desde un WhatsApp común puede hacer que te bloqueen el número. Para automatizar el envío hace falta la vía oficial ([WhatsApp](#w1-opciones)) o un CRM como **dlastcrm**.

## Cómo sé que funcionó
- La planilla tiene segmento, fechas y los 3 mensajes por persona.
- El **Run now** te muestra a quién escribirle hoy.
- Prueba de la voz:

```prompt
Leé mensajes.md y decime si cada mensaje suena a nosotros según marca/voz.md de mi cerebro. Marcá las palabras que nunca usaríamos y proponé un cambio.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Casi todos quedan en "sin datos" | Falta la columna de cómo quedó cada uno. Sumala a mano (3 o 4 palabras por persona) y corré `/seguimiento` de nuevo. |
| Los mensajes no suenan a vos | Pegale 2 o 3 mensajes reales tuyos (sin datos de clientes): "Reescribí todo con este estilo y guardalo en marca/voz.md". |
| No encuentra tu cerebro | Pedí: "Buscá la carpeta cerebro-[TU-EMPRESA] en Documentos y usá esa ruta". |
| La tarea no corrió | La app tiene que estar abierta y la compu despierta. En el historial de la tarea dice por qué se salteó. |
| La tarea no lee la planilla | Revisá Google Drive en **Customize › Connectors** y que el nombre de la planilla sea exacto. |

## Para seguir solo
- **Medí qué segmento responde más:** a fin de mes, pedile a Claude que lea la planilla y cuente respuestas y ventas por segmento y por mensaje.
- **Clientes viejos:** una vez por mes, sumá a quienes compraron hace más de [X] meses, con un mensaje sobre lo próximo.
- **Del manual al automático:** cuando funcione un mes a mano, el envío se puede pasar a **dlastcrm** con los mismos segmentos y mensajes.
