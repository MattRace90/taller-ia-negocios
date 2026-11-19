---
titulo: Cuentas en la nube
bloque: Setup
tiempo: 30 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s4-github
resultado: Cuentas de Vercel, Supabase, Cloudflare y Lovable creadas, sabés qué plan usar y dónde van las claves de cada una.
---

Claude Code arma la web o la app en tu compu. Para que la vea el mundo, tiene que vivir en algún servidor. Estos cuatro servicios son esos servidores, y todos tienen un plan gratis para empezar.
Ejemplo: una empresa arma su app de pedidos en Lovable, los datos quedan en Supabase y una escuela publica su web en Vercel o en Cloudflare.

| Servicio | Qué es | Lo usás hoy para |
|---|---|---|
| **Vercel** | Publicar webs | Subir la web que armás con Claude Code ([Tu web](#p5-web-propia)) |
| **Supabase** | Base de datos con login de usuarios | Guardar los datos de tus apps y planillas |
| **Cloudflare** | Dominios, DNS (la "guía telefónica" que conecta tu dominio con tu web) y "Workers" (programas chicos en la nube) | Alternativa gratis a Vercel y el servidor del bot de Telegram |
| **Lovable** | Armar apps conversando, sin código | [App en Lovable](#p6-lovable-y-calendario) |

## Antes de empezar
- [ ] Cuenta de GitHub con tu sesión iniciada en el navegador ([GitHub](#s4-github)). Vas a entrar a casi todo con **Continue with GitHub**.
- [ ] Node instalado ([Herramientas base](#s3-herramientas-base)): lo necesita `wrangler`, la herramienta de Cloudflare.
- [ ] Un gestor de contraseñas (el de tu navegador, el de tu celular, 1Password, Bitwarden…). Ahí van las claves que aparezcan hoy.

> **Datos:** las claves de estos servicios **nunca** se pegan en un chat con Claude, en el cerebro ni en GitHub. Cada servicio tiene su lugar para guardarlas: lo marcamos en cada paso.

> **Tip:** cuando entrás con **Continue with GitHub**, GitHub te pregunta si dejás que ese servicio use tu cuenta. Tocá el botón verde para autorizar (**Authorize…**). El servicio nunca ve tu contraseña de GitHub.

## Paso 1 · Creá tu cuenta de Vercel
1. Entrá a **[vercel.com/signup](https://vercel.com/signup)**.
2. Elegí **Continue with GitHub** y autorizá (botón verde).
3. Si te pregunta el tipo de uso, elegí **Hobby** para probar hoy.

> **Costo:** el plan **Hobby** es gratis, pero según los Términos de Vercel es **solo para uso personal o no comercial**. La web de tu empresa es uso comercial: para dejarla publicada ahí necesitás **Pro (USD 20/mes)**, o publicarla gratis en Cloudflare (Paso 3). Hoy podés probar en Hobby. Además, si en Hobby te pasás de un límite, en general tenés que esperar 30 días: no se puede comprar más.

Dónde van las claves en Vercel: en tu proyecto › **Settings › Environment Variables** (variables de entorno: un nombre y un valor que la web lee sin que estén en el código). Cada cambio se aplica en el próximo **deploy** (la próxima vez que publicás una versión), no en la que ya está publicada.

**Tenés que ver:** tu panel de Vercel, vacío, con el botón para crear o importar un proyecto.

## Paso 2 · Creá tu cuenta de Supabase y tu primer proyecto
1. Entrá a **[supabase.com/dashboard/sign-up](https://supabase.com/dashboard/sign-up)** y elegí **Continue with GitHub**.
2. Creá una organización (poné el nombre de tu empresa) y elegí el plan **Free**.
3. Creá un proyecto nuevo:
   - **Name:** `[TU-EMPRESA]-prueba`
   - **Database Password:** tocá generar una contraseña y **guardala en tu gestor de contraseñas**.
   - **Region:** la más cercana a tus clientes que te ofrezca la lista (para Argentina suele ser **São Paulo**).
4. Esperá un par de minutos mientras se crea.

**Tenés que ver:** el panel de tu proyecto con el menú de la izquierda (**Table Editor**, **SQL Editor**, etc.).

### Dónde están la URL y las claves
- **URL del proyecto:** botón **Connect** arriba del panel. Elegí tu tipo de proyecto y vas a ver la URL y la clave pública.
- **Claves:** **Settings › API Keys**.

| Clave | Empieza con | ¿Se puede ver en el navegador? |
|---|---|---|
| **Publishable** (la vieja se llamaba `anon`) | `sb_publishable_` | Sí. Está pensada para la web o la app, y las reglas de seguridad (RLS) limitan lo que puede hacer. |
| **Secret** (la vieja se llamaba `service_role`) | `sb_secret_` | **Nunca.** Saltea todas las reglas de seguridad: con ella se puede leer y borrar toda tu base. |

> **Ojo:** la clave **Secret** (o `service_role`) no va en el código de la web, ni en una captura, ni en un chat, ni en GitHub. Si un sistema la necesita (por ejemplo n8n), va en las credenciales de ese sistema. Si se filtró, generá una nueva en **Settings › API Keys** y borrá la vieja.

> **Costo:** el plan **Free** permite **2 proyectos activos**, 500 MB de base por proyecto y 50.000 usuarios activos por mes. Si el proyecto pasa **7 días sin actividad, se pausa** (te avisan por mail antes). Para reactivarlo: abrí el proyecto y tocá **Resume project**. Se puede restaurar hasta 1 año después. Los planes pagos (desde **USD 25/mes**) no se pausan.

## Paso 3 · Creá tu cuenta de Cloudflare e iniciá sesión con wrangler
1. Entrá a **[dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up)**, registrate con tu mail y confirmalo. Si el mail de confirmación no llega en 2 minutos, mirá en **Spam** o **Promociones**.
2. Quedate en el plan gratis.
3. Abrí la terminal (Terminal en Mac, PowerShell en Windows) e iniciá sesión con `wrangler`, la herramienta de Cloudflare para la terminal. `npx` la descarga y la corre sin instalarla:

> **Ojo:** en Windows, si el comando de abajo sale en rojo con "running scripts is disabled", escribí `npx.cmd wrangler login` (con `.cmd`). Lo mismo para `npx.cmd wrangler whoami`.

```bash
npx wrangler login
```

Si te pregunta `Need to install the following packages… Ok to proceed? (y)`, escribí `y` y apretá **Enter**. Se abre el navegador: tocá **Allow** para autorizar.

4. Verificá:

```bash
npx wrangler whoami
```

> **Costo:** **Workers Free** permite **100.000 requests por día** (un request es cada pedido que recibe: una visita, un mensaje al bot) (se reinicia a la medianoche UTC) y 10 ms de procesador por request. Para un bot de una pyme sobra. Si te pasás, el Worker da error hasta el día siguiente. **Workers Paid** cuesta **USD 5/mes** por cuenta e incluye 10 millones de requests por mes.

Dónde van las claves en Cloudflare: como **secretos** del Worker. Con la terminal:

```bash
npx wrangler secret put [NOMBRE_DE_LA_CLAVE]
```

Reemplazá `[NOMBRE_DE_LA_CLAVE]` por el nombre que te diga el tutorial (por ejemplo `ANTHROPIC_API_KEY`). Este comando se corre parado en la carpeta del proyecto del Worker, que vas a crear en el tutorial: hoy solo sabé que existe. `wrangler` te pide el valor, lo pegás vos y no lo muestra en pantalla. También se hace desde el panel: **Workers & Pages** › tu Worker › **Settings › Variables and Secrets** › **Add** › tipo **Secret**. Nunca en el archivo de configuración del proyecto.

**Tenés que ver:** `wrangler whoami` muestra tu mail y tu cuenta de Cloudflare.

## Paso 4 · Creá tu cuenta de Lovable
1. Entrá a **[lovable.dev](https://lovable.dev)** y tocá para registrarte. Si te ofrece GitHub, usalo; si no, tu mail o Google.
2. Quedate en **Free** por ahora.

> **Costo:** **Free** da **5 créditos por día, con tope de 30 por mes**. Cada mensaje gasta créditos (un cambio chico, medio crédito; uno grande, más). Los 30 se van rápido en un día de pruebas: hoy usalos con cuidado. **Pro** cuesta **USD 25/mes** (o USD 250 por año) con 100 créditos por mes, y los créditos que no usás pasan al mes siguiente mientras la suscripción siga activa. Free permite proyectos privados; dominio propio, solo en planes pagos.

**Tenés que ver:** la pantalla de inicio de Lovable, con el cuadro para escribir qué app querés construir.

## Cómo sé que funcionó
- Entrás a Vercel, Supabase, Cloudflare y Lovable sin volver a registrarte.
- `npx wrangler whoami` muestra tu cuenta.
- Sabés dónde está la clave **Secret** de Supabase y no la copiaste a ningún lado.

Prueba con Claude Code:

```prompt
Explicame en 5 líneas, para alguien que no programa, qué diferencia hay entre Vercel, Cloudflare Workers, Supabase y Lovable, y cuál conviene para: una web institucional de mi negocio, un bot de Telegram y una app de turnos con login. Mi negocio: [DESCRIBÍ TU NEGOCIO EN UNA LÍNEA].
```

**Tenés que ver:** una respuesta que coincide con la tabla del principio.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `npx: command not found` | Te falta Node: [Herramientas base](#s3-herramientas-base), Paso 1. |
| Windows: `npx` dice "running scripts is disabled" | Mirá esa fila en [Herramientas base](#s3-herramientas-base), **Si algo falla**. |
| `wrangler login` abre el navegador pero la terminal se queda esperando | Revisá que tocaste **Allow**. Si sigue, cortá con **Ctrl+C** y repetí. |
| Supabase: "proyecto pausado" | Abrí el proyecto y tocá **Resume project**. |
| Supabase no te deja crear un tercer proyecto | El plan Free permite 2 activos. Pausá o borrá uno de prueba. |
| Lovable: "no credits left" | Esperá al día siguiente (5 por día) o al mes siguiente si llegaste a 30. |
| Pegaste una clave secreta donde no iba | Generá una nueva en el servicio y borrá la vieja. No alcanza con borrar el mensaje. |

## Para seguir solo
- Si tu web va a quedar publicada en Vercel para tu empresa, pasá a **Pro** y en **Settings › Billing** bajá el aviso de gasto a un número que te resulte cómodo.
- Conectá estos servicios a Claude Code por MCP para manejarlos conversando ([Conectores y MCP](#s8-conectores-y-mcp)).
- En Supabase, pedile a Claude Code que active **RLS** (Row Level Security: reglas que dicen quién puede ver o cambiar cada fila de una tabla) en cada tabla antes de usar datos reales.

## Fuentes
Consultadas el 18/11/2026.
- Vercel, plan Hobby y límites: https://vercel.com/docs/plans/hobby
- Vercel, Términos (uso comercial, §4): https://vercel.com/legal/terms
- Vercel, precios y Pro: https://vercel.com/pricing · https://vercel.com/docs/plans/pro-plan
- Vercel, variables de entorno: https://vercel.com/docs/environment-variables
- Supabase, precios: https://supabase.com/pricing
- Supabase, pausa de proyectos Free: https://supabase.com/docs/guides/platform/free-project-pausing
- Supabase, claves de API: https://supabase.com/docs/guides/api/api-keys
- Cloudflare Workers, precios y límites: https://developers.cloudflare.com/workers/platform/pricing/ · https://developers.cloudflare.com/workers/platform/limits/
- Wrangler, comandos (`login`, `whoami`): https://developers.cloudflare.com/workers/wrangler/commands/general/
- Cloudflare, secretos: https://developers.cloudflare.com/workers/configuration/secrets/
- Lovable, planes y créditos: https://docs.lovable.dev/introduction/subscription-plans · https://docs.lovable.dev/introduction/plans-and-credits · https://lovable.dev/pricing
