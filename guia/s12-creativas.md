---
titulo: Herramientas creativas (Higgsfield, HeyGen, ElevenLabs, Canva, Metricool)
bloque: Setup
tiempo: 30 a 50 min (10 por herramienta que conectes)
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude, s2-claude-code, s10-conectar-todo
resultado: Las herramientas creativas que vas a usar, con cuenta creada, conectadas a Claude y probadas con un pedido real.
---

Con estas cinco herramientas, Claude pasa de escribir el guion a **producir la pieza**: la imagen, el video con avatar, la voz, la placa y el posteo programado. Es lo que usamos en la agencia todas las semanas.
Ejemplo: Celve le pide a Claude "armá 3 placas de la promo de la semana y programalas para martes, jueves y sábado". Claude diseña en Canva y deja todo en Metricool, sin salir del chat.

| Herramienta | Para qué la usamos | ¿Hay plan gratis útil? | Cómo se conecta |
|---|---|---|---|
| **Higgsfield** | Imágenes y videos con IA (producto, UGC: videos tipo "cliente real hablando", b-roll: tomas de apoyo) | No: el MCP pide plan pago | Conector custom + CLI y skills en Claude Code |
| **HeyGen** | Avatar (vos o uno de stock) hablando a cámara | Sí, 3 videos por mes con marca de agua | MCP remoto oficial |
| **ElevenLabs** | Voz: locuciones, clon de tu voz, música | Sí, para probar | MCP remoto oficial |
| **Canva** | Placas, carruseles, presentaciones | Sí, con límites | Conector oficial |
| **Metricool** | Programar y medir redes | Sí (1 marca, 20 posts por mes) | Conector / MCP remoto, también en el plan gratis |

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude ([Claude](#s1-claude)).
- [ ] Leíste el método para conectar ([Conectá cualquier herramienta](#s10-conectar-todo)).
- [ ] Sabés qué vas a producir (mirá tu ruta en [Fábrica de contenidos](#u-fabrica) o [Video](#p7-video)).
- [ ] Tu marca escrita en el cerebro (`marca/`): colores, tipografías, voz ([Armá el cerebro](#p1-cerebro)).

> **Costo:** todo lo que se genera por Claude **descuenta créditos de cada herramienta**, igual que si lo hicieras en su web. Antes de producir en serie, pedile a Claude que te diga cuánto va a gastar y que te pida confirmación.

> **Datos:** clonar una voz o una cara requiere el **consentimiento de esa persona**. Solo la tuya, o la de alguien que lo autorizó por escrito.

## Paso 1 · Higgsfield: imagen y video
**Qué es:** una plataforma que junta los mejores modelos de imagen y video (los cambia seguido). La usamos para fotos de producto, b-roll y videos tipo UGC.

1. Entrá a **[higgsfield.ai](https://higgsfield.ai)** y registrate (Google o mail).
2. Elegí un plan pago: el gratis **no trae créditos** y el conector **requiere una suscripción activa**.

> **Ojo:** el pago es en dólares con tarjeta. Si hoy no querés pagar (o la tarjeta no pasa), salteá Higgsfield: mirá la demo de Mati y probá HeyGen, ElevenLabs, Canva o Metricool, que tienen plan gratis.

> **Costo:** Starter **USD 15/mes** (200 créditos), Plus **USD 49/mes** (1.000), Ultra **USD 129/mes** (3.000), según el blog oficial de oct 2026. Los precios cambiaron varias veces este año: verificá en [higgsfield.ai/pricing](https://higgsfield.ai/pricing) (nov 2026). Las generaciones por Claude **siempre** descuentan créditos, aunque tu plan tenga "ilimitados" en la web.

**En la app de Claude:** **Customize › Connectors** › **+** › **Add custom connector** › **Name:** `Higgsfield` › **URL:** `https://mcp.higgsfield.ai/mcp` › **Add** › **Connect** › autorizá en la ventana de Higgsfield.

**En Claude Code** (el camino que recomienda Higgsfield): pedile a Claude que instale su **CLI** (un programa que se usa desde la terminal) y sus skills.

```prompt
Instalá Higgsfield para que pueda generar imágenes y videos desde acá. Usá la CLI oficial (@higgsfield/cli) y sus skills (higgsfield-ai/skills). Mostrame cada comando antes de correrlo. El inicio de sesión lo hago yo en el navegador.
```

Por detrás corre `npm i -g @higgsfield/cli`, `higgsfield auth login` y `npx skills add higgsfield-ai/skills`. Cuando Claude te pida permiso para cada comando, leelo y aceptá.

> **Ojo:** también circula el comando `claude mcp add --transport http --scope user higgsfield https://mcp.higgsfield.ai/mcp`. La URL es la oficial, pero la ayuda de Higgsfield no publica ese comando para Claude Code: si lo usás, verificá con `/mcp`.

**Tenés que ver:** Higgsfield conectado en **Customize › Connectors** (o `higgsfield` en `/mcp` / en `/skills`).

## Paso 2 · HeyGen: avatar y voz
**Qué es:** videos de una persona hablando a cámara a partir de un texto. Podés usar un avatar de stock o crear tu "gemelo digital" con tu cara y tu voz.

1. Entrá a **[heygen.com](https://heygen.com)** y registrate.
2. Para probar alcanza el **Free**.

> **Costo:** Free **USD 0** (3 videos por mes, hasta 1 minuto, con marca de agua). Creator **USD 29/mes** (24 con pago anual). Pro **USD 49/mes**. Business **USD 149/mes** + USD 20 por asiento (nov 2026, [heygen.com/pricing](https://www.heygen.com/pricing)). El MCP está en **todos los planes** y usa los créditos de tu plan, sin cargo extra.

**En la app de Claude:** **Customize › Connectors** › **+** › **Add custom connector** › **Name:** `HeyGen` › **URL:** `https://mcp.heygen.com/mcp/v1/` › **Add** › **Connect** › aprobá en HeyGen.

**En Claude Code** (en una terminal, no adentro de Claude Code):

```bash
claude mcp add --transport http --scope user heygen https://mcp.heygen.com/mcp/v1/
```

Después, `/mcp` › **heygen** › **Authenticate**.

> **Ojo:** HeyGen confirma que su MCP remoto funciona con Claude Code, pero no publica el comando exacto: este es el formato estándar.

**Tenés que ver:** HeyGen conectado. Pedí "mostrame mis avatares" y aparece la galería.

## Paso 3 · ElevenLabs: voz
**Qué es:** voces realistas en español (también rioplatense), clon de tu voz, efectos y música. Es la voz que usan nuestros agentes telefónicos de [Vapi](#s13-vapi).

1. Entrá a **[elevenlabs.io](https://elevenlabs.io)** y registrate.
2. Free para probar. Si vas a publicar lo que generás o clonar tu voz, **Starter**.

> **Costo:** Free **USD 0** (10.000 créditos/mes). Starter **USD 6/mes** (30.000 créditos, licencia comercial y clon de voz instantáneo). Creator **USD 22/mes** (121.000 créditos y clon profesional). Pro **USD 99/mes** (nov 2026, [elevenlabs.io/pricing](https://elevenlabs.io/pricing)). El plan gratis no figura con licencia comercial.

**En la app de Claude:** **Customize › Connectors** › **+** › **Add custom connector** › **Name:** `ElevenLabs` › **URL:** `https://api.elevenlabs.io/v1/mcp` › **Add** › elegí tu espacio de trabajo › **Authorize**.

> **Tip:** ElevenLabs también tiene una versión en el directorio de conectores, pero es **recortada** (no genera música ni imágenes). Para todo, usá el conector custom con la URL de arriba.

**En Claude Code:**

```bash
claude mcp add --transport http --scope user elevenlabs https://api.elevenlabs.io/v1/mcp
```

> **Ojo:** ElevenLabs dice que cualquier cliente MCP funciona igual (URL + inicio de sesión), pero no publica el comando para Claude Code: verificá con `/mcp`. El MCP local viejo (`uvx elevenlabs-mcp` con API key) está **discontinuado**: no lo uses.

**Tenés que ver:** ElevenLabs conectado y, al pedir "listame voces en español", una lista.

## Paso 4 · Canva: placas y diseños
**Qué es:** el diseño de siempre, ahora manejado por Claude: crea diseños nuevos, los adapta a tu marca, los redimensiona y los exporta.

1. Si no tenés cuenta, entrá a **[canva.com](https://canva.com)** y registrate.
2. En la app de Claude: **Customize › Connectors** › buscá **Canva** en el directorio › **Connect** › iniciá sesión y aceptá.

**En Claude Code:** si conectaste Canva en la app con la misma cuenta, ya aparece. Si querés agregarlo aparte:

```bash
claude mcp add --transport http --scope user canva https://mcp.canva.com/mcp
```

> **Costo:** el conector no se paga aparte. **Canva Pro**, según terceros, cuesta **USD 18/mes o USD 180/año** (sep 2026): verificá en [canva.com/pricing](https://www.canva.com/pricing/). Con Canva gratis podés crear diseños, pero el **Brand Kit** y las plantillas de marca son de los planes pagos.

> **Ojo:** las fuentes no coinciden en si el conector funciona completo con una cuenta de Canva gratis. Probalo con la tuya; si te limita, es el plan.

**Tenés que ver:** Canva conectado en **Customize › Connectors**.

## Paso 5 · Metricool: programar y medir
**Qué es:** el calendario de redes. Claude puede ver tus mejores horarios, leer métricas y dejar posteos programados (o en borrador para que vos los apruebes).

1. Entrá a **[metricool.com](https://metricool.com)**, registrate y conectá tus redes (Instagram, Facebook, TikTok…) adentro de Metricool.
2. En la app de Claude: **Customize › Connectors** › buscá **Metricool** › **Connect**. Si no aparece: **+** › **Add custom connector** › **Name:** `Metricool` › **URL:** `https://ai.metricool.com/mcp`.

**En Claude Code:**

```bash
claude mcp add --transport http --scope user metricool https://ai.metricool.com/mcp
```

> **Costo:** Free **USD 0** (1 marca, 20 posts programados por mes, sin LinkedIn ni X, **incluye el MCP**). Starter desde **USD 25/mes** o **USD 20/mes** con pago anual, hasta 5 marcas (nov 2026, [metricool.com/pricing](https://metricool.com/pricing/)).

> **Ojo:** Metricool publica la URL para la app de Claude; el comando para Claude Code es el formato estándar. Verificá con `/mcp`.

**Tenés que ver:** Metricool conectado. Pedí "¿qué tengo programado esta semana?" y responde con tu calendario.

## Cómo sé que funcionó
Probá una cadena completa en la app de Claude (usá solo las que conectaste):

```prompt
Leé la voz y los colores de mi marca en [PEGÁ O ADJUNTÁ TU ARCHIVO DE MARCA].
1. Con Canva, armá una placa cuadrada para esta promo (dato inventado para probar): "[PROMO DE PRUEBA]".
2. Con Higgsfield, generá UNA imagen de producto para acompañarla. Antes decime cuántos créditos va a gastar y esperá mi OK.
3. Con ElevenLabs, generá una locución de 10 segundos con el texto de la placa.
4. Con Metricool, decime cuál es el mejor horario para publicar esta semana y dejá la publicación como BORRADOR, sin publicar.
No publiques ni envíes nada.
```

**Tenés que ver:** la placa en tu Canva, la imagen y el audio con link, y un borrador en Metricool.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Higgsfield dice que no tenés suscripción o créditos | El conector necesita un plan pago activo. Revisá tu plan en [higgsfield.ai](https://higgsfield.ai). |
| El conector custom pide "OAuth client ID" | Dejá vacías las opciones avanzadas: estas cinco herramientas inician sesión solas. |
| Claude genera de más y te gasta créditos | Agregá a tu `CLAUDE.md`: "Antes de generar imagen, video o voz, decime el costo estimado y esperá mi confirmación". |
| HeyGen o ElevenLabs no ven tus avatares o voces | Iniciaste sesión con otra cuenta o espacio de trabajo. Desconectá y volvé a conectar eligiendo el correcto. |
| Metricool no muestra una red | Esa red no está conectada adentro de Metricool, o es LinkedIn/X en el plan gratis. |
| `/mcp` muestra "needs authentication" | Elegí el servidor › **Authenticate** y aceptá en el navegador. |
| Mac: al instalar Higgsfield sale `EACCES: permission denied` | Pedile a Claude: "Instalalo sin usar sudo, con la forma que recomiende npm". Si sigue, avisá en la mesa de ayuda. |

## Para seguir solo
- Armá una skill con tu receta de contenido ("guion → placa en Canva → borrador en Metricool") y corrila cada lunes ([Fábrica de contenidos](#u-fabrica)).
- Si hacés video con avatar seguido, creá tu gemelo digital en HeyGen y tu clon de voz en ElevenLabs, y guardá sus nombres en `marca/` del cerebro.
- Al mes, pedile a Claude con Metricool qué piezas funcionaron mejor y ajustá el plan siguiente.

## Fuentes
Consultadas el 18/11/2026.
- Higgsfield con agentes (URL del MCP, CLI, skills, créditos): https://higgsfield.ai/creator-hub/help-center/integrations/how-do-i-connect-higgsfield-to-ai-agent
- Higgsfield, precios: https://higgsfield.ai/pricing · https://higgsfield.ai/blog/higgsfield-pricing-explained
- HeyGen MCP remoto: https://developers.heygen.com/mcp/overview · precios: https://www.heygen.com/pricing
- ElevenLabs MCP alojado: https://elevenlabs.io/docs/eleven-api/resources/mcp-server · MCP local discontinuado: https://github.com/elevenlabs/elevenlabs-mcp · precios: https://elevenlabs.io/pricing
- Canva MCP: https://www.canva.com/help/mcp-agent-setup/ · https://claude.com/connectors/canva · precio de terceros: https://stylefactoryproductions.com/blog/canva-pricing
- Metricool MCP y precios: https://help.metricool.com/how-to-connect-metricools-mcp-with-claude-0l84v · https://metricool.com/pricing/
