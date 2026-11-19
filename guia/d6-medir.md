---
titulo: "Desafío: medí y decidí con números"
bloque: Desafío
tiempo: 30 a 90 min
para: Todos
necesitas: p1-cerebro
cuentas_mvp: ""
cuentas_completa: s8-conectores-y-mcp, s14-meta-y-google
resultado: Un reporte con 3 números clave y 3 acciones armado desde tu planilla y, si invertís en publicidad, un equipo de agentes que te dice cuánto invertir, con tu aprobación.
---

"¿Estamos ganando plata?" Armar ese informe a mano lleva horas y no se hace. El desafío: que salga en minutos, simple, con qué decidir.

**En 30 segundos**
- **Cuánto tarda:** 30 min la MVP, 90 min la completa.
- **Por dónde empezar:** la **Versión MVP**, acá abajo. Solo necesitás la **pestaña Code** de la app de Claude y una planilla.

## Dos versiones: MVP y completa

| | MVP (hoy, rápido) | Completa |
|---|---|---|
| **Qué te llevás** | 3 números, qué cambió y 3 acciones, desde tu planilla. | Reporte automático cada lunes y Meta Ads con agentes (solo tocan si escribís APROBADO). |
| **Tiempo** | 30 min | 90 min |
| **Cuentas que necesitás** | Ninguna extra | [Conectores](#s8-conectores-y-mcp) · [Meta y Google](#s14-meta-y-google) |
| **Costo** | Tu plan de Claude | Tu plan de Claude; la inversión en anuncios es aparte |

### Versión MVP, paso a paso
1. **Bajá tu planilla.** En Google Sheets: **Archivo › Descargar › Valores separados por comas (.csv)**. ¿No tenés una? Pedile a Claude una de práctica con el prompt de [El reporte que llega solo](#p10-extras), Paso 4.

Mové ese archivo a una carpeta `datos` dentro de la carpeta de tu cerebro.

**Tenés que ver:** el archivo `.csv` dentro de `datos`.

2. **Pedí el reporte.** En la app de Claude, abrí la **pestaña Code**, elegí la carpeta de tu cerebro y pegá:

```prompt
Sos mi analista. Leé el archivo .csv de la carpeta datos/. Es una planilla de [VENTAS / LEADS / GASTOS / STOCK] de mi negocio. Dame:
1. Los 3 números más importantes de la última semana, comparados con la anterior.
2. Qué cambió y por qué podría ser (decí si es una suposición).
3. 3 acciones concretas para esta semana.
Lenguaje simple, máximo media página. Si falta un dato o algo no cierra, decilo. No inventes números.
```

**Tenés que ver:** 3 números, una explicación corta y 3 acciones.

3. **Chequeá un número a mano.** Elegí uno del reporte y buscalo en tu planilla.

**Tenés que ver:** coincide. Si no, pedile a Claude que muestre la cuenta.

4. **Guardalo como receta.** En la misma pestaña Code, pegá:

```prompt
Convertí el pedido del reporte en una skill de este proyecto llamada mi-reporte: que lea el .csv más nuevo de datos/ y arme el mismo reporte, con las mismas reglas.
```

**Tenés que ver:** en una sesión nueva, `/mi-reporte` te arma el reporte. Cada lunes, ponés la planilla nueva en `datos` y lo escribís.

### Versión completa
El reporte que corre solo cada lunes: [El reporte que llega solo](#p10-extras), Parte B ([Tareas programadas](#t4-tareas-programadas)). Cuánto invertir en Meta: [Meta Ads con agentes](#p9-meta-ads).

Arrancá por la MVP. Si te sobra tiempo, pasá a la completa: lo que hiciste te sirve.

## Lo lograste si…
- [ ] Tenés un reporte con 3 números clave y 3 acciones concretas.
- [ ] Chequeaste un número a mano y coincide.
- [ ] El pedido quedó guardado como skill (`/mi-reporte`) para el próximo lunes.
- [ ] Sabés qué vas a hacer distinto esta semana.

## Ideas por tipo de negocio
Ejemplos inventados:
- **Producción y reparto:** costo por unidad, margen por producto y comparación con el mes anterior.
- **Venta consultiva:** leads que entraron, cuántos se contactaron y cuántos llegaron a reunión.
- **Coaching o formación:** cuánto invertir por campaña para llegar a una meta de ventas.

> **Datos:** tus métricas son información de tu negocio. No las pegues en grupos ni en herramientas que no conocés.

## Pedí ayuda a la mesa cuando…
- Los números del reporte no coinciden con tu planilla.
- La tarea programada no corrió.
