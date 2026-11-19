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

## Para seguir solo
- Tarea programada que cada lunes lea Meta Ads y te deje un resumen en un Google Doc ([Tareas programadas](#t4-tareas-programadas)).
- Seguí con [Meta Ads con agentes](#p9-meta-ads): un equipo que propone cambios y solo aplica cuando escribís `APROBADO`.
- **Avanzado:** agregar Meta Ads directo a Claude Code (sin la app) pide crear una app en [developers.facebook.com/apps](https://developers.facebook.com/apps) con su ID de cliente. No hace falta hoy.

## Fuentes
Consultadas el 18/11/2026.
- Meta Ads MCP: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started
- Meta, conectores de IA (ayuda): https://www.facebook.com/business/help/1456422242197840
- Cuenta publicitaria (terceros): https://www.leadsie.com/blog/create-facebook-ad-account
- Beta y gratuidad (terceros): https://www.jonloomer.com/meta-ads-ai-connectors-claude/
- Conectores de Google en Claude: https://support.claude.com/en/articles/10166901-use-google-workspace-connectors
- Conectores de la app dentro de Claude Code: https://code.claude.com/docs/en/mcp
