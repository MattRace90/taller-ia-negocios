---
titulo: n8n, tus automatizaciones
bloque: Setup
tiempo: 30 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s5-cuentas-nube
resultado: Cuenta de n8n Cloud en prueba, credenciales de Telegram, Google y Anthropic guardadas en n8n, y n8n conectado a Claude desde la pestaña Code.
---

n8n es una cadena de montaje: "cuando pasa esto, hacé aquello, después aquello otro". Todo corre en la nube, aunque tu compu esté apagada.
Ejemplo: Manuel Martínez le manda a su bot de Telegram la foto de un ticket, n8n se la pasa a Claude y la anota en su planilla de gastos.
Conectado a Claude por MCP (el "enchufe" entre Claude y otras apps, ver [Las piezas](#t2-piezas)), le pedís a Claude que arme y use tus flujos conversando. Un **flujo** (workflow) es una de esas cadenas; tu **instancia** es tu propio n8n, con su dirección web.

## Antes de empezar
- [ ] Un mail para la cuenta de n8n.
- [ ] Para el Paso 3: el token de tu bot, en tu gestor de contraseñas ([Telegram](#s7-telegram)).
- [ ] Para el Paso 5: una API key de Anthropic ([API de Anthropic](#s9-api-anthropic)).
- [ ] La pestaña **Code** abierta en **Local** con tu carpeta `prueba-claude` ([Claude Code](#s2-claude-code)).

> **Costo:** usamos **n8n Cloud** (nada que instalar). La prueba **no pide tarjeta** e incluye 1.000 ejecuciones; fijate la fecha de vencimiento al activarla. Después: **Starter €20/mes** y **Pro €50/mes**, con pago anual (nov 2026; el precio mensual en dólares no está confirmado, verificá en [n8n.io/pricing](https://n8n.io/pricing/)).

> **Ojo:** una "ejecución" es cada vez que corre un flujo. Uno que revisa algo cada minuto gasta 1.440 por día y se come la prueba. Para bots, usá disparadores que esperan (como el de Telegram).

## Paso 1 · Creá tu cuenta de n8n Cloud
1. Entrá a **[n8n.io](https://n8n.io)** y empezá la prueba gratis de **n8n Cloud**.
2. Registrate con tu mail y confirmalo (si no llega, mirá **Spam**).
3. Elegí un nombre para tu espacio (por ejemplo, tu empresa).

**Tenés que ver:** el panel de n8n (**Overview**) y en el navegador una dirección como `https://[TU-ESPACIO].app.n8n.cloud`. Anotala.

## Paso 2 · Aprendé a crear credenciales
Una **credencial** es una llave guardada adentro de n8n: se carga una vez y los flujos la usan sin mostrarla.

1. **Create** › **Credential** › buscá el servicio.
2. Completá, tocá **Save** y renombrala con algo claro (por ejemplo `Telegram - bot de turnos`).

> **Datos:** n8n es **el** lugar para estas claves. Las copiás del gestor de contraseñas y las pegás acá, en la web de n8n. Nunca en el chat con Claude.

**Tenés que ver:** la ventana para elegir el servicio.

## Paso 3 · Credencial de Telegram
**Create › Credential** › **Telegram** › pegá el token desde tu gestor en **Access Token** › **Save**.

**Tenés que ver:** la credencial guardada sin errores.

## Paso 4 · Credencial de Google (Drive, Gmail o Sheets)
1. **Create › Credential** › **Google Sheets**, **Gmail** o **Google Drive** (cada uno es una credencial aparte).
2. **Sign in with Google** › elegí tu cuenta › leé los permisos y aceptá.

**Tenés que ver:** la credencial conectada con tu mail de Google.

## Paso 5 · Credencial de Anthropic
**Create › Credential** › **Anthropic** › pegá tu API key desde el gestor en **API Key** › **Save**.

> **Costo:** cada vez que un flujo usa Claude, se descuenta de tu crédito de la API, **aparte** de tu plan Pro.

**Tenés que ver:** la credencial guardada sin errores.

## Paso 6 · Activá el MCP en n8n
1. **Settings** (abajo a la izquierda) › **Instance-level MCP** › **Enable MCP access**.
2. Creá un flujo vacío (**Create › Workflow**), llamalo `prueba-mcp` y guardalo. En el flujo: menú **…** › **Settings** › activá **Available in MCP**.
3. Volvé a **Settings › Instance-level MCP** › **Connect a client**. Copiá la **Server URL** (termina en `/mcp-server/http`; no es la del navegador). Esa dirección no es secreta.
4. En ese mismo cuadro, buscá la opción de **Access Token** y generá un token. **No lo copies todavía.**

> **Ojo:** los nombres de este cuadro pueden variar según la versión de n8n. Si no ves **Access Token** sino solo un inicio de sesión (OAuth), saltá al **Ojo** del Paso 7.

**Tenés que ver:** la Server URL copiada y el token generado a la vista.

## Paso 7 · Conectá n8n a Claude desde la pestaña Code
1. En la pestaña Code, pegá:

```prompt
Creá en esta carpeta un archivo .env con la línea N8N_MCP_TOKEN= vacía (si ya existe el .env, agregá la línea), asegurate de que .env esté en el .gitignore y abrime el .env en el editor de texto de mi compu. No me pidas el token por el chat.
```

2. En el editor, pegá el token de n8n después del `=`, guardá y cerralo. Escribile a Claude `listo`.
3. Pegá este pedido, reemplazando la dirección por tu **Server URL**:

```prompt
Agregá n8n como servidor MCP para mi usuario, con transporte http, en la dirección [PEGÁ-ACÁ-LA-SERVER-URL], usando el token de N8N_MCP_TOKEN del .env como encabezado "Authorization: Bearer". Usá el comando claude mcp add con --scope user. Leé el token del archivo sin mostrármelo ni repetirlo en el chat. Después decime si quedó conectado.
```

4. Aprobá el permiso para que Claude corra el comando.
5. Abrí una sesión nueva en Code (**+ New**, misma carpeta) para que cargue n8n.

> **Ojo:** si n8n solo te ofrece inicio de sesión (sin token), pedile a Claude que agregue el servidor sin encabezado y después escribí `/mcp`, elegí **n8n** y **Authenticate**: se abre el navegador para aprobar el acceso.

**Tenés que ver:** en la sesión nueva, escribís `/mcp` y n8n aparece conectado.

## Cómo sé que funcionó
En la sesión nueva de Code, pegá:

```prompt
Usá n8n y decime qué flujos tengo disponibles por MCP y qué hace cada uno. No ejecutes nada.
```

**Tenés que ver:** Claude nombra tu flujo `prueba-mcp`.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No aparece **Instance-level MCP** | Revisá que seas dueño o admin de la instancia. Si sigue, mesa de ayuda. |
| Claude se conecta pero no ve flujos | Activá **Available in MCP** en el flujo y guardalo. |
| Claude no conecta | Revisá que usaste la **Server URL** de **Connect a client** y que el token en el `.env` esté completo. Abrí una sesión nueva. |
| La credencial de Telegram da error | El token está mal copiado. Copialo de nuevo desde el gestor. |
| La credencial de Anthropic da error | Clave mal copiada o sin crédito en la Console. |
| Se terminaron las ejecuciones de prueba | Buscá el flujo que corre cada pocos minutos y desactivalo. |

## Para seguir solo
- Antes de que termine la prueba, decidí: **Starter** en Cloud (lo más simple para una pyme) o instalarlo vos.
- Pedile a Claude: "Usá n8n y armame un flujo que todos los lunes a las 9 me mande por Telegram un resumen de [QUÉ COSA]". Revisalo antes de activarlo.
- También podés usar n8n desde el **Chat** de la app: **Customize › Connectors** › **+ Add** › **Add custom connector** con la misma Server URL.

## Fuentes
Consultadas el 18/11/2026.
- Precios y prueba: https://n8n.io/pricing/
- Credenciales: https://docs.n8n.io/credentials/add-edit-credentials/
- Servidor MCP de instancia: https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server/
- Clientes MCP (Claude Code): https://docs.n8n.io/connect/connect-to-n8n-mcp-server/mcp-client-examples
- MCP en Claude Code: https://code.claude.com/docs/en/mcp
