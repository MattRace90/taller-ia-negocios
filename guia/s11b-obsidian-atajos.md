---
titulo: Usá Obsidian como un pro (atajos, opcional)
bloque: Setup
tiempo: 10 min
para: Opcional (todos)
necesitas: s11-obsidian
resultado: Te movés por tu cerebro con el teclado, ves el grafo con colores por carpeta y capturás ideas al inbox.
---

> **Opcional:** solo si ya instalaste Obsidian ([Obsidian](#s11-obsidian)). Para el taller **no hace falta**.

Las pocas teclas que usás todos los días en Obsidian.
Ejemplo: en Fondus, alguien escucha una objeción nueva en una llamada, aprieta **Cmd + N**, la anota, y después Claude la suma a `ventas/objeciones.md`.

> **Mac o Windows:** donde dice **Cmd**, en Windows es **Ctrl**. **Option** es **Alt**.

## Antes de empezar
- [ ] Obsidian abierto sobre la carpeta de tu cerebro ([Obsidian](#s11-obsidian)).
- [ ] Una carpeta `inbox/` en tu cerebro.

## Las teclas de siempre
| Tecla | Qué hace |
|---|---|
| **Cmd + O** | Abrir una nota escribiendo parte del nombre |
| **Cmd + Shift + F** | Buscar en todo el cerebro |
| **Cmd + G** | Grafo: todo el cerebro como red |
| **Cmd + N** | Nota nueva |
| **Cmd + P** | Paleta de comandos |
| **Cmd + Option + ← / →** | Atrás / adelante |
| **[[** | Link a otra nota |

## Paso 1 · Mandá las notas nuevas al inbox
**Cmd + ,** › **Archivos y enlaces** (Files and links) › **Ubicación por defecto para notas nuevas** › **En la carpeta especificada** › `inbox`.

**Tenés que ver:** con **Cmd + N**, la nota nueva cae en `inbox/`.

## Paso 2 · Pintá el grafo por carpeta
1. **Cmd + G** › engranaje arriba a la derecha › **Groups** › **New group**.
2. Escribí `path:ventas` y elegí un color. Repetí con `path:marca`, `path:negocio` y `path:inbox` (naranja).

**Tenés que ver:** un color por carpeta. Los puntos sueltos son notas sin links.

## Cómo sé que funcionó
1. **Cmd + N** y escribí: "Cliente preguntó si hacemos envíos al interior".
2. En la pestaña **Code**, con la carpeta del cerebro:

```prompt
Leé lo nuevo en inbox/, sumalo a la nota del cerebro que corresponda, enlazalo con [[...]] y mostrame qué cambiaste.
```

**Tenés que ver:** en el grafo, el punto naranja desapareció y la idea quedó conectada.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| **Cmd + G** no abre el grafo | **Cmd + ,** › **Plugins principales** › activá **Vista gráfica** (Graph view). |
| El grafo se ve gris | Faltan los grupos (Paso 2) o está mal escrito: `path:` + carpeta, sin barra. |
| La nota no cae en `inbox/` | La carpeta tiene que existir y llamarse igual. |

## Para seguir solo
- **Cmd + P** › `local graph`: ves solo la nota abierta y sus vecinas.
- **Notas diarias** (Core plugins › Daily notes) a `inbox/`, y que Claude las ordene una vez por semana.
- Escribí `/` en una línea vacía para insertar títulos, tablas o plantillas.

## Fuentes
Consultadas el 18/11/2026.
- Ayuda de Obsidian: https://help.obsidian.md
