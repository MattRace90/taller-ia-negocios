---
titulo: Stack y costos
bloque: Referencia
tiempo: 15 min de lectura
para: Todos (dueños y quien maneje la tarjeta de la empresa)
necesitas: nada
resultado: Sabés qué herramienta sirve para qué, cuánto cuesta por mes y qué necesita tu empresa según los desafíos que eligió.
---

Esta página es para decidir con números. Casi todo lo que usamos hoy tiene plan gratis; el único pago obligatorio para seguir después del taller es **Claude Pro**.
Ejemplo: una empresa que se lleva un bot de Telegram y una web puede arrancar con unos **USD 25 por mes** y crecer solo cuando lo justifique.

> **Costo:** todos los precios están en **dólares por mes, sin impuestos**, consultados el 18/11/2026. Cambian seguido: antes de pagar, mirá la página de precios de cada servicio (links en **Fuentes**). En Argentina, el monto final en pesos va a ser más alto (ver **Trampas de facturación**).

## Antes de empezar
- [ ] Mirá en [Inicio](#inicio) qué desafíos te sugerimos y cuáles elegiste. Eso es "tu ruta": las herramientas que vas a usar.
- [ ] Tené a mano cuántas personas trabajan en tu empresa (cambia el precio de algunas licencias).

## Las herramientas
| Herramienta | Para qué | El plan gratis alcanza para | Plan pago | USD/mes |
|---|---|---|---|---|
| **Claude** | Todo el taller: chat, Cowork, Claude Code, conectores | Chatear con uso limitado. **No** incluye Claude Code ni Cowork | **Pro 20** (17 con pago anual) · Max 100 · Ultra 200 | **20** |
| **API de Anthropic** | Que tus bots y flujos usen Claude solos, sin vos (se paga aparte del plan) | Crédito de prueba para cuentas nuevas (monto no publicado) | Prepago por uso. Haiku 5.5: 0,10 / 0,50 por millón de tokens. Sonnet 5.5: 2 / 10 | **≈ 5 a 10** (estimación para bots chicos) |
| **GitHub** | Guardar tu cerebro con historial | Repositorios **privados ilimitados** | Team 4 por usuario | **0** |
| **Node, Git, Python, ffmpeg, Homebrew** | Lo que Claude Code usa por detrás | Todo | — | **0** |
| **Obsidian** | Leer y editar tu cerebro | Todo, también uso comercial | Sync 5 (4 con pago anual) | **0** |
| **Vercel** | Publicar tu web | Pruebas y proyectos **personales o no comerciales** | **Pro 20** (necesario para la web de una empresa) | **0 o 20** |
| **Cloudflare Workers** | Publicar webs y bots chicos | 100.000 requests (pedidos o visitas) por día | Paid 5 | **0** |
| **Supabase** | Base de datos de tus apps | 2 proyectos, 500 MB; se pausa a los 7 días sin uso | Pro desde 25 | **0** |
| **n8n** | Automatizaciones | Prueba de Cloud sin tarjeta (1.000 ejecuciones) o self-hosted gratis | Starter **€20** · Pro **€50** (precios con pago anual) | **0 o ≈ 24** (conversión no confirmada) |
| **Lovable** | Apps sin código | 5 créditos por día, tope de 30 por mes | Pro 25 (21 con pago anual), 100 créditos | **0 o 25** |
| **Telegram** | Tu bot | Todo | — | **0** |
| **Metricool** | Programar y medir redes | 1 marca, 20 posts por mes, sin LinkedIn ni X. Incluye el MCP | Starter desde 25 (20 con pago anual) | **0 o 25** |
| **Meta Ads MCP** | Que Claude lea y gestione tus campañas | Gratis durante la beta (dato de terceros) | — | **0** |
| **Remotion** | Editor de video programático | Empresas de **hasta 3 personas** | Creators 25 por asiento | **0 o 25** |
| **Higgsfield** | Imagen y video con IA | No trae créditos (no sirve para producir). El conector con Claude **pide plan pago** | Starter 15 · Plus 49 · Ultra 129 | **0 a 49** |
| **HeyGen** | Avatar que habla a cámara | 3 videos por mes de hasta 1 minuto, con marca de agua. El MCP está en todos los planes | Creator 29 (24 con pago anual) · Pro 49 | **0 o 29** |
| **ElevenLabs** | Voz: locución y clon de voz | 10.000 créditos por mes, sin licencia comercial | Starter 6 (licencia comercial y clon instantáneo) · Creator 22 | **0 a 22** |
| **Canva** | Placas y diseños | Crear diseños; sin Brand Kit | Pro ≈ 18 (dato de terceros, sep 2026: verificar) | **0 o ≈ 18** |
| **Vapi** | Agentes de voz por teléfono | USD 5 de crédito de prueba y 1 número de EE. UU. solo para recibir | Por minuto: 0,05 de plataforma + modelo, voz y telefonía (≈ 0,10 a 0,30 en total, terceros). Core 29 | **variable** |
| **Apify** | Sacar datos de webs y redes (reseñas, competencia) | USD 5 de uso por mes | Starter 19 (17 con pago anual) | **0 o 19** |
| **Meta Business Suite** | Página, Instagram y cuenta publicitaria | Todo (los anuncios se pagan aparte) | — | **0** |
| **Google** (Drive, Gmail, Calendar) | Archivos, mails y agenda conectados a Claude | Los conectores no cuestan extra | Workspace, si tu empresa ya lo paga | **0** |
| **Notion** | Notas y bases del equipo, si ya lo usan | Plan gratis (verificar límites) | Verificar en [notion.com/pricing](https://notion.com/pricing) | **0** |
| **WhatsApp Cloud API** | Bots de WhatsApp oficiales | Los primeros 1.000 mensajes de servicio por número y por mes | Se paga **por mensaje** según tipo y país | **variable** |

> **Datos:** la tarifa por mensaje de WhatsApp para Argentina **no está confirmada al 18/11/2026** en la tabla oficial de Meta. Terceros hablan de unos USD 0,06 por mensaje de marketing y USD 0,03 por mensaje de utilidad o servicio.

## Tres escenarios
| Componente | Mínimo | Recomendado | Completo |
|---|---|---|---|
| Claude | Pro **20** | Pro **20** | Max **100** |
| API de Anthropic (estimación) | ~**5** | ~**10** | **0** extra (Max trae USD 100 de crédito de API por mes) |
| Web y bots | Cloudflare Free **0** | Vercel Pro **20** | Vercel Pro **20** + Cloudflare Paid **5** |
| Base de datos | Supabase Free **0** | Supabase Free **0** | Supabase Pro **25** |
| Automatizaciones | n8n self-hosted o prueba **0** | n8n Starter **≈ 24** | n8n Pro **≈ 58** |
| Redes | Metricool Free **0** | Metricool Starter **25** | Metricool Starter **25** |
| Apps sin código | — | — | Lovable Pro **25** |
| Imagen y video IA | — | — | Higgsfield Plus **49** |
| Video programático | Remotion gratis **0** | **0** | Remotion **25** (más de 3 personas) |
| Cerebro | Obsidian **0** | **0** | Obsidian Sync **5** |
| **Total aproximado** | **≈ USD 25** | **≈ USD 99** | **≈ USD 337** |

- **Mínimo:** Claude Code andando, un bot de Telegram con Claude y algo publicado. Con Claude Pro anual baja a unos USD 22.
- **Recomendado:** la empresa ya vende con esto. Web con licencia comercial, n8n en la nube sin mantener servidores y Metricool con LinkedIn.
- **Completo:** un equipo que produce contenido con IA y tiene apps propias.
- WhatsApp va aparte en los tres: se paga por mensaje.
- Los escenarios no incluyen HeyGen, ElevenLabs, Canva, Apify ni Vapi (el Completo ya suma Higgsfield). Si los usás, sumalos con la tabla que sigue.
- Los créditos de API del plan Max **no sirven** dentro de Claude Code ni de la app: solo para la API (bots y flujos).

### Extras: sumá si usás…
| Si querés… | Herramienta y plan | USD/mes |
|---|---|---|
| Videos con avatar | HeyGen Creator | **29** |
| Locuciones y tu voz clonada para publicar | ElevenLabs Starter (Creator para clon profesional) | **6 a 22** |
| Placas con tu Brand Kit | Canva Pro | **≈ 18** (verificar) |
| Imagen y video con IA desde Claude | Higgsfield Starter o Plus | **15 a 49** |
| Un agente que llame o atienda por teléfono | Vapi por uso (ejemplo: 300 minutos × ≈ 0,15) + número importado | **≈ 45** + el número |
| Datos de la competencia y reseñas | Apify Free o Starter | **0 a 19** |
| Fábrica de contenidos completa (Higgsfield Plus + HeyGen Creator + ElevenLabs Starter + Canva Pro) | — | **≈ 102** (≈ 53 si ya estás en el escenario Completo, que trae Higgsfield) |

Cómo se conecta cada una a Claude: [Conectá cualquier herramienta](#s10-conectar-todo), [Creativas](#s12-creativas) y [Vapi](#s13-vapi).

## Cuánto cuesta cada desafío
Estimación de lo que tendrías que pagar por mes para dejar andando lo que armaste. "Desde" es usando todo lo gratis; "hasta" suma los planes pagos que más probablemente vas a querer. A todo sumale Claude Pro (≈ 20), que es la base.
Sumá los desafíos que elegiste. Los que te sugerimos según tu empresa están en [Inicio](#inicio).

| Desafío | Herramientas | USD/mes extra |
|---|---|---|
| [D1 · Automatizá una tarea](#d1-automatiza) | Telegram, n8n, API de Anthropic, conector de Google Drive | **desde 5** (API prepaga) **hasta ≈ 29** (n8n Starter) |
| [D2 · Un agente que responde](#d2-agente) | Telegram, Cloudflare Workers, API de Anthropic | **≈ 5** (Workers Free alcanza; API prepaga) |
| [D3 · Tu web o tu app](#d3-web-app) | GitHub, Vercel o Cloudflare, Supabase, Lovable | **desde 0 hasta ≈ 45** (Vercel Pro 20 si es web comercial, Lovable Pro 25) |
| [D4 · Tu fábrica de contenido](#d4-contenido) | Fábrica de contenidos, Node + ffmpeg, Canva, Metricool, Higgsfield o HeyGen (opcional) | **desde 0 hasta ≈ 40** (Metricool 25, Higgsfield 15) · +25 de Remotion si son más de 3 personas |
| [D5 · Vendé más](#d5-vender) | n8n o Claude Code, conectores de Google, tu CRM | **desde 0 hasta ≈ 24** (n8n Starter) |
| [D6 · Medí y decidí](#d6-medir) | Meta Ads MCP, tareas programadas, conectores de Google | **0** (los anuncios se pagan aparte) |
| [D7 · Tu bot de WhatsApp](#d7-whatsapp) | Ver [opciones](#w1-opciones) | Según el camino: costo por mensaje de Meta + la plataforma |

Cómo se suman los "hasta": n8n Starter ≈ 24, Vercel Pro 20 (si la web queda en Vercel y no en Cloudflare), Lovable Pro 25 (si los 30 créditos gratis no alcanzan) y Metricool Starter 25 (si necesitás más de 20 posts por mes o LinkedIn). Si sumás WhatsApp, agregá el costo por mensaje.

## Trampas de facturación
- **Dólar tarjeta e impuestos.** Las compras en dólares con tarjeta argentina suman percepciones e impuestos sobre servicios digitales. El precio de esta página es antes de eso: el resumen en pesos va a venir más alto. Consultá con tu contador cómo te impacta. Algunas tarjetas de débito no funcionan para pagos en dólares.
- **Anual vs. mensual.** El precio "por mes con pago anual" es más barato, pero pagás los 12 meses juntos y te comprometés por un año. Ojo con n8n: su página **solo muestra precios con pago anual**. Probá un mes en mensual antes de pasar a anual.
- **Pruebas gratis.** Anotá en tu calendario cuándo vence cada prueba (n8n Cloud, Vercel Pro). Si no te sirvió, cancelala antes.
- **Créditos que vencen.** Los de la API de Anthropic vencen al año y no se devuelven. Los de Lovable pasan al mes siguiente solo mientras sigas suscripto. Los packs de Higgsfield, según terceros, vencen a los 90 días.
- **Recargas automáticas.** El **auto-reload** de la API de Anthropic puede cobrarte en el momento en que lo activás. Usalo con un límite de gasto mensual puesto.
- **Avisos de gasto.** En Vercel Pro el aviso de gasto viene en USD 200 por defecto: bajalo. En la API de Anthropic, poné un **Monthly spend limit** ([API de Anthropic](#s9-api-anthropic)).
- **Planes gratis con letra chica.** Vercel Hobby no permite uso comercial. Supabase Free pausa el proyecto a los 7 días sin uso. Remotion es gratis solo hasta 3 personas en la empresa, aunque lo use una sola.
- **Suscripción ≠ API.** Pagar Claude Pro no te da crédito para tus bots. La API se carga aparte.
- **Créditos que se van por Claude.** Higgsfield, HeyGen y ElevenLabs descuentan créditos por cada cosa que Claude genera, igual que en su web. En Higgsfield, lo "ilimitado" de la web **no aplica** por el conector. Pedile a Claude que te diga el costo y espere tu OK antes de generar.
- **Vapi cobra por minuto y por partes.** La tarifa de USD 0,05 es solo la plataforma: el modelo, la voz y la telefonía se suman. Mirá el costo de cada llamada de prueba antes de llamar a una lista.
- **Licencia comercial.** El plan gratis de ElevenLabs no figura con licencia comercial: para publicar o usar en anuncios, Starter.
- **WhatsApp cobra por mensaje.** Desde el 1/10/2026, los mensajes de servicio se cobran después de los primeros 1.000 por número y por mes.

## Para seguir solo
- Una vez por mes, revisá los resúmenes de cada servicio y la página **Usage** de la Console de Anthropic.
- Antes de pasar algo a pago, pedile a Claude: "Con este uso real [PEGÁ LOS NÚMEROS DE USO, SIN DATOS DE CLIENTES], ¿me conviene el plan gratis, el mensual o el anual?".
- Si en 60 días una herramienta paga no te ahorró tiempo o no te trajo ventas, cancelala.

## Fuentes
Todas consultadas el 18/11/2026. El relevamiento completo está en `investigacion/stack-y-costos.md`.

**Claude y API de Anthropic**
- https://claude.com/pricing
- https://support.claude.com/en/articles/8325606-what-is-the-pro-plan
- https://support.claude.com/en/articles/17154008-monthly-api-credits-for-max-ultra-and-team-plans
- https://platform.claude.com/docs/en/about-claude/pricing
- https://support.claude.com/en/articles/8977456
- https://platform.claude.com/docs/api/rate-limits

**Herramientas base y GitHub**
- https://github.com/pricing
- https://nodejs.org/en/download
- https://www.python.org/downloads/
- https://ffmpeg.org/download.html
- https://brew.sh/
- https://obsidian.md/pricing

**Web, datos y automatización**
- https://vercel.com/pricing · https://vercel.com/docs/plans/hobby · https://vercel.com/legal/terms
- https://developers.cloudflare.com/workers/platform/pricing/
- https://supabase.com/pricing · https://supabase.com/docs/guides/platform/free-project-pausing
- https://n8n.io/pricing/
- https://lovable.dev/pricing · https://docs.lovable.dev/introduction/subscription-plans
- Terceros (n8n en USD mensual): https://toolradar.com/tools/n8n/pricing

**Contenido y redes**
- https://core.telegram.org/bots/faq
- https://metricool.com/pricing/
- https://www.remotion.dev/docs/license/pricing
- https://higgsfield.ai/blog/higgsfield-pricing-explained
- Terceros (créditos de Higgsfield): https://www.heygen.com/blog/higgsfield-pricing

**Creativas, voz y datos**
- https://www.heygen.com/pricing · https://developers.heygen.com/mcp/overview
- https://elevenlabs.io/pricing
- Terceros (Canva Pro): https://stylefactoryproductions.com/blog/canva-pricing
- https://higgsfield.ai/creator-hub/help-center/integrations/how-do-i-connect-higgsfield-to-ai-agent
- https://vapi.ai/pricing · https://docs.vapi.ai/phone-calling
- Terceros (costo total de Vapi por minuto): https://www.activepieces.com/blog/vapi-pricing-2026-the-real-cost-per-minute
- https://apify.com/pricing

**Meta y WhatsApp**
- https://developers.facebook.com/docs/whatsapp/pricing
- https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-overview
- Terceros (tarifas para Argentina): https://srileo.com/tools/whatsapp-api-pricing-calculator/argentina/ · https://help.sleekflow.io/en_US/whatsapp/pricing
- Terceros (Meta Ads MCP gratis en beta): https://contextbolt.com/blog/meta-ads-mcp/
