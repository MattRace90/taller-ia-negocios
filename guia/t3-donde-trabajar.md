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

## Claude Code en la web (agente en la nube)
Claude Code corriendo en una compu de Anthropic, no en la tuya. Le das una tarea y **sigue trabajando aunque cierres la laptop**.
- Se abre en la app de escritorio eligiendo **Cloud** en el selector de entorno, en [claude.ai/code](https://claude.ai/code) o en la pestaña **Code** de la app del celular.
- Trabaja sobre un **repo de GitHub**: lo copia, hace los cambios en una **rama** nueva (una copia aparte) y te propone un **pull request** (PR): un pedido para sumar esos cambios, que vos revisás y aceptás. Por eso necesitás [GitHub](#s4-github) conectado. Estas palabras están en el [glosario](#t2-piezas).
- Consume el mismo límite de uso de tu plan. La compu de la nube no se cobra aparte.

Ejemplo: desde el celular, Viajes TDH le pide "cambiá el precio del paquete a Mendoza en la web y abrí el PR". A la noche revisa el cambio y lo publica.

**Probalo** (entorno **Cloud**, con el repo de tu cerebro o tu web):

```prompt
Leé el CLAUDE.md de este repo. Revisá los archivos y armame una lista de lo que está desactualizado o dice PENDIENTE. No cambies nada: solo dejame la lista en notas/pendientes.md y abrí un PR.
```

## Pasar una sesión de tu compu a la nube
1. **Antes que nada:** subí tus cambios a GitHub (en GitHub Desktop: **Commit to main** y **Push origin**). La nube copia lo que está en GitHub.
2. En la pestaña Code, abrí el menú de la sesión (al lado del título, o en la fila de la barra lateral) › **Open in** › **Cloud**.
3. Leé el aviso: te dice qué pasa con los archivos y con la sesión local. Confirmá.

**Tenés que ver:** la sesión en la nube, trabajando (también la ves en [claude.ai/code](https://claude.ai/code)).

> **Ojo:** si tu carpeta no está en GitHub, puede subir una copia de la carpeta, con archivos sensibles como `.env`. Antes, revisá que no haya claves en la carpeta.

> **Tip:** planificá en tu compu y ejecutá en la nube. Usá el modo **Plan**, guardá el plan en un archivo, subilo a GitHub y abrí una sesión **Cloud** con "Ejecutá el plan de notas/plan-web.md".

## Remote Control: seguir desde el celular
Distinto de la nube: con Remote Control, **Claude sigue trabajando en tu compu** (con tus archivos y conexiones) y vos lo mirás y le escribís desde el celular o desde otro navegador.
1. En la sesión de la pestaña Code, activá el interruptor **Remote Control** (en la tarjeta **Environment** de la sesión) o escribí `/remote-control`. La primera vez confirmás con **Enable Remote Control**.
2. En el celular, abrí la app de Claude › **Code** y buscá la sesión. Las sesiones conectadas tienen un ícono de compu con un punto verde.
3. Para desconectar, apagá el interruptor o escribí `/remote-control` otra vez.

> **Ojo:** la compu tiene que quedar **prendida** y la app **abierta**. Si se duerme o se corta internet, se reconecta sola cuando vuelve. Si querés que siga con la compu apagada, usá la nube.

**Probalo:**

```prompt
/remote-control Taller
```

Después abrí la app de Claude en el celular, entrá a **Code** y mandá un mensaje a la sesión "Taller".

**Tenés que ver:** tu mensaje del celular aparece en la compu y Claude responde.

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

## Para seguir solo
- Creá un Proyecto en [claude.ai](https://claude.ai) con los archivos de tu cerebro y usalo una semana desde el celular.
- Mandá una tarea chica a la nube antes de irte a dormir y revisá el PR a la mañana.
- **Avanzado, en la terminal:** Claude Code también se usa escribiendo `claude` en la terminal, parado en la carpeta. Desde ahí, `claude --cloud "[TAREA]"` arranca una sesión en la nube, `claude --teleport` (o `/teleport` adentro) trae a tu compu una sesión de la nube, y `claude --remote-control` abre una sesión ya conectada al celular (con QR).
