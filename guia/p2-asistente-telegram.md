---
titulo: "Tu asistente en Telegram: propuestas y gastos"
bloque: Tutorial
tiempo: 60 a 90 min
para: Todos (sobre todo Manuel Martínez Oratoria, Viajes TDH, Celve y Denvet)
necesitas: p1-cerebro, s2-claude-code, s6-n8n, s7-telegram, s9-api-anthropic
resultado: Un bot de Telegram tuyo que con /propuesta te devuelve una propuesta con tu marca en PDF y con /gasto carga el comprobante en tu planilla.
---

Es la versión completa del [D1](#d1-automatiza): hoy hacé primero la MVP; esto es para si te sobra tiempo. Un solo bot, dos trabajos: con **/propuesta** le pasás lo que se habló en una llamada y te devuelve la propuesta con tu logo; con **/gasto** le mandás la foto del ticket y queda en tu planilla. Ejemplo: Manuel arma la propuesta In Company apenas corta con la empresa; Celve carga los comprobantes desde el celular.

> **Tip:** **n8n** une apps sin programar; cada automatización es un **workflow** y cada cajita, un **nodo**. Una **credencial** es la llave guardada en n8n para entrar a otra app. El **MCP** es el enchufe para que Claude maneje n8n ([Las piezas](#t2-piezas)).

## Antes de empezar
- [ ] Tu cerebro con `negocio/oferta-y-precios.md` y `marca/voz.md` ([Armá el cerebro](#p1-cerebro)).
- [ ] La app de escritorio de Claude con la pestaña **Code** ([S2 · Claude Code en la pestaña Code](#s2-claude-code)).
- [ ] Cuenta de n8n Cloud con el MCP conectado a Claude ([n8n](#s6-n8n), Pasos 1 y 6).
- [ ] Un bot de Telegram: su **token** y tu **chat ID** ([Telegram](#s7-telegram)).
- [ ] Clave de API de Anthropic con crédito ([API de Anthropic](#s9-api-anthropic)).
- [ ] Una cuenta de Google (Drive, Docs y Sheets).

> **Costo:** n8n Cloud desde €20/mes con pago anual, con prueba gratis ([precios](https://n8n.io/pricing/), nov 2026). Cada propuesta o gasto, centavos de API. Detalle en [Stack y costos](#r-stack-y-costos).

> **Datos:** no le mandes DNI, tarjetas ni datos de salud. Para probar, usá los ejemplos inventados de esta página.

## Paso 1 · Prepará Google
Creá tres cosas y anotá el **ID** de cada una (el pedazo largo de la dirección entre `/d/` y `/edit`; en carpetas, lo que va después de `/folders/`):
1. Una planilla `Gastos [TU-EMPRESA]`, hoja `Gastos`, con estos títulos en la fila 1: `Fecha · Monto · Moneda · Categoría · Concepto · Proveedor · Origen · Cargado` (uno por columna).
2. Una carpeta de Drive `Propuestas`.
3. Un Google Docs `Plantilla propuesta` con tu logo, tus colores y este texto tal cual:

```text
{{TITULO}}
Fecha: {{FECHA}} · Para: {{CLIENTE}}
Contexto: {{CONTEXTO}}
El problema: {{PROBLEMA}}
Nuestra propuesta: {{SOLUCION}}
Alcance: {{ALCANCE}}
Inversión: {{INVERSION}}
Próximos pasos: {{PROXIMOS_PASOS}}
```

**Tenés que ver:** los tres IDs anotados.

## Paso 2 · Cargá las credenciales en n8n (vos, en la web)
Las claves las pegás vos en n8n, nunca en el chat de Claude. En n8n, abrí un workflow vacío y agregá un nodo de cada uno; en **Credential to connect with › Create new credential**:
- **Telegram:** pegá el token. Nombre: `Telegram [TU-EMPRESA]`.
- **Anthropic:** pegá tu clave de API. Nombre: `Anthropic`.
- **Google Sheets**, **Google Drive** y **Google Docs:** **Sign in with Google** y aceptá.

Después borrá ese workflow (las credenciales quedan).

**Tenés que ver:** las 5 credenciales en la lista de credenciales de n8n.

## Paso 3 · Abrí la pestaña Code e instalá la skill
1. En la app de Claude: **Code** › **Local** › **Open folder…** › tu carpeta `cerebro-[TU-EMPRESA]`.
2. En el [Kit del taller](#r-kit), tocá **Copiar** en la skill `propuesta-comercial` y pegala debajo de este pedido:

```prompt
Creá una skill personal llamada propuesta-comercial con el texto que pego abajo, exacto y sin cambios, en la carpeta de skills de mi usuario (~/.claude/skills/propuesta-comercial/SKILL.md). Decime dónde quedó.

[PEGÁ ACÁ EL CONTENIDO DE LA SKILL]
```

3. Aprobá el permiso para crear el archivo. Si al escribir `/` no aparece `propuesta-comercial`, abrí una sesión nueva en la misma carpeta.

**Tenés que ver:** `propuesta-comercial` en la lista al escribir `/`.

> **Ojo:** el nombre de los botones puede variar según la versión de la app.

## Paso 4 · Que Claude arme el workflow
Antes, en Claude, **Customize › Connectors**: n8n tiene que figurar conectado ([n8n](#s6-n8n), Paso 6). Reemplazá los corchetes y pegá:

```prompt
Con el conector de n8n, armá un workflow "Asistente Telegram [TU-EMPRESA]". Antes leé CLAUDE.md, negocio/, marca/voz.md, datos/reglas.md y la skill propuesta-comercial.

1. Telegram Trigger con la credencial "Telegram [TU-EMPRESA]", Download Images/Files activado y Restrict to Chat IDs = [TU-CHAT-ID]. Zona horaria America/Argentina/Cordoba.
2. Switch: foto o texto que empieza con /gasto → GASTO; texto que empieza con /propuesta → PROPUESTA; otra cosa → responder cómo usarlo.
3. GASTO: Anthropic (claude-haiku-5-5) lee la foto o el texto y devuelve solo JSON con fecha, monto (número; null si no se lee), moneda, categoria (una de: [TUS-CATEGORÍAS]), concepto y proveedor. En Argentina el punto separa miles. Si monto es null, pedí que lo escriban y cortá. Si no, Append Row en la planilla [ID-DE-LA-PLANILLA], hoja Gastos, y respondé "Anotado: ...".
4. PROPUESTA: Anthropic (claude-sonnet-5-5) con la skill y mi cerebro en el System Message; salida en JSON. Copiá la plantilla [ID-DE-LA-PLANTILLA] a la carpeta [ID-DE-LA-CARPETA], reemplazá los marcadores {{...}}, bajala como PDF y mandala por Telegram con el link al Doc y lo que quedó PENDIENTE.
5. Antes de crear, decime qué credencial vas a usar en cada nodo. Si falta alguna, frená.
6. Creá, validá y corregí errores. NO lo publiques. Dame el link.
```

Aprobá los permisos de las herramientas de n8n a medida que aparecen.

**Tenés que ver:** el link al workflow. En n8n: un disparador de Telegram, un Switch y dos ramas.

## Paso 5 · Publicalo y probalo
1. En n8n, abrí el workflow y tocá **Publish**.
2. En Telegram, mandale a tu bot (datos inventados):

```text
/gasto gasté 12.000 en nafta para el reparto
```

```text
/propuesta Llamada con Laura, RRHH de una logística. 12 jefes de depósito que se traban al presentar resultados. Quieren algo en la empresa en marzo, dos o tres encuentros.
```

3. Si algo falla, en Code:

```prompt
Revisá la última ejecución con error del workflow "Asistente Telegram [TU-EMPRESA]" en n8n, decime qué falló en una línea y corregilo.
```

**Tenés que ver:** una fila nueva en la planilla, el "Anotado:" en Telegram y un PDF con tu logo en el chat y en `Propuestas`.

## Cómo sé que funcionó
Con la compu cerrada, desde el celular, mandá un `/propuesta` con un caso tuyo. Te llega un PDF con tu oferta real y `PENDIENTE` donde falta un dato (no inventa precios). Un `/gasto` aparece en la planilla en menos de un minuto.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| El bot no responde | ¿El workflow está publicado? Un bot manda sus mensajes a un solo lugar: despublicá otros flujos que usen el mismo bot. |
| En n8n no aparece ninguna ejecución | Revisá el chat ID en **Restrict to Chat IDs** ([Telegram](#s7-telegram)). |
| Claude no ve n8n | Revisá [n8n](#s6-n8n), Paso 6, y abrí una sesión nueva en Code. |
| La propuesta inventa un precio | "Reforzá en el System Message la regla de no inventar precios" y probá de nuevo. |
| Los marcadores `{{CONTEXTO}}` no se reemplazan | Escribilos de corrido en la plantilla, sin negritas ni espacios en el medio. |

## Para seguir solo
- **Audios:** sumá una credencial de OpenAI en n8n y pedile a Claude que transcriba los audios de voz antes de armar la propuesta.
- **Resumen del mes:** un workflow que el día 1 te mande por Telegram el total por categoría.
- **Tu equipo:** sumá sus chat IDs en **Restrict to Chat IDs** y una columna "Cargado por".
