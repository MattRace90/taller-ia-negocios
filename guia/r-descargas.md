---
titulo: Qué tiene cada descarga y cómo usarla
bloque: Referencia
tiempo: 5 min por descarga
para: Todos
necesitas: s2-claude-code
resultado: Sabés qué hay en cada ZIP, cuál te sirve y cómo dejarlo funcionando en tu compu.
---

Todas las descargas del taller están en una sola carpeta de Drive. No hace falta cuenta de Google para bajarlas.

[Abrí la carpeta de descargas](https://drive.google.com/drive/folders/1X5C1NtBXbjxZdh8FMy6JiupVl5S-3GgN)

Un **ZIP** es una carpeta comprimida: un solo archivo que adentro tiene muchos. Antes de usarlo hay que descomprimirlo.

## Las descargas de un vistazo
| Archivo | Qué es | Para quién | Peso |
|---|---|---|---|
| `taller-completo.zip` | Toda esta guía en archivos `.md`, más las skills y los agentes del taller | Todos | 0,3 MB |
| `fabrica-de-contenidos.zip` | 3 skills de contenido con instalador de doble clic: plan del mes, imágenes y edición de video | Quien eligió [D4 · Contenido](#d4-contenido) | 1 MB |
| `plan-b/` (8 ZIP) | Skills extra que usamos en la agencia, sin datos de clientes | Quien quiera ir más allá | 3 KB a 2 MB c/u |

## Antes de empezar
- [ ] Claude Code instalado ([S2](#s2-claude-code)).
- [ ] Sabés dónde se guardan tus descargas (normalmente la carpeta **Descargas**).

## Paso 1 · Bajá el ZIP
1. Abrí la [carpeta de descargas](https://drive.google.com/drive/folders/1X5C1NtBXbjxZdh8FMy6JiupVl5S-3GgN).
2. Hacé clic derecho sobre el archivo › **Descargar**. Si Google avisa que no puede revisar si tiene virus, tocá **Descargar de todas formas**: son archivos de texto y código nuestros.

**Tenés que ver:** el archivo `.zip` en tu carpeta **Descargas**.

## Paso 2 · Descomprimilo

<div data-os="mac">

Hacé doble clic en el ZIP. Aparece una carpeta con el mismo nombre al lado.

> **Ojo:** si bajaste con Safari, puede que ya lo haya descomprimido solo y veas directamente la carpeta. Está bien: seguí con esa.

</div>
<div data-os="win">

Clic derecho sobre el ZIP › **Extraer todo…** › **Extraer**. Aparece una carpeta con el mismo nombre.

> **Ojo:** no lo abras con doble clic para trabajar desde adentro: Windows te muestra el contenido, pero los programas no lo pueden usar hasta que lo extraés.

</div>

**Tenés que ver:** una carpeta normal (sin `.zip`) con archivos adentro.

## Paso 3 · Usalo según cuál sea

### taller-completo.zip · la guía en tu compu
**Qué tiene adentro:** la carpeta `taller-ia-para-negocios` con:
- `guia/`: todas las páginas de esta guía (teoría, cuentas, desafíos, tutoriales, WhatsApp);
- `kit/skills/`: las 8 skills del taller;
- `kit/agentes/`: los 5 agentes de Meta Ads;
- `kit/ejemplos/`: datos inventados para practicar;
- `LEEME.md`.

**Cómo se usa:**
1. Mové la carpeta `taller-ia-para-negocios` a **Documentos**.
2. Abrila en [Obsidian](#s11-obsidian) con **Abrir carpeta como bóveda**: la leés con formato, sin internet.
3. O abrí Claude Code parado en esa carpeta y pedile:

```prompt
Leé guia/inicio.md y guiame paso a paso por el desafío [NOMBRE DEL DESAFÍO]. Andá de a un paso y esperá que te diga "listo" antes de seguir.
```

### fabrica-de-contenidos.zip · tu fábrica de contenido
**Qué tiene adentro:** tres skills (plan-de-contenidos, imagenes-para-redes y video-para-redes), el instalador para Mac (`INSTALAR-Mac.command`), el de Windows (`INSTALAR-Windows.bat`) y una guía en PDF.

**Cómo se usa:** seguí el tutorial completo, que tiene el instalador y 3 ejercicios: [Fábrica de contenidos](#u-fabrica).

> **Ojo:** la fábrica edita video que ya grabaste: no genera video desde cero. Para video 100% con IA mirá [Herramientas creativas](#s12-creativas).

### plan-b · las skills de la agencia
Cada ZIP es **una skill**: una carpeta con un archivo `SKILL.md` (la receta que sigue Claude) y, a veces, scripts o referencias.

| ZIP | Qué hace | Necesita |
|---|---|---|
| `creador-angulos-publicitarios.zip` | Arma con vos, paso a paso, un ángulo de venta: público, dolor, mecanismo y promesa | Nada extra |
| `nomenclador-ads.zip` | Analiza un anuncio y le pone un nombre ordenado, para saber después qué rinde | Nada extra |
| `rediseno-9x16.zip` | Rediseña una placa cuadrada como historia o reel vertical, sin estirarla | Nada extra |
| `static-remix.zip` | Recrea anuncios ganadores de la competencia con tu producto y tu marca | Higgsfield (pago), ver [S12](#s12-creativas) |
| `estrategia-benchmark.zip` | Analiza y puntúa los anuncios de tu competencia en Meta y arma una presentación de estrategia | Python, ver [S3](#s3-herramientas-base) |
| `product-bible.zip` | Arma una carpeta por producto con ficha, colores, mensajes, reseñas e imágenes | Python |
| `frontend-design.zip` | Guía de diseño (de Anthropic) para que tus webs y landings no parezcan de plantilla | Nada extra |
| `animaciones.zip` | 20 estilos de animación en código para animar una escena de tu negocio | Node.js, ver [S3](#s3-herramientas-base) |

**Cómo se instala una skill del plan B:**
1. Descomprimí el ZIP (Paso 2).
2. Abrí Claude Code en cualquier carpeta y pegá este prompt. Para no escribir la ruta a mano, arrastrá la carpeta descomprimida a la ventana de la terminal: se pega sola.

```prompt
Instalá como skill personal la carpeta que está en [ARRASTRÁ ACÁ LA CARPETA DESCOMPRIMIDA]. Copiala entera, sin cambiar nada, a la carpeta de skills de mi usuario (~/.claude/skills/ en Mac; C:\Users\[MI-USUARIO]\.claude\skills\ en Windows). Revisá que adentro quede un SKILL.md y decime la ruta final.
```

3. Salí con `/exit`, volvé a entrar con `claude` y escribí `/skills`.

**Tenés que ver:** la skill nueva en la lista de `/skills`.

> **Tip:** para usarla en la app de Claude (web y celular), subí el ZIP **tal cual lo bajaste** en **Customize › Skills**. Antes activá **Settings › Capabilities › Code execution and file creation**. Más detalle en el [Kit](#r-kit).

## Cómo sé que funcionó
- La guía se abre en Obsidian o Claude Code te guía desde `guia/inicio.md`.
- `/skills` muestra la fábrica o las skills del plan B que instalaste.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Drive dice "no se puede analizar en busca de virus" | Es normal en archivos ZIP. Tocá **Descargar de todas formas**. |
| Mac: "no se puede abrir porque es de un desarrollador no identificado" | Es el instalador de la fábrica. Seguí el aviso de Gatekeeper del tutorial [Fábrica de contenidos](#u-fabrica). |
| Windows: el ZIP se abre pero los archivos "no están" | No lo extrajiste. Clic derecho › **Extraer todo…** |
| La skill no aparece en `/skills` | Revisá que la carpeta quedó en `~/.claude/skills/<nombre>/SKILL.md`, no anidada dos veces (`<nombre>/<nombre>/SKILL.md`). Pedíselo a Claude: "Fijate si mi skill [NOMBRE] quedó anidada y arreglala". |
| La app de Claude rechaza el ZIP | Subí el ZIP original, no uno que hayas vuelto a comprimir: adentro tiene que estar la carpeta de la skill. |

## Para seguir solo
- Cuando cambie la guía, volvé a bajar `taller-completo.zip` y reemplazá la carpeta.
- Guardá tus skills favoritas también en el repo de tu cerebro, en `.claude/skills/`, para que tu equipo las tenga.
- Pedile a Claude que adapte una skill a tu negocio: "Leé mi skill [NOMBRE] y adaptala a cómo trabajamos nosotros".
