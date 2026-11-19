---
titulo: "Apify, datos de la web para tu negocio (opcional)"
bloque: Setup
tiempo: 15 min
para: Opcional (útil para D4, D5 y D6)
necesitas: s1-claude
resultado: Cuenta de Apify creada y conectada a Claude, y tu primer informe de reseñas de un competidor.
---

Apify junta **datos públicos** de la web: reseñas de Google Maps, posteos de Instagram de la competencia, precios, anuncios activos. Con Apify conectado, Claude los busca y te los resume.
Lo usamos en la agencia para encontrar dolores reales de clientes y analizar competidores. **Es opcional.**

> **Costo:** **Free** trae USD 5 de uso por mes; cuando se acaban, se frena hasta el mes siguiente (no te cobra de más). **Starter** USD 19/mes ([precios](https://apify.com/pricing), nov 2026).

## Antes de empezar
- [ ] Tu cuenta de Claude funcionando ([S1](#s1-claude)).
- [ ] El nombre de 1 o 2 competidores (su Instagram o su ficha de Google Maps).

## Paso 1 · Creá tu cuenta
1. Entrá a [apify.com](https://apify.com) › **Sign up** (se puede con Google).
2. Confirmá tu mail.

**Tenés que ver:** el panel de Apify (**Console**) con tu nombre arriba.

## Paso 2 · Conectala a Claude
**Lo más simple:** en la app de Claude, **Customize › Connectors** › **+** › **Add custom connector** › **Name:** `Apify` › **URL:** `https://mcp.apify.com` › **Connect** › iniciá sesión en Apify. Aparece solo en la pestaña **Code** (misma cuenta).

Si preferís hacerlo desde la pestaña **Code**, pedíselo:

```prompt
Agregá el MCP de Apify con esta dirección: https://mcp.apify.com (para todas mis carpetas). Avisame cuando esté y después decime cómo inicio sesión.
```

**Tenés que ver:** Apify conectado en **Customize › Connectors**, o en la lista al escribir `/mcp` en la pestaña Code.

## Paso 3 · Tu primer informe
En la pestaña **Code** (o en un chat):

```prompt
Con Apify, buscá las últimas 20 reseñas públicas de Google Maps de [NOMBRE DEL COMPETIDOR, CIUDAD] y resumime:
1) los 5 dolores que más se repiten,
2) lo que más elogian,
3) una frase textual de ejemplo para cada punto.
No guardes nombres de personas. Antes de correr, decime cuánto va a costar y esperá mi OK.
```

**Tenés que ver:** el costo estimado antes de correr y después un resumen con dolores, elogios y frases reales.

Otras ideas: "traé los últimos 10 posteos de Instagram de [COMPETIDOR] y decime qué temas tienen más interacción", o "buscá sus anuncios activos en la Biblioteca de anuncios de Meta y agrupalos por ángulo". Pedile que guarde lo que salga en `negocio/competencia.md` de tu cerebro.

> **Datos:** solo datos públicos y agregados. No armes listas de personas (nombres, teléfonos, mails).

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude dice que no tiene Apify | Revisá **Customize › Connectors** o `/mcp`. Si dice "needs auth", iniciá sesión de nuevo. |
| "Not enough credits" | Se terminaron los USD 5 del mes. Esperá o pasá a Starter. |
| El resultado vino vacío | Usá el nombre exacto de la ficha, o pegá el link de la ficha o del perfil. |

## Para seguir solo
- Una vez por mes, pedile a Claude que actualice `negocio/competencia.md`.
- Combinalo con [Tareas programadas](#t4-tareas-programadas) para que el informe te llegue solo.
- Más ideas en [Conectar cualquier cosa](#s10-conectar-todo).
