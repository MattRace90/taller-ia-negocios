---
titulo: "'Tareas programadas: que Claude trabaje solo'"
bloque: Teoría
tiempo: 30 min
para: Todos
necesitas: t3-donde-trabajar
resultado: Sabés elegir dónde programar una tarea, creaste una de prueba desde la app que corre los lunes a las 9 y sabés ver sus ejecuciones y pausarla.
---

Una tarea programada es un pedido que Claude hace solo, cuando vos le digas: todos los lunes a las 9, cada hora, una vez el jueves que viene. Es el "reporte que llega solo".
Ejemplo: Fondus recibe cada lunes a las 9 un resumen de las consultas de la semana, cuáles quedaron sin respuesta y a quién llamar primero. Nadie lo arma: lo arma Claude. Todo se hace desde la app de Claude, con botones.

> **Datos:** verificado en la documentación oficial el 18 y 19/11/2026. Las tareas en la nube están en "research preview": pueden cambiar. Antes se llamaban **Routines**: si tu app dice **Routines** / **New routine**, es lo mismo que **Scheduled** / **New task**.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude.
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)) y la carpeta de tu cerebro (`Documentos/cerebro-[TU-EMPRESA]`, [Tu cerebro](#p1-cerebro)).
- [ ] Para la nube: tu cerebro subido a [GitHub](#s4-github).
- [ ] Una tarea que ya hiciste a mano y salió bien. **Nunca programes algo que no viste funcionar.**

## Dónde programar
| Opción | Dónde corre | Compu prendida | Toca archivos de tu compu | Ideal para |
|---|---|---|---|---|
| **A · Pestaña Code › Scheduled** (tarea local) | Tu compu | Sí, con la app abierta | Sí | Lo del taller: tareas sobre tu cerebro y tus archivos |
| **B · Cowork › Scheduled** | Nube, salvo que elijas una carpeta | No (sí, si elegís una carpeta) | Solo si elegís una carpeta | Informes y resúmenes de oficina con tus conectores |
| **C · Claude Code en la nube** (`/schedule` o **Scheduled › Cloud**) | Nube de Anthropic | No | No: trabaja sobre tu repo de GitHub | Que corra sí o sí, con la compu apagada |
| **D · n8n** (un horario automático) | Tu servidor de n8n | No | No | Flujos fijos que mandan a WhatsApp, Telegram o una planilla |

> **Tip:** regla simple. ¿Necesita archivos de tu compu? **A**. ¿Tiene que correr con la compu apagada? **C**. ¿Siempre los mismos pasos, sin criterio? **D**.

## Paso 0 · Escribí las instrucciones en un archivo
La tarea corre sola: nadie le va a aclarar nada. Las instrucciones van en un archivo del cerebro, así todas las opciones usan las mismas.

1. En la app, **Code › + New › Local › Open folder…** y elegí `cerebro-[TU-EMPRESA]`.
2. Pegá esto. Reemplazá `[NOMBRE DE LA PLANILLA]` por una planilla tuya de Google Drive, o borrá esa parte:

```prompt
Creá el archivo operacion/resumen-semanal.md con este texto, exacto:

---
Resumen semanal (corre los lunes a las 9:07, hora de Argentina):
1. Leé CLAUDE.md y negocio/empresa.md.
2. Revisá objetivos/pendientes.md, lo que haya en inbox/ (si existe) y la planilla [NOMBRE DE LA PLANILLA] de Google Drive.
3. Armá un resumen de 10 líneas: qué se vendió, qué quedó pendiente, las 3 personas a llamar primero y por qué.
4. Guardalo en reportes/AAAA-MM-DD-semanal.md, con la fecha de hoy.
Reglas: no mandes mensajes a nadie, no cambies precios ni borres nada. Si falta un dato, escribí PENDIENTE. Si algo salió raro, empezá el resumen con "REVISAR:".
---
```

3. Tocá **Permitir** cuando te pida crear el archivo.
4. Si vas a usar la **Opción C** (nube): en GitHub Desktop escribí un resumen, tocá **Commit to main** y **Push origin**. La nube solo ve lo que está en GitHub.

**Tenés que ver:** el archivo `operacion/resumen-semanal.md` en tu carpeta.

> **Ojo:** la hora en punto (9:00) es la más cargada. Usá 9:07.

## Opción A · Pestaña Code › Scheduled (la del taller)

**La forma más fácil:** pedíselo en la sesión que tenés abierta en la carpeta del cerebro.

```prompt
Armá una tarea programada local que corra todos los lunes a las 9:07 en esta carpeta y siga las instrucciones de operacion/resumen-semanal.md. Llamala resumen-semanal. Cuando la crees, decime cuándo va a correr la próxima vez.
```

**Tenés que ver:** Claude confirma el nombre y la próxima ejecución, y la tarea aparece en **Scheduled**.

**Con el formulario (si preferís botones):**
1. En la pestaña **Code**, tocá **Scheduled** en la barra lateral (o en el menú **More**).
2. Tocá **New task**. Si te ofrece **Create with Claude** o **Set up manually**, elegí **Set up manually**.
3. **Name**: `resumen-semanal`. En el cuadro de instrucciones: `Seguí las instrucciones de operacion/resumen-semanal.md`.
4. Abrí **Advanced settings**, pestaña **General**, activá **Only on this computer** y en **Local folder** elegí `cerebro-[TU-EMPRESA]`.
5. En **Trigger** elegí **Weekly**, día lunes, 9:07.
6. Elegí el modo de permiso y el modelo (en el cuadro de instrucciones) y tocá **Create**.

> **Ojo:** el formulario cambia según la versión de la app (a veces **Only on this computer** está arriba de todo, o te pregunta **Local** o **Cloud**). Si no lo encontrás, usá la forma fácil: pedíselo a Claude.

### Probala ya, sin esperar al lunes
En la página de la tarea tocá **Run now**. Aprobá los permisos que pida con **Permitir siempre**: así las próximas no se traban.

**Tenés que ver:** una ejecución nueva en **History** y el archivo `reportes/…-semanal.md` creado.

### Ver, pausar, editar, borrar
En **Scheduled**, tocá la tarea:
- **History**: cada ejecución. Tocala para ver qué hizo.
- **Status**: **Active** o **Paused**.
- El lápiz (**Edit**): cambiar instrucciones, horario o carpeta.
- **Delete**: borrarla.

También podés pedírselo a Claude: "mostrame mis tareas programadas" o "pausá resumen-semanal".

- Solo corre con la app **abierta** y la compu **despierta**. Si estaba dormida, al despertar hace **una** sola ejecución de recuperación.
- Para que no se duerma: **Keep computer awake** en **Settings** de la app (**Desktop app** o **This computer › System**, según la versión). Cerrar la tapa igual la duerme.

> **Ojo:** "salió bien" significa que terminó sin error, no que hizo bien el trabajo. Las primeras semanas, abrí cada ejecución y leé qué hizo.

## Opción B · Cowork
1. En la app, abrí **Cowork** y tocá **Scheduled** en la barra lateral.
2. **New task** › **Create with Claude** (le contás qué querés) o **Set up manually** (nombre, prompt, modo de aprobación, frecuencia y, si querés, carpeta).
3. Confirmá con **Schedule** o **Save**.

Corre en la nube aunque la compu esté dormida, **salvo** que elijas una carpeta de tu compu: ahí solo corre con la app abierta. Desde **Scheduled** editás, pausás, borrás o corrés una ya.

**Tenés que ver:** la tarea nueva en **Scheduled**, con su próxima fecha.

> **Ojo:** si una herramienta de un conector está en "Always ask", la tarea se queda esperando tu respuesta o termina sin usarla.

## Opción C · Claude Code en la nube
Corre con la compu apagada, sobre una copia de tu repo de GitHub.

En la pestaña Code, con la carpeta del cerebro abierta:

```prompt
/schedule todos los lunes a las 9:07, armá el resumen semanal siguiendo las instrucciones de operacion/resumen-semanal.md
```

Claude te pregunta lo que falta (repo, horario) y la guarda en tu cuenta.

O con botones: **Scheduled › New task**, elegí **Cloud** (o entrá a [claude.ai/code/routines](https://claude.ai/code/routines)), poné nombre y prompt, en **Trigger** elegí la frecuencia, en **Repository** el repo de tu cerebro, en **Connectors** sacá los que no necesita, y **Create**. Probala con **Run now**.

**Tenés que ver:** la tarea con su próxima ejecución y, después de **Run now**, una fila en **History**.

**Límites:** como mínimo cada 1 hora. Consume el uso de tu plan. Mirá el consumo en [claude.ai/settings/usage](https://claude.ai/settings/usage).

> **Ojo:** si usás **Custom** con una expresión cron en la nube, la hora va en **UTC** (lunes 9:07 de Argentina = `7 12 * * 1`). En la tarea local (Opción A), **Custom** va en tu hora local. Más fácil: usá las opciones de la lista.

## Opción D · n8n
Para flujos fijos: "todos los lunes a las 9, leé la planilla, pasásela a Claude y mandá el resultado por Telegram".
1. En n8n, creá un workflow con el nodo **Schedule Trigger**: **Weeks**, **Monday**, 9:07. Zona horaria del workflow: **America/Argentina/Cordoba**.
2. Sumá los pasos (planilla, Claude con tu clave de API, envío) y probalo con **Execute workflow**.
3. Activalo (**Active** o **Publish**, según tu versión). Las ejecuciones se ven en **Executions**.

**Tenés que ver:** en **Executions**, la prueba en verde.

Cuenta y conexión: [n8n](#s6-n8n). Ejemplo completo: [Reporte que llega solo](#p10-extras).

## Cómo sé que funcionó
Tocaste **Run now** (o **Execute workflow**), la ejecución aparece en el historial y `reportes/…-semanal.md` (o el mensaje) tiene el resumen que esperabas.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo **Scheduled** | Actualizá la app. Buscalo en el menú **More** de la barra lateral, o como **Routines**. |
| `/schedule` no existe | Actualizá la app. Si sigue, tu cuenta no tiene habilitada la nube: usá la Opción A. |
| La tarea en la nube no ve mis archivos | Corre sobre GitHub: hacé **Commit** y **Push** en GitHub Desktop. |
| Corrió a una hora rara | La compu estaba dormida y corrió al despertar. En la nube, la cron va en UTC. |
| Se quedó trabada esperando | Abrí la ejecución en **History** y respondé el permiso. Para la próxima, **Permitir siempre**. |
| "Salió bien" pero el resumen está vacío | Leé la ejecución. Casi siempre falta un archivo o un conector. Sumá al prompt: "si no encontrás X, escribí PENDIENTE". |

## Para seguir solo
- Empezá con una tarea de **solo lectura** (un resumen) y dejala 2 semanas antes de darle permiso para escribir o mandar algo.
- Programá un "cierre de semana" los viernes: qué se decidió y qué quedó pendiente, guardado en `notas/`.
- Antes de dejar algo corriendo solo, pasá el [checklist del agente seguro](#t6-datos-y-seguridad).
- **Avanzado, en la terminal:** el programador de tareas de tu compu (`cron` en Mac, `schtasks` / **Programador de tareas** en Windows) puede correr `claude -p "Seguí operacion/resumen-semanal.md"` a una hora fija. Solo si ya te manejás con la terminal: la Opción A hace lo mismo con botones.
