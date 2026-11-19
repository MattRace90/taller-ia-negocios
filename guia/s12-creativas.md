---
titulo: "Herramientas creativas (Higgsfield, HeyGen, ElevenLabs, Canva, Metricool)"
bloque: Setup
tiempo: 30 a 50 min (10 por herramienta que conectes)
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude, s2-claude-code, s10-conectar-todo
resultado: Las herramientas creativas que vas a usar, con cuenta creada, conectadas a Claude y probadas con un pedido real.
---

Con estas cinco herramientas, Claude pasa de escribir el guion a **producir la pieza**: imagen, video con avatar, voz, placa y posteo programado.
Ejemplo: Celve le pide a Claude "armá 3 placas de la promo de la semana y programalas para martes, jueves y sábado". Claude diseña en Canva y deja todo en Metricool.

| Herramienta | Para qué | ¿Plan gratis útil? | Dirección para conectar |
|---|---|---|---|
| **Higgsfield** | Imágenes y videos con IA (producto, UGC, b-roll) | No: pide plan pago | `https://mcp.higgsfield.ai/mcp` |
| **HeyGen** | Avatar hablando a cámara | Sí, 3 videos/mes con marca de agua | `https://mcp.heygen.com/mcp/v1/` |
| **ElevenLabs** | Voz, clon de voz, música | Sí, para probar | `https://api.elevenlabs.io/v1/mcp` |
| **Canva** | Placas, carruseles | Sí, con límites | Directorio de conectores |
| **Metricool** | Programar y medir redes | Sí (1 marca, 20 posts/mes) | Directorio o `https://ai.metricool.com/mcp` |

**Cómo se conecta cada una (igual para las cinco):** en la app de Claude, **Customize › Connectors**. Lo que conectás ahí **aparece solo en la pestaña Code** (misma cuenta). Si una no está en el directorio: **+** › **Add custom connector** › **Name** y **URL** de la tabla › **Add** › **Connect** › iniciás sesión en esa herramienta.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude ([Claude](#s1-claude)) y la pestaña **Code** andando ([Claude Code](#s2-claude-code)).
- [ ] Leíste el método para conectar ([Conectá cualquier herramienta](#s10-conectar-todo)).
- [ ] Sabés qué vas a producir ([Fábrica de contenidos](#u-fabrica) o [Video](#p7-video)).
- [ ] Tu marca escrita en el cerebro (`marca/`): colores, tipografías, voz ([Armá el cerebro](#p1-cerebro)).

> **Costo:** todo lo que genera Claude **descuenta créditos de cada herramienta**, igual que en su web. Antes de producir en serie, pedile el costo estimado y que espere tu OK.

> **Datos:** clonar una voz o una cara requiere el **consentimiento de esa persona**. Solo la tuya, o la de alguien que lo autorizó por escrito.

## Paso 1 · Higgsfield: imagen y video
1. Entrá a **[higgsfield.ai](https://higgsfield.ai)**, registrate y elegí un plan pago (el gratis no trae créditos y el conector pide suscripción activa).
2. Conectalo en **Customize › Connectors** con la URL de la tabla.
3. Opcional (lo que recomienda Higgsfield para Claude Code): abrí la pestaña **Code**, elegí la carpeta de tu cerebro y pedí:

```prompt
Instalá Higgsfield para que pueda generar imágenes y videos desde acá: la CLI oficial (@higgsfield/cli) y sus skills (higgsfield-ai/skills). Explicame en simple qué hace cada paso antes de pedirme permiso. El inicio de sesión lo hago yo en el navegador.
```

Aprobá cada permiso después de leerlo.

> **Costo:** Starter **USD 15/mes**, Plus **USD 49/mes**, Ultra **USD 129/mes** (blog oficial, oct 2026). Cambian seguido: verificá en [higgsfield.ai/pricing](https://higgsfield.ai/pricing) (nov 2026). Por Claude **siempre** descuenta créditos.

> **Ojo:** si hoy no querés pagar, salteá Higgsfield y mirá la demo de Mati.

**Tenés que ver:** Higgsfield conectado en **Customize › Connectors** (y, si hiciste el paso 3, Claude te confirma la instalación).

## Paso 2 · HeyGen: avatar
1. Entrá a **[heygen.com](https://heygen.com)** y registrate. Para probar alcanza el **Free**.
2. Conectalo en **Customize › Connectors** con la URL de la tabla y aprobá en HeyGen.

> **Costo:** Free **USD 0** (3 videos/mes, hasta 1 min, con marca de agua). Creator **USD 29/mes**. Pro **USD 49/mes** (nov 2026, [heygen.com/pricing](https://www.heygen.com/pricing)). El MCP usa los créditos de tu plan.

**Tenés que ver:** pedís "mostrame mis avatares" y aparece la galería.

## Paso 3 · ElevenLabs: voz
1. Entrá a **[elevenlabs.io](https://elevenlabs.io)** y registrate. Free para probar; **Starter** si vas a publicar o clonar tu voz.
2. Conectalo como **custom connector** con la URL de la tabla › elegí tu espacio de trabajo › **Authorize**.

> **Tip:** la versión del directorio es **recortada** (no hace música). Usá la custom.

> **Costo:** Free **USD 0** (10.000 créditos/mes, sin licencia comercial). Starter **USD 6/mes**. Creator **USD 22/mes** (nov 2026, [elevenlabs.io/pricing](https://elevenlabs.io/pricing)).

**Tenés que ver:** pedís "listame voces en español" y aparece una lista.

## Paso 4 · Canva: placas
1. Si no tenés cuenta, registrate en **[canva.com](https://canva.com)**.
2. **Customize › Connectors** › buscá **Canva** › **Connect** › aceptá.

> **Costo:** el conector no se paga. **Canva Pro**, según terceros, **USD 18/mes** (sep 2026): verificá en [canva.com/pricing](https://www.canva.com/pricing/). El **Brand Kit** es de los planes pagos.

**Tenés que ver:** Canva conectado en **Customize › Connectors**.

## Paso 5 · Metricool: programar y medir
1. Registrate en **[metricool.com](https://metricool.com)** y conectá tus redes adentro de Metricool.
2. **Customize › Connectors** › buscá **Metricool** › **Connect** (si no aparece, custom con la URL de la tabla).

> **Costo:** Free **USD 0** (1 marca, 20 posts/mes, sin LinkedIn ni X, **incluye el MCP**). Starter desde **USD 25/mes** (nov 2026, [metricool.com/pricing](https://metricool.com/pricing/)).

**Tenés que ver:** pedís "¿qué tengo programado esta semana?" y responde con tu calendario.

## Cómo sé que funcionó
En la pestaña **Code**, con la carpeta de tu cerebro abierta (usá solo las que conectaste):

```prompt
Leé la voz y los colores de mi marca en la carpeta marca/.
1. Con Canva, armá una placa cuadrada para esta promo inventada: "[PROMO DE PRUEBA]".
2. Con Higgsfield, generá UNA imagen de producto. Antes decime cuántos créditos gasta y esperá mi OK.
3. Con ElevenLabs, generá una locución de 10 segundos con el texto de la placa.
4. Con Metricool, decime el mejor horario de esta semana y dejá la publicación como BORRADOR.
No publiques ni envíes nada.
```

**Tenés que ver:** la placa en tu Canva, la imagen y el audio con link, y un borrador en Metricool.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Higgsfield dice que no tenés suscripción o créditos | El conector necesita plan pago activo. |
| El conector custom pide "OAuth client ID" | Dejá vacías las opciones avanzadas: estas herramientas inician sesión solas. |
| En la pestaña Code no aparece una herramienta | Escribí `/mcp` en el cuadro. Si dice "needs authentication", elegila › **Authenticate**. Revisá que sea la misma cuenta de Claude. |
| Claude gasta créditos de más | Pedile: "Agregá a mi CLAUDE.md: antes de generar imagen, video o voz, decime el costo y esperá mi OK". |
| HeyGen o ElevenLabs no ven tus avatares o voces | Conectaste otra cuenta o espacio. Desconectá y volvé a conectar. |
| Mac: la instalación de Higgsfield da `EACCES` | Decile a Claude: "Instalalo sin sudo, como recomienda npm". Si sigue, mesa de ayuda. |

## Para seguir solo
- Armá una skill con tu receta ("guion → placa en Canva → borrador en Metricool") y corrila cada lunes ([Fábrica de contenidos](#u-fabrica)).
- Creá tu gemelo digital en HeyGen y tu clon de voz en ElevenLabs, y guardá sus nombres en `marca/`.
- Al mes, pedile a Claude con Metricool qué piezas funcionaron mejor.

## Fuentes
Consultadas el 18/11/2026.
- Higgsfield: https://higgsfield.ai/creator-hub/help-center/integrations/how-do-i-connect-higgsfield-to-ai-agent · https://higgsfield.ai/pricing
- HeyGen MCP: https://developers.heygen.com/mcp/overview · https://www.heygen.com/pricing
- ElevenLabs MCP: https://elevenlabs.io/docs/eleven-api/resources/mcp-server · https://elevenlabs.io/pricing
- Canva MCP: https://www.canva.com/help/mcp-agent-setup/ · https://claude.com/connectors/canva
- Metricool MCP: https://help.metricool.com/how-to-connect-metricools-mcp-with-claude-0l84v · https://metricool.com/pricing/
- Conectores de la app en Claude Code: https://code.claude.com/docs/en/mcp
