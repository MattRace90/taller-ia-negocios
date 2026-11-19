---
titulo: 'Kit del taller: skills y agentes'
bloque: Referencia
tiempo: 5 min por skill
para: Todos
necesitas: s2-claude-code
resultado: Las skills del taller instaladas en tu Claude Code (y, si querés, en la app de Claude).
---

Una **skill** es un proceso escrito una vez que Claude ejecuta mil veces: cómo armar una propuesta, cómo extraer una carta a una planilla, cómo hacer el seguimiento. Un **agente** (subagente) es un especialista con su propio rol, al que Claude le delega una parte del trabajo.
Todas las de esta página las escribimos para el taller. Copialas, instalalas y cambialas a tu medida: son texto.

## Antes de empezar
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] Tu carpeta del cerebro creada ([Tu cerebro](#p1-cerebro)).

## Cómo instalar una skill en Claude Code
1. Abrí la terminal (en Mac, **Terminal**; en Windows, **PowerShell**) y escribí `claude` para abrir Claude Code. Sirve cualquier carpeta.
2. Tocá **Copiar** en la skill que quieras (más abajo).
3. Pegá este prompt en Claude Code y, abajo, el contenido copiado. Cambiá `[NOMBRE-DE-LA-SKILL]` por el nombre de la skill (por ejemplo `seguimiento`). En Windows, `[MI-USUARIO]` es tu usuario de Windows; si no lo sabés, dejalo así: Claude Code lo averigua.

```prompt
Creá una skill personal llamada [NOMBRE-DE-LA-SKILL]. Guardá el texto que pego abajo, exacto y sin cambios, en el archivo SKILL.md de la carpeta de skills de mi usuario (~/.claude/skills/[NOMBRE-DE-LA-SKILL]/SKILL.md; en Windows C:\Users\[MI-USUARIO]\.claude\skills\[NOMBRE-DE-LA-SKILL]\SKILL.md). Cuando termines, decime la ruta exacta.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

4. Salí con `/exit`, volvé a entrar con `claude` y escribí `/` para verla en la lista.

**Tenés que ver:** la skill aparece en `/skills`.

## Cómo usarla también en la app de Claude (web y celular)
La app pide la skill como un archivo ZIP.
1. En Claude Code:

```prompt
Comprimí la carpeta de mi skill [NOMBRE-DE-LA-SKILL] (la carpeta entera, con SKILL.md adentro) en un archivo [NOMBRE-DE-LA-SKILL].zip en mi Escritorio.
```

2. En [claude.ai](https://claude.ai): **Settings › Capabilities** y activá **Code execution and file creation**.
3. **Customize › Skills** › subí el ZIP que quedó en tu Escritorio.

**Tenés que ver:** la skill en la lista de **Customize › Skills**, activada.

## Las skills
### armar-mi-cerebro · [Tu cerebro](#p1-cerebro)
Entrevista, ordena y escribe el cerebro de tu empresa en archivos `.md`.

<div data-include="kit/skills/armar-mi-cerebro/SKILL.md"></div>

### propuesta-comercial · [Tu asistente en Telegram](#p2-asistente-telegram)
De la transcripción de una llamada a una propuesta con tu marca.

<div data-include="kit/skills/propuesta-comercial/SKILL.md"></div>

### agente-de-respuestas · [Un agente que responde y filtra](#p3-agente-preguntas)
Genera el agente que responde y filtra, sus casos de prueba y el código del bot.

<div data-include="kit/skills/agente-de-respuestas/SKILL.md"></div>

### extraer-a-tabla · [De foto a planilla](#p4-foto-a-tabla)
De fotos o PDF a una planilla, con lo dudoso separado para revisar.

<div data-include="kit/skills/extraer-a-tabla/SKILL.md"></div>

### editar-video · [Tu editor de video](#p7-video)
Corta silencios, subtitula, agrega tu placa final y renderiza.

<div data-include="kit/skills/editar-video/SKILL.md"></div>

### seguimiento · [Seguimiento a quien no compró](#p8-seguimiento)
Segmenta a quienes no compraron y escribe los mensajes de seguimiento en tu voz.

<div data-include="kit/skills/seguimiento/SKILL.md"></div>

### meta-ads-semanal · [Meta Ads con agentes](#p9-meta-ads)
La revisión semanal de campañas con el equipo de agentes.

> **Ojo:** esta skill no va en tu usuario: va **dentro de la carpeta de tu cerebro** (`.claude/skills/`). Instalala con el prompt del Paso 3 de [Meta Ads con agentes](#p9-meta-ads), no con el de arriba.

<div data-include="kit/skills/meta-ads-semanal/SKILL.md"></div>

### reporte-semanal · [El reporte que llega solo](#p10-extras)
El reporte que llega solo cada lunes.

> **Ojo:** esta también va **dentro de la carpeta de tu cerebro**. Instalala con el prompt del Paso 5 de [Extras](#p10-extras).

<div data-include="kit/skills/reporte-semanal/SKILL.md"></div>

## Los agentes de Meta Ads
Estos no van en la carpeta de skills: van en `.claude/agents/` **dentro de la carpeta de tu cerebro**. Los pasos están en [Meta Ads con agentes](#p9-meta-ads), Paso 2.

<div data-include="kit/agentes/meta-ads/orquestador.md"></div>
<div data-include="kit/agentes/meta-ads/analista.md"></div>
<div data-include="kit/agentes/meta-ads/estratega.md"></div>
<div data-include="kit/agentes/meta-ads/creativo.md"></div>
<div data-include="kit/agentes/meta-ads/ejecutor.md"></div>

## Fábrica de contenidos
Tres skills que se instalan juntas con doble clic: **plan-de-contenidos** (el plan del mes en PDF), **imagenes-para-redes** (placas, carruseles e historias) y **video-para-redes** (edita lo que grabás con el celular). Los pasos están en el tutorial [Fábrica de contenidos](#u-fabrica).

[Descargá la fábrica](kit/descargas/fabrica-de-contenidos.zip) (ZIP de 1 MB, Mac y Windows).

## Plan B: skills de la agencia
Skills que usamos en la agencia, limpias de datos de clientes. Se descargan como ZIP y se instalan como dice [Fábrica de contenidos › Plan B](#u-fabrica).

- [creador-angulos-publicitarios](kit/plan-b/creador-angulos-publicitarios.zip): arma con vos, paso a paso, un ángulo de venta (público, dolor, mecanismo y promesa).
- [nomenclador-ads](kit/plan-b/nomenclador-ads.zip): analiza un anuncio y le pone un nombre ordenado para saber después qué rinde.
- [rediseno-9x16](kit/plan-b/rediseno-9x16.zip): rediseña una placa cuadrada como historia o reel vertical, sin estirarla.
- [static-remix](kit/plan-b/static-remix.zip): recrea anuncios ganadores de la competencia con tu producto y tu marca (usa Higgsfield, pago).
- [estrategia-benchmark](kit/plan-b/estrategia-benchmark.zip): analiza y puntúa los anuncios de tu competencia en Meta y arma una presentación de estrategia.
- [product-bible](kit/plan-b/product-bible.zip): arma una carpeta por producto con ficha, colores, mensajes, reseñas e imágenes.
- [frontend-design](kit/plan-b/frontend-design.zip): guía de diseño de Anthropic para webs y landings que no parezcan de plantilla.
- [animaciones](kit/plan-b/animaciones.zip): 20 estilos de animación en código para animar una escena de tu negocio (necesita Node.js). Guía para instalarlas y usarlas: [20 estilos de animación (Notion)](https://vivid-armadillo-c06.notion.site/20-estilos-de-animaci-n-para-tus-v-deos-se-instalan-una-vez-y-se-piden-con-un-comando-41242dad0d3881b3b9a8d83cfc972946).

## Skills de otros
¿Buscás algo que no está acá? Mirá [Skills y repos de otros](#r-skills-externas): dónde buscar, cómo revisarlas antes de instalar y dos ejemplos (animaciones para video y agent-desktop).

## Toda la guía en un ZIP
Todas las páginas del taller, las skills y los agentes en una carpeta para tu compu: [Descargá la guía completa](kit/descargas/taller-completo.zip).

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| La skill no aparece en `/` | Salí y volvé a entrar. Si sigue igual: "Fijate si existe ~/.claude/skills/[NOMBRE]/SKILL.md y si el name del encabezado coincide con la carpeta". |
| Claude cambió el texto al guardarla | Pedile que la guarde "exacta, sin cambios" de nuevo. |
| La app de Claude rechaza el ZIP | El ZIP tiene que tener adentro la carpeta de la skill, no el SKILL.md suelto. |

## Para seguir solo
- Pedile a Claude: "Leé mi skill propuesta-comercial y adaptala a cómo cotizamos nosotros". Las skills mejoran con el uso.
- Cuando repitas un pedido 3 veces, convertilo en skill: "Convertí lo que hicimos recién en una skill".
- Guardá tus skills en el repo **privado** de tu cerebro (`.claude/skills/`) para que tu equipo las tenga.
