---
titulo: "Una app en Lovable + tu calendario de contenido"
bloque: Tutorial
tiempo: "50 a 60 min (Parte A 30 min, Parte B 20 a 30 min)"
para: Denvet, Fondus, Manuel Martínez Oratoria, Celve (y cualquiera que quiera una app o programar contenido)
necesitas: p1-cerebro, s1-claude, s2-claude-code, s8-conectores-y-mcp
resultado: Una app interna tuya funcionando en un link de Lovable, con login, y dos semanas de publicaciones escritas por Claude con tu voz y cargadas en Metricool para que las revises.
---

Es la versión completa del [D3](#d3-web-app) (Parte A) y del [D4](#d4-contenido) (Parte B): hoy hacé primero la MVP; esto es para si te sobra tiempo. Las dos partes se hacen por separado. **A:** una app con login, roles y datos que se guardan (el control de maples de Denvet, un mini CRM de leads para Fondus). **B:** Claude lee tu cerebro, arma el calendario y lo deja **en Metricool para que lo apruebes**.

## Antes de empezar
- [ ] Tu cerebro armado ([Tu cerebro](#p1-cerebro)).
- [ ] La app de escritorio de Claude con la pestaña **Code** ([S2 · Claude Code en la pestaña Code](#s2-claude-code)).
- [ ] Parte A: cuenta en [lovable.dev](https://lovable.dev) ([Cuentas en la nube](#s5-cuentas-nube), Paso 4).
- [ ] Parte B: cuenta en [metricool.com](https://metricool.com) con tu marca y tus redes conectadas.

> **Datos:** en la app de práctica, datos inventados. Con leads o alumnos reales, son datos personales: login obligatorio.

## Parte A · Tu app en Lovable

## Paso A1 · Elegí la app en una frase
Una tarea que hoy vive en papel, en WhatsApp o en una planilla desordenada. Ejemplos: control diario de maples (la granja carga producción, roturas y conteo; la app calcula el stock), mini CRM de leads (cada lead con estado, quién lo tiene y cuándo volver a escribirle), portal de alumnos (cada uno ve sus encuentros y su feedback).

**Tenés que ver:** una frase: quién usa la app, qué carga y qué quiere ver.

## Paso A2 · Que Claude escriba el prompt desde tu cerebro
En la app de Claude: **Code** › **Local** › **Open folder…** › `cerebro-[TU-EMPRESA]`. Pegá:

```prompt
Quiero una app interna en Lovable: [TU-FRASE-DEL-PASO-A1].
Leé mi cerebro (CLAUDE.md, operacion/, equipo/ y marca/) y escribí UN prompt para Lovable, en español, con: qué es y para quién; roles y qué puede hacer cada uno; pantallas una por una; tablas con sus campos y cómo se relacionan; cálculos automáticos; login con email, pensada para el celular; mis colores y tipografías; 10 registros de ejemplo INVENTADOS.
Si no sabés algo de mi operación, preguntame antes (máximo 5 preguntas). Guardalo en apps/[NOMBRE-DE-LA-APP]/prompt-lovable.md y mostramelo.
```

**Tenés que ver:** el prompt en pantalla y en `prompt-lovable.md`.

## Paso A3 · Creá la app en Lovable
Entrá a [lovable.dev](https://lovable.dev), pegá el prompt en la caja principal y envialo. Si te pide activar **Cloud** (base de datos y login), aprobalo: no hace falta crear nada en Supabase.

**Tenés que ver:** la app funcionando en la vista previa, con los datos de ejemplo.

## Paso A4 · Iterá de a un cambio por mensaje
Cada mensaje gasta créditos: un pedido claro por vez. Probala como si fueras el usuario y pedí, por ejemplo:

```prompt
Revisá la seguridad: que sin login no se vea ninguna pantalla ni dato, y que solo el dueño pueda editar la configuración. Explicame en 3 líneas cómo quedó.
```

**Tenés que ver:** cada cambio aplicado. Si algo se rompe: "Volvé a como estaba antes del último cambio".

## Paso A5 · Publicala
Tocá **Publish**. Queda en una dirección `*.lovable.app`. Los cambios posteriores se publican con **Publish changes**.

**Tenés que ver:** la app abierta en tu celular, pidiendo login.

> **Ojo:** el link lo abre cualquiera que lo tenga: por eso el login. Revisá en el menú de **Publish** si tu plan permite restringir el acceso.

## Parte B · Tu calendario con Metricool

## Paso B1 · Conectá Metricool a Claude
En la app de Claude: **Customize › Connectors**, buscá **Metricool**, **Connect**, iniciá sesión y **Grant access**. El conector aparece también en la pestaña **Code** (misma cuenta).

**Tenés que ver:** Metricool como **Connected**.

> **Ojo:** para conectar Instagram dentro de Metricool, la cuenta tiene que ser **profesional** y Meta te puede pedir un código. Si no se conecta hoy, igual hacé el Paso B2.

> **Costo:** el plan gratis de Metricool permite 20 publicaciones programadas por mes ([precios](https://metricool.com/pricing/), nov 2026; verificar en la web oficial). Para 2 semanas alcanza.

## Paso B2 · Que Claude arme el calendario
En **Code**, con la carpeta del cerebro abierta:

```prompt
Armá el calendario de contenido de 2 semanas desde el [FECHA-DE-INICIO].
1. Leé marca/voz.md, negocio/cliente-ideal.md, ventas/objeciones.md y ventas/preguntas-frecuentes.md.
2. Con Metricool, mirá mis mejores días y horarios en Instagram y lo que ya tengo programado, para no pisarlo.
3. [CANTIDAD] publicaciones por semana: una objeción respondida, cómo trabajamos, una prueba que YA esté en mi cerebro (nada inventado) y una invitación a escribirnos.
4. Para cada una: fecha y hora, red, formato, texto completo en mi voz y qué imagen o video hace falta.
5. Guardalo en contenido/calendario-[AAAA-MM].md y mostramelo. Todavía no cargues nada.
```

**Tenés que ver:** la tabla en pantalla. Corregí lo que no suene a vos: "el del martes está muy formal".

## Paso B3 · Cargalo para revisión

```prompt
Cargá en Metricool las publicaciones que aprobé, para revisión (no publicadas directo), en sus fechas y horarios. Si falta la imagen, cargala igual y anotá "falta subir el archivo". Al final, listame qué quedó cargado.
```

**Tenés que ver:** en el **Planificador** de Metricool, las publicaciones pendientes de tu revisión. Las imágenes las subís vos al revisar ([Placas en tu voz](#p10-extras)).

## Cómo sé que funcionó
- La app abre desde tu celular, pide login y guarda lo que cargás.
- En Metricool ves dos semanas de publicaciones con tus textos.
- En Code: "Con Metricool, decime qué tengo programado la semana que viene y si algún texto usa palabras que mi cerebro dice que no usamos".

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Lovable armó algo distinto | No pidas todo de nuevo: señalá una sola cosa a cambiar. |
| Se terminaron los créditos de Lovable | Se renuevan por día y por mes. Mientras, afiná el pedido en Claude. |
| Metricool no aparece en el directorio | **Customize › Connectors › Add › Add custom connector**, nombre `Metricool`, URL `https://ai.metricool.com/mcp`. |
| Claude no ve Metricool en Code | Abrí una sesión nueva en Code. Revisá que sea la misma cuenta de Claude. |
| Claude publicó en vez de dejar para revisión | Editala o borrala en Metricool. La próxima, pedí que te muestre el listado antes de cargar. |

## Para seguir solo
- **Una app por mes:** cada planilla que nadie entiende es candidata. Arrancá siempre por el Paso A2.
- **Rutina del lunes:** en Code, **Scheduled**, una tarea que cada lunes arme el calendario y te lo deje para revisar ([Tareas programadas](#t4-tareas-programadas)).
- **Publicar sin intermediarios:** con una app propia en Meta for Developers y la API de Instagram. Más control, más mantenimiento (tokens, revisión de Meta). Metricool sigue siendo el camino recomendado.
