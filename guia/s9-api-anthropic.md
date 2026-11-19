---
titulo: API de Anthropic
bloque: Setup
tiempo: 15 min
para: Según tu desafío (bots y flujos de n8n)
necesitas: s1-claude
resultado: Cuenta en la Console de Anthropic con crédito cargado, límite de gasto mensual y una API key guardada en un lugar seguro.
---

Tu plan Pro sirve para que **vos** uses Claude. Cuando un **bot** o un flujo de n8n usa Claude solo, sin vos adelante, paga por uso con la **API**: una cuenta aparte, con su propio crédito.
Ejemplo: el bot de Viajes TDH que responde "¿qué incluye el paquete a Bariloche?" llama a Claude por la API. Cada respuesta cuesta fracciones de centavo.

> **Costo:** el plan Pro de [claude.ai](https://claude.ai) y la API se pagan **por separado**. El Pro **no** incluye crédito de API.

## Antes de empezar
- [ ] Una tarjeta de crédito que acepte pagos en dólares.
- [ ] Un gestor de contraseñas (el del navegador, el del celular, 1Password, Bitwarden…).

## Paso 1 · Creá tu cuenta en la Console
1. Entrá a **[platform.claude.com](https://platform.claude.com)** y registrate (podés usar el mismo mail que en claude.ai).
2. Completá el nombre de tu empresa.

**Tenés que ver:** el panel de la Claude Console.

## Paso 2 · Cargá crédito
La API es **prepaga**: si se termina el saldo, tu bot deja de responder.
1. **Settings › Billing** ([link directo](https://platform.claude.com/settings/billing)) › **Buy credits** › poné el monto y confirmá. Para el taller alcanza con poco.

> **Costo:** el monto mínimo **no está confirmado al 18/11/2026** (lo ves en **Buy credits**). Los créditos **vencen al año** y **no se reembolsan**. No actives **auto-reload** hoy.

> **Ojo:** muchas tarjetas de débito lo rechazan y el banco puede pedir aprobación. Si no pasa, avisá en la mesa de ayuda; mientras, podés armar el prompt de tu bot.

**Tenés que ver:** en **Billing**, tu **Credit balance** con lo que cargaste.

## Paso 3 · Poné un límite de gasto mensual
1. Entrá a **[platform.claude.com/settings/spend-limits](https://platform.claude.com/settings/spend-limits)**.
2. **Monthly spend limit** › **Set limit** (o **Adjust limit**) › por ejemplo **USD 10**.

Es tu red de seguridad si un bot queda en un bucle.

**Tenés que ver:** **Monthly spend limit** con tu tope.

## Paso 4 · Creá una API key y guardala en tu gestor
1. **Settings › API Keys** › **+ Create Key**.
2. Nombre según dónde la vas a usar, por ejemplo `n8n-bot-telegram`. Una clave por uso.
3. **Copy Key** y guardala ya en tu gestor de contraseñas (`Anthropic API - [NOMBRE]`). **Se muestra una sola vez.**

**Tenés que ver:** la clave en la lista de **API Keys** y en tu gestor.

## Paso 5 · Ponela solo donde se usa (nunca en el chat)
La API key es una contraseña que **gasta tu plata**. Nunca la pegues en el chat con Claude, en el cerebro, en GitHub, en un mail ni en una captura.

| Dónde corre tu bot | Dónde va la clave |
|---|---|
| n8n | **Create › Credential › Anthropic** › **API Key** ([n8n](#s6-n8n)) |
| Vercel | Proyecto › **Settings › Environment Variables** |
| Cloudflare o un proyecto en tu compu | En un archivo `.env` que pegás vos (abajo) |

Para el `.env`, abrí la pestaña **Code** en la carpeta del proyecto y pedí:

```prompt
Creá el archivo .env con la línea ANTHROPIC_API_KEY= vacía, asegurate de que .env esté en el .gitignore y abrímelo en el editor de texto de mi compu. No me pidas la clave: la pego yo.
```

Pegá la clave después del `=` (sin espacios ni comillas), guardá (**Cmd + S** / **Ctrl + S**), cerrá el archivo y escribile a Claude **"listo"**.

> **Tip:** para Cloudflare, después pedí: "Subí a Cloudflare como secreto la ANTHROPIC_API_KEY que está en el .env, sin mostrarla en el chat". Más en [Cuentas en la nube](#s5-cuentas-nube).

> **Ojo:** **no** la cargues como variable general de tu compu con el nombre `ANTHROPIC_API_KEY`: Claude Code la usaría y te cobraría por API en vez de usar tu plan Pro.

**Tenés que ver:** la clave en tu gestor y en un solo lugar más. En el chat, nada.

## Cuánto cuesta
Precios oficiales por millón de **tokens** (pedazos de palabra; se cobra lo que lee y lo que escribe):

| Modelo | Entrada | Salida | 1.000 respuestas de un bot simple* |
|---|---|---|---|
| **Haiku 5.5** | USD 0,10 | USD 0,50 | **≈ USD 0,35** |
| **Sonnet 5.5** | USD 2 | USD 10 | **≈ USD 7** |

*Cálculo nuestro: 2.000 tokens de entrada + 300 de salida por respuesta. Si el bot lee mucho de tu cerebro en cada mensaje, sube: que lea solo lo que necesita.

> **Costo:** los números reales los ves en la Console, en **Usage**. Revisalos la primera semana.

## Cómo sé que funcionó
**Billing** muestra saldo, **Monthly spend limit** tiene tu tope y la clave está en **API Keys** y en tu gestor, en ningún chat. Para calcular lo tuyo (sin pasarle ninguna clave):

```prompt
Voy a tener un bot que responde consultas de [TU NEGOCIO], unas [CANTIDAD] por mes. Cada respuesta lee unos [CANTIDAD] tokens y escribe unos 300. Calculá cuánto me costaría por mes con Claude Haiku 5.5 (USD 0,10 entrada / 0,50 salida por millón) y con Sonnet 5.5 (USD 2 / 10). Mostrame la cuenta y recomendame un límite de gasto mensual.
```

**Tenés que ver:** dos montos mensuales y una recomendación de límite.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo **Buy credits** | Tu usuario no es Admin o Billing. Pedíselo a quien creó la organización. |
| La tarjeta es rechazada | Probá con otra de crédito que acepte dólares. |
| El bot dice "credit balance is too low" | Se terminó el saldo. Cargá más en **Billing**. |
| El bot dice que llegaste al límite | Subí el **Monthly spend limit** o esperá al mes siguiente. |
| Pegué la clave en el chat o en GitHub | Borrala en **API Keys** y creá otra. Borrar el mensaje no alcanza. |

## Para seguir solo
- Cuando el bot ande bien, probá Haiku en vez de Sonnet: si la calidad alcanza, cuesta unas 20 veces menos.
- Si el bot lee siempre el mismo texto largo, pedile a Claude que use **caché**: lo ya leído cuesta mucho menos.
- Una clave por bot: sabés qué gasta cada uno y cortás uno sin tocar los demás.

## Fuentes
Consultadas el 18/11/2026.
- Precios: https://platform.claude.com/docs/en/about-claude/pricing
- Créditos, auto-reload, vencimiento: https://support.claude.com/en/articles/8977456
- Límites de gasto: https://platform.claude.com/docs/api/rate-limits
- `ANTHROPIC_API_KEY` y Claude Code: https://code.claude.com/docs/en/setup
