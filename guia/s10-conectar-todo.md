---
titulo: Conectá cualquier herramienta (mapa y checklist de cuentas)
bloque: Setup
tiempo: 30 min
para: Todos
necesitas: s1-claude, s2-claude-code
resultado: Sabés la diferencia entre conector, MCP, API y skill, tenés un método para conectar cualquier herramienta a Claude y una checklist con todas las cuentas del taller.
---

Cada herramienta nueva que aparece dice "tenemos integración con IA". Esta página es el mapa para no perderte: qué tipo de enchufe tiene cada una, en qué orden probar y dónde va cada clave.
Ejemplo: Celve quiere que Claude programe los posteos de la semana. Metricool tiene conector oficial: se conecta en dos minutos, sin claves ni código.

## Antes de empezar
- [ ] Cuenta de Claude en plan **Pro** o superior ([Tu cuenta de Claude](#s1-claude)).
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] Leíste la parte teórica de [Las piezas](#t2-piezas) (opcional, pero ayuda).
- [ ] Un gestor de contraseñas (el del navegador, el del celular, 1Password, Bitwarden…).

> **Datos:** conectar una herramienta le da a Claude **el mismo acceso que tenés vos** en esa herramienta. Conectá solo lo que vas a usar y, cuando Claude pida permiso para **enviar, publicar, borrar, gastar o llamar**, leé antes de aceptar.

## Los 4 enchufes, en una tabla
| | Qué es | Dónde se configura | Cómo te identificás | Ejemplo del taller |
|---|---|---|---|---|
| **Conector** | Un MCP ya armado, listo para usar en la app de Claude | **Customize › Connectors** (claude.ai y app de escritorio) | Iniciás sesión con tu usuario de esa herramienta | Google Drive, Canva, Metricool |
| **MCP remoto** | El enchufe estándar, alojado por la empresa de la herramienta (una URL) | Como **conector custom** en la app o con `claude mcp add --transport http` en Claude Code | Casi siempre iniciás sesión (OAuth). A veces, con un token | Vapi, HeyGen, Supabase, Vercel |
| **MCP local** | Un programa chico que corre en tu compu y habla con la herramienta | `claude mcp add … -- npx …` en Claude Code | Una clave (API key) que va en la configuración | El MCP viejo de ElevenLabs, el MCP de n8n de la comunidad |
| **API** | La puerta "de programador" de la herramienta. Se usa desde código, n8n o un bot | Un archivo `.env`, n8n, Cloudflare o Vercel | Una API key que **gasta tu plata o tus créditos** | API de Anthropic para el bot de Telegram |
| **Skill** | Una receta escrita: le enseña a Claude **cómo** usar una herramienta | `~/.claude/skills/` o **Customize › Skills** | No tiene clave propia: usa el conector, el MCP o la API que haya | Skills de Higgsfield para generar video |

> **Tip:** el MCP le da a Claude **las manos** (puede tocar la herramienta). La skill le da **el método** (sabe qué hacer y en qué orden). Las mejores integraciones traen las dos.

Lo que conectás en **Customize › Connectors** con tu cuenta de Claude **también aparece en Claude Code** si iniciaste sesión con la misma cuenta. Por eso, cuando hay conector, conviene empezar por ahí.

## Paso 1 · Aprendé el método para conectar cualquier herramienta
Probá en este orden. Apenas uno funciona, frenás.

1. **¿Tiene conector en el directorio de Claude?** **Customize › Connectors** › buscá el nombre. Si aparece: **Connect**, iniciás sesión y listo.
2. **¿Tiene MCP remoto oficial?** Buscalo en la documentación de la herramienta ("MCP server"). Si tiene una URL tipo `https://mcp.[herramienta].com/mcp`:
   - En la app: **Customize › Connectors** › **+** › **Add custom connector** › nombre + URL › **Add** › **Connect**.
   - En Claude Code: `claude mcp add --transport http --scope user [NOMBRE] [URL]`.
3. **¿Tiene MCP local?** Solo en Claude Code. Pide una API key: seguí el Paso 4 para no dejarla expuesta.
4. **¿Solo tiene API?** Claude Code puede escribir un script chico que la use, con la clave en un `.env`. Después lo convertís en **skill** para repetirlo.
5. **¿No tiene nada de eso, pero está en n8n?** Usá **n8n como puente**: un flujo de n8n habla con la herramienta y Claude habla con n8n por su MCP ([n8n](#s6-n8n)).

> **Ojo:** desconfiá de MCP "para [HERRAMIENTA]" hechos por terceros que piden tu clave. Preferí siempre el oficial. Si usás uno de la comunidad, que sea de una fuente conocida y con poco acceso.

Para no buscar a mano, pedíselo a Claude Code:

```prompt
Buscá en la documentación oficial de [HERRAMIENTA] si tiene un conector para Claude o un servidor MCP oficial (no de terceros).
Decime: 1) la URL del MCP, 2) si se inicia sesión con el navegador (OAuth) o pide una clave, 3) el comando exacto `claude mcp add` con --scope user, 4) qué permisos pide y qué podría cambiar o gastar.
Pasame los links de donde lo sacaste. No agregues nada hasta que yo te confirme.
```

**Tenés que ver:** una respuesta con link a la documentación oficial y un comando para revisar antes de correrlo.

## Paso 2 · Conectá una herramienta con el método
Elegí una que uses de verdad (por ejemplo, Canva o Metricool) y seguí el orden del Paso 1.

Si es un MCP remoto, el comando lo corrés **vos, en una terminal** (no adentro de Claude Code; en Windows, PowerShell). Reemplazá `[NOMBRE]` por un nombre corto en minúsculas (por ejemplo `canva`) y `[URL-DEL-MCP]` por la dirección que encontraste en el Paso 1:

```bash
claude mcp add --transport http --scope user [NOMBRE] [URL-DEL-MCP]
```

Después abrí Claude Code y escribí `/mcp` › elegí el servidor › **Authenticate** › aceptá en el navegador.

**Tenés que ver:** en `/mcp`, la herramienta como conectada y su lista de herramientas.

## Paso 3 · Mirá y quitá conexiones
**En la app de Claude:** **Customize › Connectors**. Ahí ves todo lo conectado. Tocá uno para desconectarlo o cambiar sus permisos. Dentro de un chat, **+ › Connectors** prende o apaga cada uno solo para esa conversación.

**En Claude Code:**

```bash
claude mcp list
```

Lista todos tus MCP y si están conectados.

```bash
claude mcp remove [NOMBRE]
```

Lo quita. Adentro de Claude Code, `/mcp` muestra el estado de cada uno y te deja apagar en esa carpeta los conectores que vienen de la app.

> **Tip:** una vez por mes, abrí **Customize › Connectors** y `claude mcp list` y sacá lo que no usaste. Menos conexiones = menos riesgo y menos ruido para Claude.

**Tenés que ver:** la lista de lo que tenés conectado, en los dos lugares.

## Paso 4 · Guardá las claves donde corresponde
Cuando una herramienta no tiene inicio de sesión con el navegador, te da una **API key** o un **token**. Es una contraseña: quien la tiene, usa tu cuenta (y a veces gasta tu plata).

| Dónde se usa | Dónde va la clave |
|---|---|
| Un proyecto en tu compu (script, skill) | Archivo `.env` en la carpeta del proyecto, que figure en el `.gitignore` |
| Un MCP en Claude Code | Lo escribís **vos** en la terminal, en el comando `claude mcp add` (queda en la configuración de tu compu) |
| n8n | **Credentials** de n8n ([n8n](#s6-n8n)) |
| Cloudflare Workers | `npx wrangler secret put [NOMBRE]` ([Cuentas en la nube](#s5-cuentas-nube)) |
| Vercel | Proyecto › **Settings › Environment Variables** |

Nunca: en el chat con Claude, en el cerebro, en GitHub, en un mail, en una captura.

Pedile a Claude Code que te prepare el `.env` sin ver la clave:

```prompt
En esta carpeta creá un archivo .env con la línea [NOMBRE_DE_LA_CLAVE]= vacía, y asegurate de que .env esté en el .gitignore. No me pidas la clave: la pego yo a mano en el archivo.
```

Después abrí el `.env` vos y pegá la clave después del `=`. Cómo abrirlo (es un archivo oculto): [Datos y seguridad](#t6-datos-y-seguridad), "Cómo crear el `.env`".

> **Ojo:** no pongas `ANTHROPIC_API_KEY` como variable general de tu compu: Claude Code la usaría y te cobraría por API en vez de usar tu plan ([API de Anthropic](#s9-api-anthropic)).

**Tenés que ver:** `.env` creado, con tu clave pegada por vos, y listado en `.gitignore`.

## Paso 5 · Elegí el alcance: para vos o para el proyecto
Cuando agregás un MCP en Claude Code, decidís dónde vale:

| Alcance | Flag | Vale en | Se comparte |
|---|---|---|---|
| **Local** (el que viene por defecto) | `--scope local` o nada | Solo la carpeta donde lo agregaste | No |
| **User** | `--scope user` | Todas tus carpetas | No |
| **Project** | `--scope project` | Esa carpeta, para todo el equipo | Sí: queda en `.mcp.json` y viaja con GitHub |

Regla simple: herramientas tuyas (Canva, Higgsfield, Vapi) en **user**. Herramientas de un proyecto puntual (la base de Supabase de tu app) en **project**, sin claves adentro del `.mcp.json`.

**Tenés que ver:** sabés qué alcance usar antes de correr el próximo `claude mcp add`.

## Cómo sé que funcionó
En Claude Code:

```prompt
Hacé un inventario de mis conexiones: listá los conectores de mi cuenta de Claude y los MCP de Claude Code (con su alcance). Para cada uno decime en una línea qué puede hacer y si puede enviar, publicar, gastar o borrar algo. No ejecutes ninguna acción.
```

**Tenés que ver:** la lista completa y cuáles pueden hacer cambios. Si alguno no lo usás, quitalo (Paso 3).

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| La herramienta no está en el directorio de conectores | Seguí el método: buscá su MCP remoto y agregalo como **Add custom connector**. |
| En el plan gratis de Claude no me deja agregar otro conector custom | El plan Free permite uno solo. Pasate a Pro o quitá el que tenés. |
| `claude mcp add` dice que el nombre ya existe | Ya está agregado. Mirá con `claude mcp list`; si querés rehacerlo, `claude mcp remove [NOMBRE]` y repetí. |
| `/mcp` muestra el servidor con error o "needs authentication" | Elegilo › **Authenticate**. Si sigue, revisá la URL en la documentación oficial. |
| Pegué una clave en el chat o en GitHub | Andá a la herramienta, **borrá esa clave y creá una nueva**. Borrar el mensaje no alcanza. |
| Un conector de la app no aparece en Claude Code | Revisá que iniciaste sesión en Claude Code con la misma cuenta (`/login`) y que no esté apagado en `/mcp`. |

## Checklist de cuentas del taller
Revisala con tu equipo y anotá lo que ya tienen. **Obligatoria** = la hace todo el mundo a la mañana. El resto la hacés **solo si elegiste ese desafío** (D1 a D7), en el momento en que lo arrancás; si no, queda acá para después. Precios en USD por mes, sin impuestos, consultados en nov 2026: el detalle y los links están en [Stack y costos](#r-stack-y-costos).

| Cuenta | Para qué | ¿Cuándo la necesitás? | Costo (nov 2026) | Cómo se conecta a Claude | Página |
|---|---|---|---|---|---|
| **Claude** | Todo el taller | **Obligatoria** | Pro 20 | Es la base | [Claude](#s1-claude) |
| **GitHub** | Guardar tu cerebro con historial | **Obligatoria** | Gratis | GitHub Desktop; MCP opcional con token | [GitHub](#s4-github) |
| **Obsidian** | Leer y editar tu cerebro | **Obligatoria** | Gratis (Sync 5) | No se conecta: Claude escribe los `.md` y Obsidian los muestra | [Obsidian](#s11-obsidian) |
| **Google** (Drive, Gmail, Calendar) | Archivos, mails y agenda | D1 · D6 (recomendada para todos) | Gratis | Conector oficial en **Customize › Connectors** | [Meta y Google](#s14-meta-y-google) |
| **Vercel** | Publicar tu web | D3 | Hobby 0 (no comercial) · Pro 20 | MCP remoto en Claude Code | [Nube](#s5-cuentas-nube) |
| **Supabase** | Base de datos de tus apps | D3 | Free 0 · Pro desde 25 | MCP remoto en Claude Code | [Nube](#s5-cuentas-nube) |
| **Cloudflare** | Webs y bots chicos | D2 · D3 | Free 0 · Workers Paid 5 | `wrangler` en la terminal; MCP remoto opcional | [Nube](#s5-cuentas-nube) |
| **Lovable** | Apps sin código | D3 | Free 0 (30 créditos/mes) · Pro 25 | Conector / MCP remoto | [Nube](#s5-cuentas-nube) |
| **n8n** | Automatizaciones (y puente para lo que no tiene MCP) | D1 · D5 | Prueba 0 · Starter ≈ €20 | MCP de tu instancia | [n8n](#s6-n8n) |
| **Telegram** | Tu bot | D1 · D2 · D5 | Gratis | No se conecta a Claude: el bot usa la API vía n8n o Cloudflare | [Telegram](#s7-telegram) |
| **API de Anthropic** | Que tus bots usen Claude solos | D1 · D2 · D5 | Prepago por uso | API key en n8n, Cloudflare o `.env` | [API de Anthropic](#s9-api-anthropic) |
| **Meta Business** | Página, Instagram y anuncios | D6 · D7 | Gratis (los anuncios se pagan aparte) | MCP oficial de Meta Ads (beta) como conector custom | [Meta y Google](#s14-meta-y-google) |
| **Higgsfield** | Imagen y video con IA | D4 (opcional) | Starter 15 · Plus 49 (necesita plan pago) | Conector custom + CLI y skills en Claude Code | [Creativas](#s12-creativas) |
| **HeyGen** | Avatar que habla a cámara | D4 (opcional) | Free 0 (3 videos) · Creator 29 | MCP remoto oficial | [Creativas](#s12-creativas) |
| **ElevenLabs** | Voz (locución, clon de voz) | D4 (opcional) | Free 0 · Starter 6 | MCP remoto oficial | [Creativas](#s12-creativas) |
| **Canva** | Placas y diseños | D4 | Free 0 · Pro ≈ 18 (verificar) | Conector oficial | [Creativas](#s12-creativas) |
| **Metricool** | Programar y medir redes | D4 | Free 0 · Starter 25 | Conector / MCP remoto (también en el plan gratis) | [Creativas](#s12-creativas) |
| **Vapi** | Agentes de voz por teléfono | D2 (extra: voz) | Pago por uso (USD 5 de prueba) | MCP remoto oficial | [Vapi](#s13-vapi) |
| **Apify** | Sacar datos de webs y redes (reseñas, competencia) | Opcional (D5, D6) | Free (USD 5 de uso/mes) · Starter 19 | MCP remoto oficial | abajo |
| **Notion** | Notas y bases de tu equipo, si ya lo usan | Opcional | Free 0 (verificar planes) | Conector / MCP remoto oficial | abajo |

### Apify y Notion, en corto
**Apify** junta datos públicos de la web (reseñas de Google Maps, posteos de la competencia, precios). Es lo que usamos en la agencia para minar dolores de clientes.
- Cuenta: **[apify.com](https://apify.com)** › sign up. El plan **Free** trae USD 5 de uso por mes; cuando se acaba, se frena hasta el mes siguiente ([precios](https://apify.com/pricing)).
- Conexión: MCP remoto `https://mcp.apify.com` con inicio de sesión. En la app, **Add custom connector**; en Claude Code:

```bash
claude mcp add --transport http --scope user apify https://mcp.apify.com
```

> **Ojo:** la documentación de Apify da la URL y recomienda su plugin para Claude Code, pero no publica este comando exacto: es la forma estándar de `claude mcp add`. Verificalo con `/mcp`.

**Notion**: si tu equipo ya trabaja en Notion, conectalo para que Claude lea y escriba páginas. **Customize › Connectors** › **Notion** › **Connect**. En Claude Code:

```bash
claude mcp add --transport http --scope user notion https://mcp.notion.com/mcp
```

Prompt de prueba:

```prompt
Con Apify, buscá las últimas 20 reseñas públicas de Google Maps de [UN COMPETIDOR] y resumime los 5 dolores que más se repiten. No guardes nombres de las personas. Antes de correr, decime cuánto va a costar aproximadamente.
```

## Para seguir solo
- Cada vez que adoptes una herramienta nueva, pasala por el método del Paso 1 antes de pagar una integración de terceros.
- Cuando repitas algo tres veces con un conector, pedile a Claude que lo convierta en una **skill** ("Convertí lo que acabamos de hacer en una skill llamada [NOMBRE]").
- Revisá cada mes el inventario del "Cómo sé que funcionó" y desconectá lo que no usaste.

## Fuentes
Consultadas el 18/11/2026.
- MCP en Claude Code (alcances, `claude mcp list/remove`, `/mcp`, variables): https://code.claude.com/docs/en/mcp
- Directorio de conectores: https://claude.com/docs/connectors/directory
- Conectores custom: https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp
- Apify MCP y precios: https://docs.apify.com/platform/integrations/mcp · https://apify.com/pricing
- Notion MCP: https://code.claude.com/docs/en/mcp (ejemplo oficial con Notion)
- Resto de herramientas: ver Fuentes de cada página enlazada en la checklist.
