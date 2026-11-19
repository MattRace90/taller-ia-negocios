---
titulo: Tu cuenta y la app de Claude
bloque: Setup
tiempo: 20 min
para: Todos
necesitas: nada
resultado: Cuenta de Claude con plan Pro (o superior), la app de escritorio instalada y sabés dónde está cada cosa.
---

Todo el taller pasa por Claude. Con el plan gratis podés chatear, pero Claude Code, Cowork y las skills necesitan un plan pago (**Pro** o superior).
Si en tu empresa van a usarlo varias personas, cada una necesita su propia cuenta.

## Antes de empezar
- [ ] Un mail al que tengas acceso desde el celular (te llega un código).
- [ ] Una tarjeta que acepte pagos en dólares, para el plan Pro (USD 20/mes, nov 2026). Detalle en [Stack y costos](#r-stack-y-costos). Si la tarjeta es de la empresa, que la cargue quien la maneja: nunca pegues números de tarjeta en un chat.

## Paso 1 · Creá la cuenta (o entrá a la tuya)
1. Abrí tu navegador (Chrome, Safari o Edge), escribí **[claude.ai](https://claude.ai)** en la barra de arriba y apretá **Enter**.
2. Tocá **Sign up** (o **Continue with Google**, si tu mail es de Gmail). Si no usás Google, escribí tu mail y tocá el botón para continuar.
3. Si elegiste mail: abrí tu correo, buscá el mail de Anthropic y copiá el código (o tocá el link) que te llega.
4. Si te pide tu nombre y para qué lo vas a usar, completalo.

**Tenés que ver:** la pantalla de chat de Claude con tu nombre abajo a la izquierda.

## Paso 2 · Pasate a Pro

> **Ojo:** muchas tarjetas de débito y algunas corporativas rechazan pagos en dólares, y a veces el banco pide aprobar la compra con un código por SMS o en su app. Tené el celular a mano. Si la tarjeta no pasa, no te trabes: avisá en la mesa de ayuda y seguí en dupla con alguien de tu empresa mientras lo resuelven.

1. Abajo a la izquierda, tocá tu nombre › **Settings › Billing** (o el botón **Upgrade**).
2. Elegí **Pro** y pagá con tarjeta.

> **Costo:** Pro alcanza para el taller y para el uso diario de una persona. Si en el taller te quedás sin uso, avisanos: te mostramos cómo ver tu consumo con `/usage`.

**Tenés que ver:** en **Settings › Billing** figura tu plan como **Pro**.

## Paso 3 · Instalá la app de escritorio
Descargá la app desde **[claude.ai/download](https://claude.ai/download)**.

> **Ojo:** si el wifi del salón está lento y la descarga no avanza, seguí en **[claude.ai](https://claude.ai)** desde el navegador (Chat y Projects andan igual) y bajá la app en el próximo corte. Si la compu es de la empresa y no te deja instalar programas (te pide una clave de administrador que no tenés, o el antivirus lo bloquea), pedí ayuda a la mesa.

<div data-os="mac">

1. Abrí el archivo `.dmg` (está en **Descargas**) y arrastrá **Claude** a **Aplicaciones**.
2. Abrila desde **Aplicaciones** (o con **Cmd+Espacio** y escribiendo "Claude"). Si macOS pregunta si querés abrir una app descargada de internet, tocá **Abrir**.
3. Iniciá sesión con la misma cuenta.

</div>
<div data-os="win">

1. Abrí el instalador `.exe` (está en **Descargas**) y seguí los pasos. Si tu compu tiene procesador ARM (por ejemplo, algunas Surface), descargá la versión ARM64. Si Windows pregunta si permitís que la app haga cambios, tocá **Sí**.
2. Abrí **Claude** desde el menú Inicio.
3. Iniciá sesión con la misma cuenta.

</div>

**Tenés que ver:** la app abierta, con tu cuenta, y arriba de la barra lateral las pestañas **Chat**, **Cowork** y **Code**. En algunas versiones nuevas, Chat y Cowork están juntos y se eligen en el cuadro de mensaje: también está bien.

## Paso 4 · Recorrido: dónde está cada cosa
| Dónde | Qué es | Para qué lo vas a usar hoy |
|---|---|---|
| **Chat** | Conversación con Claude | Preguntas sueltas, borradores |
| **Projects** | Carpetas de chats con conocimiento fijo | Subir tu cerebro para usarlo desde el celular |
| **Cowork** | Un agente que trabaja con los archivos de tu compu | Ordenar carpetas, armar documentos y planillas |
| **Code** | Claude Code dentro de la app | Todo lo técnico del taller, sin terminal |
| **Customize › Skills** | Tus procesos escritos | Instalar las skills del taller en la app |
| **Customize › Connectors** | Conexiones con Drive, Gmail, Calendar, Canva y más | [Conectores](#s8-conectores-y-mcp) |
| **Settings › Capabilities** | Permisos de Claude | Activar **Code execution and file creation** (las skills lo necesitan) |

Hacé ahora el último punto de la tabla:
1. Abajo a la izquierda, tocá tu nombre › **Settings**.
2. Entrá a **Capabilities**.
3. Activá el interruptor **Code execution and file creation**.

**Tenés que ver:** el interruptor de **Code execution and file creation** encendido (de color).

> **Datos:** en **Settings › Privacy** revisá si tus chats se usan para mejorar los modelos y elegí lo que prefieras. De todas formas, la regla del taller es no pegar datos personales de tus clientes.

## Paso 5 · Tu primer pedido con contexto
Probá la diferencia entre un pedido pelado y uno con contexto:

```prompt
Escribí un mensaje para un cliente que preguntó el precio y no respondió más.
```

Y ahora:

```prompt
Tengo [TU NEGOCIO, por ejemplo una escuela de oratoria en Córdoba]. Mi cliente es [QUIÉN]. Un interesado preguntó el precio de [PRODUCTO] hace 3 días y no respondió más. Escribí un mensaje de WhatsApp corto, cálido, sin presionar, que le haga una sola pregunta. Antes de escribirlo, haceme 3 preguntas si te falta algo.
```

Reemplazá lo que está entre corchetes con tus datos (los corchetes también se borran).

**Tenés que ver:** la segunda respuesta es mucho más útil. Esa diferencia es lo que vamos a guardar en tu cerebro.

## Cómo sé que funcionó
- Plan **Pro** activo, la app abierta con las pestañas **Chat**, **Cowork** y **Code**, y **Code execution and file creation** activado.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| No veo la pestaña **Code** ni **Cowork** | Revisá que el plan sea Pro o superior y actualizá la app (menú de la app › buscar actualizaciones). |
| La tarjeta es rechazada | Probá con otra tarjeta o desde la web (claude.ai). Algunas tarjetas de débito no funcionan para pagos en dólares. |
| No me llega el código por mail | Revisá spam o usá **Continue with Google**. |

## Para seguir solo
- Creá un **Project** por área (ventas, contenido, administración) y subí los archivos del cerebro que correspondan.
- Instalá la app de Claude en el celular para usar tus Projects desde cualquier lado.
- Mirá **Customize › Connectors** y conectá tu Google Drive ([Conectores](#s8-conectores-y-mcp)).
