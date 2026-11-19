---
titulo: API de Anthropic
bloque: Setup
tiempo: 15 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s1-claude
resultado: Cuenta en la Console de Anthropic con crédito cargado, límite de gasto mensual y una API key guardada en un lugar seguro.
---

Tu plan Pro sirve para que **vos** uses Claude. Cuando un **bot** o un flujo de n8n usa Claude solo, sin vos adelante, paga por uso con la **API**: una cuenta aparte, con su propio crédito.
Ejemplo: el bot de Viajes TDH que responde "¿qué incluye el paquete a Bariloche?" llama a Claude por la API. Cada respuesta cuesta fracciones de centavo y se descuenta de ese crédito.

> **Costo:** la suscripción de [claude.ai](https://claude.ai) (Pro) y la API son **cuentas y facturaciones separadas**. El plan Pro **no** incluye crédito de API.

## Antes de empezar
- [ ] Una tarjeta de crédito que acepte pagos en dólares.
- [ ] Un gestor de contraseñas (el de tu navegador, el de tu celular, 1Password, Bitwarden…).

## Paso 1 · Creá tu cuenta en la Console
1. Entrá a **[platform.claude.com](https://platform.claude.com)** y registrate. Es la **Console**: la web de Anthropic para programas y bots, distinta de [claude.ai](https://claude.ai). Podés usar el mismo mail que en [claude.ai](https://claude.ai): igual es una cuenta de facturación aparte.
2. Completá los datos de tu organización (el nombre de tu empresa).

**Tenés que ver:** el panel de la Claude Console.

## Paso 2 · Cargá crédito
La API es **prepaga**: cargás saldo y se va descontando. Si se termina, tu bot deja de responder.

> **Ojo:** este pago también es en dólares: puede pedir aprobación por SMS o en la app del banco, y muchas tarjetas de débito lo rechazan. Si no pasa, avisá en la mesa de ayuda. Las prácticas con bot (Telegram, agente) necesitan este crédito: mientras se resuelve, podés armar el prompt y los casos de prueba.

1. Entrá a **Settings › Billing** (o **[platform.claude.com/settings/billing](https://platform.claude.com/settings/billing)**). Hace falta rol Admin o Billing; si creaste la cuenta, lo tenés.
2. Tocá **Buy credits**, poné el monto y confirmá.
3. Para el taller alcanza con poco (más abajo ves cuánto rinde).

> **Costo:** el **monto mínimo de compra no está confirmado al 18/11/2026**: la ayuda oficial no lo dice y una guía de terceros habla de USD 5. Lo vas a ver en la pantalla de **Buy credits**. Los créditos **vencen al año** y **no se reembolsan**. Anthropic dice que las cuentas nuevas reciben algo de crédito gratis para probar, pero no publica cuánto.

> **Ojo:** no actives **auto-reload** (recarga automática) hoy. Si lo activás y tu saldo ya está por debajo del umbral, te cobra en el acto.

**Tenés que ver:** en **Billing**, tu saldo (**Credit balance**) con el monto que cargaste.

## Paso 3 · Poné un límite de gasto mensual
1. Entrá a **[platform.claude.com/settings/spend-limits](https://platform.claude.com/settings/spend-limits)**.
2. Al lado de **Monthly spend limit**, tocá **Set limit** (o **Adjust limit**).
3. Poné un tope cómodo, por ejemplo **USD 10**.

Si tu bot llega al tope, deja de responder hasta el mes siguiente (o hasta que subas el límite). Es tu red de seguridad si algo queda en un bucle.

**Tenés que ver:** **Monthly spend limit** con el monto que elegiste.

## Paso 4 · Creá una API key
1. Entrá a **Settings › API Keys**.
2. Tocá **+ Create Key**.
3. Ponele un nombre que diga dónde la vas a usar, por ejemplo `n8n-bot-telegram`. Una clave por uso: si una se filtra, borrás solo esa.
4. Tocá **Copy Key** y pasá directo al Paso 5. **La clave completa se muestra una sola vez:** si cerrás la ventana sin guardarla, tenés que crear otra.

**Tenés que ver:** la clave en la lista de **API Keys** con el nombre que le pusiste.

## Paso 5 · Guardala en el lugar que corresponde
La API key es una contraseña que **gasta tu plata**.

1. **Primero, en tu gestor de contraseñas**: entrada nueva `Anthropic API - [NOMBRE DE LA CLAVE]`.
2. **Después, solo donde se usa**:

| Dónde corre tu bot | Dónde va la clave |
|---|---|
| n8n | **Create › Credential › Anthropic** › **API Key** ([n8n](#s6-n8n), Paso 5) |
| Cloudflare Workers | Como secreto: `npx wrangler secret put ANTHROPIC_API_KEY` ([Cuentas en la nube](#s5-cuentas-nube)) |
| Vercel | Proyecto › **Settings › Environment Variables**, tipo **Secret** |
| Un proyecto en tu compu | En un archivo `.env` dentro de la carpeta del proyecto, que esté en el `.gitignore`. La pegás vos a mano: [cómo crear el `.env`](#t6-datos-y-seguridad) |

> **Datos:** la API key **nunca** va en el cerebro, en GitHub, en un chat (con Claude ni con nadie), en un mail ni en una captura. Si se filtró: **Settings › API Keys**, borrala y creá otra.

> **Ojo:** **no** la cargues como variable de entorno general de tu compu con el nombre `ANTHROPIC_API_KEY`. Si Claude Code la encuentra, te ofrece usarla y empieza a **cobrarte por API** en vez de usar tu plan Pro.

**Tenés que ver:** la clave guardada en tu gestor y en un solo lugar más (el que usa tu bot).

## Cuánto cuesta en la práctica
Precios oficiales por millón de **tokens** (un token es un pedazo de palabra; Claude cobra lo que lee y lo que escribe):

| Modelo | Lo que lee (entrada) | Lo que escribe (salida) | Para qué |
|---|---|---|---|
| **Haiku 5.5** (prompts de hasta 100.000 tokens) | USD 0,10 | USD 0,50 | Bots simples, clasificar mensajes, respuestas cortas |
| **Sonnet 5.5** | USD 2 | USD 10 | Respuestas que necesitan criterio o tu voz bien cuidada |

Traducido a respuestas de tu bot (cálculo nuestro con esos precios, redondeado):

| Tipo de bot | Supuesto por respuesta | 1.000 respuestas con Haiku 5.5 | 1.000 respuestas con Sonnet 5.5 |
|---|---|---|---|
| Bot simple (instrucciones cortas + la pregunta) | 2.000 tokens de entrada + 300 de salida | **≈ USD 0,35** | **≈ USD 7** |
| Bot que lee mucho de tu cerebro en cada respuesta | 10.000 tokens de entrada + 300 de salida | **≈ USD 1,15** | **≈ USD 23** |

Lo que manda el precio es cuánto le das a leer en cada mensaje. Por eso conviene que el bot lea solo la parte del cerebro que necesita.

> **Tip:** si tu bot lee siempre el mismo texto largo, se puede usar **caché**: lo que Claude ya leyó cuesta mucho menos la segunda vez (en Sonnet 5.5, USD 0,10 por millón en vez de USD 2). Pedíselo a Claude Code cuando armes el bot.

> **Costo:** los números reales los ves en la Console, en **Usage**. Revisalos la primera semana y ajustá el límite.

## Cómo sé que funcionó
- **Billing** muestra saldo, **Monthly spend limit** tiene tu tope y la clave está en **API Keys**.
- La clave está en tu gestor y en ningún chat.

Para calcular lo tuyo, en Claude (sin pasarle ninguna clave):

```prompt
Voy a tener un bot que responde consultas de [TU NEGOCIO]. Recibo unas [CANTIDAD] consultas por mes. Cada respuesta lee unos [CANTIDAD] tokens de instrucciones y contexto y escribe unos 300. Calculá cuánto me costaría por mes con Claude Haiku 5.5 (USD 0,10 entrada / USD 0,50 salida por millón de tokens) y con Claude Sonnet 5.5 (USD 2 / USD 10). Mostrame la cuenta y recomendame un límite de gasto mensual.
```

**Tenés que ver:** dos montos mensuales y una recomendación de límite.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo **Buy credits** | Tu usuario no tiene rol Admin o Billing. Pedíselo a quien creó la organización. |
| La tarjeta es rechazada | Probá con otra tarjeta de crédito que acepte pagos en dólares. |
| El bot dice "credit balance is too low" o similar | Se terminó el saldo. Cargá más en **Billing**. |
| El bot dice que llegaste al límite de uso | Llegaste a tu **Monthly spend limit**. Subilo o esperá al mes siguiente. |
| Claude Code me ofrece usar una API key | Tenés `ANTHROPIC_API_KEY` en el entorno. Decile que no y sacá esa variable. |
| Perdí la clave | Creá otra en **API Keys** y borrá la vieja. |

## Para seguir solo
- Cuando tu bot ande bien, probá cambiar Sonnet por Haiku: si la calidad alcanza, el costo baja unas 20 veces.
- Si activás **auto-reload**, poné un monto de recarga chico y mantené el límite mensual.
- Una clave por bot o por flujo: así sabés qué gasta cada cosa y podés cortar uno sin tocar los demás.

## Fuentes
Consultadas el 18/11/2026.
- Precios de la API: https://platform.claude.com/docs/en/about-claude/pricing
- Comprar créditos, auto-reload, vencimiento y reembolsos: https://support.claude.com/en/articles/8977456
- Límites de gasto y de uso: https://platform.claude.com/docs/api/rate-limits
- Crear una API key (pasos en la doc de n8n): https://docs.n8n.io/integrations/builtin/credentials/anthropic/
- `ANTHROPIC_API_KEY` y Claude Code: https://code.claude.com/docs/en/setup
- Terceros (mínimo de USD 5, no confirmado): https://docs.mydbsync.com/cloud-workflow/create-your-workflow/actions/ai-agent-api-key-guides/claude-api-key
