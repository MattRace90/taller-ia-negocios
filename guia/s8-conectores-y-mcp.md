---
titulo: Conectores y MCP
bloque: Setup
tiempo: 25 min
para: Según tu desafío (mirá la tabla de abajo)
necesitas: s1-claude, s2-claude-code
resultado: "Claude conectado a tus herramientas (Google, Canva, Metricool, Meta Ads) y la pestaña Code con los MCP de tu ruta, verificados con /mcp."
---

Sin conectores, Claude solo sabe lo que le pegás. Con conectores, lee tu Drive, mira tu agenda, arma una placa en Canva o revisa tus campañas de Meta, siempre con tu permiso.
Ejemplo: Fondus pide "revisá cómo vienen las campañas de esta semana" y Claude lee los números directo de Meta Ads, sin exportar planillas.

- **MCP** es el enchufe estándar para que una IA se conecte con una herramienta.
- **Conector** es ese enchufe ya armado en la app de Claude: se conecta con un clic y tu usuario.
- Lo que conectás en **Customize › Connectors** **aparece solo en la pestaña Code** (misma cuenta). Por eso siempre empezás por ahí.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude ([Tu cuenta](#s1-claude)).
- [ ] La pestaña **Code** andando ([Claude Code](#s2-claude-code)).
- [ ] Sesión iniciada en el navegador en las cuentas que vas a conectar (Google, Canva, Metricool, Meta Business, Supabase, Vercel o n8n, según tu ruta).

> **Datos:** un conector le da a Claude el mismo acceso que tenés vos. Conectá solo lo que vas a usar. Cuando Claude quiera **enviar, publicar, borrar o cambiar** algo, te pide permiso: leé antes de aceptar.

## Paso 1 · Conectá Google Drive, Gmail y Calendar
Si lo hacés en [Meta y Google](#s14-meta-y-google), salteá este paso y el 3.
1. En la app de Claude: **Customize › Connectors** › buscá **Google Drive** › **Connect**. Repetí con **Gmail** y **Google Calendar**.
2. Elegí tu cuenta de Google, leé los permisos y aceptá.

> **Ojo:** Google avisa que Claude podría enviar mails. Claude solo envía con tu aprobación.

**Tenés que ver:** los tres como conectados en **Customize › Connectors**.

## Paso 2 · Conectá Canva y Metricool
1. **Customize › Connectors** › buscá **Canva** › **Connect** › iniciá sesión y aceptá.
2. Repetí con **Metricool**.

> **Tip:** si Metricool no aparece: **Customize › Connectors** › **+ Add** › **Add custom connector** › **Name:** `Metricool` › **URL:** `https://ai.metricool.com/mcp` › **Add** › **Connect**. Anda también con el plan gratis.

**Tenés que ver:** Canva y Metricool como conectados.

## Paso 3 · Conectá Meta Ads (MCP oficial de Meta)
Está en **beta**. Que ande con todas las cuentas de Argentina **no está confirmado al 18/11/2026**.
1. **Customize › Connectors** › **+ Add** › **Add custom connector**.
2. **Name:** `Meta Ads` · **URL:** `https://mcp.facebook.com/ads` › **Add** › **Connect**.
3. Entrá con la cuenta de Facebook que administra tus anuncios y elegí **solo** las cuentas publicitarias de tu empresa.

> **Ojo:** este conector puede **cambiar presupuestos y campañas**. Hasta el [tutorial de Meta Ads](#p9-meta-ads), usalo solo para leer.

**Tenés que ver:** Meta Ads como conectado. Si dice que tu cuenta no está habilitada, avisá en la mesa de ayuda: en el tutorial de Meta Ads hay un plan B.

## Paso 4 · Agregá los MCP técnicos desde la pestaña Code
Estos (Supabase, Vercel, n8n) no tienen conector armado, así que se los pedís a Claude. Abrí la pestaña **Code**, elegí la carpeta del proyecto (por ejemplo, tu cerebro) y pedí **solo los de tu ruta** (tabla de abajo). Claude te va a pedir permiso para correr un comando: leé y tocá **Permitir**.

**Vercel** (tus webs publicadas):

```prompt
Agregá el MCP de Vercel con esta dirección https://mcp.vercel.com para todas mis carpetas y decime cuando esté. Después decime cómo inicio sesión.
```

**Supabase** (tu base de datos), solo para esta carpeta y en modo lectura:

```prompt
Agregá el MCP de Supabase solo para esta carpeta, con esta dirección https://mcp.supabase.com/mcp?read_only=true, y decime cuando esté. Después decime cómo inicio sesión.
```

**n8n** (tus automatizaciones). La dirección la copiás en n8n: **Settings › Instance-level MCP › Connect a client** ([n8n](#s6-n8n), Paso 6):

```prompt
Agregá el MCP de n8n con esta dirección [PEGÁ-ACÁ-LA-SERVER-URL] para todas mis carpetas y decime cuando esté. Después decime cómo inicio sesión.
```

**Tenés que ver:** Claude te confirma que agregó cada uno.

## Paso 5 · Iniciá sesión y verificá
1. Abrí una sesión nueva en la misma carpeta (**+ New**) para que tome los MCP nuevos.
2. Escribí `/mcp` en el cuadro.
3. En cada uno que diga que necesita autenticación: elegilo › **Authenticate** › aceptá en el navegador.

> **Ojo:** el nombre del botón puede variar según la versión de la app. Si no lo ves, pedile a Claude "Decime cómo inicio sesión en el MCP de [NOMBRE]".

**Tenés que ver:** en `/mcp`, cada servidor conectado. Los conectores de la app también aparecen ahí.

## Cómo sé que funcionó
En la pestaña Code:

```prompt
Listame los conectores y MCP que tenés disponibles en esta carpeta y, para cada uno, una cosa que podrías hacer por mí. Después decime qué reuniones tengo esta semana en Google Calendar. No envíes, publiques ni cambies nada.
```

**Tenés que ver:** la lista con los de tu ruta y tus reuniones reales.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo **Customize › Connectors** | Actualizá la app o entrá a [claude.ai](https://claude.ai) en el navegador. |
| Un conector de la app no aparece en Code | Revisá que sea la misma cuenta y abrí una sesión nueva. En `/mcp`, fijate que no esté apagado. |
| Claude dice que el MCP ya existe | Ya estaba. Pedile "Mostrame mis MCP y sacá el de [NOMBRE] si está repetido". |
| `/mcp` muestra un servidor con error | Elegilo › **Authenticate** de nuevo. En n8n, la dirección termina en `/mcp-server/http`. |
| Meta Ads dice que la cuenta no está habilitada | Es una beta. Avisá en la mesa de ayuda. |

## Qué conectar según tu ruta
| Si tu ruta tiene… | En la app (Customize › Connectors) | En la pestaña Code (Paso 4) |
|---|---|---|
| [Asistente en Telegram](#p2-asistente-telegram) | Google Drive | n8n (opcional) |
| [Agente que responde](#p3-agente-preguntas) | — (ver [Cuentas en la nube](#s5-cuentas-nube)) | — |
| [Foto a planilla](#p4-foto-a-tabla) | Google Drive | — |
| [Tu web](#p5-web-propia) | — | Vercel y Supabase (opcionales) |
| [Calendario de contenido](#p6-lovable-y-calendario) | **Metricool** (obligatorio), Google Calendar | — |
| [Video](#p7-video) | Google Drive | — |
| [Seguimiento](#p8-seguimiento) | Google Drive y Gmail (opcionales) | — |
| [Meta Ads con agentes](#p9-meta-ads) | **Meta Ads** (obligatorio) | — |
| [Placas y reportes](#p10-extras) | **Canva** y **Google Drive** | — |

## Para seguir solo
- Mirá el directorio completo en **Customize › Connectors** (Notion, HubSpot, Shopify, Slack…) y desconectá cada tanto lo que no usás.
- Cuando una herramienta diga "tenemos MCP", ya sabés: conector custom en la app o "Agregá el MCP de X con esta dirección…" en Code. Método completo en [Conectá cualquier herramienta](#s10-conectar-todo).
- Avanzado: el MCP de GitHub pide un **token** (no inicia sesión con el navegador). Para hoy **GitHub Desktop alcanza** ([GitHub](#s4-github)). Si lo querés, pedile a Claude que lo configure leyendo el token de un `.env` que pegás vos en el editor, nunca en el chat.

## Fuentes
Consultadas el 18/11/2026.
- Conectores y conectores custom: https://claude.com/docs/connectors/directory · https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp
- Google Workspace: https://support.claude.com/en/articles/10166901-use-google-workspace-connectors
- MCP en Claude Code y pestaña Code: https://code.claude.com/docs/en/mcp · https://code.claude.com/docs/en/desktop
- Metricool: https://help.metricool.com/how-to-connect-metricools-mcp-with-claude-0l84v
- Meta Ads MCP: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-overview
- Supabase: https://supabase.com/docs/guides/getting-started/mcp · Vercel: https://vercel.com/docs/agent-resources/vercel-mcp · n8n: https://docs.n8n.io/connect/connect-to-n8n-mcp-server/mcp-client-examples
