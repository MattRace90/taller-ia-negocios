---
titulo: Skills y repos de otros (buscá, revisá, instalá)
bloque: Referencia
tiempo: 10 min por skill
para: Todos
necesitas: s2-claude-code
resultado: Sabés dónde buscar skills que armó otra gente, cómo revisarlas antes de instalarlas y cómo sumarlas pidiéndoselo a Claude en la pestaña Code.
---

No tenés que inventar todo vos. Mucha gente publica sus **skills** (recetas para Claude) y herramientas en GitHub, gratis. Si alguien ya resolvió lo que necesitás, lo bajás, lo revisás y lo adaptás a tu negocio.
Una skill es una carpeta con un archivo `SKILL.md` adentro. Las del taller están en el [Kit](#r-kit). Todo lo de esta página se hace en la **pestaña Code** de la app de Claude: vos pedís, Claude corre los comandos.

## Dónde buscar
| Dónde | Qué hay |
|---|---|
| [github.com/anthropics/skills](https://github.com/anthropics/skills) | Las skills oficiales de Anthropic: documentos, planillas, presentaciones, diseño. |
| [skills.sh](https://skills.sh) | Un directorio de skills de la comunidad, con el comando para instalar cada una. |
| [GitHub](https://github.com/search?q=SKILL.md&type=code) | Buscá `SKILL.md` + un tema (por ejemplo "SKILL.md video" o "SKILL.md ventas"). |
| `/plugin` en la pestaña Code | Plugins: paquetes de skills, comandos y agentes listos. |

> **Ojo:** `/plugin` puede variar según la versión de la app. Si no aparece, usá las otras fuentes de la tabla.

También le podés pedir a Claude, en la pestaña Code, que busque por vos:

```prompt
Buscá en GitHub skills para Claude Code que sirvan para [LO QUE NECESITÁS, por ejemplo editar videos verticales]. Mostrame las 3 mejores con: qué hacen, quién las publicó, cuántas estrellas tienen, la licencia y si instalan programas. No instales nada todavía.
```

## Antes de instalar: revisala (2 minutos)
Una skill le da instrucciones a Claude y a veces trae programas. Instalá solo lo que entendés.
- [ ] **¿Quién la publicó?** Preferí empresas conocidas o repos con muchas estrellas y actividad reciente.
- [ ] **¿Qué licencia tiene?** Si no dice, preguntá antes de usarla para algo comercial.
- [ ] **¿Qué hace por dentro?** Pedile a Claude que la lea antes:

```prompt
Leé el repo [PEGÁ EL LINK DE GITHUB] sin instalar nada. Explicame en simple qué hace, qué programas instala, a qué páginas se conecta y si pide claves o permisos especiales. Decime si ves algo raro.
```

> **Ojo:** nunca pegues claves ni contraseñas para "que ande" una skill de un desconocido. Si te pide algo así, no la instales.

## Cómo se instala
En la app de Claude, abrí la **pestaña Code**, elegí una carpeta (sirve la de tu cerebro) y pegá:

```prompt
Instalá como skill personal la skill del repo [PEGÁ EL LINK DE GITHUB]. Si skills.sh muestra un comando "npx skills add" para esa skill, corrélo vos; si no, copiá su carpeta (la que tiene el SKILL.md) a la carpeta de skills de mi usuario. Si necesita instalar programas, primero decime cuáles y esperá mi OK. Al final, decime la ruta donde quedó.
```

Claude te va a pedir permiso para correr comandos o crear archivos: leé qué va a hacer y tocá **Permitir**. Después abrí una sesión nueva en la pestaña Code y escribí `/`.

**Tenés que ver:** la skill nueva en la lista al escribir `/`.

## Dos ejemplos para probar

### Animaciones para tus videos
[github.com/remonkevin99-collab/animaciones](https://github.com/remonkevin99-collab/animaciones): 30 estilos de animación en código para Claude Code (holograma, plastilina, pixel art, cómic, grafiti y más), gratis y en español. Sirve para animar una escena de tu negocio y sumarla a un reel.
- Necesita **Node.js** ([S3](#s3-herramientas-base)) y usa **Remotion** (gratis hasta 3 personas en la empresa; si son más, revisá la licencia de Remotion).
- **Guía paso a paso para instalarlas y pedirlas con un comando:** [20 estilos de animación para tus videos (Notion)](https://vivid-armadillo-c06.notion.site/20-estilos-de-animaci-n-para-tus-v-deos-se-instalan-una-vez-y-se-piden-con-un-comando-41242dad0d3881b3b9a8d83cfc972946).
- También está en el plan B del [Kit](#r-kit).

```prompt
Instalá como skill la carpeta del repo https://github.com/remonkevin99-collab/animaciones y después mostrame los estilos que tiene. Con el estilo [ESTILO], armá una animación de 10 segundos de [UNA ESCENA DE TU NEGOCIO] en formato vertical 9:16.
```

### Que Claude use las apps de tu compu
[github.com/vercel-labs/agent-desktop](https://github.com/vercel-labs/agent-desktop) (Vercel Labs): le da a Claude la posibilidad de **ver y usar programas de tu compu** (Finder, el Explorador de Windows, otras apps de escritorio) leyendo sus botones, sin capturas de pantalla. Funciona en Mac, Windows y Linux.

```prompt
Instalá agent-desktop: corré "npm install -g agent-desktop" y después "npx skills add https://github.com/vercel-labs/agent-desktop --skill agent-desktop". Si me falta Node.js, avisame antes. Al final, decime si quedó funcionando.
```

En Mac, la primera vez te pide permiso de **Accesibilidad**. Pedile a Claude: "Corré agent-desktop permissions --guide y explicame en simple qué tengo que tocar". El permiso lo das vos en la configuración de la Mac.

> **Datos:** esta herramienta puede leer lo que hay en tus ventanas. Usala con las apps que querés que Claude toque y cerrá lo privado (banco, mails personales) antes de pedirle algo.

> **Tip:** es avanzado. Probalo primero con algo inofensivo, por ejemplo: "Abrí el Finder y decime qué carpetas hay en Descargas".

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| La skill no aparece al escribir `/` | Abrí una sesión nueva. Si sigue igual: "Fijate si mi skill [NOMBRE] quedó en la carpeta de skills de mi usuario y no anidada dos veces". |
| El comando `npx` da error | Te falta Node.js: instalalo con doble clic desde [Herramientas base](#s3-herramientas-base) y pedile a Claude que lo intente de nuevo (en Windows, Claude sabe usar `npx.cmd` si hace falta). |
| La skill hace algo que no esperabas | Pedile: "Borrá la skill [NOMBRE] de mi carpeta de skills". Después abrí una sesión nueva. |

## Para seguir solo
- Cuando una skill de otro te sirva, pedile a Claude que la adapte a tu negocio y guardá tu versión en el repo de tu cerebro.
- Si armaste una skill que te sirve, subila a GitHub para tu equipo.
- Las skills del taller y las de la agencia están en el [Kit](#r-kit) y en [Qué tiene cada descarga](#r-descargas).
