---
titulo: "Desafío: automatizá una tarea que hoy hacés a mano"
bloque: Desafío
tiempo: 30 a 90 min
para: Todos
necesitas: p1-cerebro
cuentas_mvp: ""
cuentas_completa: s6-n8n, s7-telegram, s9-api-anthropic, s14-meta-y-google
resultado: Una tarea repetitiva (cargar datos, anotar un gasto) que ahora hace Claude y vos solo revisás.
---

Pasar papeles a una planilla, anotar gastos: come horas y se cuelan errores. Elegí **una** tarea y dejala resuelta hoy. **La IA propone, una persona aprueba.**

**En 30 segundos**
- **Cuánto tarda:** 30 min la MVP, 90 min la completa.
- **Por dónde empezar:** la **Versión MVP**, acá abajo. Solo necesitás la **pestaña Code** de la app de Claude.

## Dos versiones: MVP y completa

| | MVP (hoy, rápido) | Completa |
|---|---|---|
| **Qué te llevás** | De foto a tabla en la pestaña Code de Claude, guardado como skill (receta). | Una carpeta entera procesada, y un bot de Telegram que anota tus tickets. |
| **Tiempo** | 30 min | 90 min o más |
| **Cuentas que necesitás** | Solo Claude ([Tu cuenta](#s1-claude)) | [n8n](#s6-n8n) · [Telegram](#s7-telegram) · [Clave de API](#s9-api-anthropic) · [Google](#s14-meta-y-google) |
| **Costo** | Tu plan de Claude, nada extra | n8n desde €20/mes ([precios](https://n8n.io/pricing/), nov 2026) + centavos de API |

### Versión MVP, paso a paso
1. **Juntá 3 documentos de prueba** del mismo tipo: fotos o PDF de remitos, tickets o cartas. Tapá datos de clientes. Copialos a una carpeta `entrada` dentro de la carpeta de tu cerebro.

**Tenés que ver:** los 3 archivos dentro de `entrada`.

2. **Pasalos a tabla.** En la app de Claude, abrí la **pestaña Code**, elegí la carpeta de tu cerebro y pegá:

```prompt
Leé los 3 archivos de la carpeta entrada/. Son [QUÉ SON: remitos, tickets, cartas]. Pasalos a una tabla con estas columnas: [COLUMNAS, por ejemplo: fecha, proveedor, concepto, total]. Una fila por documento.
Si un dato no se lee o no estás seguro, no lo inventes: dejalo vacío y agregá una columna "revisar" con el motivo.
Mostrame la tabla acá y guardala como salidas/tabla.csv.
```

Cuando Claude pida permiso para crear el archivo, tocá **Permitir**.

**Tenés que ver:** una tabla con 3 filas, lo dudoso marcado en "revisar" y el archivo `salidas/tabla.csv` creado.

3. **Pasala a tu planilla.** En Google Sheets: **Archivo › Importar › Subir** y elegí `tabla.csv`.

**Tenés que ver:** cada dato en su columna.

4. **Guardalo como receta.** En la misma pestaña Code, pegá:

```prompt
Convertí lo que hicimos recién en una skill de este proyecto llamada carga-de-tickets: que lea los archivos nuevos de entrada/, los pase a la tabla con las mismas columnas y la regla de "revisar", y la guarde en salidas/ con la fecha de hoy en el nombre.
```

**Tenés que ver:** en una sesión nueva de la pestaña Code, escribís `/carga-de-tickets` con 1 foto nueva en `entrada` y te devuelve la fila.

### Versión completa
Una carpeta entera a planilla con la skill `extraer-a-tabla`: [De foto a planilla](#p4-foto-a-tabla). Un bot que anota tus gastos: [Tu asistente en Telegram](#p2-asistente-telegram) (o, sin clave de API, el patrón de la MVP del [D2](#d2-agente)).

Arrancá por la MVP. Si te sobra tiempo, pasá a la completa: lo que hiciste te sirve.

## Lo lograste si…
- [ ] Pasaste 3 documentos y salieron 3 filas correctas.
- [ ] Lo dudoso quedó marcado para revisar, no cargado en silencio.
- [ ] El pedido quedó guardado como skill (`/carga-de-tickets`) para repetirlo.
- [ ] Sabés cuánto tardabas antes y cuánto tardás ahora.

## Ideas por tipo de negocio
Ejemplos inventados:
- **Producción y reparto:** la foto del remito en papel pasa a una fila de ventas.
- **Marketplace o app:** la carta de un restaurante pasa a una tabla de platos con su etiqueta "sin TACC" o "vegano".
- **Venta consultiva:** la solicitud escaneada pasa a los campos del sistema y avisa si falta alguno.

## Pedí ayuda a la mesa cuando…
- n8n o Telegram te piden un **token** (la clave de tu bot) o un **chat ID** (el número de tu chat) y no sabés cuál.
- Llevás 15 minutos trabado en el mismo paso. Levantá la mano.
