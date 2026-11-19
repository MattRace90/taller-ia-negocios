---
titulo: Meta Ads con un equipo de agentes
bloque: Tutorial
tiempo: 45 a 60 min (demo guiada + práctica)
para: La Consejera del Éxito, Fondus (y cualquiera que invierta en Meta)
necesitas: p1-cerebro, s2-claude-code, s8-conectores-y-mcp
resultado: Un equipo de agentes instalado en la carpeta de tu cerebro que revisa tus campañas, te dice cuánto invertir con números y solo toca tu cuenta cuando vos escribís APROBADO.
---

"¿Cuánto tengo que invertir en Meta?" La respuesta depende de cuánto ganás por venta, cuántas consultas necesitás para cerrar una y cuánto te cuesta cada consulta hoy.
Hoy armás un equipo de agentes que hace esa cuenta cada semana: uno analiza, uno propone dónde poner la plata, uno escribe creativos y uno aplica los cambios. **El que aplica nunca toca nada sin tu aprobación por escrito.** Todo desde la pestaña **Code** de la app de Claude.

> **Tip:** palabras de esta página. **Agente (subagente):** un asistente con un solo rol y sus reglas, al que Claude le pasa una parte del trabajo ([Las piezas](#t2-piezas)). **CSV:** una planilla guardada como texto. **Conector:** el permiso para que Claude use otra app, acá tu cuenta de Meta Ads. **Punto de equilibrio:** lo máximo que podés pagar por una consulta sin perder plata.

## Antes de empezar
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)).
- [ ] Tu cerebro armado, idealmente con precio y margen en `negocio/oferta-y-precios.md` ([Tu cerebro](#p1-cerebro)). Si falta, el estratega te lo pide.
- [ ] El kit del taller descargado (`taller-completo.zip`, en [Descargas](#r-descargas)) o abierto el [Kit del taller](#r-kit) en otra pestaña.
- [ ] Para practicar: **nada más**. Usamos un CSV de campañas inventado.
- [ ] Para tu cuenta real (opcional, Paso 6): acceso de administrador a tu cuenta publicitaria en el portfolio comercial de Meta.

> **Datos:** las métricas de campañas no son datos personales, pero sí información de tu negocio. El CSV de práctica es **inventado**: una academia que no existe, con montos que no son de nadie.

## Cómo es el equipo
| Agente | Qué hace | Qué puede tocar |
|---|---|---|
| **analista** | Lee gasto, resultados, costo por resultado y frecuencia. Marca ganadores, fatiga y anuncios sin tracción. | Solo lectura. |
| **estratega** | Calcula tu punto de equilibrio y propone apagar, escalar o mover plata, con escenarios. | Solo archivos. |
| **creativo** | Propone 3 ángulos y 9 primeras líneas con los dolores de tu cerebro. | Solo archivos. |
| **ejecutor** | Aplica en Meta **solo** lo que aprobaste, con antes y después. | Tu cuenta de Meta, por el conector oficial. |

Quien coordina es la skill `meta-ads-semanal`: llama a cada agente en orden y te pide la aprobación.

> **Ojo:** la regla de oro es **ningún cambio que gaste plata sin confirmación de una persona**. La confirmación es escribir `APROBADO` y los números ("APROBADO 1, 3"). "Dale" u "ok" no alcanzan.

## Paso 1 · Abrí tu cerebro en la pestaña Code
App de Claude › **Code** › en el selector de entorno elegí **Local** › **Open folder…** › elegí `cerebro-[TU-EMPRESA]` (en Documentos).

**Tenés que ver:** el cuadro para escribir, con el nombre de tu carpeta arriba.

## Paso 2 · Pedile a Claude que cree los agentes, la skill y el CSV
Elegí un camino.

**Si bajaste el kit completo** (`taller-completo.zip`, descomprimido en Descargas):

```prompt
En mi carpeta Descargas está el kit del taller (la carpeta taller-ia-para-negocios). Copiá a este proyecto, sin cambiar nada:
1. Los 5 archivos de kit/agentes/meta-ads/ a .claude/agents/
2. La carpeta kit/skills/meta-ads-semanal/ a .claude/skills/meta-ads-semanal/
3. El archivo kit/ejemplos/meta-ads-ejemplo.csv a meta-ads/datos/
Creá también la carpeta meta-ads/informes/. Al final, listame lo que quedó.
```

**Si no lo bajaste:** en el [Kit del taller](#r-kit), sección **Los agentes de Meta Ads**, tocá **Copiar** en cada agente y pegalos todos, uno debajo del otro, después de este prompt:

```prompt
Te pego varios agentes. Cada uno empieza con una línea --- y un name:. Guardá cada uno, exacto y sin cambios, en .claude/agents/[name].md de este proyecto. Cuando termines, listame los archivos.

[PEGÁ ACÁ LOS AGENTES]
```

Después, igual con la skill `meta-ads-semanal` (en el Kit, tocá **Copiar**) y con el CSV de práctica (botón **Copiar** de abajo):

```prompt
Guardá el texto que pego abajo, exacto y sin cambios, en .claude/skills/meta-ads-semanal/SKILL.md de este proyecto.

[PEGÁ ACÁ LA SKILL]
```

```prompt
Creá meta-ads/datos/meta-ads-ejemplo.csv con el texto que pego abajo, exacto y sin cambios (son datos inventados), y la carpeta meta-ads/informes/.

[PEGÁ ACÁ EL CSV]
```

<div data-include="kit/ejemplos/meta-ads-ejemplo.csv"></div>

Claude te pide permiso para crear los archivos: leé y tocá **Permitir**.

**Tenés que ver:** `.claude/agents/` con `analista.md`, `estratega.md`, `creativo.md`, `ejecutor.md` y `orquestador.md`; la skill en `.claude/skills/meta-ads-semanal/`; y el CSV con 15 anuncios.

## Paso 3 · Abrí una sesión nueva y revisá el equipo
Claude carga los agentes al empezar una sesión. Abrí una **sesión nueva** en la misma carpeta y preguntá:

```prompt
¿Qué subagentes y skills tenés en este proyecto? Para cada uno, una línea con qué hace.
```

**Tenés que ver:** los agentes listados y la skill `meta-ads-semanal` (también aparece al escribir `/`).

> **Ojo:** el nombre del botón de sesión nueva puede variar según la versión de la app.

## Paso 4 · Corré el equipo con el CSV de práctica (demo guiada)
Para obtener los mismos números que abajo, usá 60.000, 50 y 8:

```prompt
/meta-ads-semanal Revisá la semana del 9 al 15 de noviembre con el CSV de práctica meta-ads/datos/meta-ads-ejemplo.csv. Es una academia inventada que vende un curso a [PRECIO, ej. 60.000] pesos, con [MARGEN, ej. 50]% de margen, y cierra 1 venta cada [CONSULTAS, ej. 8] conversaciones de WhatsApp. Usá esos números en lugar de los de mi cerebro y aclaralo en el informe.
```

Vas a ver a Claude llamar al analista, al estratega y al creativo. Aprobá los permisos para crear archivos.

**Tenés que ver:**
1. El diagnóstico en 5 líneas: un video que convierte barato, un conjunto con fatiga y una imagen que gastó sin traer casi nada.
2. El punto de equilibrio: 30.000 pesos de ganancia por venta ÷ 8 conversaciones = **3.750 pesos por conversación como máximo**. Los anuncios que cuestan más pierden plata en cada venta.
3. Una tabla de escenarios (inversión actual, +50%, +100%) y una lista numerada de cambios.
4. Tres ángulos y nueve primeras líneas, y el pedido de aprobación.

Ahora aprobá uno o dos cambios:

```prompt
APROBADO 1, 2
```

Sin cuenta conectada, el ejecutor trabaja en **modo práctica**: simula el cambio y lo marca como SIMULADO.

**Tenés que ver:** en `meta-ads/informes/[FECHA-DE-HOY]/` los archivos `analisis.md`, `plan.md`, `creativos.md`, `aprobacion.md`, `cambios-aplicados.md` y `resumen.md`.

> **Tip:** probá romper la regla: respondé "dale, hacé todo". No tiene que ejecutar: te vuelve a mostrar la lista y te pide `APROBADO`.

## Paso 5 · Tu caso: "¿cuánto invierto?"
Ahora con **tu** negocio, en la misma sesión:

```prompt
Sin datos de campañas todavía: quiero saber cuánto invertir en Meta por mes para vender [CANTIDAD] [PRODUCTO] por mes. Usá el estratega con el precio y el margen de mi cerebro. Si te falta cuántas consultas necesito para cerrar una venta o cuánto me cuesta hoy cada consulta, preguntámelo. Mostrame el punto de equilibrio, el costo por consulta máximo y tres escenarios, explicados para alguien que no sabe de publicidad. Guardá en mi cerebro los datos que te dé.
```

**Tenés que ver:** tu costo por consulta máximo y una tabla "si invierto X, espero entre A y B ventas".

> **Ojo:** son estimaciones, no promesas. Al subir el presupuesto, el costo por resultado suele empeorar: por eso se escala de a 20% o 30%.

## Paso 6 · Conectá tu cuenta real (opcional, después del taller)
El ejecutor usa la **vía oficial de Meta**: el conector **Meta Ads AI connectors** (beta abierta desde abril de 2026).

1. En la app de Claude: **Customize › Connectors › Add › Add custom connector**. Nombre: `Meta Ads`. URL: `https://mcp.facebook.com/ads`.
2. Iniciá sesión con el usuario de Facebook que administra la cuenta publicitaria y revisá los permisos que pide.
3. Abrí una sesión nueva en la pestaña **Code**, en tu cerebro, y pegá una vez:

```prompt
Buscá entre tus herramientas las del conector de Meta Ads y decime el prefijo exacto (empieza con mcp__). Después actualizá la línea tools de .claude/agents/analista.md y .claude/agents/ejecutor.md para que usen ese prefijo, con el formato mcp__NOMBRE-DEL-SERVIDOR__*. No cambies nada más.
```

**Tenés que ver:** con `/meta-ads-semanal usá el conector de Meta Ads, últimos 7 días`, un análisis con tus campañas reales.

> **Ojo:** la primera semana, usá el equipo **solo para analizar y proponer**. Los cambios aplicalos vos en el Administrador de anuncios. Cuando confíes, aprobá cambios chicos.

> **Tip:** Meta permite poner **reglas** al conector desde el portfolio comercial (por ejemplo: no subir presupuestos más de 20%). Es un segundo candado además de tu `APROBADO`. Disponibilidad limitada.

> **Datos:** el conector actúa con tus permisos de Meta. Nunca pegues tokens ni contraseñas en el chat.

## Cómo sé que funcionó
- `/meta-ads-semanal` con el CSV de práctica te devuelve análisis, plan, creativos y pedido de aprobación.
- Si respondés "dale", **no** ejecuta. Con `APROBADO 1`, aparece `cambios-aplicados.md`.
- Prueba final, en una sesión nueva:

```prompt
/meta-ads-semanal con el CSV de práctica. Pará antes de pedir aprobación y decime qué cambio ahorra más plata y por qué.
```

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Dice que faltan agentes | Pedí: "Revisá .claude/agents/ de esta carpeta y decime qué hay". Si están, abrí una sesión nueva. |
| Claude hace el análisis él solo, sin agentes | Pedí: "Usá los subagentes analista, estratega y creativo, como dice la skill". |
| El estratega inventa el margen | Decile: "No inventes, preguntame". Y cargá el dato en `negocio/oferta-y-precios.md`. |
| El ejecutor dice que no tiene el conector | Normal en modo práctica. Con cuenta real: revisá el Paso 6 y que el conector esté activo. |
| No aplica un cambio aprobado | Hace bien: algo no coincidía. Leé el motivo en `cambios-aplicados.md`. |

## Para seguir solo
- **Cada lunes, 20 minutos:** `/meta-ads-semanal` con el CSV de la semana (Administrador de anuncios: últimos 7 días, nivel anuncio, **Exportar**). Compara con la revisión anterior.
- **Que el análisis llegue solo:** programá la skill para los lunes a la mañana, **sin ejecutar** (se frena sola si no hay una persona). Ver [Tareas programadas](#t4-tareas-programadas).
- **Avanzado, en la terminal:** `claude --agent orquestador` abre la sesión entera como coordinador del equipo (para eso está `orquestador.md`). Y con tu propia app de Meta: `claude mcp add --transport http --client-id [ID-DE-TU-APP] meta-ads https://mcp.facebook.com/ads`.

## Fuentes
- Meta, Meta Ads AI connectors (beta abierta 29/04/2026; reglas 16/07/2026): https://www.facebook.com/business/news/meta-ads-ai-connectors
- Meta for Developers, servidor MCP de anuncios: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-overview · primeros pasos: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started · reglas: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-rules-best-practices
- Claude Code, subagentes (`.claude/agents/`, `claude --agent`, herramientas `mcp__servidor__*`): https://code.claude.com/docs/en/sub-agents
- Claude Code en la app de escritorio: https://code.claude.com/docs/en/desktop
- Verificado el 18/11/2026.
