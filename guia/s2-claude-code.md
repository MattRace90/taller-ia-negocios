---
titulo: Claude Code en la pestaña Code de la app
bloque: Setup
tiempo: 15 min
para: Todos
necesitas: s1-claude
resultado: La pestaña Code abierta en una carpeta de tu compu, con Claude creando un archivo después de pedirte permiso.
---

Claude Code es Claude trabajando en tu compu: lee y escribe archivos, instala programas, arma bots y webs. Hoy lo usamos **desde la pestaña Code de la app de Claude**: es el mismo Claude Code, con botones, sin terminal y sin instalar nada aparte.
Ejemplo: Celve abre su carpeta del cerebro en Code y le pide "armame la lista de precios en una planilla"; Claude le pide permiso, crea el archivo y se lo muestra.

## Antes de empezar
- [ ] Plan **Pro** o superior y la app de escritorio instalada ([Tu cuenta](#s1-claude)). El plan gratis no incluye Claude Code.
- [ ] Mac con **macOS 13 (Ventura) o superior**, o Windows 10 actualizado o Windows 11.

## Paso 1 · Abrí la pestaña Code
En la app de Claude, tocá **Code** arriba de la barra lateral (al lado de **Chat** y **Cowork**).

**Tenés que ver:** un cuadro para escribir y, abajo de él, una fila de controles: el primero es el **selector de entorno** (dónde trabaja Claude) y al lado el de la **carpeta**.

## Paso 2 · Creá tu carpeta de prueba

<div data-os="mac">

Abrí **Finder** › **Documentos** › clic derecho en un lugar vacío › **Nueva carpeta** › llamala `prueba-claude`.

</div>
<div data-os="win">

Abrí el **Explorador de archivos** › **Documentos** › clic derecho en un lugar vacío › **Nuevo › Carpeta** › llamala `prueba-claude`.

</div>

**Tenés que ver:** la carpeta `prueba-claude` dentro de **Documentos**.

## Paso 3 · Elegí Local y la carpeta
1. En el selector de entorno, elegí **Local** (tu compu; no la nube).
2. Tocá el control de carpeta › **Open folder…** y elegí `Documentos/prueba-claude`.

> **Ojo:** el nombre del botón puede variar según la versión de la app (**Open folder…**, **Elegir carpeta** o el nombre de la última carpeta usada). Para una sesión nueva, también está **+ New** en la barra lateral.

**Tenés que ver:** el nombre `prueba-claude` en el control de carpeta, abajo del cuadro.

## Paso 4 · Tu primer pedido

```prompt
Creá un archivo hola.md con 3 ideas para usar IA en un negocio como el mío: [DESCRIBÍ TU NEGOCIO EN UNA LÍNEA]. Después mostrame qué archivos hay en esta carpeta.
```

Antes de crear el archivo, Claude te muestra un **pedido de permiso con botones** (permitir esta vez, permitir siempre o no). Leé qué va a hacer y aprobalo.

> **Tip:** los permisos son tu freno de mano. Si no entendés qué quiere hacer, tocá que no y preguntale "¿qué ibas a hacer y por qué?".

**Tenés que ver:** el cambio en pantalla y `hola.md` en la lista. Para verlo vos, abrí la carpeta `prueba-claude` en **Finder** o en el **Explorador**.

<div data-os="win">

> **Ojo:** si en Windows aparece un aviso de que falta **Git**, instalalo como dice [Herramientas base](#s3-herramientas-base), Paso 1, cerrá la app de Claude, volvé a abrirla y repetí.

</div>

## Paso 5 · Probá un comando
Escribí en el cuadro y mandalo:

```prompt
/context
```

**Tenés que ver:** cuánto de la memoria de la conversación está usada. Los demás comandos (`/compact`, `/clear`, `/btw`, las skills con `/nombre`) se escriben igual: están en la [machete de atajos](#t5-atajos).

## Cómo sé que funcionó
La pestaña **Code** está abierta en **Local** con la carpeta `prueba-claude`, y `hola.md` existe adentro.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo la pestaña **Code** | Revisá que el plan sea Pro o superior y actualizá la app (menú de la app › buscar actualizaciones). |
| No aparece **Local** en el selector | Actualizá la app. Si sigue, avisá en la mesa de ayuda. |
| Claude dice que no puede ver o tocar tus archivos | Revisá que elegiste **Local** y la carpeta correcta. Abrí una sesión nueva con **+ New** y elegila otra vez. |
| Tocaste "no" en un permiso sin querer | Pedile lo mismo de nuevo: te vuelve a preguntar. |
| Dice que tu plan no incluye Claude Code | Cerrá sesión y volvé a entrar con la cuenta que tiene Pro. |

## Para seguir solo
- Abrí siempre Code **en la carpeta del proyecto** (por ejemplo, la de tu cerebro): así Claude lee el `CLAUDE.md` de esa carpeta.
- Probá los modos de permiso (**Manual**, **Accept edits**, **Plan**…) en el selector de modo, o con **Cmd+Shift+M** (Mac) / **Ctrl+Shift+M** (Windows) para pasar al modo plan ([atajos](#t5-atajos)).
- Avanzado: cosas como `claude -p` o `claude --agent` (correr Claude sin conversación, o con un agente fijo) son de la versión de terminal. Mirá la alternativa de abajo.

## Alternativa: Claude Code en la terminal (opcional)
Si querés la versión de terminal (no hace falta hoy), abrí **Terminal** (Mac) o **PowerShell** (Windows) y pegá:

<div data-os="mac">

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

</div>
<div data-os="win">

```powershell
irm https://claude.ai/install.ps1 | iex
```

</div>

Cerrá la terminal, abrí una nueva, entrá a tu carpeta y escribí `claude`. La primera vez te pide iniciar sesión con tu cuenta de Claude. Si algo raro pasa, `claude doctor` te dice qué arreglar.

## Fuentes
Consultadas el 19/11/2026.
- App de escritorio y pestaña Code: https://code.claude.com/docs/en/desktop
- Instalación por terminal: https://code.claude.com/docs/en/setup
