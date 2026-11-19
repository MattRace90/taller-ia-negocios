---
titulo: "Tu web: copiá la estructura de un referente y publicala"
bloque: Tutorial
tiempo: 90 min
para: Manuel Martínez Oratoria, Viajes TDH, La Consejera del Éxito, Denvet (y cualquiera que quiera web)
necesitas: p1-cerebro, s2-claude-code, s3-herramientas-base, s4-github, s5-cuentas-nube
resultado: Tu web publicada en internet, con tus textos y tu marca, y un formulario de contacto que guarda cada consulta en tu base de datos.
---

Es la versión completa del [D3](#d3-web-app): hoy hacé primero la MVP en Lovable; esto es para si te sobra tiempo. Elegís la web de alguien de tu rubro que te guste, Claude la desarma (qué secciones tiene, en qué orden argumenta, dónde pide el contacto) y arma **tu** web con esa estructura, con tus textos y tu marca. Todo desde la pestaña **Code**; subís con **GitHub Desktop** y publicás desde la web de **Vercel** (o Cloudflare).

> **Tip:** **repositorio (repo):** tu proyecto guardado en GitHub; **commit**, guardar una versión; **push**, subirla. **Supabase:** la base de datos donde caen las consultas. **Variable de entorno:** una línea `NOMBRE=valor` con un dato de configuración fuera del código.

## Antes de empezar
- [ ] Tu cerebro con `negocio/` y `marca/` ([Tu cerebro](#p1-cerebro)).
- [ ] La app de escritorio de Claude con la pestaña **Code** ([S2 · Claude Code en la pestaña Code](#s2-claude-code)).
- [ ] Node.js instalado ([Herramientas base](#s3-herramientas-base), Paso 1).
- [ ] GitHub Desktop con tu cuenta ([GitHub](#s4-github)).
- [ ] Cuentas de Vercel y Supabase, con Vercel conectado a tu GitHub ([Cuentas en la nube](#s5-cuentas-nube)).
- [ ] El link de **una** web de referencia de tu rubro (mejor de otro país).

> **Ojo:** copiamos la **estructura**, no el contenido. Nada de textos, fotos ni logos ajenos: eso tiene dueño.

## Paso 1 · Creá la carpeta y abrila en Code
1. En **Documentos**, creá la carpeta `web-[TU-EMPRESA]`, aparte del cerebro (el cerebro es privado; la web, pública).
2. En la app de Claude: **Code** › **Local** › **Open folder…** › `web-[TU-EMPRESA]`.

**Tenés que ver:** Code abierto con `web-[TU-EMPRESA]` como carpeta.

## Paso 2 · Que Claude analice la referencia

```prompt
Quiero hacer la web de mi empresa usando la ESTRUCTURA de esta web: [URL-DE-REFERENCIA]
1. Entrá a sus páginas principales y escribí analisis-referencia.md: secciones del inicio en orden y para qué sirve cada una, orden de los argumentos, todos los botones de llamado a la acción y qué hace bien para generar confianza.
2. No copies textos, imágenes ni marcas. Solo estructura y lógica.
3. Leé mi cerebro en Documentos/cerebro-[TU-EMPRESA] (CLAUDE.md, negocio/, marca/) y agregá "Cómo la adaptamos a nosotros": qué secciones tomamos, sacamos y agregamos.
Mostrame el plan antes de escribir código.
```

Aprobá los permisos para entrar a la web y leer el cerebro.

**Tenés que ver:** `analisis-referencia.md` y un plan de secciones. Corregí lo que no te cierre ("sacá la sección de equipo").

## Paso 3 · Que arme tu web

```prompt
Armá la web con ese plan, en Astro y estática.
- Textos de mi cerebro, con la voz de marca/voz.md. Si falta un dato, poné [PENDIENTE: qué falta] y anotalo en pendientes-web.md. No inventes precios, testimonios ni cifras.
- Colores, tipografías y logo de marca/. Pensada primero para el celular.
- Páginas: inicio, una por servicio, preguntas frecuentes y contacto. Botón de WhatsApp a [TU-NÚMERO-CON-CÓDIGO-DE-PAÍS].
- Formulario de contacto (nombre, WhatsApp o email, mensaje), todavía sin guardar.
Instalá lo necesario, levantá la vista previa y abrímela en el navegador.
```

**Tenés que ver:** tu web en el navegador, en una dirección tipo `http://localhost:4321`. Pedí cambios en lenguaje normal: "el título es muy largo".

> **Tip:** para usar tus fotos, arrastralas a una carpeta `imagenes/` dentro de `web-[TU-EMPRESA]` y pedí "usá las fotos de imagenes/".

## Paso 4 · Creá la tabla de consultas en Supabase (vos, en la web)
En [supabase.com](https://supabase.com), en tu proyecto: **SQL Editor**, pegá esto y tocá **Run**. Crea la tabla y la regla: desde la web **solo se puede agregar**, nadie puede leer.

```sql
create table public.consultas (
  id uuid primary key default gen_random_uuid(),
  creada_en timestamptz not null default now(),
  nombre text not null check (char_length(nombre) between 2 and 120),
  contacto text not null check (char_length(contacto) between 5 and 160),
  mensaje text check (char_length(mensaje) <= 2000),
  pagina text
);
alter table public.consultas enable row level security;
grant insert on table public.consultas to anon;
create policy "La web solo puede agregar consultas"
on public.consultas for insert to anon with check ( true );
```

Dejá abierta la pestaña: en **Settings › API Keys** está la **Publishable key** (`sb_publishable_…`) y en el botón **Connect**, la URL del proyecto.

**Tenés que ver:** en **Table Editor**, la tabla `consultas` vacía, con RLS activado.

> **Ojo:** la **Secret key** (`sb_secret_…`) nunca va en la web, ni en GitHub, ni en el chat.

## Paso 5 · Conectá el formulario

```prompt
Conectá el formulario a la tabla consultas de Supabase (columnas nombre, contacto, mensaje, pagina) con @supabase/supabase-js y las variables PUBLIC_SUPABASE_URL y PUBLIC_SUPABASE_PUBLISHABLE_KEY. Insert sin .select(). Validá los campos, mostrá "¡Gracias! Te respondemos a la brevedad" y sumá un campo trampa oculto contra spam.
Creá el archivo .env con las dos variables vacías, asegurate de que .env esté en .gitignore, creá .env.example sin valores y abrime .env en el editor de texto de mi compu. No leas ni me muestres su contenido después.
```

En la ventana que se abre, pegá después de cada `=` la URL y la Publishable key del Paso 4. Guardá, cerrá y escribile a Claude "listo, reiniciá la vista previa". Mandá un mensaje de prueba desde el formulario.

**Tenés que ver:** en Supabase, **Table Editor › consultas**, la fila con tu mensaje.

> **Datos:** pedí solo lo necesario y poné debajo del botón: "Usamos tus datos solo para responder tu consulta".

## Paso 6 · Subila a GitHub con GitHub Desktop

```prompt
Revisá que .gitignore excluya .env, node_modules, dist y .DS_Store, y confirmame que ningún archivo que se va a subir tiene una clave.
```

En **GitHub Desktop**: **File › Add local repository** › `web-[TU-EMPRESA]`. Si dice que no es un repositorio, tocá la opción para **crear uno ahí**. Escribí "Web inicial" en el resumen, **Commit to main** y **Publish repository** (puede quedar privado).

**Tenés que ver:** el repo en [github.com](https://github.com), **sin** archivo `.env`.

> **Ojo:** el nombre de los botones de GitHub Desktop puede variar según la versión.

## Paso 7 · Publicala con Vercel (en la web)
1. En [vercel.com](https://vercel.com): **Add New… › Project** › buscá `web-[TU-EMPRESA]` › **Import**. Si no aparece, ajustá los permisos de GitHub con el link de esa pantalla.
2. En **Environment Variables**, cargá `PUBLIC_SUPABASE_URL` y `PUBLIC_SUPABASE_PUBLISHABLE_KEY` con los valores de tu `.env`.
3. **Deploy**.

**Tenés que ver:** tu web en una dirección tipo `web-[tu-empresa].vercel.app`.

> **Tip:** desde ahora, cada cambio: pedíselo a Claude, después **Commit** y **Push origin** en GitHub Desktop. En un minuto está online.

> **Costo:** el plan gratis de Vercel (**Hobby**) es para uso personal o no comercial ([términos](https://vercel.com/legal/terms), nov 2026). Para practicar alcanza; para dejar la web de tu empresa, Vercel **Pro** o **Cloudflare Pages**, cuyo plan gratis no tiene esa restricción ([Stack y costos](#r-stack-y-costos)).

**Alternativa, Cloudflare Pages:** en el panel de Cloudflare, **Workers & Pages › Create application › Pages › Connect to Git** › tu repo › framework Astro (build `npm run build`, salida `dist`) › las dos variables › **Save and Deploy**. Queda en `*.pages.dev`.

> **Ojo:** verificá en pantalla los nombres de los menús de Vercel y Cloudflare.

## Cómo sé que funcionó
Desde el celular, con datos móviles, abrí tu web y mandá el formulario con datos inventados ("Prueba Taller"). La fila aparece en Supabase. Después pedile a Claude: "Sin cambiar nada, ¿alguien desde la web podría LEER las consultas? Explicámelo en 3 líneas". La respuesta correcta: no, la única regla permite agregar.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude no puede entrar a la referencia | Elegí otra, o guardala desde el navegador (**Archivo › Guardar como**) en la carpeta y pedile que analice ese archivo. |
| `new row violates row-level security policy` | "Sacá el .select() del insert". |
| En Vercel el formulario no anda, en tu compu sí | Faltan las variables en Vercel (**Settings › Environment Variables**). Cargalas y hacé **Redeploy**. |
| GitHub Desktop quiere subir el `.env` | Pará. "Sacá .env del repo y agregalo a .gitignore". Si ya se subió, rotá la clave en Supabase. |

## Para seguir solo
- **SEO y "aparecer en ChatGPT":** pedí "Revisá la web para Google y asistentes de IA: título y descripción únicos por página, datos estructurados de negocio local y de preguntas frecuentes con mi cerebro, sitemap.xml y robots.txt". Commit y push.
- **Dominio propio:** comprá tu `.com.ar` en NIC Argentina y conectalo en **Settings › Domains** de Vercel.
- **Aviso por cada consulta:** con [n8n](#s6-n8n), que cada fila nueva te llegue por [Telegram](#s7-telegram).
