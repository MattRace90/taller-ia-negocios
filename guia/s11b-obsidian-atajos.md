---
titulo: Usá Obsidian como un pro (atajos)
bloque: Setup
tiempo: 15 min
para: Todos
necesitas: s11-obsidian
resultado: Te movés por tu cerebro con el teclado, ves el grafo con colores por carpeta y capturás ideas al inbox en dos segundos.
---

Ya tenés tu cerebro abierto en Obsidian. Ahora aprendé las 10 teclas que usás todos los días: abrir una nota, ver con qué se conecta, anotar una idea al vuelo.
Ejemplo: en Fondus, alguien del equipo escucha una objeción nueva en una llamada. Aprieta **Cmd + N**, la anota, y el lunes Claude la ordena y la suma a `ventas/objeciones.md`.

> **Mac o Windows:** donde dice **Cmd**, en Windows es **Ctrl**. Donde dice **Option**, en Windows es **Alt**.

## Antes de empezar
- [ ] Obsidian abierto sobre la carpeta de tu cerebro ([Obsidian](#s11-obsidian)).
- [ ] Al menos 3 notas con links `[[...]]` entre ellas.
- [ ] Una carpeta `inbox/` en tu cerebro.

## Las teclas que vas a usar siempre
| Tecla | Qué hace |
|---|---|
| **Cmd + O** | Abrir una nota escribiendo parte del nombre |
| **Cmd + Shift + F** | Buscar una palabra en todo el cerebro |
| **Cmd + G** | Vista de grafo: todo el cerebro como red |
| **Cmd + N** | Nota nueva |
| **Cmd + P** | Paleta de comandos: cualquier cosa, escribiendo |
| **Cmd + E** | Pasar de editar a leer (y volver) |
| **Cmd + clic** en un link | Abrir la nota en otra pestaña |
| **Cmd + Option + ← / →** | Atrás / adelante, como en el navegador |
| **Cmd + ,** | Ajustes |
| **[[** | Insertar un link a otra nota |

## Paso 1 · Movete sin el mouse
1. Apretá **Cmd + O**, escribí `obj` y Enter: se abre `objeciones` (o la nota que tengas).
2. Hacé clic en cualquier link `[[...]]` de esa nota.
3. Volvé con **Cmd + Option + ←**.

**Tenés que ver:** saltaste de una nota a otra y volviste, sin tocar la lista de archivos.

## Paso 2 · Pintá el grafo por carpeta
1. **Cmd + G**. Cada punto es una nota y cada línea, un link.
2. Arriba a la derecha del grafo, tocá el **engranaje** › **Groups** (Grupos) › **New group**.
3. En el buscador del grupo escribí `path:ventas` y elegí un color. Repetí con `path:marca`, `path:negocio`, `path:operacion` y `path:inbox` (al inbox dale naranja).
4. En **Filters**, apagá **Tags** para que solo se vean notas.

**Tenés que ver:** el grafo con un color por carpeta. Los puntos sueltos son notas sin links: ahí falta conectar.

> **Tip:** para ver una sola parte, en **Filters** escribí `path:ventas`. Para resaltarla entre todas, creá un grupo y arrastralo **arriba de todo** (gana el primero que coincide).

## Paso 3 · Mirá quién apunta a cada nota
1. Abrí una nota importante (por ejemplo `negocio/oferta.md`).
2. Apretá **Cmd + P**, escribí `grafo local` (o `local graph`) y Enter: ves solo esa nota y sus vecinas. En su engranaje, subí **Depth** a 2.
3. Apretá **Cmd + P**, escribí `backlinks` (enlaces entrantes) y Enter: aparecen las notas que la linkean.
4. Abajo, en **Menciones sin enlazar**, tocá **Enlazar** en las que nombran la nota sin link.

**Tenés que ver:** la nota con sus vecinas en el grafo local y la lista de notas que la mencionan.

## Paso 4 · Capturá todo al inbox
1. **Cmd + ,** › **Archivos y enlaces** (Files and links) › **Ubicación por defecto para notas nuevas** › **En la carpeta especificada** › `inbox`.
2. **Cmd + ,** › **Plugins principales** (Core plugins) › activá **Notas diarias** (Daily notes). En sus opciones, carpeta: `inbox`.
3. Probá: **Cmd + N**, escribí una idea en una línea y cerrá la pestaña. Se guarda sola.

**Tenés que ver:** la nota nueva adentro de `inbox/`.

## Paso 5 · Armá tus propios atajos
1. **Cmd + ,** › **Atajos de teclado** (Hotkeys).
2. Buscá `grafo local` › tocá el **+** › apretá **Cmd + Shift + G**.
3. Repetí: `backlinks` › **Cmd + Shift + B** · `nota diaria` (Open today's daily note) › **Cmd + Option + D**.

**Tenés que ver:** al apretar **Cmd + Shift + G** se abre el grafo local de la nota en la que estás.

## Plantillas (opcional, 5 min)
1. Creá la carpeta `_plantillas/` con una nota `reunion.md`:
   ```text
   ---
   tipo: reunion
   fecha: {{date}}
   ---
   # {{title}}
   ## Decisiones
   ## Próximos pasos
   - [ ] Quién · qué · para cuándo
   ```
2. **Cmd + ,** › **Plugins principales** › activá **Plantillas** (Templates) › carpeta: `_plantillas`.
3. En una nota nueva: **Cmd + P** › `insertar plantilla` › `reunion`.

## Cómo sé que funcionó
1. **Cmd + N** y escribí: "Cliente preguntó si hacemos envíos al interior".
2. En Claude Code, parado en la carpeta del cerebro:

```prompt
Leé lo nuevo en inbox/. Decime en qué nota del cerebro lo sumarías y con qué notas lo enlazarías con [[...]]. Después hacelo y mostrame qué cambiaste.
```

3. En Obsidian, **Cmd + G**.

**Tenés que ver:** el punto naranja del inbox desapareció y la idea quedó conectada a su nota en el grafo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| **Cmd + G** no abre el grafo | **Cmd + ,** › **Plugins principales** › activá **Vista gráfica** (Graph view). |
| El grafo se ve todo gris | Faltan los grupos de color (Paso 2) o la consulta está mal escrita: es `path:` + nombre de carpeta, sin barra. |
| Aparecen puntos de notas que no existen | Son links a notas que no se crearon. En **Filters**, apagá **Existing files only**, o hacé clic y creala. |
| La nota nueva no cae en `inbox/` | Revisá el Paso 4.1: la carpeta tiene que existir y llamarse igual. |
| Un atajo no hace nada | Otro comando ya lo usa: en **Atajos de teclado** aparece en rojo. Elegí otra combinación. |

## Para seguir solo
- Fijá tus notas clave en **Marcadores**: clic derecho en la pestaña › **Marcar**.
- Escribí `/` en una línea vacía para insertar títulos, listas, tablas o plantillas sin recordar nada.
- Cuando tengas muchas notas, pedile a Claude que les agregue propiedades (`tipo`, `cliente`, `estado`) arriba de todo: Obsidian y Claude filtran mucho mejor.

## Fuentes
Consultadas el 18/11/2026.
- Atajos y plugins principales de Obsidian (vista gráfica, enlaces entrantes, notas diarias, plantillas): https://help.obsidian.md
- Configuración probada en Obsidian 1.15 sobre el cerebro de demo del taller.
