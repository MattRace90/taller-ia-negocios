---
titulo: Seguimiento a quien no compró
bloque: Tutorial
tiempo: 45 a 60 min
para: La Consejera del Éxito, Viajes TDH, Manuel Martínez Oratoria, Fondus
necesitas: s2-claude-code, p1-cerebro
resultado: Una planilla con cada persona que consultó y no compró, su segmento, 3 mensajes en tu voz y un aviso cada mañana con a quién escribirle hoy.
---

La mayoría de las consultas no compra en el primer contacto, y casi nadie las vuelve a llamar. No es falta de ganas: es falta de tiempo y de saber qué decir.
Hoy vas a armar el sistema: Claude separa a cada persona según dónde quedó (preguntó el precio y no contestó, dijo "es caro", compró una vez y no volvió), escribe 3 mensajes por grupo en la voz de tu marca y cada mañana te dice "hoy recontactá a estos 8". **Vos mandás los mensajes.**

## Antes de empezar
- [ ] Claude Code instalado y con tu sesión iniciada ([Instalá Claude Code](#s2-claude-code)).
- [ ] Tu cerebro con `marca/voz.md` y `ventas/objeciones.md` ([Armá el cerebro](#p1-cerebro)). Si están flojos, la skill te hace preguntas.
- [ ] La lista de personas que consultaron y no compraron (el paso 1 explica cómo sacarla). Con 20 o 30 alcanza para practicar.
- [ ] Una cuenta de Google para la planilla.
- [ ] Para el aviso de cada mañana: la app de escritorio de Claude con la pestaña **Code**, o [n8n](#s6-n8n) y [Telegram](#s7-telegram).

> **Datos:** los nombres y teléfonos de tus clientes quedan en la planilla de Google y en una carpeta de trabajo **aparte**. **No** van al cerebro ni a GitHub. A Claude pasale lo mínimo: nombre de pila, canal, teléfono o mail, qué consultó, la fecha y cómo quedó. Nunca DNI, deudas, situación crediticia, datos de salud ni datos de tarjetas.

## Paso 1 · Exportá a quienes no compraron
Juntá todo en un archivo (CSV, Excel o texto). Un **CSV** es una planilla guardada como texto. No importa el formato: la skill lo ordena. Lo ideal es que tenga nombre, contacto, canal, qué consultó, fecha del último contacto y cómo quedó.

| Dónde están tus contactos | Cómo sacarlos (en general) |
|---|---|
| Una planilla (Google Sheets o Excel) | Google Sheets: **Archivo › Descargar › Valores separados por comas (.csv)**. Excel: **Guardar como** › CSV. |
| MailerLite | En **Subscribers** (Suscriptores), filtrá el grupo o segmento y usá la opción de exportar. No lo verificamos paso a paso: si no la encontrás, buscá "export subscribers" en la ayuda de MailerLite. |
| WhatsApp Business | No tiene un botón para exportar la lista con cómo quedó cada uno. Dos caminos: (a) armá la lista a mano en una planilla mirando tus chats y etiquetas (unos 20 minutos para 30 contactos); (b) exportá chats puntuales con **Exportar chat** › **Sin archivos** (en el menú del chat en Android, o tocando el nombre del contacto en iPhone) para que Claude lea dónde quedó la conversación. |
| Un CRM (dlastcrm u otro) | Buscá **Exportar** en la lista de contactos u oportunidades y filtrá por "perdida" o "sin respuesta". Si no sabés si se puede, preguntale a quien lo administra o a soporte. |
| Contactos de Google | En [contacts.google.com](https://contacts.google.com), **Exportar** › CSV de Google. Ojo: ahí no dice cómo quedó cada uno; sumalo a mano en una columna. |

**Tenés que ver:** un archivo con al menos 20 personas que no compraron.

## Paso 2 · Armá la carpeta de trabajo
Esta carpeta va **fuera** de tu carpeta del cerebro, para que los datos de clientes nunca terminen en GitHub.

<div data-os="mac">

1. En **Finder › Documentos** creá la carpeta `seguimiento-[TU-EMPRESA]` y, adentro, `entrada` y `salida`.
2. Copiá tu archivo exportado en `entrada`.
3. Abrí la **Terminal** (**Cmd + Espacio**, escribí `Terminal` y Enter) y escribí:

```bash
cd ~/Documents/seguimiento-[TU-EMPRESA]
claude
```

</div>
<div data-os="win">

1. En el **Explorador de archivos › Documentos** creá la carpeta `seguimiento-[TU-EMPRESA]` y, adentro, `entrada` y `salida`.
2. Copiá tu archivo exportado en `entrada`.
3. Abrí **PowerShell** (tecla **Windows**, escribí `PowerShell` y Enter) y escribí:

```powershell
cd $HOME\Documents\seguimiento-[TU-EMPRESA]
claude
```

</div>

**Tenés que ver:** Claude Code abierto en `seguimiento-[TU-EMPRESA]`.

## Paso 3 · Instalá la skill "seguimiento"
Una **skill** es una receta escrita que Claude sigue siempre igual. En [Kit del taller](#r-kit) (abrilo en otra pestaña) tocá **Copiar** en la skill `seguimiento` y pegala debajo de este prompt. En Windows, `[MI-USUARIO]` es tu usuario de Windows; si no lo sabés, dejalo así: Claude Code lo averigua.

```prompt
Creá una skill personal llamada seguimiento. Guardá el texto que pego abajo, exacto y sin cambios, en el archivo SKILL.md de la carpeta de skills de mi usuario (~/.claude/skills/seguimiento/SKILL.md; en Windows es C:\Users\[MI-USUARIO]\.claude\skills\seguimiento\SKILL.md). Cuando termines, decime la ruta exacta donde quedó.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

Aceptá el permiso, salí con `/exit` y volvé a entrar con `claude`.

**Tenés que ver:** si escribís `/` aparece `seguimiento` en la lista.

## Paso 4 · Segmentá por dónde quedó cada persona

```prompt
/seguimiento
Mi cerebro está en la carpeta [RUTA DE TU CARPETA DEL CEREBRO, POR EJEMPLO ~/Documents/cerebro-miempresa]. Los contactos están en entrada/. Segmentalos según dónde quedó cada persona y mostrame cuántos hay en cada grupo antes de escribir los mensajes.
```

Claude va a leer tu voz y tus objeciones (te puede pedir permiso para leer fuera de la carpeta: aceptá) y te propone grupos como estos:

| Segmento | Quiénes son |
|---|---|
| Preguntó el precio y no respondió | Recibió el precio o el presupuesto y no contestó más. |
| Tuvo una objeción | Uno por cada objeción de tu cerebro: "es caro", "no confío", "lo tengo que pensar", "lo consulto con mi pareja". |
| Pidió información y desapareció | Nunca llegó a ver el precio. |
| Compró una vez y no volvió | Cliente viejo, ideal para la próxima salida, curso o nivel. |
| Sin datos suficientes | No se sabe dónde quedó. Lo decidís vos. |

Si una persona está mal ubicada, decíselo: "[NOMBRE] no tuvo una objeción de precio, dijo que viaja el año que viene. Movelo a [SEGMENTO]".

**Tenés que ver:** una tabla con los segmentos y cuántas personas hay en cada uno.

## Paso 5 · Escribí 3 mensajes por segmento
Contestá **"ok, escribí los mensajes"**. Para cada segmento, Claude escribe un mensaje para el día 1, otro para el día 3 y otro para el día 7, con tu voz y con la respuesta a la objeción que figura en tu cerebro.

Ejemplo para el segmento "es caro" (inventado, para un curso):
- **Día 1:** "Hola {nombre}, ¿cómo estás? Me quedé pensando en lo que me dijiste del precio. ¿Te sirve si te paso cómo queda en cuotas?"
- **Día 3:** "{nombre}, te comparto lo que nos dijo alguien que también dudaba por el precio: [TESTIMONIO REAL]. ¿Querés que te guarde un lugar para el próximo grupo?"
- **Día 7:** "{nombre}, no te escribo más por esto para no llenarte el chat. Si más adelante querés retomarlo, respondeme con un 'sí' y te paso todo."

Corregilo como corregirías a un vendedor nuevo: "más corto", "no digas 'estimado'", "en el día 3 no menciones cuotas".

> **Ojo:** la skill no inventa testimonios, descuentos ni fechas límite. Si no están en tu cerebro, deja un hueco entre corchetes para que lo completes. Tampoco promete lo que tu cerebro prohíbe (por ejemplo, si tu cerebro dice que tu producto no es un préstamo, nunca lo presenta así).

**Tenés que ver:** un archivo `mensajes.md` con 3 mensajes por segmento. Claude te ofrece copiar esos modelos (sin datos de nadie) a `ventas/seguimiento.md` de tu cerebro: decile que sí.

## Paso 6 · Armá la planilla de seguimiento
Claude te pregunta **cuántas personas podés recontactar por día** y reparte las fechas para no pasarte. Después escribe `salida/planilla-seguimiento.csv` con estas columnas:

`id · nombre · canal · contacto · segmento · motivo · envio_1 · enviado_1 · envio_2 · enviado_2 · envio_3 · enviado_3 · estado · mensaje_1 · mensaje_2 · mensaje_3 · notas`

- `envio_1`, `envio_2`, `envio_3`: cuándo toca cada mensaje (día 1, 3 y 7).
- `enviado_1`, `enviado_2`, `enviado_3`: vacías. Las completás vos con la fecha cuando mandás.
- `estado`: arranca en "en seguimiento". Lo cambiás a "respondió", "compró" o "no molestar".
- `mensaje_1` a `mensaje_3`: el texto listo para copiar, con el nombre ya puesto.

Subila a Google Sheets:
1. Abrí [sheets.new](https://sheets.new) y ponele de nombre `Seguimiento [TU EMPRESA]`.
2. **Archivo › Importar › Subir** (en inglés: **File › Import › Upload**), elegí `planilla-seguimiento.csv`, reemplazá la hoja actual y tocá **Importar datos**.

**Tenés que ver:** la planilla con una fila por persona y las fechas de envío completas.

> **Datos:** cuando la planilla esté en Google Sheets, borrá los archivos exportados de `entrada/`. La información ya está en la planilla y no conviene tener copias sueltas.

## Paso 7 · El aviso de cada mañana
Elegí una de las dos opciones.

### Opción A · Tarea programada de Claude
Corre en tu compu: solo funciona con la app de escritorio de Claude **abierta** y la compu **despierta**. Si la compu estaba dormida a esa hora, corre una vez cuando se despierta.

1. Conectá **Google Drive** en Claude: **Customize › Connectors** ([Conectores](#s8-conectores-y-mcp)). Así Claude puede leer tu planilla.
2. En la app de escritorio, pestaña **Code**, abrí una sesión en la carpeta `seguimiento-[TU-EMPRESA]` y pegá:

```prompt
Creá una tarea programada local llamada recontactar-hoy, que corra de lunes a viernes a las [HORA, POR EJEMPLO 8:30], en esta carpeta, con estas instrucciones: "Abrí con el conector de Google Drive la planilla [NOMBRE DE TU PLANILLA]. Usá la fecha de hoy. Buscá las filas con estado 'en seguimiento' que tengan una fecha en envio_1, envio_2 o envio_3 igual o anterior a hoy y el enviado correspondiente vacío. Ordenalas de la más atrasada a la más nueva. Mostrá como máximo [CANTIDAD POR DÍA]: nombre, canal, contacto, qué mensaje toca (1, 2 o 3) y el texto listo para copiar. Empezá con una línea: 'Hoy recontactá a estas N personas'. No mandes mensajes a nadie y no modifiques la planilla."
```

3. Si preferís hacerlo a mano: pestaña **Code › Scheduled › New task**. Si aparece un menú, elegí **Set up manually** (o **Local**). Completá el nombre, las instrucciones (el texto entre comillas de arriba), la carpeta y, en la frecuencia, **Weekdays**.
4. Abrí la tarea y tocá **Run now**. Si Claude pide permisos, elegí la opción de permitir siempre: así las próximas corridas no se frenan.

**Tenés que ver:** en **Scheduled**, la tarea `recontactar-hoy`; y en su historial, una corrida con la lista de hoy.

> **Tip:** ¿querés que la lista te llegue por mail? Conectá **Gmail** y sumá a las instrucciones: "Mandame la lista por Gmail a [TU MAIL]". Claude pide aprobación antes de cada envío, salvo en modo automático: probalo con **Run now**. Si cada mañana queda frenada esperando tu OK, sacá esa línea y usá la opción B.

### Opción B · n8n + Telegram
Te llega al celular aunque la compu esté apagada (si tu n8n está en la nube) y no usa IA: es una regla fija. Armala siguiendo [n8n](#s6-n8n) y [Telegram](#s7-telegram) con estos nodos:
1. **Schedule Trigger**: de lunes a viernes a la hora que elijas.
2. **Google Sheets**: leer las filas de tu planilla de seguimiento.
3. **Filter** (o **Code**): quedarse con las filas en "en seguimiento" que tienen una fecha de envío de hoy o anterior y el enviado vacío.
4. **Telegram**: mandarte un mensaje con la lista y los textos.

**Tenés que ver:** un mensaje en tu Telegram con la lista del día.

## Paso 8 · Mandá y anotá
El envío sigue siendo **manual**: copiás el mensaje de la planilla o del aviso, lo mandás desde tu WhatsApp o tu mail y ponés la fecha en `enviado_1`, `enviado_2` o `enviado_3`.
- Si responde: `estado` = "respondió". No le llega ningún mensaje más de la secuencia.
- Si compra: "compró". Si pide que no le escriban: "no molestar", y se respeta.

**Tenés que ver:** en la planilla, la fecha puesta en `enviado_1` de cada persona a la que le escribiste hoy.

> **Ojo:** mandar mensajes automáticos desde un WhatsApp común puede hacer que te bloqueen el número. Para automatizar el envío más adelante hace falta la vía oficial ([WhatsApp](#w1-opciones)) o un CRM que lo haga bien, como **dlastcrm**, el CRM que usamos en la agencia.

## Cómo sé que funcionó
- La planilla tiene una fila por persona, con segmento, fechas y los 3 mensajes con el nombre ya puesto.
- El aviso de mañana (o un **Run now** hoy) te muestra a quién escribirle.
- Mandaste los primeros 3 mensajes y anotaste la fecha.

Prueba de la voz, en Claude Code:

```prompt
Leé mensajes.md y decime, para cada mensaje, si suena a nosotros según marca/voz.md de mi cerebro. Marcá las palabras que nunca usaríamos y proponé un cambio.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Casi todos quedaron en "sin datos suficientes" | Al exportado le falta la columna de cómo quedó cada uno. Sumala a mano (alcanza con 3 o 4 palabras por persona) y corré `/seguimiento` de nuevo. |
| Los mensajes no suenan a vos | Pegale a Claude 2 o 3 mensajes reales tuyos (sin nombres ni teléfonos de clientes) y pedile: "Reescribí todo con este estilo y guardá lo aprendido en marca/voz.md de mi cerebro". |
| Claude no encuentra tu cerebro | Pasale la ruta completa de la carpeta. En Windows, por ejemplo: `C:\Users\[MI-USUARIO]\Documents\cerebro-[TU-EMPRESA]`. |
| La tarea programada no corrió | La app de Claude tiene que estar abierta y la compu despierta. Mirá el historial de la tarea en **Scheduled**: al pasar el mouse por una corrida salteada, dice por qué. |
| La tarea no lee la planilla | Revisá que Google Drive esté conectado en **Customize › Connectors** y que el nombre de la planilla sea exacto. |
| Le escribí dos veces a la misma persona | Faltó anotar la fecha en `enviado_`. El aviso solo sabe lo que dice la planilla. |

## Para seguir solo
- **Medí qué segmento responde más.** A fin de mes, pedile a Claude que lea la planilla y te diga cuántos respondieron y compraron por segmento y por mensaje. Reescribí el que peor funciona.
- **Clientes que ya compraron.** Una vez por mes, sumá a la planilla a quienes compraron hace más de [X] meses, con un mensaje sobre lo próximo (una salida grupal, el nivel 2, el nuevo grupo).
- **Del manual al automático.** Cuando el sistema funcione un mes a mano, el envío se puede pasar a **dlastcrm** con los mismos segmentos y mensajes.
