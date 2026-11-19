---
titulo: Conectá cualquier herramienta (mapa y checklist de cuentas)
bloque: Setup
tiempo: 25 min
para: Todos
necesitas: s1-claude, s2-claude-code
resultado: Sabés la diferencia entre conector, MCP, API y skill, tenés un método para conectar cualquier herramienta a Claude y una checklist con todas las cuentas del taller.
---

Cada herramienta nueva dice "tenemos integración con IA". Esta página es el mapa: qué tipo de enchufe tiene cada una, en qué orden probar y dónde va cada clave.
Ejemplo: Celve quiere que Claude programe los posteos de la semana. Metricool tiene conector oficial: se conecta en dos minutos, sin claves.

## Antes de empezar
- [ ] Cuenta de Claude en plan **Pro** o superior ([Tu cuenta de Claude](#s1-claude)).
- [ ] La pestaña **Code** andando ([Claude Code](#s2-claude-code)).
- [ ] Leíste [Las piezas](#t2-piezas) (opcional, ayuda).
- [ ] Un gestor de contraseñas.

> **Datos:** conectar una herramienta le da a Claude **tu mismo acceso**. Conectá solo lo que usás y, cuando Claude pida permiso para **enviar, publicar, borrar, gastar o llamar**, leé antes de aceptar.

## Los enchufes, en una tabla
| | Qué es | Dónde se configura | Cómo entrás | Ejemplo |
|---|---|---|---|---|
| **Conector** | Un MCP ya armado en la app de Claude | **Customize › Connectors** | Tu usuario de esa herramienta | Google Drive, Canva, Metricool |
| **MCP remoto** | El enchufe estándar, una dirección web de la herramienta | Conector custom en la app, o pedido en la pestaña Code | Casi siempre iniciás sesión; a veces, una clave | Vapi, HeyGen, Supabase, Vercel |
| **MCP local** | Un programa chico que corre en tu compu | Pedido en la pestaña Code | Una clave (va en un `.env`) | MCP de la comunidad |
| **API** | La puerta "de programador". Se usa desde n8n, un bot o un script | `.env`, n8n, Cloudflare o Vercel | Una clave que **gasta tu plata o créditos** | API de Anthropic para tu bot |
| **Skill** | Una receta: le enseña a Claude **cómo** usar una herramienta | **Customize › Skills** o la carpeta de skills | No tiene clave propia | Skills de Higgsfield |

> **Tip:** el MCP le da a Claude **las manos**; la skill, **el método**. Lo que conectás en **Customize › Connectors** aparece solo en la pestaña Code (misma cuenta): por eso conviene empezar por ahí.

## Paso 1 · Seguí el método, en este orden
Apenas uno funciona, frenás.
1. **¿Tiene conector?** **Customize › Connectors** › buscá el nombre › **Connect**.
2. **¿Tiene MCP remoto oficial?** (una dirección tipo `https://mcp.[herramienta].com/mcp`). En la app: **Customize › Connectors** › **+ Add** › **Add custom connector** › nombre + dirección › **Add** › **Connect**.
3. **¿Solo MCP local o solo API?** Se lo pedís a Claude en la pestaña Code, con la clave en un `.env` (Paso 3).
4. **¿Nada de eso, pero está en n8n?** Usá **n8n como puente** ([n8n](#s6-n8n)).

> **Ojo:** desconfiá de MCP "para [HERRAMIENTA]" de terceros que piden tu clave. Preferí el oficial.

Para no buscar a mano, en la pestaña Code:

```prompt
Buscá en la documentación oficial de [HERRAMIENTA] si tiene conector para Claude o un servidor MCP oficial (no de terceros). Decime: 1) la dirección del MCP, 2) si se inicia sesión con el navegador o pide una clave, 3) qué permisos pide y qué podría cambiar o gastar. Pasame los links. No agregues nada hasta que te confirme.
```

**Tenés que ver:** la respuesta con link a la documentación oficial.

## Paso 2 · Conectá una herramienta
Elegí una que uses de verdad. Si tiene conector o MCP remoto, hacelo en **Customize › Connectors** (Paso 1). Si preferís que lo haga Claude, en la pestaña Code:

```prompt
Agregá el MCP de [HERRAMIENTA] con esta dirección [DIRECCIÓN-DEL-MCP] para todas mis carpetas y decime cuando esté. Después decime cómo inicio sesión.
```

Aprobá el permiso que te pide. Abrí una sesión nueva (**+ New**), escribí `/mcp` › elegí el servidor › **Authenticate** › aceptá en el navegador.

**Tenés que ver:** en `/mcp`, la herramienta conectada.

## Paso 3 · Si pide clave: va en el `.env`, nunca en el chat
Una API key o token es una contraseña: quien la tiene, usa tu cuenta (y a veces gasta tu plata). En la pestaña Code, en la carpeta del proyecto:

```prompt
Creá el archivo .env con la línea [NOMBRE_DE_LA_CLAVE]= vacía, asegurate de que .env esté en el .gitignore y abrímelo en el editor de texto de mi compu. No me pidas la clave: la pego yo.
```

Pegá la clave después del `=`, guardá, cerrá y escribile **"listo"**.

| Dónde se usa | Dónde va la clave |
|---|---|
| Un proyecto, script o MCP local en tu compu | `.env` (como arriba) |
| n8n | **Credentials** de n8n ([n8n](#s6-n8n)) |
| Cloudflare / Vercel | Como secreto del proyecto ([Cuentas en la nube](#s5-cuentas-nube)) |

> **Ojo:** nunca en el chat, en el cerebro, en GitHub, en un mail ni en una captura. Y no pongas `ANTHROPIC_API_KEY` como variable general de tu compu ([API de Anthropic](#s9-api-anthropic)).

**Tenés que ver:** `.env` con tu clave pegada por vos, y listado en `.gitignore`.

## Paso 4 · Mirá y quitá conexiones
- **App:** **Customize › Connectors** › tocá uno para desconectarlo.
- **Pestaña Code:** `/mcp` muestra el estado de cada uno. Para sacar uno: "Sacá el MCP de [NOMBRE]".

> **Tip:** al agregar un MCP, decí si es **"para todas mis carpetas"** (herramientas tuyas: Canva, Vapi) o **"solo para esta carpeta"** (la base de Supabase de una app). Una vez por mes, sacá lo que no usaste.

**Tenés que ver:** la lista de lo conectado, en los dos lugares.

## Cómo sé que funcionó
En la pestaña Code:

```prompt
Hacé un inventario de mis conexiones: los conectores de mi cuenta de Claude y los MCP que tenés en esta carpeta. Para cada uno, en una línea: qué puede hacer y si puede enviar, publicar, gastar o borrar algo. No ejecutes ninguna acción.
```

**Tenés que ver:** la lista completa y cuáles pueden hacer cambios.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No está en el directorio de conectores | Buscá su MCP remoto (Paso 1) y agregalo como **Add custom connector**. |
| En el plan gratis no me deja otro conector custom | El plan Free permite uno solo. Pasate a Pro o quitá el que tenés. |
| `/mcp` muestra error o "needs authentication" | Elegilo › **Authenticate**. Si sigue, revisá la dirección en la documentación oficial. |
| Un conector de la app no aparece en Code | Misma cuenta en los dos, sesión nueva, y que no esté apagado en `/mcp`. |
| Pegué una clave en el chat o en GitHub | Borrala en la herramienta y creá otra. Borrar el mensaje no alcanza. |

## Checklist de cuentas del taller
**Obligatoria** = la hace todo el mundo a la mañana. El resto, **solo si elegiste ese desafío** (D1 a D7). Precios en USD por mes, nov 2026: detalle y links en [Stack y costos](#r-stack-y-costos).

| Cuenta | Para qué | ¿Cuándo? | Costo (nov 2026) | Cómo se conecta | Página |
|---|---|---|---|---|---|
| **Claude** | Todo el taller | **Obligatoria** | Pro 20 | Es la base | [Claude](#s1-claude) |
| **GitHub** | Guardar tu cerebro con historial | **Obligatoria** | Gratis | GitHub Desktop | [GitHub](#s4-github) |
| **Obsidian** | Ver y editar tu cerebro como cuaderno | Opcional | Gratis | No se conecta: abre la misma carpeta | [Obsidian](#s11-obsidian) |
| **Google** (Drive, Gmail, Calendar) | Archivos, mails y agenda | D1 · D6 (recomendada) | Gratis | Conector oficial | [Meta y Google](#s14-meta-y-google) |
| **Vercel** | Publicar tu web | D3 | Hobby 0 · Pro 20 | MCP remoto (pestaña Code) | [Nube](#s5-cuentas-nube) |
| **Supabase** | Base de datos de tus apps | D3 | Free 0 · Pro desde 25 | MCP remoto (pestaña Code) | [Nube](#s5-cuentas-nube) |
| **Cloudflare** | Webs y bots chicos | D2 · D3 | Free 0 · Workers Paid 5 | Claude lo maneja desde la pestaña Code | [Nube](#s5-cuentas-nube) |
| **Lovable** | Apps sin código | D3 | Free 0 · Pro 25 | Conector / MCP remoto | [Nube](#s5-cuentas-nube) |
| **n8n** | Automatizaciones (y puente) | D1 · D5 | Prueba 0 · Starter ≈ €20 | MCP de tu instancia | [n8n](#s6-n8n) |
| **Telegram** | Tu bot | D1 · D2 · D5 | Gratis | No se conecta: el bot usa la API | [Telegram](#s7-telegram) |
| **API de Anthropic** | Que tus bots usen Claude solos | D1 · D2 · D5 | Prepago por uso | Clave en n8n, Cloudflare o `.env` | [API de Anthropic](#s9-api-anthropic) |
| **Meta Business** | Página, Instagram y anuncios | D6 · D7 | Gratis (anuncios aparte) | MCP oficial de Meta Ads (beta) | [Meta y Google](#s14-meta-y-google) |
| **Higgsfield** | Imagen y video con IA | D4 (opcional) | Starter 15 · Plus 49 | Conector custom + skills | [Creativas](#s12-creativas) |
| **HeyGen** | Avatar que habla a cámara | D4 (opcional) | Free 0 · Creator 29 | MCP remoto oficial | [Creativas](#s12-creativas) |
| **ElevenLabs** | Voz | D4 (opcional) | Free 0 · Starter 6 | MCP remoto oficial | [Creativas](#s12-creativas) |
| **Canva** | Placas y diseños | D4 | Free 0 · Pro ≈ 18 (verificar) | Conector oficial | [Creativas](#s12-creativas) |
| **Metricool** | Programar y medir redes | D4 | Free 0 · Starter 25 | Conector (también plan gratis) | [Creativas](#s12-creativas) |
| **Vapi** | Agentes de voz por teléfono | D2 (extra) | Por uso (USD 5 de prueba) | MCP remoto oficial | [Vapi](#s13-vapi) |
| **Apify** | Datos de webs y redes (reseñas, competencia) | Opcional (D5, D6) | Free (USD 5/mes) · Starter 19 | MCP remoto oficial | [Apify](#s15-apify) |
| **Notion** | Notas de tu equipo, si ya lo usan | Opcional | Free 0 (verificar) | Conector oficial | abajo |

**Notion:** **Customize › Connectors** › **Notion** › **Connect**. Aparece solo en la pestaña Code.

## Para seguir solo
- Cada herramienta nueva, pasala por el método del Paso 1 antes de pagar una integración de terceros.
- Cuando repitas algo tres veces con un conector: "Convertí lo que acabamos de hacer en una skill llamada [NOMBRE]".
- Una vez por mes, corré el inventario del "Cómo sé que funcionó" y desconectá lo que no usaste.

## Fuentes
Consultadas el 18/11/2026.
- MCP en Claude Code: https://code.claude.com/docs/en/mcp · pestaña Code: https://code.claude.com/docs/en/desktop
- Conectores y conectores custom: https://claude.com/docs/connectors/directory · https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp
- Resto de herramientas: ver Fuentes de cada página enlazada.
