---
titulo: Usá tu borrador y mantenelo vivo
bloque: Tu cerebro
tiempo: 40 min hoy + 15 min por semana
para: Todos
necesitas: p1-cerebro
resultado: Tu borrador guardado en la carpeta del cerebro, integrado a su estructura, conectado a Claude donde trabajes, en GitHub privado y con una rutina para mantenerlo.
---

Antes del taller armamos para tu empresa un archivo `CONTEXTO-borrador.md`. Lo descargás de la tabla de abajo. Lo armamos con tu formulario y el material que nos compartiste. No es tu cerebro terminado: es el punto de partida, con lo que sabemos ordenado y lo que falta marcado como `PENDIENTE` o `⚠️ CONFIRMAR`.
Esta página te dice dónde guardarlo, cómo hacer que Claude lo use en cualquier lugar donde trabajes y cómo mantenerlo al día sin que se vuelva otro documento olvidado.

> **Tip:** si ya hiciste [Armá tu cerebro](#p1-cerebro), los Pasos 1 y 2 de esta página ya están hechos: chequeá el **Tenés que ver** de cada uno y seguí desde el Paso 3.

## Descargá tu borrador
| Empresa | Tu borrador |
|---|---|
| Fondus | [Descargar](https://drive.usercontent.google.com/download?id=1gbWsJwa3srqf8l8LlgPRoNdcmDcZe0Ok&export=download) · [Ver](https://drive.google.com/file/d/1gbWsJwa3srqf8l8LlgPRoNdcmDcZe0Ok/view) |
| La Consejera del Éxito | [Descargar](https://drive.usercontent.google.com/download?id=17kJd3u073gjzCPQkPjCsOLWn37Ch93bP&export=download) · [Ver](https://drive.google.com/file/d/17kJd3u073gjzCPQkPjCsOLWn37Ch93bP/view) |
| Manuel Martínez Oratoria | [Descargar](https://drive.usercontent.google.com/download?id=1fZWVkIVVbCPtkw7k_EM0b0KAK9-TW9gx&export=download) · [Ver](https://drive.google.com/file/d/1fZWVkIVVbCPtkw7k_EM0b0KAK9-TW9gx/view) |
| Denvet | [Descargar](https://drive.usercontent.google.com/download?id=1V3NIi539JU53E5P13wyZvH1QhG8hat50&export=download) · [Ver](https://drive.google.com/file/d/1V3NIi539JU53E5P13wyZvH1QhG8hat50/view) |
| Celve | [Descargar](https://drive.usercontent.google.com/download?id=1QJXVTH7eTUACHmgvSaW16JXfhPWbWCqh&export=download) · [Ver](https://drive.google.com/file/d/1QJXVTH7eTUACHmgvSaW16JXfhPWbWCqh/view) |
| Viajes TDH Docta | [Descargar](https://drive.usercontent.google.com/download?id=1FbzzahCkxQtXiT8KyqOkNl-h4FhmhC9o&export=download) · [Ver](https://drive.google.com/file/d/1FbzzahCkxQtXiT8KyqOkNl-h4FhmhC9o/view) |

> **Tip:** "Descargar" baja el archivo `.md` directo. Si el navegador lo abre como texto en vez de bajarlo, usá **Archivo › Guardar como…** y guardalo con el nombre `CONTEXTO-borrador.md`.

## Antes de empezar
- [ ] Tu archivo `CONTEXTO-borrador.md`, descargado de la tabla de abajo (queda en tu carpeta **Descargas**). Si no lo encontrás, pedilo en la mesa de ayuda.
- [ ] La carpeta del cerebro creada: `Documentos/cerebro-[TU-EMPRESA]` ([Armá tu cerebro](#p1-cerebro), Paso 1).
- [ ] Claude Code instalado ([Claude Code](#s2-claude-code)).
- [ ] Cuenta de GitHub, GitHub Desktop y tu nombre y mail cargados en Git ([GitHub](#s4-github), Pasos 1 a 4), para el Paso 5.

> **Datos:** el borrador es tuyo y es privado. No lo subas a ningún lugar público, no lo pegues en grupos y no lo compartas con otras empresas del taller.

## Paso 1 · Guardá el borrador en tu carpeta
Adentro de la carpeta del cerebro, creá una subcarpeta `fuentes` y guardá ahí el archivo. `fuentes/` es donde viven los documentos de origen: Claude los lee, pero no son el cerebro en sí.

<div data-os="mac">

La ruta queda así:

```
~/Documents/cerebro-[TU-EMPRESA]/fuentes/CONTEXTO-borrador.md
```

1. En **Finder › Documentos › cerebro-[TU-EMPRESA]**, creá la carpeta `fuentes` (clic derecho en un lugar vacío › **Nueva carpeta**). Si ya existe, no hagas nada.
2. Arrastrá el `CONTEXTO-borrador.md` desde **Descargas** a `fuentes`.

</div>
<div data-os="win">

La ruta queda así:

```
C:\Users\[TU-USUARIO]\Documents\cerebro-[TU-EMPRESA]\fuentes\CONTEXTO-borrador.md
```

1. En el **Explorador de archivos › Documentos › cerebro-[TU-EMPRESA]**, creá la carpeta `fuentes` (clic derecho en un lugar vacío › **Nuevo › Carpeta**). Si ya existe, no hagas nada.
2. Arrastrá el `CONTEXTO-borrador.md` desde **Descargas** a `fuentes`.

> **Ojo:** si tu Windows guarda Documentos en OneDrive, la ruta es `C:\Users\[TU-USUARIO]\OneDrive\Documentos\cerebro-[TU-EMPRESA]`. Funciona igual, pero conviene que la carpeta del cerebro **no** esté sincronizada con OneDrive y GitHub a la vez. Si dudás, preguntá en la mesa.

</div>

> **Tip:** si lo dejaste suelto en la carpeta principal del cerebro, está bien igual: la skill `armar-mi-cerebro` lo encuentra y lo mueve sola a `fuentes/`.

**Tenés que ver:** la carpeta `fuentes` con el archivo adentro. Si lo abrís, son secciones numeradas del 1 al 15.

## Paso 2 · Que Claude lo integre a la estructura del cerebro
El borrador es un solo archivo largo. El cerebro son varios archivos cortos, uno por tema, y un `CLAUDE.md` que Claude lee siempre. Hay que repartirlo.

Abrí Claude Code parado en la carpeta del cerebro.

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

> **Tip:** si el `cd` da error, escribí `cd ` (con espacio), arrastrá la carpeta del cerebro a la ventana de la terminal, apretá **Enter** y después escribí `claude`.

**Opción A (recomendada):** si instalaste la skill en [Armá tu cerebro](#p1-cerebro), escribí `/armar-mi-cerebro`. Hace todo esto y te entrevista.

**Opción B:** si no tenés la skill, pegá este prompt:

```prompt
En fuentes/CONTEXTO-borrador.md está el borrador del cerebro de mi empresa. Quiero que lo conviertas en un cerebro ordenado en esta carpeta.

1. Leelo entero y contame en 5 líneas qué entendiste del negocio y cuántos PENDIENTE y ⚠️ CONFIRMAR tiene.
2. Creá esta estructura (si algo ya existe, completalo, no lo borres): CLAUDE.md, README.md, negocio/ (empresa, oferta-y-precios, cliente-ideal, competencia), marca/ (voz, identidad-visual), ventas/ (proceso, preguntas-frecuentes, objeciones, guiones), equipo/organizacion.md, operacion/ (herramientas, procesos, donde-se-va-el-tiempo), datos/reglas.md, objetivos/ (casos-de-uso, pendientes).
3. Pasá cada sección del borrador al archivo que corresponde, reescrita y ordenada, no copiada en bloque. No inventes nada: lo que no está, queda como PENDIENTE.
4. Juntá todos los PENDIENTE y ⚠️ CONFIRMAR en objetivos/pendientes.md, ordenados: primero los que bloquean casos de uso, después la voz de la marca, después el resto.
5. Escribí un CLAUDE.md de menos de 80 líneas: quiénes somos, reglas que nunca se rompen, cómo hablamos y dónde está cada cosa.
6. Dejá el borrador original en fuentes/ sin tocarlo.

Antes de escribir, mostrame el plan y esperá mi OK.
```

**Tenés que ver:** las carpetas nuevas (`negocio/`, `marca/`, `ventas/`…), un `CLAUDE.md` corto y `objetivos/pendientes.md` con la lista de lo que falta.

## Paso 3 · Resolvé los PENDIENTE y los ⚠️ CONFIRMAR
- `PENDIENTE` = un dato que no tenemos. Ejemplo: la respuesta oficial a una pregunta frecuente.
- `⚠️ CONFIRMAR` = un dato que tenemos, pero con dos versiones que no coinciden (por ejemplo, dos personas del equipo contestaron distinto en el formulario).

En tu `LEEME.md` te marcamos los 5 o 6 más importantes. Arrancá por esos. Pegá esto:

```prompt
Entrevistame para resolver los pendientes del cerebro. Reglas:
- Leé objetivos/pendientes.md y arrancá por estos, en este orden: [PEGÁ ACÁ LOS PENDIENTES CLAVE DE TU LEEME, O BORRÁ ESTA LÍNEA].
- Preguntame de a 3, numeradas. Si el cerebro da una pista, sumá "Sugerencia: …" y yo contesto "sí", "no", "después" o la respuesta correcta.
- En los ⚠️ CONFIRMAR, mostrame las dos versiones y preguntame cuál vale.
- Después de cada tanda, guardá las respuestas en el archivo que corresponde, tachá lo resuelto en objetivos/pendientes.md y decime en una línea qué guardaste y dónde, y cuántos pendientes quedan.
- Nunca guardes datos personales de clientes, contraseñas ni claves, aunque yo los escriba.
- Si digo "basta por hoy", cerrá con un resumen.
```

Cómo contestar para que rinda:
- Contestá como le hablarías a un empleado nuevo: corto y concreto.
- Para la voz de tu marca, pegá 2 o 3 mensajes reales tuyos (un WhatsApp, un posteo, la transcripción de un audio). Rinde más que describirte.
- Si la respuesta la sabe otra persona del equipo, contestá "después: lo sabe [NOMBRE]" y Claude lo anota con su nombre.

**Tenés que ver:** el número de pendientes bajando después de cada tanda.

> **Tip:** no hace falta resolver todo hoy. Con los 5 o 6 clave ya tenés un cerebro que sirve para los desafíos de la tarde.

## Paso 4 · Conectalo a Claude donde trabajes
El cerebro son archivos. Cada forma de usar Claude los lee de una manera distinta.

| Dónde trabajás | Cómo lo lee | Qué hacés |
|---|---|---|
| **Claude Code** (terminal o pestaña **Code** de la app) | Lee `CLAUDE.md` solo, cada vez que lo abrís en la carpeta. El resto lo lee cuando lo necesita. | Abrís Claude Code **parado en la carpeta del cerebro**. Nada más. |
| **Proyectos** de [claude.ai](https://claude.ai) (web, app y celular) | Lee los archivos que subiste como conocimiento del proyecto. | Creás un proyecto y subís los archivos (ver abajo). |
| **Cowork** (app de escritorio) | Lee y escribe en la carpeta que le das. | Le das acceso a la carpeta del cerebro. |
| **Obsidian** | No es una IA: es para que **vos** leas y edites el cerebro cómodo. | **Abrir carpeta como bóveda** ([Obsidian](#s11-obsidian)). |

**Claude Code:** en la pestaña **Code** de la app, elegí **Local › Open folder…** y abrí `cerebro-[TU-EMPRESA]`. En la terminal, `cd` a la carpeta y `claude`. Para chequear que lo lee, preguntá:

```prompt
Sin que te cuente nada: ¿qué vendemos, a quién y cuál es la regla que nunca rompemos?
```

**Proyectos (para usarlo desde el celular o con tu equipo):**
1. En [claude.ai](https://claude.ai), entrá a **Projects** y creá uno nuevo: `Cerebro [TU EMPRESA]`.
2. En el conocimiento del proyecto (la zona para agregar archivos), arrastrá desde Finder o el Explorador el `CLAUDE.md` y los archivos de `negocio/`, `marca/` y `ventas/`. No subas `fuentes/`.
3. En las instrucciones del proyecto pegá: "Sos el asistente de [TU EMPRESA]. Antes de responder, usá los archivos del proyecto. Si un dato no está, decí que no lo sabés."

> **Ojo:** los nombres exactos de los botones de Proyectos cambian seguido. Verificá en tu pantalla. Los archivos que subís son una **copia**: cuando cambies el cerebro, volvé a subir los archivos que cambiaron (ver la rutina mensual). Si tu plan lo permite, también podés agregar archivos directo desde tu repo de GitHub.

**Cowork:** en la app de escritorio, abrí **Cowork** y, cuando te pida una carpeta, elegí `cerebro-[TU-EMPRESA]`. Pedile: "Leé el CLAUDE.md de esta carpeta antes de cada tarea".

> **Ojo:** verificá en tu app dónde se elige la carpeta en Cowork; la ubicación del botón puede variar según la versión.

**Tenés que ver:** en cualquiera de los tres, Claude responde sobre tu negocio sin que le expliques nada.

## Paso 5 · Guardalo en GitHub (privado)
Si ya lo hiciste en [Armá tu cerebro](#p1-cerebro), Paso 6, saltá este paso.

1. En Claude Code:

```prompt
Prepará esta carpeta para Git: creá un .gitignore que excluya .env, *.key, .DS_Store y cualquier archivo de fuentes/ que tenga datos personales de clientes (el CONTEXTO-borrador.md no se excluye: va al repo privado). Inicializá el repositorio y hacé el primer commit con el mensaje "Cerebro inicial con el borrador integrado".
```

2. En **GitHub Desktop › File › Add local repository**, tocá **Choose…**, elegí `cerebro-[TU-EMPRESA]` (en **Documentos**) y tocá **Add repository**.
3. Arriba, tocá **Publish repository**, dejá tildado **Keep this code private** y tocá **Publish Repository**.

**Tenés que ver:** en [github.com](https://github.com), tu repo `cerebro-[TU-EMPRESA]` con el candado de privado.

> **Ojo:** el borrador tiene información interna de tu empresa. El repo tiene que ser **privado** siempre.

## Paso 6 · Mantenelo vivo
Un cerebro desactualizado es peor que no tenerlo: la IA responde con seguridad cosas que ya no son así. Dos rutinas cortas alcanzan.

**Cada semana (15 min, por ejemplo el lunes):**

```prompt
Rutina semanal del cerebro:
1. Mostrame los 5 pendientes más importantes de objetivos/pendientes.md y preguntámelos de a uno.
2. Preguntame si esta semana cambió algo: precios, productos, promociones, equipo, herramientas, una pregunta nueva de clientes o una objeción nueva.
3. Guardá cada respuesta en su archivo y al final listame qué archivos cambiaste.
```

Después, en **GitHub Desktop**: abajo a la izquierda, en **Summary**, escribí un resumen ("Rutina semana 24/11"), tocá **Commit to main** y después, arriba, **Push origin**.

**Cada mes (30 min, por ejemplo el primer día hábil):**

```prompt
Revisión mensual del cerebro:
1. Buscá datos viejos o que se contradicen entre archivos (precios, fechas, nombres, promociones vencidas) y listámelos.
2. Revisá que CLAUDE.md siga teniendo menos de 80 líneas y que todo lo que dice esté vigente.
3. Decime qué archivos cambiaron este mes, así los vuelvo a subir a mi Proyecto de claude.ai.
4. Proponeme 1 caso de uso nuevo según lo que aprendimos este mes.
No cambies nada sin mostrarme antes qué vas a cambiar.
```

> **Tip:** podés dejar la rutina semanal programada para que Claude te la recuerde o arranque sola ([Tareas programadas](#t4-tareas-programadas)).

**Tenés que ver:** después de la rutina, en GitHub Desktop la lista de archivos que cambiaron, y en [github.com](https://github.com) tu commit nuevo.

**Quién lo actualiza:**
- **Un responsable** del cerebro (en general, el dueño o quien coordina). Es quien aprueba los cambios y hace el **Push**.
- El resto del equipo **propone**: le manda al responsable lo que cambió ("subió el precio de X", "nos preguntan mucho Y"), o edita en una rama si ya maneja GitHub.
- Regla simple: si algo cambia en el negocio, cambia en el cerebro **esa misma semana**.

**Lo que nunca va adentro:**
- Contraseñas, claves de API, tokens, números de cuenta o de tarjeta.
- Datos personales de clientes: nombres, DNI, teléfonos, mails, deudas, datos de salud.
- Grabaciones o transcripciones de llamadas con clientes (de ahí se saca **el método**, no los datos).
- Contratos firmados o documentos con datos de terceros.

## Cómo sé que funcionó
- [ ] El borrador está en `fuentes/` y el cerebro tiene sus carpetas y un `CLAUDE.md` corto.
- [ ] Resolviste al menos los pendientes clave de tu `LEEME.md`.
- [ ] Claude responde bien sobre tu negocio en Claude Code (y en un Proyecto, si lo armaste).
- [ ] El repo está en GitHub como **privado**.
- [ ] Agendaste la rutina semanal.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude no encuentra el borrador | Abriste `claude` fuera de la carpeta. Cerrá con `/exit`, hacé `cd` a `cerebro-[TU-EMPRESA]` y abrilo de nuevo. |
| Copió el borrador entero en un solo archivo | "Repartilo en los archivos de la estructura, uno por tema, y dejá CLAUDE.md en menos de 80 líneas." |
| Inventó una respuesta que estaba como PENDIENTE | "Eso no lo dijimos nosotros. Volvelo a PENDIENTE y preguntámelo." |
| En el Proyecto de [claude.ai](https://claude.ai) responde algo viejo | Los archivos del proyecto son una copia: subí de nuevo los que cambiaste. |
| GitHub Desktop no reconoce la carpeta | Falta inicializar Git: hacé el Paso 5.1. |
| El commit falla con "Please tell me who you are" | Git no tiene tu nombre y mail: hacé [GitHub](#s4-github), Paso 4, y pedile a Claude que repita el commit. |
| No sé qué contestar en un ⚠️ CONFIRMAR | Contestá "después: lo define [NOMBRE]" y seguí. Lo importante es que quede anotado. |

## Para seguir solo
- **Sumá a tu equipo:** invitalos a tu repo privado en GitHub (**Settings › Collaborators**) o compartiles el Proyecto de [claude.ai](https://claude.ai).
- **Usá el cerebro en todo:** cada desafío de la tarde (agente, propuestas, contenido, reportes) lee de esta carpeta. Cuanto mejor el cerebro, mejores los resultados.
- **Guardá lo que aprendés:** cuando Claude te sirva una respuesta nueva para un cliente, pedile "guardá esto en ventas/preguntas-frecuentes.md". Así el cerebro crece solo con el uso.
