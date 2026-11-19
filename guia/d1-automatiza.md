---
titulo: "Desafío: automatizá una tarea que hoy hacés a mano"
bloque: Desafío
tiempo: 30 a 90 min
para: Todos
necesitas: p1-cerebro
resultado: Una tarea repetitiva (cargar datos, armar un documento, anotar un gasto) que ahora hace Claude y vos solo revisás.
---

Todas las empresas tienen esa tarea que nadie quiere hacer: pasar papeles a una planilla, anotar gastos, armar el mismo documento por décima vez. No es difícil, pero come horas y se cuelan errores.
El desafío: elegí **una** de esas tareas y dejala resuelta hoy. La regla de siempre: **la IA propone, una persona aprueba.**

**En 30 segundos**
- **Qué te llevás:** una tarea repetitiva (cargar datos, anotar gastos) que ahora hace Claude. Vos solo revisás.
- **Cuánto tarda:** 30 min el camino Rápido, 90 min el Completo.
- **Por dónde empezar:** si es tu primera vez, abrí [De foto a planilla](#p4-foto-a-tabla) y seguí el Paso 1.

## Qué problema resuelve
- Carga manual de datos desde fotos, PDF o capturas (remitos, cartas, tickets, formularios).
- Gastos que se anotan tarde o nunca.
- Tareas que dependen de una sola persona porque "solo ella sabe cómo se hace".

## Elegí tu camino

| Nivel | Qué hacés | Tutorial |
|---|---|---|
| **Rápido · 30 min** | Una carpeta donde tirás fotos o PDF y Claude te devuelve una planilla limpia, con lo dudoso separado para que lo revises. | [De foto a planilla](#p4-foto-a-tabla) |
| **Completo · 90 min** | Un asistente en Telegram: le mandás la foto de un ticket y lo anota en tu planilla; le pasás lo que hablaste en una llamada y te devuelve el documento armado. | [Tu asistente en Telegram](#p2-asistente-telegram) |
| **Pro · para después** | Que funcione solo: los archivos que caen en una carpeta de Drive se procesan sin que lo pidas y te llega un resumen. | [n8n](#s6-n8n) + [Tareas programadas](#t4-tareas-programadas) |

> **Tip:** si nunca automatizaste nada, hacé el Rápido. Si te sobra tiempo, seguí con el Completo: usan la misma lógica.

## Qué cuentas necesitás
- [ ] Claude con plan Pro o superior ([Tu cuenta](#s1-claude)) y Claude Code ([Claude Code](#s2-claude-code)). Alcanza para el Rápido.
- [ ] Para el Completo: n8n, el programa que une apps sin programar ([n8n](#s6-n8n)); un bot de Telegram ([Telegram](#s7-telegram)); una clave de API, que es la llave para que otros programas usen Claude ([Clave de API](#s9-api-anthropic)); y tu Google conectado ([Meta y Google](#s14-meta-y-google)).
- [ ] Si te perdés con tantas cuentas: [la checklist de todo](#s10-conectar-todo).

## Lo lograste si…
- [ ] Le pasaste 3 documentos reales (o de prueba) y salieron 3 filas correctas en la planilla.
- [ ] Lo dudoso quedó separado o marcado para revisar, no cargado en silencio.
- [ ] Sabés cuánto tardabas antes y cuánto tardás ahora con esa tarea.
- [ ] Alguien más del equipo podría usarlo sin que se lo expliques.

## Ideas por tipo de negocio
Ejemplos inventados, para que te des una idea:
- **Producción y reparto:** la foto del remito en papel pasa a una fila de ventas, y se ve qué remitos faltan cargar.
- **Marketplace o app:** la carta de un restaurante (foto o PDF) pasa a una tabla de platos con su etiqueta "sin TACC" o "vegano".
- **Venta consultiva (planes, seguros, inmobiliaria):** la solicitud escaneada pasa a los campos del sistema, y avisa si falta alguno.
- **Escuela o cursos:** cada video de alumno se renombra y se guarda en su carpeta (está en el [tutorial de video](#p7-video), Parte 2).
- **Agencia de viajes o servicios:** el ticket de un gasto del viaje de un grupo se anota solo desde el celular.
- **Cualquier negocio:** los comprobantes del mes pasan a una planilla de gastos por categoría.

> **Datos:** para practicar, usá documentos de prueba o tapá nombres, DNI y teléfonos de clientes antes de sacar la foto.

## Pedí ayuda a la mesa cuando…
- Claude Code no arranca o no encuentra tu carpeta.
- n8n o Telegram te piden algo que no entendés. Por ejemplo: un **token** (una clave larga que identifica a tu bot), un **webhook** (la dirección a la que un servicio le avisa a otro que pasó algo) o un **chat ID** (el número de tu chat de Telegram).
- Llevás 15 minutos trabado en el mismo paso. No lo pelees solo: levantá la mano.
