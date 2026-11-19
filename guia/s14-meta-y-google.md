---
titulo: Meta Business y Google conectados a Claude
bloque: Setup
tiempo: 40 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude, s2-claude-code, s10-conectar-todo
resultado: Portfolio comercial de Meta con cuenta publicitaria, el MCP oficial de Meta Ads conectado en modo lectura, y Google Drive, Gmail y Calendar conectados a Claude.
---

Meta y Google son donde ya vive tu negocio: anuncios, Instagram, mails, agenda y archivos. Conectarlos le da a Claude tus datos reales, sin exportar planillas.
Ejemplo: Fondus pregunta "¿qué campaña me trajo consultas más baratas esta semana y qué tengo agendado con esos interesados?". Claude cruza Meta Ads con Google Calendar en una respuesta.

**Todo se conecta en la app de Claude** (**Customize › Connectors**) y **aparece solo en la pestaña Code** con la misma cuenta. No hace falta terminal.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude ([Claude](#s1-claude)) y la pestaña **Code** andando ([Claude Code](#s2-claude-code)).
- [ ] Una cuenta de Google (Gmail o Google Workspace de tu empresa).
- [ ] Para Meta: tu Facebook personal, la **página de Facebook** de la empresa y, si tenés, el **Instagram** profesional.
- [ ] Leíste el método para conectar ([Conectá cualquier herramienta](#s10-conectar-todo)).

> **Datos:** Gmail y Drive tienen datos de tus clientes. Claude los lee **solo cuando se lo pedís** y te pide permiso antes de enviar, responder o borrar. No copies datos personales de clientes al cerebro ni a GitHub.

## Parte A · Meta

## Paso 1 · Creá (o revisá) tu portfolio comercial
El **portfolio comercial** (antes "Business Manager") es la carpeta de tu empresa en Meta: página, Instagram, cuenta publicitaria y personas con acceso.

1. Entrá a **[business.facebook.com](https://business.facebook.com)** con tu Facebook.
2. Si ya tenés portfolio, elegilo arriba a la izquierda y pasá al Paso 2.
3. Si no: creá uno con el nombre de la empresa, tu nombre y un mail de trabajo, y confirmá el mail.
4. En **Configuración** › **Cuentas** › **Páginas**, agregá tu página. En **Cuentas de Instagram**, conectá tu Instagram.

> **Ojo:** Meta puede pedir un código por SMS o frenar un portfolio nuevo con una "verificación de seguridad" que tarda horas o días. Si te bloquea, seguí con el CSV de práctica de [Meta Ads con agentes](#p9-meta-ads). Los nombres de los menús cambian seguido: si no encontrás algo, usá el buscador de la configuración.

> **Costo:** el portfolio es **gratis**. Solo pagás lo que invertís en anuncios.

**Tenés que ver:** tu portfolio con la página y el Instagram adentro.

## Paso 2 · Creá tu cuenta publicitaria
Si ya pautás, revisá que la cuenta esté **dentro del portfolio** y pasá al Paso 3.

1. **Configuración** › **Cuentas** › **Cuentas publicitarias** › **Agregar** › **Crear una cuenta publicitaria nueva**.
2. Nombre (por ejemplo `[TU-EMPRESA] - Principal`), **zona horaria** y **moneda**.
3. Elegí que es para **tu negocio**, aceptá y agregate con **control total**.
4. El medio de pago lo cargás vos, en la pantalla de Meta, cuando vayas a pautar. Nunca en un chat.

> **Ojo:** la **moneda y la zona horaria no se cambian** después. Un portfolio nuevo empieza con **una** cuenta publicitaria.

**Tenés que ver:** la cuenta en **Cuentas publicitarias**, con vos como administrador.

## Paso 3 · Conectá el MCP oficial de Meta Ads
Meta tiene un MCP propio para Ads, en **beta**. Lee tus campañas y, si lo dejás, las cambia.

1. En la app de Claude: **Customize › Connectors** › **+** › **Add custom connector**.
2. **Name:** `Meta Ads` · **URL:** `https://mcp.facebook.com/ads` › **Add**.
3. **Connect** › iniciá sesión con Facebook y elegí **solo** el portfolio y las cuentas de tu empresa.

| Permiso que pide | Para qué |
|---|---|
| `ads_read` | **Leer** campañas, gasto y resultados |
| `ads_management` | **Crear y cambiar** campañas y presupuestos |
| `ads_mcp_management` | Usar el MCP (siempre) |
| `business_management`, `pages_show_list`, `instagram_basic`, `catalog_management` | Opcionales: portfolio, páginas, Instagram, catálogo |

> **Ojo:** con `ads_management`, Claude **puede gastar plata**. Hasta [Meta Ads con agentes](#p9-meta-ads), usalo solo para leer: en el chat, **+ › Connectors**, desactivá las herramientas que crean o modifican. Nunca apruebes un cambio sin leerlo.

> **Ojo:** al 18/11/2026 no está confirmado que la beta esté habilitada para todas las cuentas de Argentina, ni hasta cuándo es gratis. Si no aparece tu cuenta, hay plan B en [Meta Ads con agentes](#p9-meta-ads).

**Tenés que ver:** Meta Ads conectado en **Customize › Connectors**.

## Parte B · Google

## Paso 4 · Conectá Drive, Gmail y Calendar
Si ya lo hiciste en [Conectores y MCP](#s8-conectores-y-mcp), saltá al Paso 5.

1. En la app de Claude: **Customize › Connectors**.
2. Conectá **Google Drive**, **Gmail** y **Google Calendar**.
3. Elegí tu cuenta de Google, leé los permisos y aceptá.

> **Ojo:** Google avisa que Claude podría enviar mails o crear eventos. Claude lo hace solo **con tu aprobación**.

> **Tip:** con **Google Workspace**, puede que el administrador tenga que habilitar a Claude. Si ves "acceso bloqueado por el administrador", pasale esta página.

**Tenés que ver:** los tres conectados en **Customize › Connectors**.

## Paso 5 · Revisá que aparezcan en la pestaña Code
1. Abrí la pestaña **Code** y elegí la carpeta de tu cerebro.
2. Escribí `/mcp` en el cuadro.

**Tenés que ver:** Meta Ads, Gmail, Drive y Calendar en la lista, con el prefijo **claude.ai** (por ejemplo, `claude.ai Gmail`). Si alguno pide iniciar sesión, eso se hace en **Customize › Connectors** de la app.

## Cómo sé que funcionó
En la pestaña **Code** (o en un chat):

```prompt
Sin cambiar, enviar ni publicar nada:
1. Con Meta Ads, decime cuánto gasté los últimos 7 días, la campaña con resultados más baratos y la más cara.
2. Con Google Calendar, listame las reuniones de esta semana.
3. Con Gmail, decime cuántos mails sin leer parecen consultas de clientes (sin mostrarme datos personales).
4. Con Google Drive, mostrame los 3 archivos que modifiqué más recientemente.
```

**Tenés que ver:** números reales de tu cuenta publicitaria y tus datos de Google. Si todavía no pautaste, Meta dice que no hay gasto: está bien.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Meta Ads dice que la cuenta no está habilitada | Es una beta. Mesa de ayuda y plan B de [Meta Ads con agentes](#p9-meta-ads). |
| Claude no ve mi cuenta publicitaria | No la tildaste al conectar o no está en el portfolio. Desconectá y volvé a conectar. |
| No tengo permisos en la cuenta publicitaria | Pedile **control total** a quien administra el portfolio. |
| Google: "acceso bloqueado por el administrador" | Lo habilita el administrador de Google de tu empresa. |
| En la pestaña Code no aparecen los conectores | Revisá que la app y la pestaña Code usen la misma cuenta de Claude, y que no estén apagados en `/mcp`. |

## Para n8n: tu app de Meta y el token
Solo si querés que un **flujo de n8n** lea (o cambie) tus campañas, por ejemplo un reporte que se arma solo cada lunes ([n8n](#s6-n8n)). Para usar Meta Ads con Claude **no hace falta**: alcanza con el Paso 3.

n8n no usa el conector de Claude. Necesita dos cosas: una **app de Meta** (el "enchufe" de tu empresa en Meta for Developers) y un **token** (una llave larga) de un **usuario del sistema** (un usuario robot de tu portfolio, que no es una persona y no se desloguea).

> **Datos:** el token es como la llave de tu cuenta publicitaria. **Nunca** lo pegues en el chat de Claude, en el cerebro ni en GitHub. Va directo de la pantalla de Meta a la credencial de n8n. Si se filtra, revocalo (Paso 5 de esta sección) y generá otro.

Necesitás ser **administrador del portfolio comercial**. Tené n8n abierto en otra pestaña antes de generar el token.

**1 · Creá la app.** Entrá a [developers.facebook.com](https://developers.facebook.com) con tu Facebook › **My Apps** (Mis apps) › **Create App** (Crear app). Poné un nombre (por ejemplo `[TU-EMPRESA] n8n`) y tu mail. En **casos de uso**, elegí **Measure ad performance data with Marketing API** (solo leer) o **Create & manage ads with Marketing API** (leer y cambiar). Si te pregunta el tipo de app, elegí **Business**. Vinculala a tu portfolio comercial.

**Tenés que ver:** el panel de tu app, con el caso de uso de Marketing API.

> **Ojo:** Meta cambió hace poco este asistente. En la versión vieja se elegía **Other › Business** y después se agregaba el producto **Marketing API** desde el panel. Si ves esa versión, hacelo así.

**2 · Activá los permisos de la app.** En el menú de la izquierda, **Use cases** (Casos de uso) › tu caso de Marketing API › tocá **Add** al lado de `ads_read`. Sumá `ads_management` **solo** si el flujo va a modificar campañas.

**3 · Creá el usuario del sistema.** En [business.facebook.com](https://business.facebook.com) › **Configuración** › **Usuarios** › **Usuarios del sistema** › **Agregar**. Nombre: `n8n`. Rol: **Empleado** (no le des Administrador si no hace falta).

**Tenés que ver:** el usuario `n8n` en la lista.

**4 · Dale tu cuenta publicitaria y tu app.** Con el usuario `n8n` elegido › **Asignar activos** › **Cuentas publicitarias** › tu cuenta › permiso de **ver rendimiento** (y **administrar campañas** solo si va a modificar) › **Guardar**. Repetí con **Apps** › tu app.

**Tenés que ver:** la cuenta publicitaria y la app en los activos del usuario `n8n`.

> **Ojo:** no pudimos verificar en pantalla los nombres exactos de los botones y permisos en español (cambian seguido). Si no los encontrás, usá el buscador de la configuración del portfolio.

**5 · Generá el token.** Con el usuario `n8n` elegido › **Generar nuevo token** › elegí tu app › vencimiento **Nunca** (si te deja elegir) › tildá `ads_read` (y `ads_management` solo si va a modificar) › **Generar**. Copialo y pegalo directo en n8n (punto 7). Meta lo muestra **una sola vez**. Para anularlo: en el mismo usuario, **Revocar tokens**.

> **Ojo:** según la documentación de Meta, el token de un usuario del sistema **no vence**, pero deja de andar si alguien lo revoca o cambian los permisos de la app.

**6 · Probalo en el Graph API Explorer.** Entrá a [developers.facebook.com/tools/explorer](https://developers.facebook.com/tools/explorer), pegá el token en **Access Token**, escribí `me/adaccounts?fields=name,account_id` y tocá **Submit**. Es una herramienta de Meta: el token no sale de Meta.

**Tenés que ver:** el nombre de tu cuenta publicitaria y su número. Para ver vencimiento y permisos: [Access Token Debugger](https://developers.facebook.com/tools/debug/accesstoken).

**7 · Cargalo en n8n.** En n8n › **Credentials** › **Create credential** › buscá **Facebook Graph API** › pegá el token en **Access Token** › **Save**. Esa credencial la usa el nodo **Facebook Graph API** (por ejemplo, nodo `act_[NÚMERO-DE-CUENTA]/insights` para traer gasto y resultados).

**Tenés que ver:** la credencial guardada sin error y, al probar el nodo, los datos de tu cuenta.

> **Tip:** ¿no sabés armar el flujo? En la pestaña Code, pedile a Claude: "Armame un flujo de n8n que cada lunes traiga el gasto y los resultados de los últimos 7 días de mi cuenta de Meta Ads con la credencial Facebook Graph API y me los mande por mail". Claude arma el flujo; el token ya está en n8n y nunca pasa por el chat.

## Para seguir solo
- Tarea programada que cada lunes lea Meta Ads y te deje un resumen en un Google Doc ([Tareas programadas](#t4-tareas-programadas)).
- Seguí con [Meta Ads con agentes](#p9-meta-ads): un equipo que propone cambios y solo aplica cuando escribís `APROBADO`.
- **Avanzado:** agregar Meta Ads directo a Claude Code (sin la app) pide una app de Meta como la de "Para n8n", con su ID de cliente. No hace falta hoy.

## Fuentes
Consultadas el 18 y 19/11/2026.
- Meta Ads MCP: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started
- Meta, conectores de IA (ayuda): https://www.facebook.com/business/help/1456422242197840
- Cuenta publicitaria (terceros): https://www.leadsie.com/blog/create-facebook-ad-account
- Beta y gratuidad (terceros): https://www.jonloomer.com/meta-ads-ai-connectors-claude/
- Conectores de Google en Claude: https://support.claude.com/en/articles/10166901-use-google-workspace-connectors
- Conectores de la app dentro de Claude Code: https://code.claude.com/docs/en/mcp
- Marketing API, autenticación y tokens de usuario del sistema: https://developers.facebook.com/documentation/ads-commerce/marketing-api/get-started/authentication
- Marketing API, casos de uso al crear la app: https://developers.facebook.com/documentation/development/create-an-app/marketing-api-use-cases
- Usuarios del sistema (Meta for Developers): https://developers.facebook.com/docs/business-management-apis/system-users
- Tokens de acceso (Meta for Developers): https://developers.facebook.com/docs/facebook-login/guides/access-tokens
- Graph API Explorer: https://developers.facebook.com/tools/explorer
- n8n, credencial Facebook Graph API: https://docs.n8n.io/integrations/builtin/credentials/facebookgraph/
