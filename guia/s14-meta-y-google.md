---
titulo: Meta Business y Google conectados a Claude
bloque: Setup
tiempo: 40 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude, s2-claude-code, s10-conectar-todo
resultado: Portfolio comercial de Meta con cuenta publicitaria, el MCP oficial de Meta Ads conectado en modo lectura, y Google Drive, Gmail y Calendar conectados a Claude.
---

Meta y Google son donde ya vive tu negocio: tus anuncios, tu Instagram, tus mails, tu agenda y tus archivos. Conectarlos le da a Claude los datos reales para trabajar, sin exportar planillas.
Ejemplo: Fondus le pregunta a Claude "¿qué campaña me trajo consultas más baratas esta semana y qué tengo agendado con esos interesados?". Claude cruza Meta Ads con Google Calendar en una sola respuesta.

## Antes de empezar
- [ ] Plan **Pro** o superior en Claude ([Claude](#s1-claude)).
- [ ] Una cuenta de Google (Gmail o Google Workspace de tu empresa).
- [ ] Para Meta: tu perfil personal de Facebook, la **página de Facebook** de tu empresa y, si tenés, la cuenta de **Instagram** profesional.
- [ ] Leíste el método para conectar ([Conectá cualquier herramienta](#s10-conectar-todo)).

> **Datos:** Gmail y Drive tienen datos de tus clientes. Claude los lee **solo cuando se lo pedís** y te pide permiso antes de enviar, responder o borrar. No le pidas que copie datos personales de clientes al cerebro ni a GitHub.

## Parte A · Meta

## Paso 1 · Creá (o revisá) tu portfolio comercial
El **portfolio comercial** (antes "Business Manager") es la carpeta de tu empresa en Meta: adentro van la página, el Instagram, la cuenta publicitaria y las personas con acceso.

> **Ojo:** Meta a veces pide un código por SMS o de tu app de autenticación, o frena un portfolio nuevo con una "verificación de seguridad" que puede tardar horas o días. Tené el celular a mano. Si te bloquea, no pelees con eso en el taller: seguí con el CSV de práctica de [Meta Ads con agentes](#p9-meta-ads) y conectás tu cuenta real después.

1. Entrá a **[business.facebook.com](https://business.facebook.com)** con tu Facebook personal.
2. Si ya tenés un portfolio de tu empresa, elegilo arriba a la izquierda y pasá al Paso 2.
3. Si no: tocá para crear un portfolio comercial, poné el nombre de tu empresa, tu nombre y un mail de trabajo, y confirmá el mail.
4. En **Configuración** (**Settings**) › **Cuentas** › **Páginas**, agregá tu página de Facebook. En **Cuentas de Instagram**, conectá tu Instagram.

> **Costo:** el portfolio y Meta Business Suite son **gratis**. Lo único que se paga es lo que invertís en anuncios.

> **Ojo:** Meta cambia los nombres de sus menús seguido (y según el idioma). Si no encontrás algo, buscá en el buscador de la configuración del portfolio.

**Tenés que ver:** tu portfolio con la página y el Instagram de la empresa adentro.

## Paso 2 · Creá tu cuenta publicitaria
Si ya pautás, revisá que tu cuenta publicitaria esté **dentro del portfolio** y pasá al Paso 3.

1. **Configuración** › **Cuentas** › **Cuentas publicitarias** › **Agregar** › **Crear una cuenta publicitaria nueva**.
2. Poné nombre (por ejemplo `[TU-EMPRESA] - Principal`), **zona horaria** y **moneda**.
3. Elegí que es para **tu negocio** y aceptá los términos.
4. Agregate como persona con **control total**. El medio de pago cargalo recién cuando vayas a pautar, vos, en la pantalla de Meta (nunca en un chat).

> **Ojo:** la **moneda y la zona horaria no se pueden cambiar** después. Elegí bien (pesos argentinos o dólares, según cómo vayas a pagar). Un portfolio nuevo empieza pudiendo crear **una** cuenta publicitaria; según terceros, el límite sube cuando empezás a pautar y pagar.

**Tenés que ver:** la cuenta publicitaria en **Cuentas publicitarias**, con vos como administrador.

## Paso 3 · Conectá el MCP oficial de Meta Ads
Meta tiene un MCP propio para Ads, en **beta**. Le permite a Claude leer tus campañas y, si se lo permitís, cambiarlas.

**En la app de Claude** (el camino simple):
1. **Customize › Connectors** › **+** › **Add custom connector**.
2. **Name:** `Meta Ads` · **URL:** `https://mcp.facebook.com/ads` › **Add**.
3. **Connect** › iniciá sesión con Facebook y elegí **solo** el portfolio y las cuentas publicitarias de tu empresa.

Lo que conectás en la app **también aparece en Claude Code** si iniciaste sesión con la misma cuenta. Para el taller, no hace falta más.

**Qué permisos pide** (según la documentación de Meta):

| Permiso | Para qué |
|---|---|
| `ads_mcp_management` | Usar el MCP (siempre) |
| `ads_read` | **Leer** campañas, gasto y resultados |
| `ads_management` | **Crear y cambiar** campañas, anuncios y presupuestos |
| `business_management`, `pages_show_list`, `instagram_basic`, `catalog_management` | Opcionales: ver tu portfolio, páginas, Instagram y catálogo |

> **Ojo:** con `ads_management`, Claude **puede cambiar presupuestos y gastar plata**. Hasta que hagas [Meta Ads con agentes](#p9-meta-ads), usalo solo para leer: en el chat, **+ › Connectors**, desactivá las herramientas que crean o modifican. Y nunca apruebes un cambio sin leerlo.

> **Ojo:** al 18/11/2026 no está confirmado que la beta esté habilitada para todas las cuentas de Argentina, ni hasta cuándo es gratis (terceros dicen que es gratis durante la beta). Si tu cuenta no aparece, hay plan B en [Meta Ads con agentes](#p9-meta-ads).

**Solo si querés agregarlo directo en Claude Code** (avanzado, no hace falta hoy): Meta pide crear una app en **[developers.facebook.com/apps](https://developers.facebook.com/apps)**, sumarle el caso de uso del MCP de anuncios, configurar la URL de redirección en **Facebook Login for Business** y correr en la terminal (en Windows, PowerShell; el comando es el mismo):

```bash
claude mcp add --transport http --client-id [ID-DE-TU-APP-DE-META] meta-ads https://mcp.facebook.com/ads
```

**Tenés que ver:** Meta Ads conectado en **Customize › Connectors**.

## Parte B · Google

## Paso 4 · Conectá Drive, Gmail y Calendar en la app
Son conectores oficiales, sin claves. Si ya los conectaste en [Conectores y MCP](#s8-conectores-y-mcp), Paso 1, saltá al Paso 5.

1. En la app de Claude: **Customize › Connectors**.
2. Buscá y conectá **Google Drive**, **Gmail** y **Google Calendar** (o en un chat: **+ › Connectors** y activalos).
3. Elegí tu cuenta de Google, leé los permisos y aceptá.

> **Ojo:** Google te avisa que Claude podría enviar mails o crear eventos. Claude solo envía, responde o agenda **con tu aprobación**.

> **Tip:** si tu empresa usa **Google Workspace**, puede que el administrador tenga que permitir el acceso de Claude. Si te aparece un aviso de "acceso bloqueado por el administrador", pasale esta página a quien maneja las cuentas.

**Tenés que ver:** los tres como conectados en **Customize › Connectors**.

## Paso 5 · Usalos en Claude Code
No tenés que hacer nada más: con la misma cuenta de Claude, Drive, Gmail y Calendar **aparecen solos** en Claude Code.

1. Abrí Claude Code (en la terminal, `claude`; o la pestaña **Code** de la app) y escribí `/mcp`.
2. Buscá los que empiezan con **[claude.ai](https://claude.ai)** (por ejemplo, `claude.ai Gmail`).

> **Ojo:** si un conector de la app pide iniciar sesión, eso se hace desde la app de Claude, no desde Claude Code.

> **Tip:** Google tiene además sus propios MCP oficiales para Gmail, Drive y Calendar, pero al 18/11/2026 están en **programa de vista previa para desarrolladores** y piden un proyecto de Google Cloud y credenciales propias. No hacen falta para el taller: los conectores de la app alcanzan.

**Tenés que ver:** en `/mcp`, los conectores de Google listados como conectados.

## Cómo sé que funcionó
En la app de Claude (o en Claude Code):

```prompt
Sin cambiar, enviar ni publicar nada:
1. Con Meta Ads, decime cuánto gasté los últimos 7 días en mi cuenta publicitaria, cuál fue la campaña con resultados más baratos y cuál la más cara.
2. Con Google Calendar, listame las reuniones de esta semana.
3. Con Gmail, decime cuántos mails sin leer tengo que parezcan consultas de clientes (sin mostrarme datos personales).
4. Con Google Drive, mostrame los 3 archivos que modifiqué más recientemente.
```

**Tenés que ver:** números reales de tu cuenta publicitaria y tus datos de Google. Si todavía no pautaste, Meta va a decir que no hay gasto: está bien.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Meta Ads dice que la cuenta no está habilitada | Es una beta. Avisá en la mesa de ayuda y seguí con el plan B de [Meta Ads con agentes](#p9-meta-ads). |
| Claude no ve mi cuenta publicitaria | Al conectar no la elegiste, o no está dentro del portfolio. Desconectá, volvé a conectar y tildala. |
| No tengo permisos en la cuenta publicitaria | Pedile a quien la administra que te dé **control total** desde la configuración del portfolio. |
| Google: "acceso bloqueado por el administrador" | Tu cuenta de Workspace no permite apps externas. Lo habilita el administrador de Google de tu empresa. |
| Gmail o Calendar conectados pero Claude no los usa | En el chat: **+ › Connectors** y activalos para esa conversación. |
| En Claude Code no aparecen los conectores | Revisá con `/login` que sea la misma cuenta de la app, y que no estén apagados en `/mcp`. |

## Para seguir solo
- Armá una tarea programada que cada lunes lea Meta Ads y te deje un resumen en un Google Doc ([Tareas programadas](#t4-tareas-programadas)).
- Cuando tengas confianza, seguí con [Meta Ads con agentes](#p9-meta-ads): un equipo que propone cambios y solo los aplica cuando escribís `APROBADO`.
- Una vez por mes, revisá en tu cuenta de Google (**Seguridad › Apps de terceros**) y en el portfolio de Meta qué apps tienen acceso, y sacá lo que no uses.

## Fuentes
Consultadas el 18/11/2026.
- Meta Ads MCP, inicio y permisos: https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started · https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-overview
- Meta, conectores de IA para anuncios (ayuda): https://www.facebook.com/business/help/1456422242197840
- Cuenta publicitaria en el portfolio (terceros, límites y moneda): https://www.leadsie.com/blog/create-facebook-ad-account · https://help.leadsie.com/article/131-add-ad-account-meta-business-portfolio
- Beta y gratuidad (terceros): https://www.jonloomer.com/meta-ads-ai-connectors-claude/ · https://contextbolt.com/blog/meta-ads-mcp/
- Conectores de Google Workspace en Claude: https://support.claude.com/en/articles/10166901-use-google-workspace-connectors
- Conectores de [claude.ai](https://claude.ai) dentro de Claude Code: https://code.claude.com/docs/en/mcp
- MCP oficiales de Google (vista previa): https://developers.google.com/workspace/guides/configure-mcp-servers
