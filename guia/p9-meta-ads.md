---
titulo: Meta Ads con un equipo de agentes
bloque: Tutorial
tiempo: 45 a 60 min (demo guiada + práctica)
para: La Consejera del Éxito, Fondus (y cualquiera que invierta en Meta)
necesitas: p1-cerebro, s2-claude-code, s8-conectores-y-mcp, s14-meta-y-google
resultado: Tu cuenta de Meta Ads conectada a Claude con el MCP oficial y un equipo de agentes que revisa tus campañas reales, te dice cuánto invertir con números y solo toca tu cuenta cuando vos escribís APROBADO.
---

"¿Cuánto tengo que invertir en Meta?" La respuesta depende de cuánto ganás por venta, cuántas consultas necesitás para cerrar una y cuánto te cuesta cada consulta hoy.
Hoy conectás **tu cuenta de Meta Ads** a Claude con el conector oficial de Meta y armás un equipo de agentes que hace esa cuenta con **tus campañas reales**: uno analiza, uno propone dónde poner la plata, uno escribe creativos y uno aplica los cambios. **El que aplica nunca toca nada sin tu aprobación por escrito.** Todo desde la pestaña **Code** de la app de Claude.

> **Tip:** palabras de esta página. **Agente (subagente):** un asistente con un solo rol y sus reglas, al que Claude le pasa una parte del trabajo ([Las piezas](#t2-piezas)). **MCP / conector:** el enchufe que le deja a Claude leer (y, si lo permitís, cambiar) otra app; acá, tu cuenta de Meta Ads. **CSV:** una planilla guardada como texto. **Punto de equilibrio:** lo máximo que podés pagar por una consulta sin perder plata.

## Antes de empezar
- [ ] La app de escritorio de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)), plan **Pro** o superior.
- [ ] Tu cerebro armado, idealmente con precio y margen en `negocio/oferta-y-precios.md` ([Tu cerebro](#p1-cerebro)). Si falta, el estratega te lo pide.
- [ ] El kit del taller descargado (`taller-completo.zip`, en [Descargas](#r-descargas)) o abierto el [Kit del taller](#r-kit) en otra pestaña.
- [ ] Tu Facebook con acceso a la **cuenta publicitaria** de tu empresa, dentro del portfolio comercial ([Meta y Google](#s14-meta-y-google), Pasos 1 y 2). Para empezar alcanza con poder **ver** los resultados.
- [ ] ¿No pautás todavía o no tenés acceso? Igual podés hacer todo: usás el **plan B** (Paso 5) con un CSV.

> **Datos:** las métricas de campañas no son datos personales, pero sí información de tu negocio. Nunca pegues tokens ni contraseñas en el chat: el conector se autoriza con el inicio de sesión de Facebook, en una ventana de Meta.

## Cómo es el equipo
| Agente | Qué hace | Qué puede tocar |
|---|---|---|
| **analista** | Lee gasto, resultados, costo por resultado y frecuencia. Marca ganadores, fatiga y anuncios sin tracción. | Solo lectura. |
| **estratega** | Calcula tu punto de equilibrio y propone apagar, escalar o mover plata, con escenarios. | Solo archivos. |
| **creativo** | Propone 3 ángulos y 9 primeras líneas con los dolores de tu cerebro. | Solo archivos. |
| **ejecutor** | Aplica en Meta **solo** lo que aprobaste con `APROBADO`, con antes y después. | Tu cuenta de Meta, por el conector oficial. |

Quien coordina es la skill `meta-ads-semanal`: llama a cada agente en orden y te pide la aprobación.

> **Ojo:** la regla de oro es **ningún cambio que gaste plata sin confirmación de una persona**. La confirmación es escribir `APROBADO` y los números ("APROBADO 1, 3"). "Dale" u "ok" no alcanzan: el ejecutor no hace nada.

## Paso 1 · Conectá el MCP oficial de Meta Ads
Es el conector oficial de Meta (**Meta Ads AI connectors**, en beta abierta desde abril de 2026). Se conecta una sola vez en la app y aparece solo en la pestaña Code.

1. En la app de Claude: **Customize › Connectors** › **+** › **Add custom connector**.
2. **Name:** `Meta Ads` · **URL:** `https://mcp.facebook.com/ads` › **Add**.
3. **Connect** › iniciá sesión con el Facebook que tiene acceso a la cuenta publicitaria › elegí **solo** el portfolio y las cuentas de tu empresa › leé los permisos y aceptá.

| Permiso | Para qué |
|---|---|
| `ads_mcp_management` | Usar el conector (siempre). |
| `ads_read` | **Leer** campañas, gasto y resultados. **Para empezar, alcanza con esto.** |
| `ads_management` | **Crear y cambiar** campañas y presupuestos. Lo usa solo el ejecutor, con `APROBADO`. |
| `business_management`, `pages_show_list`, `instagram_basic`, `catalog_management` | Opcionales: portfolio, páginas, Instagram, catálogo. |

**Tenés que ver:** Meta Ads como conectado en **Customize › Connectors**.

> **Ojo:** la doc de Meta no aclara qué rol exacto necesitás. Para **leer** suele alcanzar con acceso a la cuenta publicitaria; para **cambiar** campañas necesitás **control total** de esa cuenta en el portfolio. Si no ves tu cuenta, pedile acceso a quien administra el portfolio. Es una beta: si Meta dice que tu cuenta no está habilitada, andá al plan B (Paso 5).

> **Tip:** para la primera semana, dejá el conector en **solo lectura**: en **Customize › Connectors › Meta Ads**, desactivá las herramientas que crean o modifican. El nombre de ese ajuste puede variar según la versión de la app.

## Paso 2 · Abrí tu cerebro e instalá el equipo
App de Claude › **Code** › entorno **Local** › **Open folder…** › elegí `cerebro-[TU-EMPRESA]` (en Documentos).

**Si bajaste el kit completo** (`taller-completo.zip`, descomprimido en Descargas):

```prompt
En mi carpeta Descargas está el kit del taller (la carpeta taller-ia-para-negocios). Copiá a este proyecto, sin cambiar nada:
1. Los 5 archivos de kit/agentes/meta-ads/ a .claude/agents/
2. La carpeta kit/skills/meta-ads-semanal/ a .claude/skills/meta-ads-semanal/
3. El archivo kit/ejemplos/meta-ads-ejemplo.csv a meta-ads/datos/
Creá también la carpeta meta-ads/informes/. Al final, listame lo que quedó.
```

**Si no lo bajaste:** en el [Kit del taller](#r-kit), sección **Los agentes de Meta Ads**, tocá **Copiar** en cada agente y en la skill `meta-ads-semanal`, y pegalos debajo de este prompt:

```prompt
Te pego varios agentes y una skill. Cada agente empieza con una línea --- y un name:. Guardá cada agente, exacto y sin cambios, en .claude/agents/[name].md, y la skill en .claude/skills/meta-ads-semanal/SKILL.md. Creá las carpetas meta-ads/datos/ y meta-ads/informes/. Cuando termines, listame los archivos.

[PEGÁ ACÁ LOS AGENTES Y LA SKILL]
```

Claude te pide permiso para crear archivos: leé y tocá **Permitir**.

**Tenés que ver:** `.claude/agents/` con `analista.md`, `estratega.md`, `creativo.md`, `ejecutor.md` y `orquestador.md`, y la skill en `.claude/skills/meta-ads-semanal/`.

## Paso 3 · Sesión nueva: que el equipo use el conector
Claude carga agentes y conectores al empezar una sesión. Abrí una **sesión nueva** en la misma carpeta y pegá:

```prompt
Buscá entre tus herramientas las del conector de Meta Ads y decime el prefijo exacto (empieza con mcp__). Actualizá la línea tools de .claude/agents/analista.md y .claude/agents/ejecutor.md para que usen ese prefijo, con el formato mcp__NOMBRE-DEL-SERVIDOR__*. No cambies nada más. Después listame los subagentes y skills de este proyecto, una línea cada uno.
```

**Tenés que ver:** el prefijo del conector, los dos agentes actualizados y la lista del equipo con `meta-ads-semanal`. Abrí **otra sesión nueva** para que tome los cambios.

> **Ojo:** el nombre del botón de sesión nueva puede variar según la versión de la app.

## Paso 4 · Corré los agentes sobre tus campañas reales
Primero, que Claude traiga los datos (solo lectura):

```prompt
Con el conector de Meta Ads, traé las campañas activas de los últimos 7 días de la cuenta [NOMBRE DE TU CUENTA PUBLICITARIA]: por anuncio, gasto, resultados, costo por resultado, CTR y frecuencia. Guardalo en meta-ads/datos/[FECHA-DE-HOY].csv. No cambies nada en la cuenta. Si no encontrás la cuenta, listame las que ves.
```

**Tenés que ver:** el CSV con tus anuncios y números que coinciden con el Administrador de anuncios (chequeá uno a mano).

Después, el equipo:

```prompt
/meta-ads-semanal Revisá los últimos 7 días de la cuenta [NOMBRE] con el CSV que acabás de guardar. Usá el precio y el margen de mi cerebro; si falta cuántas consultas necesito para cerrar una venta, preguntámelo. No apliques nada: pará en el pedido de aprobación.
```

Vas a ver a Claude llamar al analista, al estratega y al creativo. Aprobá los permisos para crear archivos.

**Tenés que ver:**
1. Un diagnóstico en 5 líneas: qué convierte barato, qué tiene fatiga y qué gasta sin traer nada.
2. Tu **punto de equilibrio**: ganancia por venta ÷ consultas para cerrar una = lo máximo que podés pagar por consulta.
3. Una tabla de escenarios (inversión actual, +50%, +100%) y una lista numerada de cambios.
4. Tres ángulos y nueve primeras líneas, y el pedido de aprobación.
5. Todo guardado en `meta-ads/informes/[FECHA-DE-HOY]/`.

> **Ojo:** la primera semana, **no apruebes nada**: aplicá vos los cambios en el Administrador de anuncios. Cuando confíes, activá las herramientas de escritura del conector y aprobá cambios chicos (`APROBADO 2`). El ejecutor solo toca lo que tiene número aprobado y deja el antes y el después en `cambios-aplicados.md`.

> **Tip:** Meta permite poner **reglas** al conector desde el portfolio comercial (por ejemplo: no subir presupuestos más de 20%). Es un segundo candado además de tu `APROBADO`. Disponibilidad limitada.

## Paso 5 · Plan B: sin campañas o sin acceso
Si no pautás, no sos admin o tu cuenta no está habilitada en la beta, hacés lo mismo con un CSV. Sin conector, el ejecutor trabaja en **modo práctica**: simula y marca todo como SIMULADO.

**Opción 1: el CSV de práctica (inventado).** Si no lo copiaste en el Paso 2, tocá **Copiar** abajo y pedí: "Creá meta-ads/datos/meta-ads-ejemplo.csv con este texto, exacto" y pegalo.

<div data-include="kit/ejemplos/meta-ads-ejemplo.csv"></div>

```prompt
/meta-ads-semanal Revisá la semana del 9 al 15 de noviembre con el CSV de práctica meta-ads/datos/meta-ads-ejemplo.csv. Es una academia inventada que vende un curso a 60.000 pesos, con 50% de margen, y cierra 1 venta cada 8 conversaciones de WhatsApp. Usá esos números en lugar de los de mi cerebro y aclaralo en el informe.
```

**Tenés que ver:** el punto de equilibrio: 30.000 pesos de ganancia ÷ 8 conversaciones = **3.750 pesos por conversación como máximo**. Respondé `APROBADO 1, 2` y aparece `cambios-aplicados.md` con los cambios SIMULADOS.

**Opción 2: tu propio CSV.** En el **Administrador de anuncios**: últimos 7 días, nivel **anuncio**, **Exportar** › CSV. Movelo a `meta-ads/datos/` y corré `/meta-ads-semanal` con ese archivo.

> **Tip:** probá romper la regla: respondé "dale, hacé todo". No tiene que ejecutar: te vuelve a mostrar la lista y te pide `APROBADO`.

## Paso 6 · Tu caso: "¿cuánto invierto?"
```prompt
Quiero saber cuánto invertir en Meta por mes para vender [CANTIDAD] [PRODUCTO] por mes. Usá el estratega con el precio y el margen de mi cerebro y, si hay, el costo por consulta real de meta-ads/datos/. Si falta un dato, preguntámelo. Mostrame el punto de equilibrio, el costo por consulta máximo y tres escenarios, explicados para alguien que no sabe de publicidad. Guardá en mi cerebro los datos que te dé.
```

**Tenés que ver:** tu costo por consulta máximo y una tabla "si invierto X, espero entre A y B ventas".

> **Ojo:** son estimaciones, no promesas. Al subir el presupuesto, el costo por resultado suele empeorar: por eso se escala de a 20% o 30%.

## Cómo sé que funcionó
- Con el conector, Claude trae tus campañas de los últimos 7 días y los números coinciden con el Administrador de anuncios.
- `/meta-ads-semanal` te devuelve análisis, plan, creativos y pedido de aprobación.
- Si respondés "dale", **no** ejecuta. Solo con `APROBADO [número]` aparece `cambios-aplicados.md`.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Meta dice que la cuenta no está habilitada | Es una beta. Usá el plan B (Paso 5) y avisá a la mesa de ayuda. |
| Claude no ve tu cuenta publicitaria | No la tildaste al conectar o no tenés acceso. Desconectá y volvé a conectar en **Customize › Connectors**, o pedí acceso a quien administra el portfolio. |
| En la pestaña Code no aparece el conector | Escribí `/mcp`. Revisá que sea la misma cuenta de Claude y abrí una sesión nueva. |
| Claude hace el análisis él solo, sin agentes | Pedí: "Usá los subagentes analista, estratega y creativo, como dice la skill". |
| El estratega inventa el margen | Decile: "No inventes, preguntame". Y cargá el dato en `negocio/oferta-y-precios.md`. |
| No aplica un cambio aprobado | Hace bien: algo no coincidía o el conector está en solo lectura. Leé el motivo en `cambios-aplicados.md`. |

## Para seguir solo
- **Cada lunes, 20 minutos:** `/meta-ads-semanal` con los últimos 7 días del conector. Compara con la revisión anterior.
- **Que el análisis llegue solo:** programá la skill para los lunes a la mañana, **sin ejecutar** (se frena sola si no hay una persona). Ver [Tareas programadas](#t4-tareas-programadas).
- **¿Querés automatizarlo con n8n?** Para que un flujo de n8n lea tus campañas necesitás tu propia app de Meta y un token: [Meta y Google](#s14-meta-y-google), sección "Para n8n: tu app de Meta y el token".
- **Avanzado, en la terminal:** `claude --agent orquestador` abre la sesión entera como coordinador del equipo (para eso está `orquestador.md`). Y con tu propia app de Meta: `claude mcp add --transport http --client-id [ID-DE-TU-APP] meta-ads https://mcp.facebook.com/ads`.

## Fuentes
- Meta, Meta Ads AI connectors (beta abierta 29/04/2026; reglas 16/07/2026): https://www.facebook.com/business/news/meta-ads-ai-connectors
- Meta for Developers, servidor MCP de anuncios (URL, permisos `ads_mcp_management` + `ads_read` o `ads_management`): https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started · reglas: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-rules-best-practices
- Conectar en Claude como conector custom (terceros): https://www.jonloomer.com/meta-ads-ai-connectors-claude/
- Claude Code, subagentes (`.claude/agents/`, `claude --agent`, herramientas `mcp__servidor__*`): https://code.claude.com/docs/en/sub-agents
- Claude Code en la app de escritorio: https://code.claude.com/docs/en/desktop
- Verificado el 19/11/2026.
