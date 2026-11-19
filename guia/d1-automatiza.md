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
- **Por dónde empezar:** la **Versión MVP**, acá abajo. Solo necesitás Claude.

## Dos versiones: MVP y completa

| | MVP (hoy, rápido) | Completa |
|---|---|---|
| **Qué te llevás** | De foto a tabla en un chat de Claude, guardado como receta. | Una carpeta entera procesada, y un bot de Telegram que anota tus tickets. |
| **Tiempo** | 30 min | 90 min o más |
| **Cuentas que necesitás** | Solo Claude ([Tu cuenta](#s1-claude)) | [n8n](#s6-n8n) · [Telegram](#s7-telegram) · [Clave de API](#s9-api-anthropic) · [Google](#s14-meta-y-google) |
| **Costo** | Tu plan de Claude, nada extra | n8n desde €20/mes ([precios](https://n8n.io/pricing/), nov 2026) + centavos de API |

### Versión MVP, paso a paso
1. **Juntá 3 documentos de prueba** del mismo tipo: fotos o PDF de remitos, tickets o cartas. Tapá datos de clientes.

2. **Pasalos a tabla.** Abrí un chat nuevo en Claude, adjuntá los 3 archivos y pegá:

```prompt
Te paso 3 documentos de [QUÉ SON: remitos, tickets, cartas]. Pasalos a una tabla con estas columnas: [COLUMNAS, por ejemplo: fecha, proveedor, concepto, total]. Una fila por documento.
Si un dato no se lee o no estás seguro, no lo inventes: dejalo vacío y agregá una columna "revisar" con el motivo.
Al final, dame la misma tabla separada por tabulaciones, para pegarla en Google Sheets.
```

**Tenés que ver:** una tabla con 3 filas y lo dudoso marcado en "revisar".

3. **Pegala en tu planilla.** Copiá la tabla separada por tabulaciones y pegala en la celda A1 de una hoja nueva de Google Sheets.

**Tenés que ver:** cada dato en su columna.

4. **Guardalo como receta.** Creá un **Proyecto** en Claude (por ejemplo, "Carga de tickets") y pegá el prompt del paso 2 en sus instrucciones. La próxima vez, solo adjuntás las fotos.

> **Ojo:** verificá en pantalla dónde se cargan las instrucciones del Proyecto ([Dónde trabajar](#t3-donde-trabajar)).

**Tenés que ver:** un chat nuevo dentro del Proyecto que, con 1 foto y sin prompt, te devuelve la fila.

### Versión completa
Una carpeta entera a planilla con la skill `extraer-a-tabla`: [De foto a planilla](#p4-foto-a-tabla). Un bot que anota tus gastos: [Tu asistente en Telegram](#p2-asistente-telegram) (o, sin clave de API, el patrón de la MVP del [D2](#d2-agente)).

Arrancá por la MVP. Si te sobra tiempo, pasá a la completa: lo que hiciste te sirve.

## Lo lograste si…
- [ ] Pasaste 3 documentos y salieron 3 filas correctas.
- [ ] Lo dudoso quedó marcado para revisar, no cargado en silencio.
- [ ] El prompt quedó guardado en un Proyecto para repetirlo.
- [ ] Sabés cuánto tardabas antes y cuánto tardás ahora.

## Ideas por tipo de negocio
Ejemplos inventados:
- **Producción y reparto:** la foto del remito en papel pasa a una fila de ventas.
- **Marketplace o app:** la carta de un restaurante pasa a una tabla de platos con su etiqueta "sin TACC" o "vegano".
- **Venta consultiva:** la solicitud escaneada pasa a los campos del sistema y avisa si falta alguno.

## Pedí ayuda a la mesa cuando…
- n8n o Telegram te piden un **token** (la clave de tu bot) o un **chat ID** (el número de tu chat) y no sabés cuál.
- Llevás 15 minutos trabado en el mismo paso. Levantá la mano.
