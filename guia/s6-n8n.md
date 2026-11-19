---
titulo: n8n, tus automatizaciones
bloque: Setup
tiempo: 30 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s5-cuentas-nube
resultado: Cuenta de n8n Cloud en prueba, credenciales de Telegram, Google y Anthropic guardadas en n8n, y n8n conectado a Claude por MCP.
---

n8n es una cadena de montaje: "cuando pasa esto, hacé aquello, después aquello otro". Por ejemplo: llega un mensaje a tu bot de Telegram → Claude lo responde con tu cerebro → la consulta queda anotada en una planilla.
Ejemplo: Manuel Martínez le manda a su bot de Telegram la foto de un ticket y n8n la pasa a Claude, que la anota en su planilla de gastos. Todo corre en la nube, aunque su compu esté apagada.
Y conectado a Claude por MCP (el "enchufe" estándar entre Claude y otras apps, ver [Las piezas](#t2-piezas)), le podés pedir a Claude que use tus flujos conversando. En n8n, un **flujo** (workflow) es una de esas cadenas; tu **instancia** es tu propio n8n, con su dirección web.

## Antes de empezar
- [ ] Un mail para la cuenta de n8n.
- [ ] Para el Paso 3: el token de tu bot de Telegram ([Telegram](#s7-telegram)). Si todavía no lo tenés, hacé esa página y volvé.
- [ ] Para el Paso 5: una API key de Anthropic ([API de Anthropic](#s9-api-anthropic)). Mismo criterio.
- [ ] Claude Code instalado, si querés conectar n8n también ahí ([Instalá Claude Code](#s2-claude-code)).

## Cloud o en tu compu: qué elegir
| | **n8n Cloud** (recomendado hoy) | **Self-hosted** (instalado por vos, en tu compu o servidor) |
|---|---|---|
| Precio | Prueba gratis; después desde **€20/mes** | Gratis (pagás el servidor si lo subís a uno) |
| Instalación | Nada: es una web | Necesita **Docker** o **WSL** (programas técnicos para correr servidores en tu compu) |
| Bots de Telegram o WhatsApp | Funcionan directo | Necesitás un dominio con HTTPS para recibir mensajes de afuera |
| Mantenimiento | Lo hace n8n | Lo hacés vos |

> **Costo:** n8n publica sus precios en **euros** y con **pago anual**: **Starter €20/mes** (2.500 ejecuciones por mes) y **Pro €50/mes** (10.000 ejecuciones). La página tiene un selector mensual/anual pero solo muestra los precios anuales; el precio mensual y en dólares (terceros hablan de unos USD 24 para Starter) **no está confirmado al 18/11/2026**. La prueba de n8n Cloud **no pide tarjeta** y tiene 1.000 ejecuciones, 5 a la vez, 180 segundos máximo por ejecución y 1 proyecto. Cuánto dura la prueba **no figura en la página oficial** (terceros dicen 14 días): fijate la fecha de vencimiento cuando la actives.

> **Ojo:** una "ejecución" es cada vez que corre un flujo. Un flujo que revisa algo cada minuto gasta 1.440 ejecuciones por día y se come la prueba en un día. Para bots, usá disparadores que esperan (como el de Telegram), no revisiones cada X minutos.

## Paso 1 · Creá tu cuenta de n8n Cloud
1. Entrá a **[n8n.io](https://n8n.io)** y empezá la prueba gratis de **n8n Cloud**.
2. Registrate con tu mail y confirmalo. Si el mail no llega en 2 minutos, mirá en **Spam** o **Promociones**.
3. Elegí un nombre para tu espacio (por ejemplo, el de tu empresa). Ese nombre forma parte de la dirección de tu n8n.

**Tenés que ver:** el panel de n8n (**Overview**) y, en la barra del navegador, la dirección de tu instancia (algo como `https://[TU-ESPACIO].app.n8n.cloud`). Anotala: te sirve para volver a entrar.

## Paso 2 · Aprendé dónde se crean las credenciales
Una **credencial** es una llave guardada adentro de n8n. Se carga una vez y los flujos la usan sin mostrarla.

1. Tocá **Create** (arriba a la izquierda del menú o arriba a la derecha en **Overview**) › **Credential**.
2. Buscá el servicio por nombre.
3. Completá los datos y tocá **Save**. n8n prueba la credencial al guardarla.
4. Renombrala con algo claro, por ejemplo `Telegram - bot de turnos`.

> **Datos:** n8n es **el** lugar para estas claves. No las copies en el cerebro, en notas, ni en un chat con Claude.

**Tenés que ver:** la ventana para elegir el servicio de la credencial.

## Paso 3 · Credencial de Telegram
1. **Create › Credential** › buscá **Telegram**.
2. Abrí tu gestor de contraseñas, copiá el token de tu bot (lo guardaste en [Telegram](#s7-telegram), Paso 3) y pegalo en **Access Token**.
3. **Save**.

**Tenés que ver:** la credencial guardada sin errores.

## Paso 4 · Credencial de Google (Drive, Gmail o Sheets)
En n8n Cloud no hace falta crear nada en Google Cloud.

1. **Create › Credential** › buscá el servicio que vas a usar: **Google Sheets**, **Gmail** o **Google Drive** (cada uno es una credencial distinta).
2. Tocá **Sign in with Google** y elegí tu cuenta.
3. Leé los permisos que pide y aceptá.

> **Ojo:** este inicio de sesión rápido (Managed OAuth2) solo existe en **n8n Cloud** y para algunos servicios de Google (Drive, Gmail y Sheets, entre otros). En self-hosted hay que crear una app en Google Cloud: no lo hagas hoy.

**Tenés que ver:** la credencial marcada como conectada con tu mail de Google.

## Paso 5 · Credencial de Anthropic (Claude)
1. **Create › Credential** › buscá **Anthropic**.
2. Copiá desde tu gestor de contraseñas la clave que creaste en la Console de Anthropic ([API de Anthropic](#s9-api-anthropic)) y pegala en **API Key**.
3. **Save**.

> **Costo:** cada vez que un flujo usa Claude, se descuenta de tu crédito de la API de Anthropic, que es **aparte** de tu plan Pro. Por eso en la página de la API ponés un límite de gasto.

**Tenés que ver:** la credencial guardada sin errores.

## Paso 6 · Conectá n8n con Claude por MCP
Esto le da a Claude acceso a los flujos que vos habilites (no a todos).

**6.1 · Activá el MCP en n8n** (hace falta ser dueño o admin de la instancia; en tu cuenta nueva, lo sos):
1. Abrí **Settings** (suele estar abajo a la izquierda) › **Instance-level MCP** › **Enable MCP access**.
2. Creá un flujo vacío de prueba (**Create › Workflow**), llamalo `prueba-mcp` y guardalo.
3. En ese flujo: menú **…** › **Settings** › activá **Available in MCP**.
4. Volvé a **Settings › Instance-level MCP** › **Connect a client** y copiá la **Server URL**. Termina en `/mcp-server/http`. No es la dirección que ves en el navegador: usá la que muestra ese cuadro.

**6.2 · Agregalo en la app de Claude (web o escritorio):**
1. **Customize › Connectors** › **+ Add** › **Add custom connector**.
2. **Name:** `n8n`. **URL:** la **Server URL** del paso anterior. **Continue**.
3. Revisá la autenticación (dejá la que detecta) y tocá **Add**.
4. Tocá **Connect** y, cuando te lleve a n8n, aprobá el acceso.

> **Tip:** en **Connect a client** de n8n también podés elegir **[Claude.ai](https://Claude.ai)** en **Your client** y usar **One-click setup**.

**6.3 · Agregalo en Claude Code (opcional).** En una terminal (no adentro de Claude Code; en Windows, PowerShell). Reemplazá `[PEGÁ-ACÁ-LA-SERVER-URL]` por la **Server URL** que copiaste en el 6.1 (la que termina en `/mcp-server/http`):

```bash
claude mcp add --transport http n8n [PEGÁ-ACÁ-LA-SERVER-URL]
```

Después abrí `claude`, escribí `/mcp`, elegí **n8n** y **Authenticate**.

**Tenés que ver:** en **Customize › Connectors**, n8n como conectado. En Claude Code, `/mcp` muestra n8n conectado.

## Cómo sé que funcionó
En un chat nuevo de Claude, tocá **+ › Connectors**, activá n8n y pegá:

```prompt
Usá n8n y decime qué flujos tengo disponibles por MCP y qué hace cada uno. No ejecutes nada.
```

**Tenés que ver:** Claude nombra tu flujo `prueba-mcp`.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No aparece **Instance-level MCP** en **Settings** | Revisá que seas dueño o admin de la instancia. Si sigue, avisá en la mesa de ayuda. |
| Claude se conecta pero dice que no hay flujos | Activá **Available in MCP** en el flujo y guardalo. |
| Claude no conecta con la URL | Usá la **Server URL** de **Connect a client** (termina en `/mcp-server/http`), no la del navegador. |
| La credencial de Telegram da error | El token está mal copiado (sobra un espacio o falta un pedazo). Copialo de nuevo desde tu gestor de contraseñas; si lo perdiste, generá uno nuevo con `/token` en @BotFather. |
| La credencial de Anthropic da error | La clave está mal copiada o no tenés crédito cargado en la Console. |
| Las ejecuciones de la prueba se terminaron | Revisá qué flujo corre cada pocos minutos y desactivalo. |

## Para seguir solo
- Antes de que termine la prueba, decidí: **Starter** en Cloud o self-hosted. Para una pyme sin técnico, Cloud.
- Pedile a Claude: "Usá n8n y armame un flujo que todos los lunes a las 9 me mande por Telegram un resumen de [QUÉ COSA]". Revisalo antes de activarlo.
- Si en el futuro querés self-hosted, la instalación oficial es `curl -fsSL https://get.n8n.io | sh` y necesita Docker. Para producción, n8n recomienda Docker Compose.

## Fuentes
Consultadas el 18/11/2026.
- Precios y prueba de n8n Cloud: https://n8n.io/pricing/
- Instalación self-hosted: https://docs.n8n.io/hosting/
- Crear credenciales: https://docs.n8n.io/credentials/add-edit-credentials/
- Credencial de Telegram: https://docs.n8n.io/integrations/builtin/credentials/telegram/
- Credencial de Google (Managed OAuth2): https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/
- Credencial de Anthropic: https://docs.n8n.io/integrations/builtin/credentials/anthropic/
- Servidor MCP de instancia: https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server/
- Ejemplos de clientes MCP (Claude Code y Claude Desktop): https://docs.n8n.io/connect/connect-to-n8n-mcp-server/mcp-client-examples
- Conectores custom en Claude: https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp
- Terceros (precio mensual en USD): https://toolradar.com/tools/n8n/pricing
