---
titulo: Apify, datos de la web para tu negocio (opcional)
bloque: Setup
tiempo: 15 min
para: Opcional (útil para D4, D5 y D6)
necesitas: s1-claude
resultado: Cuenta de Apify creada y conectada a Claude, y tu primer informe de reseñas de un competidor.
---

Apify junta **datos públicos** de la web: reseñas de Google Maps, posteos de Instagram de la competencia, precios de una tienda, anuncios activos. Con Apify conectado, Claude los busca y te los resume, sin que copies nada a mano.
Es lo que usamos en la agencia para encontrar los dolores reales de los clientes y para el **análisis de competidores**. No es obligatoria: sumala si querés investigar a tu competencia.

> **Costo:** el plan **Free** trae USD 5 de uso por mes, que alcanzan para probar. Cuando se acaban, se frena hasta el mes siguiente: no te cobra de más. **Starter** cuesta USD 19 por mes ([precios](https://apify.com/pricing), nov 2026).

## Antes de empezar
- [ ] Tu cuenta de Claude funcionando ([S1](#s1-claude)).
- [ ] El nombre de 1 o 2 competidores (con su Instagram o su ficha de Google Maps).

## Paso 1 · Creá tu cuenta
1. Entrá a [apify.com](https://apify.com) y tocá **Sign up** (se puede con Google).
2. Confirmá tu mail.

**Tenés que ver:** el panel de Apify (**Console**) con tu nombre arriba.

## Paso 2 · Conectala a Claude
Elegí dónde la vas a usar. Podés hacer las dos.

**En la app de Claude (web o escritorio):**
1. **Customize › Connectors › Add custom connector**.
2. Nombre: `Apify`. URL: `https://mcp.apify.com`
3. Tocá **Connect** e iniciá sesión con tu cuenta de Apify.

**En Claude Code** (en la terminal, con Claude Code cerrado):

```bash
claude mcp add --transport http --scope user apify https://mcp.apify.com
```

Después abrí `claude`, escribí `/mcp`, elegí **apify** e iniciá sesión.

> **Ojo:** Apify publica la dirección del MCP, pero no este comando exacto: es la forma estándar de Claude Code. Si `/mcp` no muestra apify como conectado, pedí ayuda a la mesa.

**Tenés que ver:** en `/mcp` (o en **Connectors**), Apify como conectado.

## Paso 3 · Tu primer informe

```prompt
Con Apify, buscá las últimas 20 reseñas públicas de Google Maps de [NOMBRE DEL COMPETIDOR, CIUDAD] y resumime:
1) los 5 dolores que más se repiten,
2) lo que más elogian,
3) una frase textual de ejemplo para cada punto.
No guardes nombres de las personas. Antes de correr, decime cuánto va a costar aproximadamente y esperá mi OK.
```

**Tenés que ver:** un resumen con dolores, elogios y frases reales, y el costo estimado antes de correr.

## Otras ideas
- "Traé los últimos 10 posteos de Instagram de [COMPETIDOR] y decime qué formatos y temas tienen más interacción."
- "Buscá los anuncios activos de [COMPETIDOR] en la Biblioteca de anuncios de Meta y agrupalos por ángulo de venta."
- "Compará mis reseñas de Google con las de [COMPETIDOR]: ¿en qué nos eligen y en qué no?"

Guardá lo que salga en tu cerebro, en `negocio/competencia.md`.

> **Datos:** usá Apify solo para datos públicos y agregados. No armes listas de personas (nombres, teléfonos, mails) ni juntes datos personales de nadie.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude dice que no tiene Apify | Revisá `/mcp` (Claude Code) o **Connectors** (app). Si dice "needs auth", iniciá sesión de nuevo. |
| "Not enough credits" | Se terminaron los USD 5 del mes. Esperá al mes siguiente o pasá a Starter. |
| El resultado vino vacío | Probá con el nombre exacto de la ficha de Google Maps, o pegá el link de la ficha o del perfil. |

## Para seguir solo
- Una vez por mes, pedile a Claude que actualice `negocio/competencia.md` con reseñas y posteos nuevos.
- Combinalo con [Tareas programadas](#t4-tareas-programadas) para que el informe te llegue solo.
- Más ideas en [Conectar cualquier cosa](#s10-conectar-todo).
