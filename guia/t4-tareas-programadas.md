---
titulo: 'Tareas programadas: que Claude trabaje solo'
bloque: Teoría
tiempo: 30 min
para: Todos
necesitas: t3-donde-trabajar
resultado: Sabés elegir dónde programar una tarea, creaste una de prueba que corre los lunes a las 9 y sabés ver sus ejecuciones y pausarla.
---

Una tarea programada es un pedido que Claude hace solo, cuando vos le digas: todos los lunes a las 9, cada hora, una vez el jueves que viene. Es el "reporte que llega solo".
Ejemplo: Fondus recibe cada lunes a las 9 un resumen de las consultas de la semana, cuáles quedaron sin respuesta y a quién llamar primero. Nadie lo arma: lo arma Claude.

> **Datos:** verificado en la documentación oficial el 18/11/2026. Las tareas programadas de Claude Code en la nube están en "research preview": pueden cambiar. Antes se llamaban **Routines** y en algunas cuentas todavía aparecen con ese nombre (**New routine** en vez de **New task**).

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude.
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)) y la carpeta de tu cerebro armada (`Documentos/cerebro-[TU-EMPRESA]`, [Tu cerebro](#p1-cerebro)).
- [ ] Para la nube con Claude Code: tu cerebro subido a [GitHub](#s4-github).
- [ ] Una tarea que ya hiciste a mano y salió bien. **Nunca programes algo que no viste funcionar.**

## Dónde programar: 4 opciones
| Opción | Dónde corre | Compu prendida | Toca archivos de tu compu | Ideal para |
|---|---|---|---|---|
| **Claude Code en la nube** (`/schedule` o [claude.ai/code/routines](https://claude.ai/code/routines)) | Nube de Anthropic | No | No: trabaja sobre tu repo de GitHub | Reportes sobre tu cerebro, revisar tu web, tareas con conectores |
| **App de escritorio, pestaña Code** (tarea local) | Tu compu | Sí, y la app abierta | Sí | Tareas con archivos o programas de tu compu |
| **Cowork** (**Scheduled**) | Nube, salvo que elijas una carpeta | No (sí, si elegís una carpeta) | Solo si elegís una carpeta | Informes y resúmenes de oficina con tus conectores |
| **n8n** (cron: un horario automático) | Tu servidor de n8n | No | No | Flujos que no necesitan "pensar" en cada paso, o que mandan a WhatsApp, Telegram o una planilla |

Y una más, para el momento: `/loop 5m [TAREA]` repite algo mientras la sesión de Claude Code está abierta (por ejemplo, "fijate cada 5 minutos si terminó el render").

> **Tip:** regla simple. ¿Necesita archivos de tu compu? Tarea local. ¿Tiene que correr sí o sí, con la compu apagada? Nube. ¿Siempre los mismos pasos, sin criterio? n8n.

## Paso 0 · Escribí las instrucciones en un archivo
La tarea corre sola: no hay nadie para aclararle nada. Las instrucciones tienen que bastarse solas. Las guardamos en un archivo del cerebro, así las opciones A, B y el Extra usan las mismas.

1. Abrí Claude Code parado en la carpeta de tu cerebro.
2. Pegá esto. Reemplazá `[NOMBRE DE LA PLANILLA]` por el nombre de una planilla tuya de Google Drive, o borrá esa parte si no usás una:

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

3. Si vas a usar la **Opción A** (nube): en GitHub Desktop escribí un resumen ("Instrucciones del resumen semanal"), tocá **Commit to main** y después **Push origin**. La nube solo ve lo que está en GitHub.

**Tenés que ver:** el archivo `operacion/resumen-semanal.md` en tu carpeta (y en [github.com](https://github.com), si lo subiste).

> **Ojo:** la hora en punto (9:00) es la más cargada y puede arrancar varios minutos tarde. Usá 9:07.

## Opción A · Claude Code en la nube

### Paso 1 · Creala desde Claude Code
En una sesión de Claude Code (terminal o pestaña Code), parado en la carpeta de tu cerebro:

```prompt
/schedule todos los lunes a las 9:07, armá el resumen semanal siguiendo las instrucciones de operacion/resumen-semanal.md
```

Claude te hace preguntas (repo, horario, qué hacer) y la guarda en tu cuenta. `/routines` hace lo mismo.

**Tenés que ver:** Claude confirma el nombre de la tarea y la próxima vez que va a correr. Si te dice que no puede conectarse a tu cuenta, no se creó: corré `/login` y probá de nuevo.

### Paso 1 (alternativa) · Creala desde la web
1. Entrá a [claude.ai/code/routines](https://claude.ai/code/routines) y tocá **New task** (o **New routine**).
2. Si te pregunta **Create with Claude** o **Set up manually**: con la primera se la describís en un chat; con la segunda llenás el formulario.
3. Poné un nombre (por ejemplo `Resumen semanal`) y, como prompt: `Seguí las instrucciones de operacion/resumen-semanal.md`.
4. En **Trigger** elegí **Schedule** y la frecuencia (por hora, diaria, semanal). La hora va en **tu hora local**.
5. En **Advanced settings**, en **Repository**, elegí el repo de tu cerebro. Sin repo, la tarea queda como tarea de chat, no de Claude Code.
6. En la pestaña **Connectors**, sacá los conectores que la tarea no necesita. Vienen todos tildados y puede usarlos para escribir.
7. Tocá **Create**.

**Tenés que ver:** la página de la tarea con su nombre y la próxima vez que va a correr.

> **Ojo:** si usás **Custom** con una expresión cron, las horas van en **UTC**, no en hora de Argentina. Lunes 9:07 de Argentina (UTC−3) es `7 12 * * 1`. Más fácil: usá las opciones de la lista.

### Paso 2 · Probala ya, sin esperar al lunes
En la página de la tarea tocá **Run now**. Desde la terminal: `/schedule run`.

**Tenés que ver:** una ejecución nueva en la lista **History**. Tocala: se abre como una sesión normal donde ves qué hizo.

### Paso 3 · Ver, pausar, editar, borrar
| Querés | En la web (claude.ai/code/routines) | En Claude Code |
|---|---|---|
| Ver las ejecuciones | Página de la tarea › **History**. Cada fila dice **Error**, **Cancelled** o nada (salió bien) | `/schedule list` o "`/schedule` ¿por qué el resumen del lunes salió vacío?" |
| Pausar | El interruptor de arriba de la página (on/off) | Pediselo a Claude con `/schedule update` |
| Editar | Menú al lado del nombre › **Edit** › **Save changes** | `/schedule update` |
| Borrar | Menú al lado del nombre › **Delete** | Desde la web |

**Tenés que ver:** sabés dónde está el interruptor para pausarla. Probalo: pausala y volvé a activarla.

> **Ojo:** "salió bien" significa que la sesión terminó sin error, no que hizo bien el trabajo. Las primeras semanas, abrí cada ejecución y leé qué hizo.

**Límites:** cada 1 hora como mínimo. Consume el uso de tu plan igual que si la usaras vos. Mirá el consumo en [claude.ai/settings/usage](https://claude.ai/settings/usage).

## Opción B · Tarea local en la app de escritorio
Para cuando la tarea necesita archivos o programas de tu compu (por ejemplo, ordenar la carpeta de videos crudos de La Consejera todas las noches).
1. En la app de Claude, pestaña **Code**, tocá **Scheduled** en la barra lateral (o en el menú **More**).
2. Tocá **New task**. Si te pregunta, elegí **Set up manually**.
3. Poné un nombre y, como instrucciones: `Seguí las instrucciones de operacion/resumen-semanal.md` (o la tarea que quieras).
4. En **Advanced settings**, pestaña **General**, activá **Only on this computer** y elegí la carpeta `cerebro-[TU-EMPRESA]` en **Local folder**.
5. En **Trigger** elegí **Hourly**, **Daily**, **Weekdays** o **Weekly**.
6. Elegí el modo de permiso y el modelo, y tocá **Create**.
7. En la página de la tarea tocá **Run now** y aprobá los permisos que pida con "permitir siempre": así las próximas no se traban.

**Tenés que ver:** la tarea en la lista de **Scheduled** y, después de **Run now**, una ejecución en **History**.

También podés pedírselo en cualquier sesión: "armá una tarea que todos los días a las 20 ordene la carpeta [CARPETA]".

- **Pausar:** en la página de la tarea, **Status** › **Paused**. **Ver ejecuciones:** lista **History**. **Borrar:** **Delete**.
- Solo corre con la app **abierta** y la compu **despierta**. Si estaba dormida, al despertar hace **una** sola ejecución de recuperación.
- Para que no se duerma: **Keep computer awake** en la configuración de la app. Cerrar la tapa de la laptop igual la duerme.

## Opción C · Cowork
1. En la app de Claude, tocá **Scheduled** en la barra lateral.
2. Tocá **New task** arriba a la derecha.
3. **Create with Claude** (le contás qué querés y te pregunta lo que falta) o **Set up manually** (nombre, prompt, modo de aprobación, frecuencia y, si querés, modelo y carpeta).
4. Confirmá con **Schedule** o **Save**.

Frecuencias: por hora, diaria, semanal, días hábiles o manual. Corre en la nube aunque la compu esté dormida, **salvo** que elijas una carpeta de tu compu: ahí solo corre con la app abierta.
Desde **Scheduled** ves las próximas y las pasadas, y podés editar, pausar, borrar o correr una ya.

**Tenés que ver:** la tarea nueva en **Scheduled**, con su próxima fecha.

> **Ojo:** si una herramienta de un conector está en "Always ask", la tarea se queda esperando tu respuesta o termina sin usarla.

## Opción D · n8n con cron
Para flujos fijos: "todos los lunes a las 9, leé la planilla, pasásela a Claude por la API y mandá el resultado por Telegram".
1. En n8n, creá un workflow y agregá el nodo **Schedule Trigger**.
2. Elegí **Weeks**, día **Monday**, hora **9**, minuto **7**. Revisá que la zona horaria del workflow sea **America/Argentina/Cordoba** (en la configuración del workflow).
3. Agregá los pasos: leer la planilla, el nodo de Claude (con tu clave de API) y el envío por Telegram o WhatsApp.
4. Probalo con **Execute workflow** y, si anda, activalo (**Active** / **Publish**, según tu versión).
5. Las ejecuciones se ven en la pestaña **Executions**. Para pausar, desactivá el workflow.

**Tenés que ver:** en **Executions**, la ejecución de prueba en verde.

Cómo crear la cuenta y conectar n8n: [n8n](#s6-n8n). Ejemplo completo: [Reporte que llega solo](#p10-extras).

> **Ojo:** los nombres de los botones de n8n cambian entre versiones. Si no encontrás **Active**, buscá **Publish**.

## Extra · Claude Code con el programador de tareas de tu compu
Para quien ya se anima a la terminal. Es opcional: las opciones A a D alcanzan. Corre `claude -p` (un pedido único, sin chat) a una hora fija. Necesitás el archivo del Paso 0.

<div data-os="mac">

1. En la Terminal, buscá dónde está Claude Code y copiá lo que te responde (algo como `/Users/tu-usuario/.local/bin/claude`):

```bash
which claude
```

2. Abrí el programador de tareas (cron) con el editor **nano**, que es el más fácil:

```bash
EDITOR=nano crontab -e
```

**Tenés que ver:** la Terminal se convierte en un editor de texto (vacío o con líneas viejas).

3. Pegá esta línea (lunes 9:07). Reemplazá `[RUTA-DE-CLAUDE]` por lo que copiaste en el paso 1 y `[TU-EMPRESA]` por el nombre de tu carpeta:

```bash
7 9 * * 1 cd ~/Documents/cerebro-[TU-EMPRESA] && [RUTA-DE-CLAUDE] -p "Seguí operacion/resumen-semanal.md" --allowedTools "Read,Write" >> ~/claude-cron.log 2>&1
```

4. Guardá y salí: **Ctrl+O**, **Enter**, **Ctrl+X**.

**Tenés que ver:** el mensaje `crontab: installing new crontab`. Para revisarla: `crontab -l`.

5. Para pausarla, repetí el paso 2 y poné un `#` al principio de la línea.

> **Ojo:** verificá con una prueba real. Si el archivo `~/claude-cron.log` dice "Operation not permitted", macOS no deja que cron entre a **Documentos**: se habilita en **Configuración del Sistema › Privacidad y seguridad › Acceso total al disco**, agregando `/usr/sbin/cron`. Si no te animás, usá la Opción B, que hace lo mismo con botones.

</div>
<div data-os="win">

1. En PowerShell, buscá dónde está Claude Code y copiá lo que te responde (algo como `C:\Users\tu-usuario\.local\bin\claude.exe`):

```powershell
(Get-Command claude).Source
```

2. Creá un archivo de órdenes (`.bat`) en la carpeta de tu cerebro. Este comando abre el Bloc de notas; si pregunta si querés crear el archivo, tocá **Sí**:

```powershell
notepad "$HOME\Documents\cerebro-[TU-EMPRESA]\resumen-semanal.bat"
```

3. Pegá estas dos líneas en el Bloc de notas. Reemplazá `[RUTA-DE-CLAUDE]` por lo que copiaste en el paso 1 (dejá las comillas) y `[TU-EMPRESA]` por el nombre de tu carpeta. Después **Archivo › Guardar** y cerrá:

```text
cd /d "%USERPROFILE%\Documents\cerebro-[TU-EMPRESA]"
"[RUTA-DE-CLAUDE]" -p "Segui operacion/resumen-semanal.md" --allowedTools "Read,Write" >> "%USERPROFILE%\claude-cron.log" 2>&1
```

4. Programalo para los lunes a las 9:07:

```powershell
schtasks /Create /SC WEEKLY /D MON /ST 09:07 /TN "Claude resumen semanal" /TR "$HOME\Documents\cerebro-[TU-EMPRESA]\resumen-semanal.bat"
```

**Tenés que ver:** `CORRECTO: se creó correctamente la tarea programada…` (o `SUCCESS`, si tu Windows está en inglés).

5. Para probarla ya: abrí **Programador de tareas** (tecla Windows, escribí "Programador de tareas"), buscá "Claude resumen semanal", clic derecho › **Ejecutar**. Para pausarla: clic derecho › **Deshabilitar**.

> **Ojo:** verificá con una prueba real. Si tu nombre de usuario de Windows tiene espacios, o tu carpeta Documentos está en OneDrive, la ruta cambia y puede fallar: en ese caso usá la Opción B. La tarea corre solo con tu sesión de Windows iniciada.

</div>

`--allowedTools` limita lo que puede hacer sin preguntar. Dale lo mínimo.

## Cómo sé que funcionó
Tocaste **Run now** (o **Execute workflow**), la ejecución aparece en el historial y el archivo `reportes/…-semanal.md` (o el mensaje) tiene el resumen que esperabas.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `/schedule` dice "Unknown command" | Actualizá con `claude update`. Si sigue, tu cuenta u organización no tiene habilitadas las sesiones en la nube. |
| La tarea en la nube no ve mis archivos | Corre sobre una copia de GitHub: subí los archivos al repo (commit y push). |
| Corrió a una hora rara | En la nube, la cron va en UTC. En la tarea local, la compu estaba dormida y corrió al despertar. |
| Se quedó trabada esperando | Abrí la ejecución y respondé el permiso. Para la próxima, aprobá con "permitir siempre" o sacá esa herramienta. |
| "Salió bien" pero el resumen está vacío | Leé la ejecución. Casi siempre falta un archivo o un conector. Agregá en el prompt: "si no encontrás X, escribí PENDIENTE". |

## Para seguir solo
- Empezá con una tarea de **solo lectura** (un resumen) y dejala 2 semanas antes de darle permiso para escribir o mandar algo.
- Programá un "cierre de semana" los viernes: qué se decidió, qué quedó pendiente, guardado en `notas/`.
- Antes de dejar algo corriendo solo, pasá el [checklist del agente seguro](#t6-datos-y-seguridad).
