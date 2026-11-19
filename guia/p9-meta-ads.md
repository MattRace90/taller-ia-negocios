---
titulo: Meta Ads con un equipo de agentes
bloque: Tutorial
tiempo: 60 a 75 min (demo guiada + práctica)
para: La Consejera del Éxito, Fondus (y cualquiera que invierta en Meta)
necesitas: p1-cerebro, s2-claude-code, s8-conectores-y-mcp
resultado: Un equipo de agentes (un coordinador y 4 especialistas) instalado en la carpeta de tu cerebro que revisa tus campañas, te dice cuánto invertir con números y solo toca tu cuenta cuando vos escribís APROBADO.
---

"¿Cuánto tengo que invertir en Meta?" es la pregunta de casi todos los negocios del taller. La respuesta no es un número mágico: depende de cuánto ganás por venta, de cuántas consultas necesitás para cerrar una y de cuánto te cuesta cada consulta hoy.
Hoy armás un equipo de agentes que hace esa cuenta cada semana: un coordinador reparte el trabajo; uno analiza, uno propone dónde poner la plata, uno escribe creativos nuevos y uno aplica los cambios. **El que aplica nunca toca nada sin tu aprobación por escrito.**

> **Tip:** palabras que vas a ver en esta página:
> - **Agente (subagente):** un asistente con un solo rol y sus propias reglas, al que Claude le pasa una parte del trabajo ([Las piezas](#t2-piezas)).
> - **Orquestador:** el agente coordinador. Habla con vos y reparte el trabajo.
> - **CSV:** una planilla guardada como texto. El Administrador de anuncios de Meta exporta tus campañas así.
> - **Conector o MCP:** el permiso para que Claude use otra app, acá tu cuenta de Meta Ads.
> - **Punto de equilibrio:** lo máximo que podés pagar por una consulta sin perder plata.

## Antes de empezar
- [ ] Tu cerebro armado, con precio y margen en `negocio/oferta-y-precios.md` y tasa de cierre en `ventas/proceso.md` ([Tu cerebro](#p1-cerebro)). Si no los tenés, los cargás en el Paso 6.
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] Para practicar: **nada más**. Usamos un CSV de campañas inventado.
- [ ] Para tu cuenta real (opcional, Paso 7): acceso de administrador a tu cuenta publicitaria en el portfolio comercial de Meta.

> **Datos:** las métricas de tus campañas no son datos personales, pero sí información de tu negocio. El CSV de práctica es **inventado**: una academia de cursos que no existe, con montos en pesos que no son de nadie.

## Cómo es el equipo
| Agente | Qué hace | Qué puede tocar |
|---|---|---|
| **orquestador** | Habla con vos, reparte el trabajo y junta las respuestas. | Solo archivos de la carpeta. |
| **analista** | Lee gasto, resultados, costo por resultado, frecuencia. Marca ganadores, fatiga y anuncios sin tracción. | Solo lectura. |
| **estratega** | Calcula tu punto de equilibrio con el margen del cerebro y propone apagar, escalar o mover plata, con escenarios. | Solo archivos. |
| **creativo** | Propone 3 ángulos y 9 primeras líneas con los dolores de tu cerebro. | Solo archivos. |
| **ejecutor** | Aplica en Meta **solo** lo que aprobaste, mostrando antes y después. | Tu cuenta de Meta, por el conector oficial. |

> **Ojo:** la regla de oro es **ningún cambio que gaste plata sin confirmación explícita de una persona**. En este equipo, la confirmación es escribir `APROBADO` y los números de los cambios ("APROBADO 1, 3"). "Dale" u "ok" no alcanzan: el orquestador te vuelve a mostrar la lista.

## Paso 1 · Prepará la carpeta
Todo vive dentro de la carpeta de tu cerebro.

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

**Tenés que ver:** Claude Code abierto en tu carpeta del cerebro.

Tocá **Copiar** en el CSV de práctica (abajo) y pegalo después de este prompt:

```prompt
Creá el archivo meta-ads/datos/meta-ads-ejemplo.csv con el texto que pego abajo, exacto y sin cambios. Son datos inventados para practicar. Creá también la carpeta meta-ads/informes/.

[PEGÁ ACÁ EL CSV]
```

<div data-include="kit/ejemplos/meta-ads-ejemplo.csv"></div>

**Tenés que ver:** el archivo `meta-ads/datos/meta-ads-ejemplo.csv` con 15 filas (una por anuncio) y la línea de títulos.

## Paso 2 · Instalá los 5 agentes
Los agentes de un proyecto viven en la carpeta `.claude/agents/` de ese proyecto. Así quedan con tu cerebro y, si lo subís a GitHub, tu equipo también los tiene.

Repetí esto **5 veces**, una por agente (cambiá `[NOMBRE-DEL-AGENTE]` cada vez): `orquestador`, `analista`, `estratega`, `creativo` y `ejecutor`. El texto de cada uno está en el [Kit del taller](#r-kit), sección **Los agentes de Meta Ads**: tocá **Copiar** y pegalo después del prompt.

```prompt
Creá el archivo .claude/agents/[NOMBRE-DEL-AGENTE].md en esta carpeta con el texto que pego abajo, exacto y sin cambios (incluido el encabezado entre las líneas ---). Cuando termines, decime la ruta.

[PEGÁ ACÁ EL TEXTO DEL AGENTE]
```

Cuando estén los 5, salí con `/exit` y volvé a entrar con `claude`. Preguntá:

```prompt
¿Qué subagentes tenés disponibles en este proyecto? Para cada uno decime en una línea qué hace y qué herramientas tiene.
```

**Tenés que ver:** los 5 agentes listados. El orquestador con `Agent(analista, estratega, creativo, ejecutor), Read, Write`.

## Paso 3 · Instalá la skill de la revisión semanal
Del [Kit del taller](#r-kit), instalá la skill `meta-ads-semanal`, pero **en este proyecto** (no en tu usuario), así viaja con los agentes:

```prompt
Creá una skill de este proyecto llamada meta-ads-semanal. Guardá el texto que pego abajo, exacto y sin cambios, en .claude/skills/meta-ads-semanal/SKILL.md dentro de esta carpeta. Cuando termines, decime la ruta.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

**Tenés que ver:** el archivo `.claude/skills/meta-ads-semanal/SKILL.md`.

## Paso 4 · Corré el equipo con el CSV de práctica (demo guiada)
Salí de Claude Code (`/exit`) y abrilo **como orquestador**: así la sesión entera es el coordinador del equipo.

<div data-os="mac">

```bash
claude --agent orquestador
```

</div>
<div data-os="win">

```powershell
claude --agent orquestador
```

</div>

Para que te den los mismos números que abajo, reemplazá los corchetes por los del ejemplo: 60.000, 50 y 8.

```prompt
Hacé la revisión de la semana del 9 al 15 de noviembre con el CSV de práctica meta-ads/datos/meta-ads-ejemplo.csv. Es una academia inventada que vende un curso a [PRECIO-INVENTADO, por ejemplo 60.000] pesos, con un margen de [MARGEN-INVENTADO, por ejemplo 50]% y que cierra 1 venta cada [CONSULTAS-POR-VENTA, por ejemplo 8] conversaciones de WhatsApp. Usá esos números en lugar de los de mi cerebro y aclaralo en el informe.
```

Vas a ver al orquestador llamar al analista, después al estratega y al creativo. Puede pedirte permiso para crear archivos: aceptá.

**Tenés que ver:**
1. Un resumen de 5 líneas del analista. En estos datos inventados, por ejemplo: un anuncio de video que convierte barato, un conjunto con frecuencia alta (fatiga) y una imagen que gastó sin traer casi nada.
2. El punto de equilibrio del estratega. Con los números de ejemplo: ganancia por venta 30.000 pesos (60.000 × 50%), dividido 8 conversaciones = **3.750 pesos por conversación como máximo**. Los anuncios que cuestan menos que eso dejan ganancia; los que cuestan más (en el CSV hay tres arriba de 5.000) pierden plata en cada venta. Para la campaña de formularios te va a pedir otro dato: de cada 10 personas que se anotan a la clase gratis, cuántas compran.
3. Una tabla de escenarios (inversión actual, +50%, +100%) y una lista numerada de cambios.
4. Tres ángulos y nueve primeras líneas.
5. El pedido de aprobación.

## Paso 5 · Aprobá (o no) y mirá el antes y después
Leé la lista. Elegí uno o dos cambios y escribí, por ejemplo:

```prompt
APROBADO 1, 2
```

Como no hay cuenta conectada, el ejecutor trabaja en **modo práctica**: simula el cambio sobre el CSV y te muestra la tabla de antes y después marcada como SIMULADO.

**Tenés que ver:** en `meta-ads/informes/[FECHA-DE-HOY]/` los archivos `analisis.md`, `plan.md`, `creativos.md`, `aprobacion.md` (con tu texto exacto), `cambios-aplicados.md` y `resumen.md`.

> **Tip:** probá romper la regla: respondé "dale, hacé todo". El orquestador no tiene que ejecutar: te tiene que mostrar la lista otra vez y pedir el formato `APROBADO`.

## Paso 6 · Tu caso: "¿cuánto invierto?"
Ahora con **tu** negocio. Si te faltan precio, margen o tasa de cierre (de cada cuántas consultas cerrás una venta), el estratega te los pide. Cargalos en el cerebro para la próxima. Pegá esto en la misma sesión, cambiando los corchetes:

```prompt
Sin datos de campañas todavía: quiero saber cuánto invertir en Meta por mes para vender [CANTIDAD-DE-VENTAS] [PRODUCTO-O-PROGRAMA] por mes. Usá el estratega con el precio y el margen de mi cerebro. Si no tenés cuántas consultas necesito para cerrar una venta o cuánto me cuesta hoy cada consulta, preguntámelo. Mostrame el punto de equilibrio, el costo por consulta máximo y tres escenarios de inversión, explicados para alguien que no sabe de publicidad.
```

**Tenés que ver:** tu costo por consulta máximo y una tabla "si invierto X, espero entre A y B ventas". Ese número es el que te dice si una campaña está ganando o perdiendo plata, sin depender de la intuición.

> **Ojo:** los escenarios son estimaciones, no promesas. Cuando subís el presupuesto, el costo por resultado suele empeorar. Por eso el estratega lo muestra como rango y propone escalar de a 20% o 30%.

## Paso 7 · Conectá tu cuenta real (opcional, después del taller)
El ejecutor aplica cambios por la **vía oficial de Meta**: el conector **Meta Ads AI connectors**, un servidor MCP de Meta (en beta abierta desde abril de 2026). La dirección del servidor es `https://mcp.facebook.com/ads`.

**Opción 1, en la app de Claude:** **Customize › Connectors › Add › Add custom connector**. Nombre: `Meta Ads`. URL: `https://mcp.facebook.com/ads`. Iniciá sesión con tu usuario de Facebook que administra la cuenta publicitaria y revisá los permisos que pide. Si usás la misma cuenta de Claude, el conector aparece también en Claude Code.

**Opción 2, en Claude Code con tu propia app de Meta** (para quien ya tiene una app en [developers.facebook.com](https://developers.facebook.com) con el caso de uso **Create & manage ads with ads MCP server**):

```bash
claude mcp add --transport http --client-id [ID-DE-TU-APP-DE-META] meta-ads https://mcp.facebook.com/ads
```

Después, `/mcp` para ver el estado y autenticarte.

Los agentes analista y ejecutor buscan el conector con el nombre `meta-ads` (el de la Opción 2).

> **Ojo:** si lo conectaste en la app (Opción 1) o con otro nombre, en Claude Code las herramientas se llaman distinto (las de la app empiezan con `mcp__claude_ai_`). Sin este ajuste, el analista y el ejecutor no ven tu cuenta. Pegá esto una vez:

```prompt
Buscá entre tus herramientas las de mi conector de Meta Ads (empiezan con mcp__ y tienen "Meta" o "ads" en el nombre) y decime el prefijo exacto. Después actualizá la línea tools de .claude/agents/analista.md y .claude/agents/ejecutor.md para que usen ese prefijo, con el formato mcp__NOMBRE-DEL-SERVIDOR__*. No cambies nada más.
```

**Tenés que ver:** el conector de Meta Ads conectado en `/mcp` y, al correr el equipo con "usá el conector de Meta Ads, últimos 7 días", un análisis con tus campañas reales.

> **Ojo:** la primera semana con tu cuenta real, usá el equipo **solo para analizar y proponer**. Aplicá los cambios vos a mano en el Administrador de anuncios. Cuando confíes en las propuestas, empezá a aprobar cambios chicos.

> **Tip:** Meta permite poner **reglas** al conector desde la configuración del portfolio comercial (por ejemplo: no subir presupuestos más de 20%, no crear campañas, no pausar ni activar). Es un segundo candado además de tu `APROBADO`. Están en disponibilidad limitada: fijate si te aparecen.

> **Datos:** el conector actúa con tus permisos de Meta. Nunca pegues tokens ni contraseñas en el chat. La alternativa para desarrolladores es la Marketing API con un token de usuario del sistema; para el servidor MCP solo sirven los de rol Empleado. Para este tutorial no hace falta.

## Cómo sé que funcionó
- `claude --agent orquestador` arranca y, con el CSV de práctica, te devuelve análisis, plan, creativos y pedido de aprobación.
- Si respondés "dale", **no** ejecuta. Si respondés `APROBADO 1`, aparece `cambios-aplicados.md` con antes y después.
- Prueba final, en una sesión normal de Claude Code en la carpeta del cerebro:

```prompt
/meta-ads-semanal con el CSV de práctica. Pará antes de pedir aprobación y decime cuál es el cambio que más plata ahorra y por qué.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `claude --agent orquestador` dice que no existe | El archivo no está en `.claude/agents/` de **esta** carpeta, o el `name:` del encabezado no es `orquestador`. Abrí Claude Code normal y pedí: "Revisá .claude/agents/ y decime qué hay". |
| El orquestador hace el análisis él mismo | Revisá que su línea `tools:` diga `Agent(analista, estratega, creativo, ejecutor), Read, Write` y que los otros 4 archivos existan. |
| El estratega inventa el margen | Decile: "No inventes, preguntame". Y cargá el dato en `negocio/oferta-y-precios.md`. |
| El ejecutor dice que no tiene el conector | Normal en modo práctica. Con cuenta real: revisá el nombre del conector (Paso 7) y que esté conectado en `/mcp`. |
| El ejecutor no aplica un cambio aprobado | Hace bien: algo no coincidía (estado distinto, valor distinto). Leé el motivo en `cambios-aplicados.md`. |
| El análisis mezcla conversaciones y formularios | Pedí: "Separá el análisis por tipo de resultado". |

## Para seguir solo
- **Cada lunes, 20 minutos:** `/meta-ads-semanal` con el CSV de la semana (en el Administrador de anuncios: últimos 7 días, nivel anuncio, **Exportar**). Las revisiones quedan guardadas y el equipo compara con la anterior.
- **Que el análisis llegue solo:** programá la skill para que los lunes a la mañana haga análisis y propuesta, **sin ejecutar** (la skill lo frena sola cuando no hay una persona presente). Ver [Tareas programadas](#t4-tareas-programadas).
- **Cerrá el círculo con ventas reales:** sumá al CSV una columna con las ventas de cada campaña (de tu WhatsApp o tu CRM). Con ventas reales, el estratega deja de estimar y calcula.

## Fuentes
- Meta, presentación de Meta Ads AI connectors (beta abierta, 29/04/2026; reglas del 16/07/2026): https://www.facebook.com/business/news/meta-ads-ai-connectors
- Meta for Developers, servidor MCP de anuncios (`https://mcp.facebook.com/ads`, categorías de herramientas): https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-overview
- Meta for Developers, primeros pasos (permisos `ads_mcp_management` + `ads_read` o `ads_management`; comando de Claude Code; tokens de usuario del sistema con rol Empleado): https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started
- Meta for Developers, reglas del servidor MCP (límites de presupuesto, bloqueo de creación y de cambios de estado): https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-rules-best-practices
- Meta, ayuda para conectar los AI connectors: https://www.facebook.com/business/help/1456422242197840
- Meta, usuarios del sistema (Marketing API): https://developers.facebook.com/docs/marketing-api/system-users/overview
- Claude Code, subagentes (`.claude/agents/`, `tools: Agent(...)`, `claude --agent`, herramientas MCP con `mcp__servidor__*`): https://code.claude.com/docs/en/sub-agents
- Verificado el 18/11/2026.
