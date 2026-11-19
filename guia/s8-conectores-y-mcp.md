---
titulo: Conectores y MCP
bloque: Setup
tiempo: 30 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude, s2-claude-code
resultado: Claude conectado a tus herramientas (Google, Canva, Metricool, Meta Ads) y Claude Code con los MCP de tu ruta, verificados con /mcp.
---

Sin conectores, Claude solo sabe lo que le pegás en el chat. Con conectores, puede leer tu Drive, mirar tu agenda, armar una placa en Canva o revisar tus campañas de Meta, siempre con tu permiso.
Ejemplo: Fondus le pide a Claude "revisá cómo vienen las campañas de esta semana" y Claude lee los números directo de Meta Ads, sin exportar planillas.

**Qué es cada cosa:**
- **MCP** es el enchufe estándar: una forma común para que cualquier IA se conecte con cualquier herramienta.
- **Conector** es ese enchufe ya armado y listo para usar dentro de la app de Claude. Se conecta con un clic y tu usuario de esa herramienta.
- En **Claude Code** también podés enchufar MCP con el comando `claude mcp add`.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude ([Tu cuenta](#s1-claude)).
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] Las cuentas que vas a conectar, con tu sesión iniciada en el navegador: Google, Canva, Metricool, Meta Business, Supabase, Vercel, GitHub o n8n (según tu ruta).

> **Datos:** un conector le da a Claude el mismo acceso que tenés vos en esa herramienta. Conectá solo lo que vas a usar. Cuando Claude quiere **enviar, publicar, borrar o cambiar** algo, te pide permiso: leé antes de aceptar.

## Paso 1 · Conectá Google Drive, Gmail y Google Calendar
Si lo vas a hacer en [Meta y Google](#s14-meta-y-google), podés saltear este paso y el 3: son los mismos.
1. En la app de Claude, abrí un chat nuevo.
2. Tocá **+** (abajo a la izquierda del cuadro de texto) › **Connectors** y activá **Google Drive**, **Gmail** y **Google Calendar**.
3. Pedí algo que los use, por ejemplo: "¿Qué reuniones tengo mañana?". Claude te manda a Google para iniciar sesión.
4. Elegí tu cuenta de Google, leé los permisos y aceptá.

> **Ojo:** Google te avisa que Claude podría enviar mails. Claude solo envía, responde o reenvía con tu aprobación.

**Tenés que ver:** la respuesta con tus reuniones reales. En **Customize › Connectors**, los tres aparecen conectados.

## Paso 2 · Conectá Canva y Metricool desde el directorio
1. **Customize › Connectors** › buscá **Canva** en el directorio.
2. Tocá **Connect**, iniciá sesión en Canva y aceptá los permisos.
3. Repetí con **Metricool**.

> **Tip:** si Metricool no aparece en el directorio, agregalo como conector custom: **Customize › Connectors** › **+ Add** › **Add custom connector** › **Name:** `Metricool` › **URL:** `https://ai.metricool.com/mcp` › **Add** › **Connect**. Funciona con cualquier plan de Metricool, también el gratis.

**Tenés que ver:** Canva y Metricool como conectados en **Customize › Connectors**.

## Paso 3 · Conectá Meta Ads (MCP oficial de Meta)
Meta tiene un MCP propio para Ads. Está en **beta** (abierta desde abril de 2026, según terceros) y, según terceros, es gratis durante la beta. Que funcione para todas las cuentas de Argentina **no está confirmado al 18/11/2026**: algunas cuentas todavía figuran como no habilitadas.

1. **Customize › Connectors** › **+ Add** › **Add custom connector**.
2. **Name:** `Meta Ads`. **URL:** `https://mcp.facebook.com/ads`. Tocá **Continue** y después **Add**.
3. Tocá **Connect**. Se abre el inicio de sesión de Facebook: entrá con la cuenta que administra tus anuncios.
4. Elegí qué portfolios comerciales y cuentas publicitarias puede ver Claude. Elegí solo las de tu empresa.

> **Ojo:** este conector puede **cambiar presupuestos y campañas**. Hasta el [tutorial de Meta Ads](#p9-meta-ads), usalo solo para leer. En el chat, desde **+ › Connectors**, podés desactivar las herramientas que no necesitás.

**Tenés que ver:** Meta Ads como conectado. Si dice que tu cuenta no está habilitada, avisá en la mesa de ayuda: en el tutorial de Meta Ads hay un plan B.

## Paso 4 · Agregá MCP en Claude Code
Los conectores de la app (Pasos 1 a 3) **también aparecen en Claude Code** si iniciaste sesión con la misma cuenta. Lo que sigue son MCP técnicos que usamos solo en Claude Code.

Corré los comandos en una **terminal** (Terminal en Mac, PowerShell en Windows: los comandos son iguales), no adentro de Claude Code. Si ya tenés Claude Code abierto, salí con `/exit`. Pará la terminal en la carpeta del proyecto (por ejemplo, tu cerebro) con `cd` ([glosario](#t2-piezas)). Agregá solo los de tu ruta (tabla al final).

**Supabase** (tu base de datos):

```bash
claude mcp add --scope project --transport http supabase "https://mcp.supabase.com/mcp"
```

Queda guardado en el archivo `.mcp.json` de esa carpeta.

> **Tip:** para que Claude solo pueda leer y no cambiar tu base, usá la dirección `https://mcp.supabase.com/mcp?read_only=true`. Supabase recomienda no conectarlo a datos reales de producción sin necesidad.

**Vercel** (tus webs publicadas):

```bash
claude mcp add --transport http vercel https://mcp.vercel.com
```

**n8n** (tus automatizaciones). La dirección la sacás en n8n: **Settings › Instance-level MCP › Connect a client** ([n8n](#s6-n8n), Paso 6):

```bash
claude mcp add --transport http n8n [PEGÁ-ACÁ-LA-SERVER-URL]
```

**GitHub** (tus repositorios). **Opcional y avanzado:** para hoy, GitHub Desktop alcanza. Este es distinto: no usa inicio de sesión con navegador, sino un **token personal** (una contraseña larga solo para programas).
1. En [github.com](https://github.com): tu foto › **Settings › Developer settings › Personal access tokens › Fine-grained tokens › Generate new token**.
2. **Token name:** `claude-code`. **Expiration:** 30 días. **Repository access:** **Only select repositories** y elegí tu cerebro. Permisos: solo los que necesites.
3. **Generate token** y guardalo en tu gestor de contraseñas.
4. Escribí el comando **vos, en la terminal**, reemplazando `[TU_TOKEN]` por el token (sin corchetes). No le pases el token a Claude en el chat:

```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp -H "Authorization: Bearer [TU_TOKEN]"
```

> **Ojo:** el token queda guardado en la configuración de Claude Code en tu compu y en el historial de la terminal. Cerrá la terminal al terminar y, si dejás de usarlo, borralo en GitHub. Para lo de hoy, **GitHub Desktop alcanza** ([GitHub](#s4-github)): este MCP es opcional.

> **Tip:** por defecto, un MCP agregado con `claude mcp add` vale solo para la carpeta donde lo corriste. Para tenerlo en todas tus carpetas, agregá `--scope user` al comando.

**Tenés que ver:** cada comando termina sin error y dice que agregó el servidor.

## Paso 5 · Autenticá y verificá
1. En la terminal:

```bash
claude mcp list
```

2. Abrí Claude Code en la misma carpeta (`claude`) y escribí:

```text
/mcp
```

3. Para cada MCP que diga que necesita autenticación (Supabase, Vercel, n8n), elegilo › **Authenticate** › aceptá en el navegador.

**Tenés que ver:** en `/mcp`, cada servidor como conectado, con su lista de herramientas.

## Cómo sé que funcionó
En la app de Claude, chat nuevo:

```prompt
Usando mis conectores: decime qué reuniones tengo esta semana en Google Calendar, cuáles son los 3 archivos más recientes de mi Google Drive y, si tengo Metricool conectado, cuántas publicaciones tengo programadas. No envíes, publiques ni cambies nada.
```

Y en Claude Code:

```prompt
Listame los MCP que tenés conectados en esta carpeta y, para cada uno, una cosa que podrías hacer por mí. No ejecutes ninguna acción que cambie algo.
```

**Tenés que ver:** respuestas con tus datos reales y la lista de MCP de tu ruta.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo **Customize › Connectors** | Actualizá la app o entrá desde [claude.ai](https://claude.ai) en el navegador. |
| El conector aparece pero Claude no lo usa | En el chat: **+ › Connectors** y activalo para esa conversación. |
| `claude mcp add` dice que el nombre ya existe | Ya lo agregaste. Fijate con `claude mcp list`; para sacarlo: `claude mcp remove [NOMBRE]`. |
| `/mcp` muestra el servidor con error | Elegilo › **Authenticate** de nuevo. Si sigue, revisá la URL (en n8n, la que termina en `/mcp-server/http`). |
| Meta Ads dice que la cuenta no está habilitada | Es una beta. Avisá en la mesa de ayuda. |
| GitHub MCP da "Unauthorized" | El token venció o está mal copiado. Generá uno nuevo y repetí el comando. |

## Qué conectar según tu ruta
| Si tu ruta tiene… | Conectá en la app (Customize › Connectors) | Agregá en Claude Code |
|---|---|---|
| [Asistente en Telegram](#p2-asistente-telegram) | Google Drive; n8n (custom, opcional) | n8n (opcional) |
| [Agente que responde](#p3-agente-preguntas) | — (corre en Cloudflare: ver [Cuentas en la nube](#s5-cuentas-nube)) | — |
| [Foto a planilla](#p4-foto-a-tabla) | Google Drive | — |
| [Tu web](#p5-web-propia) | — | Vercel y Supabase (opcionales: para revisar publicaciones y tablas conversando) |
| [App en Lovable](#p6-lovable-y-calendario) | — | — |
| [Calendario de contenido](#p6-lovable-y-calendario) | **Metricool** (obligatorio), Google Calendar (opcional) | — |
| [Video](#p7-video) | Google Drive (para traer los videos) | — |
| [Seguimiento](#p8-seguimiento) | Google Drive y Gmail (opcionales) | — |
| [Meta Ads con agentes](#p9-meta-ads) | **Meta Ads** (custom, obligatorio) | — (lo toma de la app) |
| [Placas en tu voz](#p10-extras) | **Canva** (obligatorio) | — |
| [Reporte que llega solo](#p10-extras) | **Google Drive** (obligatorio), Gmail (opcional) | — |

## Para seguir solo
- Mirá el directorio completo en **Customize › Connectors**: hay conectores de Notion, HubSpot, Shopify, Slack y muchos más.
- Revisá cada tanto **Customize › Connectors** y desconectá lo que no usás.
- Cuando una herramienta tuya diga "tenemos MCP", ya sabés agregarla: conector custom en la app o `claude mcp add` en Claude Code.

## Fuentes
Consultadas el 18/11/2026.
- Directorio de conectores de Claude: https://claude.com/docs/connectors/directory · https://claude.com/connectors
- Conectores custom (Customize › Connectors, Add custom connector): https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp
- Conectores de Google Workspace: https://support.claude.com/en/articles/10166901-use-google-workspace-connectors
- MCP en Claude Code (`claude mcp add`, scopes, `/mcp`): https://code.claude.com/docs/en/mcp
- Metricool MCP: https://help.metricool.com/how-to-connect-metricools-mcp-with-claude-0l84v
- Meta Ads MCP: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-overview · https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started · https://www.facebook.com/business/news/meta-ads-ai-connectors
- Terceros (Meta Ads en Claude, beta y gratuidad): https://www.jonloomer.com/meta-ads-ai-connectors-claude/ · https://contextbolt.com/blog/meta-ads-mcp/ · https://pipeboard.co/guides/facebook-ads-mcp
- Supabase MCP: https://supabase.com/docs/guides/getting-started/mcp
- Vercel MCP: https://vercel.com/docs/agent-resources/vercel-mcp
- n8n MCP: https://docs.n8n.io/connect/connect-to-n8n-mcp-server/mcp-client-examples
- GitHub MCP para Claude: https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-claude.md
- Tokens de GitHub: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
