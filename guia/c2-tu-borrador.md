---
titulo: Usá tu borrador y mantenelo vivo
bloque: Tu cerebro
tiempo: 40 min hoy + 15 min por semana
para: Todos
necesitas: p1-cerebro
resultado: Tu borrador guardado en la carpeta del cerebro, integrado a su estructura, conectado a Claude donde trabajes, en GitHub privado y con una rutina para mantenerlo.
---

Antes del taller armamos para tu empresa un archivo `CONTEXTO-borrador.md`, con tu formulario y el material que nos compartiste. No es tu cerebro terminado: es el punto de partida, con lo que sabemos ordenado y lo que falta marcado como `PENDIENTE` o `⚠️ CONFIRMAR`.
Acá ves dónde guardarlo, cómo hacer que Claude lo use y cómo mantenerlo al día. Todo desde la **pestaña Code** de la app de Claude.

> **Tip:** si ya hiciste [Armá tu cerebro](#p1-cerebro), los Pasos 1 y 2 ya están hechos: chequeá el **Tenés que ver** de cada uno y seguí desde el Paso 3.

## Descargá tu borrador
| Empresa | Tu borrador |
|---|---|
| Fondus | [Descargar](https://drive.usercontent.google.com/download?id=1gbWsJwa3srqf8l8LlgPRoNdcmDcZe0Ok&export=download) · [Ver](https://drive.google.com/file/d/1gbWsJwa3srqf8l8LlgPRoNdcmDcZe0Ok/view) |
| La Consejera del Éxito | [Descargar](https://drive.usercontent.google.com/download?id=17kJd3u073gjzCPQkPjCsOLWn37Ch93bP&export=download) · [Ver](https://drive.google.com/file/d/17kJd3u073gjzCPQkPjCsOLWn37Ch93bP/view) |
| Manuel Martínez Oratoria | [Descargar](https://drive.usercontent.google.com/download?id=1fZWVkIVVbCPtkw7k_EM0b0KAK9-TW9gx&export=download) · [Ver](https://drive.google.com/file/d/1fZWVkIVVbCPtkw7k_EM0b0KAK9-TW9gx/view) |
| Denvet | [Descargar](https://drive.usercontent.google.com/download?id=1V3NIi539JU53E5P13wyZvH1QhG8hat50&export=download) · [Ver](https://drive.google.com/file/d/1V3NIi539JU53E5P13wyZvH1QhG8hat50/view) |
| Celve | [Descargar](https://drive.usercontent.google.com/download?id=1QJXVTH7eTUACHmgvSaW16JXfhPWbWCqh&export=download) · [Ver](https://drive.google.com/file/d/1QJXVTH7eTUACHmgvSaW16JXfhPWbWCqh/view) |
| Viajes TDH Docta | [Descargar](https://drive.usercontent.google.com/download?id=1FbzzahCkxQtXiT8KyqOkNl-h4FhmhC9o&export=download) · [Ver](https://drive.google.com/file/d/1FbzzahCkxQtXiT8KyqOkNl-h4FhmhC9o/view) |
| VetPlus | [Descargar](https://drive.usercontent.google.com/download?id=1uIdI571hR-AIgtpQYEOX8XvLtnvoNSFm&export=download) · [Ver](https://drive.google.com/file/d/1uIdI571hR-AIgtpQYEOX8XvLtnvoNSFm/view) |

> **Tip:** "Descargar" baja el archivo `.md` directo. Si el navegador lo abre como texto, usá **Archivo › Guardar como…** y guardalo como `CONTEXTO-borrador.md`.

## Antes de empezar
- [ ] Tu `CONTEXTO-borrador.md`, descargado de la tabla de arriba (queda en **Descargas**). Si no lo encontrás, pedilo en la mesa de ayuda.
- [ ] La carpeta del cerebro creada: `Documentos/cerebro-[TU-EMPRESA]` ([Armá tu cerebro](#p1-cerebro), Paso 1).
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).
- [ ] GitHub Desktop con tu cuenta iniciada ([GitHub](#s4-github)), para el Paso 5.

> **Datos:** el borrador es tuyo y es privado. No lo subas a ningún lugar público, no lo pegues en grupos y no lo compartas con otras empresas del taller.

## Paso 1 · Guardá el borrador en `fuentes/`
`fuentes/` es donde viven los documentos de origen: Claude los lee, pero no son el cerebro en sí.

<div data-os="mac">

En **Finder › Documentos › cerebro-[TU-EMPRESA]**, creá la carpeta `fuentes` (clic derecho › **Nueva carpeta**) si no existe, y arrastrá ahí el borrador desde **Descargas**.

</div>
<div data-os="win">

En el **Explorador de archivos › Documentos › cerebro-[TU-EMPRESA]**, creá la carpeta `fuentes` (clic derecho › **Nuevo › Carpeta**) si no existe, y arrastrá ahí el borrador desde **Descargas**.

> **Ojo:** si tu Documentos está en OneDrive, funciona igual, pero conviene que el cerebro **no** esté sincronizado con OneDrive y GitHub a la vez. Si dudás, preguntá en la mesa.

</div>

O pedíselo a Claude, con la carpeta del cerebro abierta en la pestaña Code:

```prompt
Buscá CONTEXTO-borrador.md en mi carpeta Descargas y movelo a la carpeta fuentes de esta carpeta (creala si no existe).
```

**Tenés que ver:** `fuentes/CONTEXTO-borrador.md`. Si lo abrís, son secciones numeradas del 1 al 15.

## Paso 2 · Que Claude lo reparta en el cerebro
El borrador es un solo archivo largo. El cerebro son varios archivos cortos, uno por tema, y un `CLAUDE.md` que Claude lee siempre.

1. En la app, **Code › + New**, entorno **Local**, **Open folder…** y elegí `cerebro-[TU-EMPRESA]`.
2. **Opción A (recomendada):** escribí `/armar-mi-cerebro` (la skill de [Armá tu cerebro](#p1-cerebro), Paso 3). Hace todo y te entrevista.
3. **Opción B:** si no tenés la skill, pegá esto:

```prompt
En fuentes/CONTEXTO-borrador.md está el borrador del cerebro de mi empresa. Convertilo en un cerebro ordenado en esta carpeta.

1. Leelo entero y contame en 5 líneas qué entendiste del negocio y cuántos PENDIENTE y ⚠️ CONFIRMAR tiene.
2. Creá esta estructura (si algo existe, completalo, no lo borres): CLAUDE.md, README.md, negocio/ (empresa, oferta-y-precios, cliente-ideal, competencia), marca/ (voz, identidad-visual), ventas/ (proceso, preguntas-frecuentes, objeciones, guiones), equipo/organizacion.md, operacion/ (herramientas, procesos, donde-se-va-el-tiempo), datos/reglas.md, objetivos/ (casos-de-uso, pendientes).
3. Pasá cada sección al archivo que corresponde, reescrita y ordenada. No inventes nada: lo que no está queda como PENDIENTE.
4. Juntá todos los PENDIENTE y ⚠️ CONFIRMAR en objetivos/pendientes.md: primero los que bloquean casos de uso, después la voz de la marca, después el resto.
5. Escribí un CLAUDE.md de menos de 80 líneas: quiénes somos, reglas que nunca se rompen, cómo hablamos y dónde está cada cosa.
6. Dejá el borrador original en fuentes/ sin tocarlo.

Antes de escribir, mostrame el plan y esperá mi OK.
```

Aprobá los pedidos de permiso para crear archivos.

**Tenés que ver:** las carpetas nuevas (`negocio/`, `marca/`, `ventas/`…), un `CLAUDE.md` corto y `objetivos/pendientes.md`.

## Paso 3 · Resolvé los PENDIENTE y los ⚠️ CONFIRMAR
- `PENDIENTE` = un dato que no tenemos (por ejemplo, la respuesta oficial a una pregunta frecuente).
- `⚠️ CONFIRMAR` = un dato con dos versiones que no coinciden (por ejemplo, dos personas del equipo contestaron distinto).

En tu `LEEME.md` te marcamos los 5 o 6 más importantes. Arrancá por esos:

```prompt
Entrevistame para resolver los pendientes del cerebro. Reglas:
- Leé objetivos/pendientes.md y arrancá por estos, en este orden: [PEGÁ ACÁ LOS PENDIENTES CLAVE DE TU LEEME, O BORRÁ ESTA LÍNEA].
- Preguntame de a 3, numeradas. Si el cerebro da una pista, sumá "Sugerencia: …" y yo contesto "sí", "no", "después" o la respuesta correcta.
- En los ⚠️ CONFIRMAR, mostrame las dos versiones y preguntame cuál vale.
- Después de cada tanda, guardá las respuestas en su archivo, tachá lo resuelto en objetivos/pendientes.md y decime en una línea qué guardaste y cuántos pendientes quedan.
- Nunca guardes datos personales de clientes, contraseñas ni claves, aunque yo los escriba.
- Si digo "basta por hoy", cerrá con un resumen.
```

Si la respuesta la sabe otra persona del equipo, contestá "después: lo sabe [NOMBRE]".

**Tenés que ver:** el número de pendientes bajando después de cada tanda.

## Paso 4 · Conectalo a Claude donde trabajes
| Dónde trabajás | Cómo lo lee | Qué hacés |
|---|---|---|
| **Pestaña Code** de la app (camino del taller) | Lee `CLAUDE.md` solo, cada vez que abrís la carpeta. El resto, cuando lo necesita. | **Code › + New › Local › Open folder…** y elegís `cerebro-[TU-EMPRESA]`. Nada más. |
| **Proyectos** de [claude.ai](https://claude.ai) (web, app y celular) | Lee los archivos que subiste al proyecto. | Creás un proyecto y subís los archivos (abajo). |
| **Cowork** (app de escritorio) | Lee y escribe en la carpeta que le das. | Le das acceso a la carpeta del cerebro. |
| **Obsidian** | No es una IA: es para que **vos** leas y edites cómodo. | **Abrir carpeta como bóveda** ([Obsidian](#s11-obsidian)). |

Para chequear que lo lee, en una sesión nueva:

```prompt
Sin que te cuente nada: ¿qué vendemos, a quién y cuál es la regla que nunca rompemos?
```

**Proyectos (celular o equipo):**
1. En [claude.ai](https://claude.ai) › **Projects**, creá `Cerebro [TU EMPRESA]`.
2. En los archivos del proyecto, arrastrá `CLAUDE.md` y lo de `negocio/`, `marca/` y `ventas/`. No subas `fuentes/`.
3. En las instrucciones: "Sos el asistente de [TU EMPRESA]. Antes de responder, usá los archivos del proyecto. Si un dato no está, decí que no lo sabés."

> **Ojo:** los nombres de los botones de Proyectos cambian seguido. Y los archivos que subís son una **copia**: cuando cambies el cerebro, volvé a subir los que cambiaron.

**Cowork:** en la app, abrí **Cowork**, elegí la carpeta `cerebro-[TU-EMPRESA]` y pedile: "Leé el CLAUDE.md de esta carpeta antes de cada tarea".

> **Ojo:** el lugar donde se elige la carpeta en Cowork puede variar según la versión de la app.

**Tenés que ver:** Claude responde sobre tu negocio sin que le expliques nada.

## Paso 5 · Guardalo en GitHub (privado)
Si ya lo hiciste en [Armá tu cerebro](#p1-cerebro), Paso 6, saltá este paso.

1. En la pestaña Code:

```prompt
Creá un .gitignore en esta carpeta que excluya .env, *.key, .DS_Store y cualquier archivo de fuentes/ con datos personales de clientes (el CONTEXTO-borrador.md sí va: el repo es privado).
```

2. En **GitHub Desktop › File › Add local repository** › **Choose…** › `cerebro-[TU-EMPRESA]` › **Add repository**. Si dice que no es un repositorio: **create a repository › Create repository**.
3. **Publish repository**, con **Keep this code private** tildado › **Publish Repository**.

**Tenés que ver:** en [github.com](https://github.com), tu repo `cerebro-[TU-EMPRESA]` con el candado de privado.

> **Ojo:** el borrador tiene información interna de tu empresa. El repo tiene que ser **privado** siempre.

## Paso 6 · Mantenelo vivo
Un cerebro desactualizado es peor que no tenerlo: la IA responde con seguridad cosas que ya no son así.

**Cada semana (15 min, por ejemplo el lunes),** en la pestaña Code con la carpeta abierta:

```prompt
Rutina semanal del cerebro:
1. Mostrame los 5 pendientes más importantes de objetivos/pendientes.md y preguntámelos de a uno.
2. Preguntame si esta semana cambió algo: precios, productos, promociones, equipo, herramientas, una pregunta o una objeción nueva.
3. Guardá cada respuesta en su archivo y al final listame qué archivos cambiaste.
```

Después, en **GitHub Desktop**: escribí un resumen en **Summary** ("Rutina semana 24/11"), tocá **Commit to main** y después **Push origin**.

**Cada mes (30 min):**

```prompt
Revisión mensual del cerebro:
1. Buscá datos viejos o que se contradicen entre archivos (precios, fechas, nombres, promociones vencidas) y listámelos.
2. Revisá que CLAUDE.md siga con menos de 80 líneas y todo vigente.
3. Decime qué archivos cambiaron este mes, así los vuelvo a subir a mi Proyecto de claude.ai.
4. Proponeme 1 caso de uso nuevo según lo que aprendimos este mes.
No cambies nada sin mostrarme antes qué vas a cambiar.
```

> **Tip:** podés dejar la rutina semanal programada desde la pestaña Code › **Scheduled** ([Tareas programadas](#t4-tareas-programadas)).

**Quién lo actualiza:** un **responsable** (en general, el dueño) aprueba los cambios y hace el **Push**. El resto del equipo le avisa lo que cambió. Regla: si algo cambia en el negocio, cambia en el cerebro **esa misma semana**.

**Lo que nunca va adentro:** contraseñas, claves, tokens, números de cuenta o tarjeta; datos personales de clientes (nombres, DNI, teléfonos, mails, deudas, salud); grabaciones o transcripciones de llamadas con clientes (de ahí se saca **el método**, no los datos); contratos firmados.

**Tenés que ver:** en GitHub Desktop, la lista de archivos que cambiaron, y en [github.com](https://github.com), tu commit nuevo.

## Cómo sé que funcionó
- [ ] El borrador está en `fuentes/` y el cerebro tiene sus carpetas y un `CLAUDE.md` corto.
- [ ] Resolviste al menos los pendientes clave de tu `LEEME.md`.
- [ ] Claude responde bien sobre tu negocio en la pestaña Code (y en un Proyecto, si lo armaste).
- [ ] El repo está en GitHub como **privado**.
- [ ] Agendaste la rutina semanal.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude no encuentra el borrador | Abriste otra carpeta. Sesión nueva › **Open folder…** › `cerebro-[TU-EMPRESA]`. |
| Copió el borrador entero en un solo archivo | "Repartilo en los archivos de la estructura, uno por tema, y dejá CLAUDE.md en menos de 80 líneas." |
| Inventó una respuesta que estaba como PENDIENTE | "Eso no lo dijimos nosotros. Volvelo a PENDIENTE y preguntámelo." |
| En el Proyecto de claude.ai responde algo viejo | Los archivos del proyecto son una copia: subí de nuevo los que cambiaste. |
| GitHub Desktop no reconoce la carpeta | Tocá **create a repository** cuando te lo ofrezca (Paso 5.2). |
| No sé qué contestar en un ⚠️ CONFIRMAR | "Después: lo define [NOMBRE]" y seguí. |

## Para seguir solo
- **Sumá a tu equipo:** invitalos a tu repo privado (**Settings › Collaborators**) o compartiles el Proyecto de [claude.ai](https://claude.ai).
- **Usá el cerebro en todo:** cada desafío de la tarde lee de esta carpeta. Mejor cerebro, mejores resultados.
- **Guardá lo que aprendés:** cuando Claude te dé una buena respuesta para un cliente, pedile "guardá esto en ventas/preguntas-frecuentes.md".
