---
titulo: Taller Intensivo de IA para Negocios
bloque: Inicio
tiempo: 10 a 18 h
para: Todos
necesitas: nada
resultado: Te vas con el cerebro de tu empresa en tu compu y en GitHub, tus herramientas conectadas, los desafíos que elegiste resueltos y las instrucciones de tu bot de WhatsApp escritas.
---

Esta guía es tu mapa del día y te queda para después. A la mañana armamos la base todos juntos. A la tarde **cada uno elige qué quiere resolver y cómo**, y nosotros te acompañamos en la mesa. Cerramos todos juntos con los bots de WhatsApp.

> **Tip:** **el cerebro** es una carpeta con archivos de texto donde queda escrito cómo funciona tu empresa (qué vendés, a quién, cómo hablás). Claude la lee antes de trabajar. **GitHub** es la web donde guardás una copia privada de esa carpeta, con historial. Las palabras técnicas del día están explicadas en una línea en [Las piezas](#t2-piezas).

## Lo primero que tenés que hacer
Hoy trabajamos en la **pestaña Code** de la app de Claude (no hace falta la terminal). Está arriba de la barra lateral de la app: **Chat · Cowork · Code**. Elegís la carpeta, escribís tu pedido y aprobás con **Permitir** cuando Claude quiere crear un archivo o correr algo.

1. Arriba de la guía, elegí tu sistema: **Mac** o **Windows**. Desde ahí, la guía te muestra solo los pasos de tu compu.
   **Tenés que ver:** el botón de tu sistema marcado.
2. Hacé las **cuentas obligatorias**, en este orden. Son las únicas que hace todo el mundo (si podés, hacelas antes del taller):
   - [ ] [S1 · Tu cuenta y la app de Claude](#s1-claude)
   - [ ] [S2 · Claude Code](#s2-claude-code)
   - [ ] [S3 · Git](#s3-herramientas-base) (de esa página, solo Git es obligatorio)
   - [ ] [S4 · GitHub](#s4-github)
3. Después, todos juntos: **tu cerebro** (obligatorio, de 12 a 13): [Armá tu cerebro](#p1-cerebro) y [Usá tu borrador](#c2-tu-borrador). Para verlo como un cuaderno con links está [Obsidian](#s11-obsidian): es **opcional**, lo mostramos en vivo y lo podés instalar en casa.
4. A la tarde **elegí tus desafíos: hasta 3, uno por ronda** (D1 a D6). En el [menú de desafíos](#inicio) de más abajo tocá **☆ Elegir** en cada uno y después **Ir a mis desafíos →**: ahí te quedan solo los tuyos. El cierre (D7, WhatsApp) no se elige: lo hacemos todos juntos. El índice de la izquierda te marca en verde **"Para vos"** las cuentas que vas a necesitar. Hacé solo esas, en el momento en que arrancás el desafío.
5. Las demás cuentas quedan en el índice, más clarito. No las necesitás hoy: están ahí para cuando quieras sumar otro desafío.

**Tenés que ver:** en el índice, el grupo **Cuentas obligatorias** con sus 4 pasos y, después de elegir, tus desafíos con una ★.

## La agenda
| Hora | Bloque | Qué hacemos |
|---|---|---|
| 10:00 | **Apertura** | Qué es un modelo y cuál usar, qué son los agentes, las skills, los conectores y los MCP, y dónde conviene trabajar: [Modelos](#t1-modelos) · [Las piezas](#t2-piezas) · [Dónde trabajar](#t3-donde-trabajar). No hace falta leerla ahora: queda para repasar. |
| 10:45 | **Atajos en vivo** | Los comandos de Claude Code que te ahorran tiempo, probados en pantalla: [Atajos](#t5-atajos). |
| 11:00 | **Cuentas y conexiones** | Cuentas, instalaciones y conectores, con mesa de ayuda. Empezá por [Tu cuenta de Claude](#s1-claude) y seguí la [checklist de todo](#s10-conectar-todo). |
| 12:00 | **Tu cerebro** | [Armá el cerebro de tu empresa](#p1-cerebro) y [usá el borrador que te preparamos](#c2-tu-borrador). |
| 13:00 | Almuerzo | |
| 13:45 | **Desafíos a elección · Ronda 1** | Elegí un desafío del menú (abajo) y arrancá por su versión **MVP**. |
| 14:30 | **Ronda 2** | Seguí con el mismo o pasá a otro. |
| 15:15 | Corte | |
| 15:25 | **Ronda 3** | Terminá lo que empezaste o sumá una MVP corta (35 min). |
| 16:00 | **Cierre: bots de WhatsApp** | Todos juntos: opciones, dos demos en vivo y las instrucciones de tu bot escritas desde tu cerebro: [Cierre: tu bot de WhatsApp](#d7-whatsapp). |
| 17:15 | **Tu plan de 30 días** | Qué seguís en casa, quién mantiene el cerebro y qué dejás programado: [Tareas programadas](#t4-tareas-programadas). |

## Cómo usar esta guía
- **Índice:** a la izquierda (en el celular, en el menú) están todas las páginas por bloque: Teoría, Cuentas y conexiones, Tu cerebro, Desafíos, Tutoriales, WhatsApp y Referencia.
- **Mac o Windows:** arriba elegís tu sistema operativo y la guía te muestra solo lo tuyo.
- **Casillas:** las `- [ ]` que tildás quedan guardadas en tu navegador. Si cambiás de compu o de navegador, empiezan vacías.
- **Botón Copiar:** cada prompt y cada comando tiene su botón. Copiá y pegá: no lo tipees a mano.
- **Lo que está [EN MAYÚSCULAS ENTRE CORCHETES]:** es un dato tuyo. Borralo **con los corchetes incluidos** y escribí tu dato. Ejemplo: `cerebro-[TU-EMPRESA]` queda `cerebro-fondus` (en minúsculas, sin espacios ni tildes).
- **"Tenés que ver:"** al final de cada paso te dice qué aparece en pantalla si salió bien. Si no lo ves, no sigas: mirá la tabla **Si algo falla** de esa página o levantá la mano.
- **Desafíos y tutoriales:** el desafío te dice qué resolver y te da 2 o 3 caminos. Cada camino te manda al tutorial con el paso a paso.
- **Tu ruta:** son los desafíos y tutoriales que elegís para la tarde. Algunas páginas de cuentas dicen "según tu ruta": conectá solo lo que vas a usar.

## El menú de desafíos
Cada uno elige. No hay un orden obligatorio: arrancá por el que más te duele hoy.

| Desafío | Qué resuelve | Tiempo | Ideal si… |
|---|---|---|---|
| [Automatizá una tarea](#d1-automatiza) | Cargar datos a mano: de foto o PDF a planilla, gastos, documentos repetidos | 30 a 90 min | Pasás horas copiando datos de papeles o capturas |
| [Un agente que responde](#d2-agente) | Las mismas 10 preguntas de siempre, y filtrar a quien no es cliente | 30 a 90 min | Te llegan muchas consultas y tardás en contestar |
| [Tu web o tu app](#d3-web-app) | No tener web, o llevar el control del negocio en papel | 30 a 90 min | No tenés presencia online o tu equipo necesita una herramienta propia |
| [Tu fábrica de contenido](#d4-contenido) | Publicar seguido, con tu voz, sin depender de una persona | 30 a 90 min | El contenido depende de vos o de la inspiración del día |
| [Vendé más](#d5-vender) | Propuestas que tardan y consultas que nadie recontacta | 30 a 90 min | Perdés ventas por demora o por falta de seguimiento |
| [Medí y decidí](#d6-medir) | Informes manuales y no saber cuánto invertir en publicidad | 30 a 90 min | Invertís en Meta o querés ver tus números sin armarlos a mano |
| [Cierre: tu bot de WhatsApp](#d7-whatsapp) | Qué bot te conviene y qué tiene que decir | 75 min | Es para todos, a las 16:00 |

> **Tip:** las 3 rondas suman unas 2 horas y media: alcanzan para 1 o 2 desafíos en nivel Completo, o 3 o 4 en nivel Rápido. Mejor uno terminado que tres a medias.

## Sugerencia por empresa
Es una sugerencia según lo que nos contaron. Podés cambiarla. En la página de tu empresa está el porqué.

| Empresa | Te sugerimos |
|---|---|
| [Fondus](#e-fondus) | [Un agente que responde](#d2-agente) · [Vendé más](#d5-vender) · [Medí y decidí](#d6-medir) |
| [La Consejera del Éxito](#e-consejera) | [Tu fábrica de contenido](#d4-contenido) · [Medí y decidí](#d6-medir) · [Vendé más](#d5-vender) |
| [Manuel Martínez Oratoria](#e-manuel) | [Automatizá una tarea](#d1-automatiza) · [Vendé más](#d5-vender) · [Tu web o tu app](#d3-web-app) |
| [Denvet](#e-denvet) | [Automatizá una tarea](#d1-automatiza) · [Tu web o tu app](#d3-web-app) · [Medí y decidí](#d6-medir) |
| [Celve](#e-celve) | [Automatizá una tarea](#d1-automatiza) · [Tu fábrica de contenido](#d4-contenido) · [Medí y decidí](#d6-medir) |
| [Viajes TDH Docta](#e-tdh) | [Un agente que responde](#d2-agente) · [Vendé más](#d5-vender) · [Tu fábrica de contenido](#d4-contenido) |
| [VetPlus](#e-vetplus) | [Un agente que responde](#d2-agente) · [Vendé más](#d5-vender) · [Medí y decidí](#d6-medir) |

## Llevate todo a tu compu
Esta guía queda online. Además podés bajarla entera (todas las páginas en `.md`, las skills y los agentes) y abrirla con Obsidian o con la pestaña Code de la app de Claude:

[Descargá la guía completa](kit/descargas/taller-completo.zip)

Descomprimí el ZIP en **Documentos** (en Mac, si bajaste con Safari, puede que ya esté descomprimido en **Descargas**: mové la carpeta a **Documentos**) y abrí la carpeta `taller-ia-para-negocios` como bóveda en [Obsidian](#s11-obsidian).

## Las 4 ideas del día
1. **La IA no sabe tu negocio.** Trabaja con lo que le das para leer. Por eso empezamos por el cerebro.
2. **Primero lo usás vos, después lo automatizás.** Nunca le des autonomía a algo que no viste funcionar.
3. **La IA propone, una persona aprueba.** Sobre todo cuando hay plata, salud o clientes de por medio.
4. **Tu cerebro es tuyo.** Son archivos en tu compu y en tu GitHub. Funcionan con Claude hoy y con cualquier IA mañana.

> **Datos:** nunca le pases a una IA contraseñas, claves, números de tarjeta o de cuenta, ni datos personales de tus clientes (DNI, salud, deudas). Para practicar, usá datos inventados. Cuando una página te dé una clave o un token, va **solo** al lugar que esa página indica (tu gestor de contraseñas, n8n, un archivo `.env`), nunca al chat ni a GitHub. Más en [Datos y seguridad](#t6-datos-y-seguridad).

## Quién te ayuda hoy
| Para… | Buscá a |
|---|---|
| Instalaciones, terminal, GitHub, conexiones, automatizaciones y bots | **Nuestro developer** (mesa técnica) |
| Contenido, placas, video y anuncios | **Fernando** |
| Tu cerebro, tus bonos (auditoría y análisis de competidores) y WhatsApp con la agencia | **Victoria** |
| Lo que no sepas a quién preguntar | **Mati** |

Victoria va a pasar por tu mesa, en el almuerzo o mientras esperás algo, con unas preguntas cortas para preparar tu auditoría y el análisis de tu competencia.

## Tus bonos
Esto suma el taller, además de la guía:

| # | Bono | Cuándo |
|---|---|---|
| 01 | **Auditoría profunda de tu negocio** | Te contactamos para coordinar la fecha. |
| 02 | **Análisis de competidores y mercado** | Te contactamos para coordinar la fecha. Ya tenemos la información de tu empresa: la investigación la hacemos nosotros después del taller. |
| 03 | **Curso de anuncios en Facebook** | Martes 8 de diciembre de 2026. |
| 04 | **Growth Marketing · 3 meses · UTN** | Empieza en febrero de 2027, cerca del 15. Te confirmamos la fecha por el grupo. |
| 05 | **Entrenamiento para delegar** | Domingo 7 de febrero de 2027. |

- [ ] Agendé el martes 8/12 y el domingo 7/2.
- [ ] Cuando me escriban para coordinar la auditoría y el análisis, respondo.
