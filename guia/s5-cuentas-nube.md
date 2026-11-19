---
titulo: Cuentas en la nube
bloque: Setup
tiempo: 25 min
para: Según tu desafío (mirá el recuadro de abajo)
necesitas: s4-github
resultado: Cuentas de Vercel, Supabase, Cloudflare y Lovable creadas, Cloudflare conectado desde la pestaña Code y sabés dónde van las claves de cada una.
---

Claude arma la web o la app en tu compu. Para que la vea el mundo, tiene que vivir en un servidor. Estos cuatro servicios son esos servidores, y todos tienen plan gratis.
Ejemplo: una empresa arma su app de pedidos en Lovable, los datos quedan en Supabase y una escuela publica su web en Vercel o en Cloudflare.

| Servicio | Qué es | Lo usás para |
|---|---|---|
| **Vercel** | Publicar webs | La web que armás con Claude ([Tu web](#p5-web-propia)) |
| **Supabase** | Base de datos con login de usuarios | Guardar los datos de tus apps |
| **Cloudflare** | Dominios y "Workers" (programas chicos en la nube) | Alternativa gratis a Vercel y servidor del bot de Telegram |
| **Lovable** | Armar apps conversando | [App en Lovable](#p6-lovable-y-calendario) |

## Antes de empezar
- [ ] Sesión de GitHub iniciada en el navegador ([GitHub](#s4-github)): vas a entrar con **Continue with GitHub**.
- [ ] Node instalado ([Herramientas base](#s3-herramientas-base), Paso 2): lo necesita la herramienta de Cloudflare.
- [ ] Un gestor de contraseñas (el del navegador, el del celular, 1Password, Bitwarden…).

> **Datos:** las claves de estos servicios **nunca** se pegan en el chat con Claude, en el cerebro ni en GitHub. Cada servicio tiene su lugar: lo marcamos en cada paso. Si Claude necesita una clave en tu compu, usás el archivo `.env` (lo ves en [Telegram](#s7-telegram), Paso 3).

> **Tip:** al entrar con **Continue with GitHub**, tocá el botón verde para autorizar (**Authorize…**). El servicio nunca ve tu contraseña de GitHub.

## Paso 1 · Creá tu cuenta de Vercel
1. Entrá a **[vercel.com/signup](https://vercel.com/signup)** › **Continue with GitHub** › autorizá.
2. Si te pregunta el tipo de uso, elegí **Hobby** para probar hoy.

> **Costo:** **Hobby** es gratis pero **solo para uso personal o no comercial** (Términos de Vercel). Para dejar publicada la web de tu empresa: **Pro, USD 20/mes** (nov 2026), o gratis en Cloudflare (Paso 3).

Las claves en Vercel van en tu proyecto › **Settings › Environment Variables**. Se aplican en la próxima publicación (**deploy**).

**Tenés que ver:** tu panel de Vercel, vacío, con el botón para crear o importar un proyecto.

## Paso 2 · Creá tu cuenta de Supabase y un proyecto
1. Entrá a **[supabase.com/dashboard/sign-up](https://supabase.com/dashboard/sign-up)** › **Continue with GitHub**.
2. Creá una organización con el nombre de tu empresa, plan **Free**.
3. Proyecto nuevo: **Name** `[TU-EMPRESA]-prueba` · **Database Password**: generala y **guardala en tu gestor** · **Region**: la más cercana (para Argentina suele ser **São Paulo**).

**Tenés que ver:** el panel del proyecto con el menú de la izquierda (**Table Editor**, **SQL Editor**…).

Las claves están en **Settings › API Keys**:

| Clave | Empieza con | ¿Puede estar en la web? |
|---|---|---|
| **Publishable** (antes `anon`) | `sb_publishable_` | Sí, con reglas de seguridad (RLS). |
| **Secret** (antes `service_role`) | `sb_secret_` | **Nunca.** Puede leer y borrar toda tu base. |

> **Costo:** **Free** permite 2 proyectos activos. Si un proyecto pasa **7 días sin uso, se pausa**: abrilo y tocá **Resume project**. Pagos desde **USD 25/mes** (nov 2026).

## Paso 3 · Creá tu cuenta de Cloudflare y conectala desde Code
1. Entrá a **[dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up)**, registrate con tu mail, confirmalo y quedate en el plan gratis.
2. En la app de Claude, abrí **Code** › **Local** › tu carpeta `prueba-claude` y pegá:

```prompt
Iniciá sesión en Cloudflare con wrangler (npx wrangler login). Se me va a abrir el navegador: esperá a que autorice. Después corré npx wrangler whoami y decime qué cuenta quedó conectada.
```

3. Aprobá el permiso para que Claude corra el comando. Cuando se abra el navegador, tocá **Allow**.

> **Costo:** **Workers Free**: 100.000 pedidos por día (nov 2026). Para el bot de una pyme sobra. **Workers Paid**: USD 5/mes.

Las claves en Cloudflare van como **secretos** del Worker: **Workers & Pages** › tu Worker › **Settings › Variables and Secrets** › **Add** › tipo **Secret**. Nunca en el archivo de configuración del proyecto.

**Tenés que ver:** Claude te dice tu mail y tu cuenta de Cloudflare.

## Paso 4 · Creá tu cuenta de Lovable
1. Entrá a **[lovable.dev](https://lovable.dev)** y registrate (con GitHub, Google o tu mail).
2. Quedate en **Free**.

> **Costo:** **Free** da 5 créditos por día, con tope de 30 por mes; cada mensaje gasta créditos. **Pro**: USD 25/mes (nov 2026). Verificá en [lovable.dev/pricing](https://lovable.dev/pricing).

**Tenés que ver:** la pantalla de inicio de Lovable, con el cuadro para escribir qué app querés.

## Cómo sé que funcionó
- Entrás a los cuatro servicios sin volver a registrarte y Claude te confirmó tu cuenta de Cloudflare.
- Sabés dónde está la clave **Secret** de Supabase y no la copiaste a ningún lado.

```prompt
Explicame en 5 líneas, para alguien que no programa, qué diferencia hay entre Vercel, Cloudflare Workers, Supabase y Lovable, y cuál conviene para: una web institucional, un bot de Telegram y una app de turnos con login. Mi negocio: [DESCRIBÍ TU NEGOCIO EN UNA LÍNEA].
```

**Tenés que ver:** una respuesta que coincide con la tabla del principio.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude dice que no encuentra `npx` | Te falta Node: [Herramientas base](#s3-herramientas-base), Paso 2. |
| Windows: `npx` da "running scripts is disabled" | Decile a Claude: "usá npx.cmd". |
| El login de wrangler se queda esperando | Revisá que tocaste **Allow**. Si sigue, pedile a Claude que lo corte y lo repita. |
| Supabase: "proyecto pausado" | Abrilo y tocá **Resume project**. |
| Lovable: "no credits left" | Esperá al día siguiente (5 por día) o al mes siguiente. |
| Pegaste una clave secreta donde no iba | Generá una nueva en el servicio y borrá la vieja. Borrar el mensaje no alcanza. |

## Para seguir solo
- Si tu web queda en Vercel para tu empresa, pasá a **Pro** y poné un aviso de gasto en **Settings › Billing**.
- Conectá estos servicios a Claude para manejarlos conversando ([Conectores y MCP](#s8-conectores-y-mcp)).
- En Supabase, pedile a Claude que active **RLS** (reglas de quién ve cada fila) antes de usar datos reales.

## Fuentes
Consultadas el 18/11/2026.
- Vercel: https://vercel.com/docs/plans/hobby · https://vercel.com/legal/terms · https://vercel.com/pricing
- Supabase: https://supabase.com/pricing · https://supabase.com/docs/guides/platform/free-project-pausing · https://supabase.com/docs/guides/api/api-keys
- Cloudflare Workers: https://developers.cloudflare.com/workers/platform/pricing/ · https://developers.cloudflare.com/workers/wrangler/commands/general/ · https://developers.cloudflare.com/workers/configuration/secrets/
- Lovable: https://docs.lovable.dev/introduction/plans-and-credits · https://lovable.dev/pricing
