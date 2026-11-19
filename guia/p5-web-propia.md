---
titulo: "Tu web: copiá la estructura de un referente y publicala"
bloque: Tutorial
tiempo: 90 min
para: Manuel Martínez Oratoria, Viajes TDH, La Consejera del Éxito, Denvet (y cualquiera que quiera web)
necesitas: p1-cerebro, s2-claude-code, s3-herramientas-base, s4-github, s5-cuentas-nube
resultado: Tu web publicada en internet, con tus textos y tu marca, y un formulario de contacto que guarda cada consulta en tu base de datos.
---

Hacer una web de cero da miedo porque no sabés por dónde empezar. Acá no empezás de cero: elegís la web de alguien de tu rubro que te guste, Claude Code la desarma (qué secciones tiene, en qué orden argumenta, dónde pide el contacto) y arma **tu** web con esa estructura, pero con tus textos y tu marca sacados del cerebro.
No importa si no tenés web, si tu web es vieja o si solo querés rehacer una página (por ejemplo, la de precios): todos arrancan igual.

> **Tip:** palabras que vas a ver en esta página:
> - **Repositorio (repo):** la carpeta de tu proyecto guardada en GitHub. **Commit** es guardar una versión; **Push** es subirla.
> - **Deploy (publicar):** poner la web en internet. Lo hace Vercel (o Cloudflare Pages).
> - **Supabase:** una base de datos en la nube. Acá guarda las consultas del formulario.
> - **SQL:** el idioma para darle órdenes a una base de datos. Lo copiás y pegás, no hace falta entenderlo.
> - **RLS (seguridad por filas):** la regla de Supabase que decide quién puede leer o escribir cada tabla.
> - **Variable de entorno:** una línea `NOMBRE=valor` que guarda un dato de configuración fuera del código (por ejemplo, la dirección de tu Supabase).
> - **Astro:** la herramienta con la que Claude arma la web. No la tocás vos.
> - **CTA:** el botón que invita a hacer algo ("Escribinos", "Reservá").

## Antes de empezar
- [ ] Tu cerebro armado, con `negocio/` y `marca/` completos ([Tu cerebro](#p1-cerebro)).
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)).
- [ ] Node y Git instalados ([Herramientas base](#s3-herramientas-base)).
- [ ] Cuenta de GitHub y GitHub Desktop ([GitHub](#s4-github)).
- [ ] Cuentas de Vercel y Supabase creadas, y Vercel conectado con tu GitHub ([Cuentas en la nube](#s5-cuentas-nube)).
- [ ] El link de **una** web de referencia de tu rubro (de otro país, mejor: no es tu competencia directa).
- [ ] Opcional: logo en PNG o SVG y 3 a 6 fotos tuyas (de tu local, tu equipo, tu producto).

> **Ojo:** copiamos la **estructura**, no el contenido. Nada de copiar textos, fotos, logos ni diseño idéntico de la web de referencia: eso tiene dueño. Lo que se aprende es el orden de las ideas: qué problema nombra primero, qué prueba muestra, dónde pone el botón.

## Paso 1 · Creá la carpeta de la web
La web va en una carpeta **aparte** del cerebro. El cerebro es privado; la web es pública.

<div data-os="mac">

1. En **Finder › Documentos** creá la carpeta `web-[TU-EMPRESA]`, al lado de `cerebro-[TU-EMPRESA]`.
2. Abrí la **Terminal** (**Cmd + Espacio**, escribí `Terminal` y Enter) y escribí:

```bash
cd ~/Documents/web-[TU-EMPRESA]
claude
```

</div>
<div data-os="win">

1. En el **Explorador de archivos › Documentos** creá la carpeta `web-[TU-EMPRESA]`, al lado de `cerebro-[TU-EMPRESA]`.
2. Abrí **PowerShell** (tecla **Windows**, escribí `PowerShell` y Enter) y escribí:

```powershell
cd $HOME\Documents\web-[TU-EMPRESA]
claude
```

</div>

**Tenés que ver:** Claude Code abierto y, arriba, la ruta de la carpeta `web-[TU-EMPRESA]`.

## Paso 2 · Que Claude Code analice la web de referencia
Pegá esto. Antes de mandarlo, cambiá `[URL-DE-LA-WEB-DE-REFERENCIA]` por el link que elegiste y `[TU-EMPRESA]` por el nombre de tu carpeta. En Windows, `[MI-USUARIO]` es tu usuario de Windows (si no lo sabés, dejalo: Claude lo averigua). Claude va a pedir permiso para entrar a la web y para leer tu cerebro (que está en otra carpeta): aceptá.

```prompt
Quiero hacer la web de mi empresa usando como referencia la ESTRUCTURA de esta web: [URL-DE-LA-WEB-DE-REFERENCIA]

1. Entrá a la web y a sus páginas principales (inicio, precios o servicios, nosotros, contacto). Si alguna no carga, decímelo y seguí con las demás.
2. Escribí en analisis-referencia.md:
   - La lista de secciones de la página de inicio, en orden, con qué función cumple cada una (enganchar, mostrar el problema, prueba social, oferta, objeciones, llamado a la acción).
   - El orden de los argumentos: qué dice primero, qué después y por qué creés que lo hace así.
   - Todos los llamados a la acción (CTA): texto del botón, dónde aparece, a dónde lleva.
   - Qué hace bien para que un cliente confíe y qué le falta.
3. No copies textos, imágenes ni marcas de esa web. Solo la estructura y la lógica.

Después leé mi cerebro en ~/Documents/cerebro-[TU-EMPRESA] (en Windows: C:\Users\[MI-USUARIO]\Documents\cerebro-[TU-EMPRESA]): CLAUDE.md, la carpeta negocio/ y la carpeta marca/. Al final de analisis-referencia.md agregá una sección "Cómo la adaptamos a nosotros": qué secciones tomamos, cuáles sacamos, cuáles agregamos según nuestro cliente ideal, nuestras objeciones y nuestras preguntas frecuentes. Mostrame ese plan antes de escribir código.
```

**Tenés que ver:** el archivo `analisis-referencia.md` y, en pantalla, un plan de secciones para tu web. Corregí lo que no te cierre: "Sacá la sección de equipo, todavía no tenemos fotos".

## Paso 3 · Que arme tu web
Cuando el plan te guste:

```prompt
Armá la web con ese plan.

- Usá Astro y que el sitio sea estático (HTML que se genera antes de publicar: carga rápido y Google lo lee bien).
- Todos los textos salen de mi cerebro, con la voz de marca/voz.md. Si falta un dato (precio, dirección, horario), poné [PENDIENTE: qué falta] en el texto y anotalo en pendientes-web.md. No inventes precios, testimonios, cifras ni clientes.
- Colores, tipografías y logo: de marca/identidad-visual.md. Si hay imágenes mías en la carpeta imagenes/, usalas; si no, dejá lugares marcados para fotos.
- Que se vea bien en el celular primero.
- Páginas: inicio, una página por servicio o programa principal, preguntas frecuentes y contacto.
- El formulario de contacto (nombre, WhatsApp o email, mensaje) todavía no guarda nada: lo conectamos en el paso siguiente.
- Botón de WhatsApp con el número de mi cerebro: [TU-NÚMERO-DE-WHATSAPP-CON-CÓDIGO-DE-PAÍS].

Cuando termines, instalá lo que haga falta y levantá la vista previa local. Decime la dirección para abrirla en el navegador.
```

Claude va a crear el proyecto y correr comandos (`npm install`, `npm run dev`). Aceptá cada permiso.

**Tenés que ver:** tu web en el navegador, en una dirección tipo `http://localhost:4321`. Recorrela desde el celular del navegador (achicá la ventana) y pedí cambios en lenguaje normal: "El título del inicio es muy largo", "Poné el botón de WhatsApp más arriba".

> **Tip:** si querés tus fotos, creá la carpeta `imagenes/` adentro de `web-[TU-EMPRESA]`, arrastralas ahí y decile a Claude: "Usá las fotos de imagenes/ en el inicio y en nosotros".

## Paso 4 · Creá la tabla de consultas en Supabase
Cada vez que alguien complete el formulario, la consulta va a caer en una tabla. Esa tabla tiene una regla: **desde la web solo se puede agregar**. Nadie puede leer, cambiar ni borrar consultas desde afuera.

1. Entrá a [supabase.com](https://supabase.com), abrí tu proyecto (o creá uno con **New project**, región São Paulo si te la ofrece).
2. En el menú de la izquierda abrí **SQL Editor**, pegá esto y tocá **Run**:

```sql
create table public.consultas (
  id uuid primary key default gen_random_uuid(),
  creada_en timestamptz not null default now(),
  nombre text not null check (char_length(nombre) between 2 and 120),
  contacto text not null check (char_length(contacto) between 5 and 160),
  mensaje text check (char_length(mensaje) <= 2000),
  pagina text
);

-- Activa la seguridad por filas: sin una política, nadie puede tocar la tabla.
alter table public.consultas enable row level security;

-- La web (usuario anónimo) solo puede INSERTAR. No puede leer, editar ni borrar.
grant insert on table public.consultas to anon;

create policy "La web solo puede agregar consultas"
on public.consultas for insert
to anon
with check ( true );
```

3. Abrí **Settings › API Keys** y copiá la **Publishable key** (empieza con `sb_publishable_`). La URL del proyecto la ves en el botón **Connect**, arriba.

**Tenés que ver:** en **Table Editor** aparece la tabla `consultas`, vacía, con la etiqueta de RLS activado.

> **Ojo:** la **Publishable key** puede ir en la web porque la tabla tiene RLS. La **Secret key** (`sb_secret_`) **nunca** va en la web ni en GitHub: saltea todas las reglas.

> **Datos:** el formulario guarda nombres y teléfonos de personas reales. Pedí solo lo necesario para responder y poné una línea debajo del botón: "Usamos tus datos solo para responder tu consulta".

## Paso 5 · Conectá el formulario
Volvé a Claude Code:

```prompt
Conectá el formulario de contacto a Supabase.

- Tabla: consultas. Columnas: nombre, contacto, mensaje, pagina (la página desde donde se envió). Las columnas id y creada_en se completan solas.
- Usá @supabase/supabase-js con dos variables de entorno: PUBLIC_SUPABASE_URL y PUBLIC_SUPABASE_PUBLISHABLE_KEY. Creá un archivo .env con esas dos variables vacías para que yo las complete, y asegurate de que .env esté en .gitignore. Creá también .env.example sin valores.
- El usuario anónimo solo tiene permiso de INSERT: hacé el insert sin pedir que devuelva la fila (sin .select()).
- Validá los campos antes de enviar, mostrá "¡Gracias! Te respondemos a la brevedad" si salió bien y un mensaje claro si falló.
- Agregá un campo trampa oculto contra spam: si viene completo, no se envía.
```

Abrí el archivo `.env` vos, a mano. Escribí esto en una terminal nueva (no en el chat de Claude):

<div data-os="mac">

```bash
cd ~/Documents/web-[TU-EMPRESA]
open -e .env
```

</div>
<div data-os="win">

```powershell
cd $HOME\Documents\web-[TU-EMPRESA]
notepad .env
```

</div>

Completá las dos líneas con lo que copiaste en el Paso 4 (la URL del botón **Connect** y la **Publishable key**), guardá y cerrá:

```bash
PUBLIC_SUPABASE_URL=[URL-DE-TU-PROYECTO]
PUBLIC_SUPABASE_PUBLISHABLE_KEY=[TU-PUBLISHABLE-KEY]
```

Después decile a Claude Code: "Reiniciá la vista previa".

Mandá un mensaje de prueba desde el formulario de la vista previa.

**Tenés que ver:** en Supabase, **Table Editor › consultas**, una fila con tu mensaje de prueba.

## Paso 6 · Subí la web a GitHub
```prompt
Prepará esta carpeta para Git: revisá que .gitignore excluya .env, node_modules, dist y .DS_Store, inicializá el repositorio y hacé el primer commit con el mensaje "Web inicial". Antes del commit, confirmame que ningún archivo que se va a subir tiene una clave.
```

Después, en **GitHub Desktop › File › Add local repository**, elegí `web-[TU-EMPRESA]` y tocá **Publish repository**. Puede quedar privado: Vercel publica igual.

**Tenés que ver:** el repo `web-[TU-EMPRESA]` en tu perfil de [github.com](https://github.com), **sin** archivo `.env`.

## Paso 7 · Publicala con Vercel
1. Entrá a [vercel.com](https://vercel.com). En el panel tocá **Create New › Project**.
2. En la lista de repositorios de GitHub, buscá `web-[TU-EMPRESA]` y tocá **Import**. Si no aparece, usá el link para ajustar los permisos de la app de GitHub y dale acceso a ese repo.
3. Vercel detecta Astro solo. Abrí **Environment Variables** y cargá las dos variables, con los mismos nombres y valores de tu `.env`:
   - `PUBLIC_SUPABASE_URL`
   - `PUBLIC_SUPABASE_PUBLISHABLE_KEY`
4. Tocá **Deploy** y esperá uno o dos minutos.

**Tenés que ver:** una pantalla de felicitaciones y la dirección pública de tu web, algo como `web-[tu-empresa].vercel.app`.

> **Tip:** desde ahora, cada cambio que subís a GitHub se publica solo. Pedile un cambio a Claude Code, hacé commit y **Push origin** en GitHub Desktop: en un minuto está online.

> **Ojo:** si agregás o cambiás una variable de entorno después, se aplica recién en la próxima publicación. Hacé **Redeploy** desde el proyecto en Vercel.

> **Costo:** el plan gratis de Vercel (**Hobby**) es, según sus términos, solo para uso **personal o no comercial**. La web de una empresa es uso comercial. Para practicar hoy alcanza; para dejarla en producción tenés dos caminos: pasar a **Pro** en Vercel o publicar en **Cloudflare Pages**, cuyo plan gratis no tiene esa restricción en sus límites publicados. Precios y detalle en [Stack y costos](#r-stack-y-costos).

### Alternativa · Publicar en Cloudflare Pages
1. En el panel de Cloudflare: **Workers & Pages › Create application › Pages › Connect to Git**.
2. Elegí **GitHub**, autorizá y seleccioná `web-[TU-EMPRESA]`. Tocá **Begin setup**.
3. En **Set up builds and deployments**: framework Astro (o comando de build `npm run build` y carpeta de salida `dist`). Cargá las dos variables de entorno.
4. **Save and Deploy**.

La web queda en una dirección `*.pages.dev`. Mismo repo, misma web: solo cambia dónde se publica.

**Tenés que ver:** tu web abierta en la dirección `*.pages.dev` y, al mandar el formulario, una fila nueva en Supabase.

## Paso 8 · SEO básico y "aparecer en ChatGPT"
Google y los asistentes de IA recomiendan lo que entienden. Que te entiendan es trabajo de texto, no de magia:

```prompt
Revisá la web para que Google y los asistentes de IA (ChatGPT, Gemini, Claude) la entiendan bien:

1. Cada página con un título y una descripción únicos, un solo H1 y textos alternativos en las imágenes.
2. Datos estructurados (JSON-LD de schema.org) en el inicio: tipo de negocio local con nombre, dirección, horario, teléfono, zona que atendemos y redes. Sacá los datos del cerebro; lo que falte va a pendientes-web.md.
3. En la página de preguntas frecuentes, datos estructurados de tipo FAQPage con las preguntas y respuestas de mi cerebro (ventas/preguntas-frecuentes.md). Respuestas cortas y directas, como las diría yo.
4. Un sitemap.xml y un robots.txt que permita indexar todo.
5. Que el nombre, la dirección y el teléfono estén escritos exactamente igual en toda la web.

Mostrame qué cambiaste y hacé commit con el mensaje "SEO básico".
```

Después hacé **Push origin** en GitHub Desktop.

**Tenés que ver:** el commit "SEO básico" en GitHub y, unos minutos después, la web actualizada en Vercel.

> **Tip:** ninguna web garantiza aparecer en ChatGPT. Lo que más ayuda: una página de preguntas frecuentes que responda lo que la gente pregunta de verdad ("¿cuánto sale un curso de oratoria en Córdoba?"), tu **Perfil de Empresa de Google** completo y los mismos datos en todos lados.

## Cómo sé que funcionó
1. Abrí tu web pública **desde el celular** (con datos móviles, no el wifi del taller).
2. Completá el formulario con datos inventados: nombre "Prueba Taller", contacto "prueba@ejemplo.com".
3. En Supabase, **Table Editor › consultas**: tiene que aparecer la fila.
4. Pedile a Claude Code:

```prompt
Sin cambiar nada, verificá la seguridad del formulario: ¿alguien desde la web podría LEER las consultas guardadas? Explicámelo en 3 líneas mirando el SQL que corrí en Supabase y el código del formulario.
```

La respuesta correcta: no, porque la única política permite insertar.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude no puede entrar a la web de referencia | Algunas webs bloquean robots. Elegí otra, o guardá la página desde el navegador (**Archivo › Guardar como**) en la carpeta y pedile que analice ese archivo. |
| `new row violates row-level security policy` | El código pide que Supabase devuelva la fila después de insertar. Decile a Claude: "Sacá el .select() del insert". |
| `permission denied for table consultas` | Faltó el `grant insert`. Volvé a correr en el **SQL Editor** solo esa línea. |
| En Vercel el formulario no anda pero en tu compu sí | Las variables de entorno no están cargadas en Vercel o están mal escritas. Revisalas en **Settings › Environment Variables** del proyecto y hacé **Redeploy**. |
| Vercel no muestra tu repo | Tu GitHub no le dio acceso a ese repo. En la pantalla de importar, usá el link para ajustar los permisos de la app de GitHub. |
| GitHub Desktop quiere subir el `.env` | Pará. Decile a Claude: "Sacá .env del repositorio y agregalo a .gitignore". Si ya se subió, rotá la clave en **Settings › API Keys** de Supabase. |

## Para seguir solo
- **Dominio propio:** comprá tu `.com.ar` en NIC Argentina o tu `.com` donde prefieras, y conectalo desde **Settings › Domains** en Vercel (o en Cloudflare).
- **Aviso por cada consulta nueva:** que cada fila nueva en `consultas` te llegue por email o Telegram con n8n ([n8n](#s6-n8n), [Telegram](#s7-telegram)).
- **Una página por pregunta:** cada pregunta frecuente que te hacen por WhatsApp puede ser una página corta con su respuesta. Pedíselo a Claude Code de a una por semana. Es la forma más simple de que te encuentren Google y los asistentes.

## Fuentes
- Vercel, crear proyecto desde Git: https://vercel.com/docs/projects/managing-projects
- Vercel, variables de entorno (los cambios se aplican en el próximo deploy): https://vercel.com/docs/environment-variables
- Vercel, Astro sin configuración: https://vercel.com/docs/frameworks/frontend/astro
- Vercel, plan Hobby: https://vercel.com/docs/plans/hobby · Términos, sección Hobby ("personal or non-commercial use"): https://vercel.com/legal/terms
- Supabase, Row Level Security (grant + policy de insert para `anon`): https://supabase.com/docs/guides/database/postgres/row-level-security
- Supabase, API keys (publishable vs secret, **Settings › API Keys**): https://supabase.com/docs/guides/api/api-keys
- Astro, variables `PUBLIC_`: https://docs.astro.build/en/guides/environment-variables/
- Cloudflare Pages, conectar con Git: https://developers.cloudflare.com/pages/get-started/git-integration/ · Límites del plan gratis: https://developers.cloudflare.com/pages/platform/limits/
- Verificado el 18/11/2026.
