---
titulo: "'Dónde trabajar: Chat, Projects, Cowork, Claude Code y la nube'"
bloque: Teoría
tiempo: 20 min de lectura
para: Todos
necesitas: t2-piezas
resultado: Sabés en qué lugar de Claude conviene hacer cada tarea, cómo pasar una sesión de tu compu a la nube y cómo seguirla desde el celular.
---

Claude no es un solo lugar. Es el mismo cerebro trabajando en distintas "oficinas": el chat, Cowork, Claude Code en tu compu y Claude Code en la nube.
**En el taller trabajamos en la pestaña Code de la app de escritorio** (Claude Code local, sin terminal). Elegir bien te ahorra horas. Ejemplo: Manuel Martínez arma el bot de su escuela en la pestaña Code, en su compu, lo deja corriendo en la nube a la noche y lo revisa desde el celular a la mañana.

> **Datos:** verificado en la documentación oficial (code.claude.com/docs y [support.claude.com](https://support.claude.com)) el 18 y 19/11/2026. Estas funciones cambian seguido: si un botón no está donde dice, buscá el nombre parecido.

## El mapa rápido
| Oficina | Analogía | Dónde corre | Toca tus archivos | Plan |
|---|---|---|---|---|
| **Chat y Projects** | La sala de reuniones: pensás en voz alta | En la nube | No (subís archivos a mano o usás conectores) | Free y pagos |
| **Cowork** | El asistente administrativo | En la nube, y en tu compu a través de la app de escritorio | Sí, las carpetas que le das | Pro o superior |
| **Claude Code local: pestaña Code de la app** (camino del taller) | El técnico que trabaja en tu escritorio | En tu compu | Sí, toda la carpeta que abrís | Pro o superior |
| **Claude Code en la nube** | El técnico que se lleva el trabajo a su taller | En una compu de Anthropic | No: trabaja sobre una copia de tu repo de GitHub (tu carpeta guardada en GitHub) | Pro, Max, Ultra o Team |
| **Remote Control** | El control remoto de la tele | En tu compu (vos mirás desde otro lado) | Sí | Pro o superior |

## Chat y Projects
El chat de [claude.ai](https://claude.ai), la app de escritorio y la del celular.
- **Chat**: una conversación. Ideal para pensar, escribir, revisar un texto, preguntar.
- **Projects (Proyectos)**: una carpeta de chats que comparten **instrucciones y archivos fijos**. Cargás los archivos de tu cerebro (`CLAUDE.md` y las carpetas `negocio/`, `marca/`, `ventas/`) una vez y todos los chats del Proyecto los saben. Es tu cerebro en el celular. Paso a paso: [Usá tu borrador](#c2-tu-borrador), Paso 4.
- **Artifacts**: documentos, páginas o apps chiquitas que Claude arma al costado del chat y podés compartir.
- Usa tus **conectores** (Drive, Gmail, Calendar) y tus **skills** (**Customize › Skills**).

Ejemplo: Celve crea un Proyecto "Atención" con su lista de productos y precios. Desde el celular, en la góndola, pregunta "¿qué le respondo a un cliente que pide sin TACC?".

**Probalo** (dentro de un Proyecto con los archivos de tu cerebro cargados):

```prompt
Con lo que sabés de mi empresa, respondé este mensaje de un cliente como lo respondería yo: "[PEGÁ UN MENSAJE INVENTADO]". Dame 2 versiones: una corta y una más cálida.
```

## Cowork
Cowork es el modo agente de la app de Claude para **trabajo de oficina**: le describís el resultado y lo hace de punta a punta, con varios pasos, mientras vos hacés otra cosa. No necesita terminal.

**Qué puede hacer con tus archivos:**
- Ordenar una carpeta de descargas por tipo y fecha.
- Renombrar 40 archivos con un formato de fecha.
- Pasar tickets o recibos a un informe de gastos.
- Armar una planilla con fórmulas que funcionan, o una presentación a partir de tus notas.
- Leer varios documentos y armar un informe.

**Cómo se usa:**
1. Abrí Claude en la app de escritorio, la web o el celular.
2. En el cuadro de mensaje elegí **Cowork**. Si no ves las opciones **Chat** y **Cowork**, tenés la versión nueva unificada: escribí directo.
3. Describí la tarea. Revisá el plan que te propone y dejalo trabajar.

**Tenés que ver:** Claude te muestra un plan con pasos y, a medida que avanza, qué está haciendo.

**Dónde corre:** por defecto en la nube, y tus sesiones te siguen en la compu, la web y el celular. Para tocar **archivos de tu compu**, tu navegador o tu computadora, usa la app de escritorio, que tiene que estar **abierta**. Solo puede entrar a las carpetas que conectaste.

**Modos de permiso** (en el selector del cuadro de mensaje):
- **Manual**: te pregunta antes de cada acción. Empezá por acá.
- **Auto**: hace solo lo de lectura; lo de escribir o borrar lo hace salvo que un control automático lo marque como riesgoso.
- **Skip**: no controla nada. Solo si confiás en todo lo que tiene a mano.

Antes de borrar archivos para siempre, siempre te pide **Allow**.

<div data-os="mac">

En Mac funciona con la app de escritorio, sin pasos extra.

</div>
<div data-os="win">

En Windows, Cowork necesita la función **Virtual Machine Platform** y **permisos de administrador** al instalar la app. En una compu de empresa sin admin, la app se instala pero Cowork no aparece: pedíselo a quien maneja las compus.

</div>

**Probalo** (en Cowork, con una carpeta de prueba conectada):

```prompt
En la carpeta [NOMBRE DE LA CARPETA] hay archivos mezclados. Proponeme cómo ordenarlos en subcarpetas por tipo y fecha, mostrame el plan y esperá mi OK antes de mover nada. No borres ningún archivo.
```

> **Ojo:** para plata, mensajes que salen a tu nombre o archivos importantes, quedate en **Manual** y mirá lo que hace.

## Claude Code en tu compu: la pestaña Code (camino del taller)
Es Claude trabajando **en tu computadora**: lee y escribe archivos, instala programas, corre comandos, arma bots y webs. Es la herramienta principal del taller, y la usamos desde la **pestaña Code** de la app de escritorio: sin terminal, con botones.
1. En la app, tocá **Code** (arriba de la barra lateral) y **+ New**.
2. En el selector de entorno (debajo del cuadro) elegí **Local**.
3. Tocá **Open folder…** y elegí la carpeta de tu cerebro o de tu proyecto.
4. Escribí tu pedido. Cuando Claude quiere crear un archivo o correr un comando, te muestra un pedido de permiso con botones: leé qué va a hacer y aprobá.

Lee el `CLAUDE.md` de la carpeta que abrís. Por eso: **abrí siempre la carpeta de tu cerebro o de tu proyecto**.
Instalación: [Instalá Claude Code](#s2-claude-code). Comandos y teclas: [Atajos](#t5-atajos).

> **Ojo:** el nombre del botón para elegir la carpeta puede variar según la versión de la app.

**Probalo:**

```prompt
Mirá qué hay en esta carpeta y explicame en 5 líneas qué es este proyecto. Después proponeme 3 cosas que podríamos automatizar acá.
```

**Tenés que ver:** un resumen de los archivos de la carpeta que abriste. Si te dice que está vacía, abriste otra carpeta.

## Claude Code en la web (sesiones en la nube)
Una **sesión en la nube** es Claude Code corriendo en una compu de Anthropic, no en la tuya. Le das una tarea y **sigue trabajando aunque cierres la laptop**. La mirás y le escribís desde [claude.ai/code](https://claude.ai/code), la app de escritorio o el celular.
- Trabaja sobre un **repo de GitHub** (tu carpeta guardada en GitHub): lo copia, hace los cambios en una **rama** (una copia aparte) y te propone un **pull request** (PR): un pedido para sumar esos cambios que vos revisás y aceptás. Palabras en el [glosario](#t2-piezas).
- **Plan:** Pro, Max, Ultra o Team (en Enterprise, con asiento premium). Usa el mismo límite de uso de tu plan: la compu de la nube no se cobra aparte.

Ejemplo: desde el celular, Viajes TDH le pide "cambiá el precio del paquete a Mendoza en la web y abrí el PR". A la noche revisa el cambio y lo publica.

### 1. Habilitar el entorno web (una sola vez)
1. Entrá a [claude.ai/code](https://claude.ai/code) con tu cuenta de Claude.
2. Conectá GitHub: te pide autorizar la **Claude GitHub App**. Dale acceso al repo de tu cerebro o de tu web. Paso a paso de GitHub: [GitHub](#s4-github).
3. El **entorno** (environment) es la configuración de la compu de la nube: a qué páginas de internet puede entrar y qué se instala al arrancar. La primera vez se crea solo uno llamado **Default**, con acceso a internet **Limited** (limitado). Para el taller alcanza.
4. Elegí el repo y escribí tu primera tarea.

En la app de escritorio: pestaña **Code** › **+ New** › en el selector de entorno (debajo del cuadro) elegí un entorno de la parte **Cloud**. Para crear otro: **New environment** (al final del selector) › pestaña **Cloud** › **Add environment**.

**Tenés que ver:** en [claude.ai/code](https://claude.ai/code), tu repo en la lista y la sesión arrancando.

> **Ojo:** en planes Team o Enterprise, el dueño de la cuenta tiene que tener habilitadas las sesiones en la nube. Si no te deja, pedíselo.

### 2. Pasar una sesión de la app a la nube (y traerla de vuelta)
**Ida (de tu compu a la nube):**
1. **Antes que nada:** subí tus cambios a GitHub (en GitHub Desktop: **Commit to main** y **Push origin**). La nube copia lo que está en GitHub.
2. En la pestaña Code, abrí el menú de la sesión (la flechita al lado del título, o la fila de la barra lateral) › **Open in** › **Cloud**.
3. Leé el aviso: te dice si se llevan los archivos y si la sesión local se archiva. Confirmá.

**Tenés que ver:** la sesión en la nube, trabajando (también aparece en [claude.ai/code](https://claude.ai/code)). La conversación pasa **resumida**, no entera.

**Vuelta (de la nube a tu compu):** lo más simple es traer el **resultado**: la sesión deja sus cambios en una rama de GitHub. En GitHub Desktop: **Fetch origin**, elegí esa rama (o aceptá el PR) y seguí en la pestaña Code con tu carpeta.

> **Ojo:** la documentación no muestra un botón para traer una sesión de la nube a la pestaña Code **Local**. La forma oficial de traer la conversación entera es **en la terminal**: en [claude.ai/code](https://claude.ai/code), menú de la sesión › **Open in** › **Terminal** copia el comando `claude --teleport ...`; lo pegás en la terminal parado en la carpeta del repo (sin cambios sin guardar). Adentro de la terminal, `/teleport` hace lo mismo.

> **Ojo:** las sesiones de **SSH** o **WSL** no se pueden pasar a la nube con **Open in**.

> **Tip:** planificá en tu compu y ejecutá en la nube. Usá el modo **Plan**, guardá el plan en un archivo, subilo a GitHub y abrí una sesión **Cloud** con "Ejecutá el plan de notas/plan-web.md".

### 3. Dejar una tarea corriendo en la nube (y retomarla después)
1. Arrancá la sesión en **Cloud** (o pasala con **Open in › Cloud**) y dale una tarea clara, con un final concreto ("…y abrí un PR").
2. Cerrá la compu. La tarea sigue.
3. Después, mirala en [claude.ai/code](https://claude.ai/code) o en la app del celular › **Code**: está en la lista de sesiones de la barra lateral.
4. Si Claude te dejó una pregunta, contestala cuando vuelvas y sigue desde ahí.

> **Ojo:** no existe una "sesión temporal" o descartable como opción. Lo que sí pasa: si la sesión queda **quieta un rato**, la compu de la nube se apaga sola. Al reabrirla desde [claude.ai/code](https://claude.ai/code) arranca una compu nueva con **toda la conversación**, pero lo que estaba corriendo en ese momento (comandos, subagentes, tareas programadas de la sesión) se corta: pedile a Claude que lo vuelva a correr.

**Cuando terminás:**
- **Archivar** (la saca de la lista, se puede recuperar): en la barra lateral, pasá el mouse sobre la sesión › **⋯** › **Archive**. Para verlas: [claude.ai/code/sessions](https://claude.ai/code/sessions) › pestaña **Archived** › **⋮** › **Unarchive**.
- **Borrar** (para siempre, no se puede deshacer): **⋯** › **Delete** y confirmás.
- **Compartir**: cambiá la visibilidad de la sesión y mandá el link. En Pro, Max y Ultra: **Private** o **Public** (la ve cualquiera con cuenta de Claude que tenga el link). En Team o Enterprise: **Private** o **Team**. El otro ve cómo estaba al abrir el link, no en vivo.

> **Ojo:** antes de poner una sesión en **Public**, revisá que no tenga claves ni datos de clientes.

Para seguirla desde el celular, mirá más abajo **Remote Control y la app del celular**, paso 3.

**Probalo** (entorno **Cloud**, con el repo de tu cerebro o tu web):

```prompt
Leé el CLAUDE.md de este repo. Revisá los archivos y armame una lista de lo que está desactualizado o dice PENDIENTE. No cambies nada: solo dejame la lista en notas/pendientes.md y abrí un PR.
```

**Tenés que ver:** la sesión en la lista de [claude.ai/code](https://claude.ai/code) y, al rato, un PR nuevo en tu repo.

## Remote Control y la app del celular
Distinto de la nube: con **Remote Control**, Claude sigue trabajando **en tu compu** (con tus archivos, programas y conexiones) y el celular es solo **una ventana** para mirarlo y escribirle. Analogía: el control remoto de la tele; la tele sigue siendo la de tu casa.

### 1. Habilitar Remote Control en la pestaña Code
Necesitás: plan **Pro, Max, Ultra, Team o Enterprise** y la app con tu cuenta de Claude. En Team o Enterprise, el dueño de la cuenta tiene que tener prendido Remote Control en la configuración de la organización.
1. Abrí tu sesión **Local** en la pestaña Code.
2. Prendé el interruptor **Remote Control** (en la tarjeta **Environment** del panel de detalles de la sesión), o escribí en el cuadro:

```prompt
/remote-control
```

(`/rc` es lo mismo, más corto.)

**Tenés que ver:** la sesión aparece en la lista de [claude.ai/code](https://claude.ai/code).

Para que **todas** las sesiones nuevas se conecten solas: **Settings › Code** (o **Settings › Claude Code**) › **Connect new sessions to Remote Control**.
Para cortar: apagá el interruptor o escribí `/remote-control` de nuevo.

### 2. Seguir la sesión desde el celular
1. Instalá la app de **Claude** ([iOS](https://apps.apple.com/us/app/claude-by-anthropic/id6473753684) o [Android](https://play.google.com/store/apps/details?id=com.anthropic.claude)). Atajo: escribí `/mobile` en el cuadro y escaneá el QR, te lleva a la tienda correcta.
2. Iniciá sesión con **la misma cuenta** que usás en la compu.
3. Tocá **Code** en el menú de la app. Ahí está la lista de sesiones: las de Remote Control tienen **un ícono de compu con un punto verde** cuando están conectadas.
4. Abrí la sesión y mandá un mensaje.

**Tenés que ver:** tu mensaje del celular aparece en la compu y Claude responde.

**Desde el celular podés:** mandar mensajes, mandar fotos y archivos (llegan a tu compu), ver los avances y los cambios, **contestar los pedidos de permiso y las preguntas de Claude**, cambiar el modo (**Manual**, **Accept edits**, **Plan**, **Auto**), el modelo y el esfuerzo, y frenar subagentes que estén corriendo.
**No podés:** usar comandos que son solo de la terminal (por ejemplo `/plugin` o `/resume`) ni elegir **Bypass permissions**.

**Probalo** (con Remote Control prendido, desde el celular):

```prompt
Contame en 3 líneas qué hiciste hasta ahora en esta sesión y qué falta. Avisame cuando termines lo que estás haciendo.
```

> **Ojo:** las notificaciones al celular ("terminé" o "necesito tu OK") se prenden con las opciones **Push when Claude decides** y **Push when actions required** de `/config`. La documentación lo explica para la terminal; en la app, `/config` abre **Settings › Code** y no confirmamos que estén ahí. Aceptá las notificaciones de la app de Claude en el celular igual.

### 3. Seguir una sesión en la nube desde el celular
No hace falta Remote Control: las sesiones en la nube ya están en tu cuenta.
1. App de Claude › **Code** › tocá la sesión.
2. Mirá cómo va, contestale si preguntó algo o cambiale el rumbo.
3. Para arrancar una nueva desde el celular: en **Code**, elegí el repo y la rama, escribí la tarea y mandala.

**Tenés que ver:** la misma sesión que arrancaste en la compu, con lo que hizo hasta ahora.

### 4. ¿Qué pasa si la compu se duerme o cerrás la app?
- **Remote Control:** la compu tiene que estar **prendida** y la app de Claude **abierta**. Si se duerme o se corta internet, se reconecta sola cuando vuelve. Si **cerrás la app**, la sesión queda desconectada hasta que la vuelvas a abrir.
- **Sesión en la nube:** sigue aunque cierres la app o apagues la compu.

> **Ojo:** la documentación no muestra una opción de la app para **mantener la compu despierta**. Si vas a usar Remote Control lejos de la compu, dejala enchufada y cambiá la opción de suspensión en la configuración de energía de tu compu (Mac: **Ajustes del Sistema**; Windows: **Configuración › Sistema › Energía**). Si tiene que andar con la compu apagada, usá la nube.

## ¿Qué uso: local, nube o Remote Control?
| | Local en la app | Sesión en la nube | Remote Control |
|---|---|---|---|
| **Dónde corre** | En tu compu | En una compu de Anthropic | En tu compu |
| **Cómo arranca** | **Code › Local › Open folder…** | **Code › Cloud**, [claude.ai/code](https://claude.ai/code) u **Open in › Cloud** | Interruptor **Remote Control** o `/remote-control` |
| **Con la compu apagada** | Se frena | Sigue | Se frena |
| **Tus archivos y conexiones** | Todos | Solo lo que está en GitHub | Todos |
| **Desde el celular** | No | Sí | Sí |
| **Ideal para** | El día a día del taller | Tareas largas o de noche, sobre un repo | Seguir algo de tu compu desde otro lado |

## Si querés X → usá Y
| Si querés… | Usá | Por qué |
|---|---|---|
| Pensar una idea, escribir un mail, revisar un texto | **Chat** | Rápido, sin instalar nada |
| Consultar tu cerebro desde el celular | **Projects** | Tus archivos cargados en todos los chats |
| Ordenar carpetas, armar planillas, informes o presentaciones sin código | **Cowork** | Trabaja tus archivos sin terminal |
| Armar tu cerebro, instalar programas, armar un bot, una web, editar video, automatizar | **Pestaña Code** de la app (Local), el camino del taller | Tiene tu compu entera a mano, con botones y sin terminal |
| Que trabaje mientras dormís o con la compu apagada | **Pestaña Code › Cloud** (Claude Code en la nube) | Corre en la compu de Anthropic |
| Cambiar algo en tu web o tu cerebro desde cualquier lado | **Claude Code en la nube** (app del celular › **Code**) | Trabaja sobre GitHub y te deja un PR |
| Seguir desde el celular algo que arrancaste en tu compu | **Remote Control** (interruptor de la sesión) | Sigue usando tus archivos y conexiones locales |
| Que algo pase solo todos los lunes | **Pestaña Code › Scheduled** | Ver [Tareas programadas](#t4-tareas-programadas) |
| Un bot que responde a clientes 24 h | **API** + n8n o un servidor | Ver [Las piezas](#t2-piezas) y [Asistente en Telegram](#p2-asistente-telegram) |

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo **Code** o no puedo elegir **Local** | Actualizá la app y revisá que tu plan sea Pro o superior ([Instalá Claude Code](#s2-claude-code)). |
| No veo **Cowork** en Windows | Falta permiso de administrador o **Virtual Machine Platform**. Reinstalá la app como admin. |
| En **Cloud** no aparece mi repo | Conectá GitHub e instalá la app de Claude en ese repo ([GitHub](#s4-github)). |
| **Open in › Cloud** da error de rama | Subí tus cambios a GitHub (**Push origin** en GitHub Desktop) y probá de nuevo. |
| Remote Control no conecta | Revisá que la compu esté prendida, con internet y la app abierta, y activalo de nuevo. |
| La sesión en la nube "se apagó" | Abrila de nuevo en [claude.ai/code](https://claude.ai/code): vuelve con la conversación. Pedile que retome lo que estaba corriendo. |

## Para seguir solo
- Creá un Proyecto en [claude.ai](https://claude.ai) con los archivos de tu cerebro y usalo una semana desde el celular.
- Mandá una tarea chica a la nube antes de irte a dormir y revisá el PR a la mañana.
- **Avanzado, en la terminal:** Claude Code también se usa escribiendo `claude` en la terminal, parado en la carpeta. Desde ahí, `claude --cloud "[TAREA]"` arranca una sesión en la nube, `claude --teleport` (o `/teleport` adentro) trae a tu compu una sesión de la nube, y `claude --remote-control` abre una sesión ya conectada al celular (con QR).
