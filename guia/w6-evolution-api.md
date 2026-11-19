---
titulo: "Tu bot de WhatsApp con Evolution API (código abierto)"
bloque: WhatsApp
tiempo: "2 a 3 horas para probarlo en tu compu. En un servidor (VPS): medio día más"
para: Equipos con alguien técnico que quieren todo propio y sin pagar plataforma
necesitas: s2-claude-code, s3-herramientas-base, s9-api-anthropic, w1-opciones
resultado: Evolution API corriendo en tu compu con Docker, un WhatsApp secundario conectado por QR y un bot mínimo que contesta con tu cerebro. Y sabés qué hace falta para pasarlo a un servidor y al modo oficial.
---

Evolution API es un programa **gratis y de código abierto** que conecta WhatsApp con bots y sistemas (n8n, Chatwoot, Typebot). Lo instalás vos, en tu compu o en un servidor, sin pagarle a ninguna plataforma. Tiene **dos modos**: por QR (no oficial, con riesgo de bloqueo) y **Cloud API** (oficial, con Meta).
Ejemplo: Denvet tiene a alguien de sistemas y quiere el bot de pedidos en su propio servidor. Lo prueba en una compu con un chip secundario y, si sirve, lo pasa al modo oficial.

> **Ojo:** **hoy en el taller** hacés la **Versión MVP** de [Cierre: tu bot de WhatsApp](#d7-whatsapp): las instrucciones de tu bot, probadas en Telegram con n8n. Esta página es para **después**. Todo lo técnico (Docker, el puente, el servidor) se lo pedís a Claude en la pestaña **Code**; las claves, nunca en el chat.

> **Ojo:** el modo QR (se llama **Baileys**) **no es oficial**. Si WhatsApp lo detecta, suspende el número y perdés sus chats. Solo con un número que no te importe perder. Para el número del negocio, el **modo Cloud API** (Paso 6).

> **Tip:** **Docker** es un programa que corre otros programas en "cajas" que traen todo lo que necesitan. Lo instalás una vez y Claude levanta Evolution API (con su base de datos) por vos. Una **instancia** es cada número conectado.

## Cuánto cuesta (nov 2026)
- **Evolution API:** gratis ([GitHub oficial](https://github.com/evolution-foundation/evolution-api)). Desde la versión 2.4.0 pide **activar la instancia** una vez con tu mail y teléfono; la licencia comunitaria es gratis ([licencia](https://docs.evolutionfoundation.com.br/licensing)).
- **Docker Desktop:** gratis para uso personal y empresas de menos de 250 empleados **y** menos de 10 millones de USD de facturación ([licencia](https://docs.docker.com/subscription/desktop-license/)).
- **Servidor (para usarlo de verdad):** un VPS de 2 GB, unos 11 a 12 USD por mes ([DigitalOcean](https://www.digitalocean.com/pricing/droplets) 12 USD; [Hetzner](https://www.hetzner.com/cloud/regular-performance/) 9,99 EUR).
- **Claude para el bot:** por uso; con Claude Haiku, del orden de 1 a 2 USD cada 1.000 mensajes ([Stack y costos](#r-stack-y-costos)).
- **Meta:** solo en modo Cloud API, por mensaje ([cómo se cobra](#w1-opciones)).

## Antes de empezar
- [ ] La app de Claude con la pestaña **Code** ([Instalá Claude Code](#s2-claude-code)) y Node.js ([Herramientas base](#s3-herramientas-base)).
- [ ] Clave de API de Anthropic con crédito ([API de Anthropic](#s9-api-anthropic)).
- [ ] Un **número secundario** con WhatsApp (chip nuevo). **Nunca** el principal.
- [ ] `bot/instrucciones-del-bot.md` de [Cierre: tu bot de WhatsApp](#d7-whatsapp) (o el prompt de [la práctica del agente](#p3-agente-preguntas)).
- [ ] Unos 5 GB libres en el disco.

## Paso 1 · Instalá Docker Desktop (con doble clic)
Descargalo de [docs.docker.com/get-started/get-docker](https://docs.docker.com/get-started/get-docker/).

<div data-os="mac">

Elegí según tu chip (menú **Apple › Acerca de esta Mac**: "Apple M…" = **Apple Silicon**; "Intel" = **Intel chip**). Abrí el `.dmg`, arrastrá Docker a **Aplicaciones**, abrilo y aceptá los permisos.

</div>
<div data-os="win">

Abrí el instalador, dejá tildado **WSL 2** y seguí. Si pide reiniciar, reiniciá. Abrí **Docker Desktop** desde el menú Inicio. Necesitás permisos de administrador.

</div>

Aceptá los términos; el inicio de sesión lo podés saltear.

**Tenés que ver:** en Docker Desktop, abajo a la izquierda, **Engine running**.

> **Ojo:** los nombres de las opciones del instalador cambian entre versiones: verificalos en pantalla.

## Paso 2 · Que Claude arme y arranque Evolution API
1. En la app de Claude, tocá **Code**, elegí **Local › Open folder…** y creá o elegí la carpeta `Documentos/evolution-api`.
2. Pegá:

```prompt
Quiero correr Evolution API en mi compu con Docker Desktop, para probar. Primero verificá que Docker esté andando. Antes de armar nada, leé el README oficial (https://github.com/evolution-foundation/evolution-api), su docker-compose.yaml y .env.example, y la guía de Docker (https://docs.evolutionfoundation.com.br/evolution-api/install/docker.md).
1. Armá un docker-compose.yml con Evolution API, PostgreSQL y Redis, basado en el oficial, con la última versión estable fija (no "latest" ni "rc").
2. Armá el .env con lo mínimo, SERVER_URL=http://localhost:8080 y una AUTHENTICATION_API_KEY larga al azar. No me la muestres. Sumá .env al .gitignore.
3. Que el puerto 8080 solo se abra en mi compu (127.0.0.1).
4. Explicame en simple qué es cada servicio y si la versión pide activar la licencia.
5. Arrancalo y decime cómo abrir el Manager.
```

**Tenés que ver:** `http://localhost:8080` en el navegador con la bienvenida de Evolution API, y el Manager en `http://localhost:8080/manager`.

> **Ojo:** desde la 2.4.0, la primera vez el Manager pide activar la instancia con tu mail y teléfono (gratis).

## Paso 3 · Creá la instancia y escaneá el QR
1. Pegá:

```prompt
Con la AUTHENTICATION_API_KEY del .env (sin mostrármela), creá la instancia "prueba" con integración Baileys y qrcode en true, y mostrame el QR para conectar como imagen.
```

2. En el celular del número secundario: **Configuración › Dispositivos vinculados › Vincular un dispositivo** (en Android, desde **⋮**) y apuntá al QR. Escanealo rápido: dura pocos segundos.

> **Tip:** también podés hacerlo desde el Manager. Para entrar, pedile a Claude que te abra el `.env` en el editor de texto y copiá la clave vos.

**Tenés que ver:** la instancia `prueba` como **open** o **connected**, y Evolution API en los **Dispositivos vinculados**.

## Paso 4 · El bot mínimo, en tu compu
Un "puente" recibe cada mensaje, le pregunta a Claude con tu cerebro y contesta. Todo en tu compu, sin publicar nada.

1. Pegá:

```prompt
Creá puente-bot/.env con las líneas ANTHROPIC_API_KEY= vacía, EVOLUTION_URL=http://localhost:8080, EVOLUTION_INSTANCIA=prueba y EVOLUTION_API_KEY con el valor de AUTHENTICATION_API_KEY del .env de Evolution (copialo sin mostrármelo). Sumalo al .gitignore y abrime puente-bot/.env en el editor de texto de mi compu para que pegue la clave de Anthropic.
```

2. Pegá tu clave de Anthropic después de `ANTHROPIC_API_KEY=`, guardá y escribile `listo`.
3. Cambiá `[RUTA-DE-TU-CEREBRO]` (por ejemplo `~/Documents/cerebro-fondus`) y pegá:

```prompt
En puente-bot armá un servidor chico en Node.js (puerto 3001) que haga de bot de WhatsApp con Evolution API, con las claves de puente-bot/.env sin mostrarlas. Antes, leé el formato del evento MESSAGES_UPSERT (https://docs.evolutionfoundation.com.br/evolution-api/configuration/webhooks.md) y cómo mandar texto (https://docs.evolutionfoundation.com.br/evolution-api/send-text-message.md).
- POST /webhook: 200 enseguida. Solo MESSAGES_UPSERT; ignorá mis propios mensajes (fromMe), grupos (@g.us), estados y repetidos.
- Si es texto, respondé con Claude Haiku usando como instrucciones [RUTA-DE-TU-CEREBRO]/bot/instrucciones-del-bot.md, con memoria de los últimos 10 mensajes por chat. Si es audio o foto, pedí que lo escriban.
- Contestá con /message/sendText esperando 3 a 8 segundos al azar. Si hay que derivar, escribilo en la consola con el motivo.
Configurá el webhook de la instancia "prueba" apuntando a http://host.docker.internal:3001/webhook con el evento MESSAGES_UPSERT. Arrancá el puente y dejalo corriendo.
```

**Tenés que ver:** Claude confirma que el puente escucha en el puerto 3001 y que el webhook quedó configurado.

## Paso 5 · Probá desde otro celular
Desde otro teléfono, escribile al número secundario 3 preguntas de tus casos y pedí hablar con una persona. Después preguntale a Claude: `¿Qué mensajes recibió el puente y hubo alguna derivación?`

**Tenés que ver:** las respuestas con tu cerebro en WhatsApp y el aviso de derivación en lo que te muestra Claude.

## Paso 6 · Servidor y modo oficial (cuando lo quieras usar de verdad)
En tu compu, el bot se apaga cuando cerrás la tapa. Alquilá un VPS con Ubuntu (2 GB o más), apuntá un subdominio (`wa.[TU-DOMINIO]`) a su IP y pedile a Claude que te guíe:

```prompt
Quiero pasar mi Evolution API de prueba a un VPS con Ubuntu. Guiame paso a paso, como a alguien que no programa, con la documentación oficial (https://docs.evolutionfoundation.com.br/evolution-api/install/docker.md y .../install/nginx.md): Docker, mi docker-compose.yml, claves nuevas (no las de prueba), HTTPS con Nginx y Let's Encrypt para wa.[TU-DOMINIO], firewall con solo 22, 80 y 443, y copias de seguridad. Las claves, siempre en archivos que abro yo en el editor, nunca en el chat. Para el bot, proponeme lo más simple: una ruta en el Worker de mi práctica del agente o un flujo de n8n. Antes de cada comando, decime qué hace.
```

**Modo oficial (Cloud API de Meta):** necesitás una app de Meta con WhatsApp, el **Phone number ID**, el **ID de la cuenta de WhatsApp Business** y un **token permanente** ([la API oficial directa](#w1-opciones)). En el servidor, pedile a Claude que cree una instancia con integración **WHATSAPP-BUSINESS** y que te abra el `.env` en el editor para cargar los valores. En Meta, webhook `https://wa.[TU-DOMINIO]/webhook/meta`, **Verify and save**, suscripción a **messages** y método de pago cargado.

> **Ojo:** verificá el modo oficial en la [guía de Cloud API de Evolution](https://docs.evolutionfoundation.com.br/evolution-api/integrations/cloudapi.md): puede cambiar.

**Tenés que ver:** `https://wa.[TU-DOMINIO]` abre con candado y el bot contesta con tu compu apagada.

## Riesgos
- **Modo QR: riesgo alto de bloqueo.** Solo número secundario, solo contestar a quien te escribió.
- **El servidor es tuyo:** actualizaciones, copias de seguridad y caídas. Sin alguien técnico, mirá [dlastcrm](#w2-bot-dlastcrm) o [Zernio](#w4-zernio).
- **La `AUTHENTICATION_API_KEY`** maneja tus números: nunca en el chat, nunca en GitHub, y el puerto 8080 cerrado al público.

## Cómo sé que funcionó
Desde un celular que no sea el conectado:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario de tu cerebro, avisar que te pasa con alguien, registrar la derivación y **no** contestarse a sí mismo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| Claude dice que Docker no responde | Abrí Docker Desktop y esperá **Engine running**. Después pedile que pruebe de nuevo. |
| En Windows, Docker pide WSL o virtualización | Seguí el aviso de Docker para instalar WSL 2 y reiniciá. Si la virtualización está apagada, se activa en la BIOS: pedí ayuda. |
| La API responde 503 "service not activated" | Versión 2.4.0 o posterior: activá la instancia desde el Manager. |
| El QR vence | Pedile a Claude un QR nuevo y escanealo rápido. |
| El bot no recibe nada | Pedile a Claude que revise que el puente esté corriendo y el webhook de la instancia. |
| El bot se contesta a sí mismo | Pedile a Claude que pare el puente, arregle el filtro de `fromMe` y lo vuelva a arrancar. |

## Para seguir solo
- **Chatwoot para el equipo:** una bandeja de código abierto para que varias personas contesten desde el mismo número.
- **Más números en el mismo servidor:** cada instancia es un número.
- **Medí antes de decidir:** si en un mes contesta bien, pasalo al modo oficial o a [dlastcrm](#w2-bot-dlastcrm). Las instrucciones pasan tal cual.

## Fuentes (consultadas el 18/11/2026)
- Evolution API: https://github.com/evolution-foundation/evolution-api · https://docs.evolutionfoundation.com.br/evolution-api/index.md · https://docs.evolutionfoundation.com.br/licensing
- Docker Desktop: https://docs.docker.com/get-started/get-docker/ · https://docs.docker.com/subscription/desktop-license/
- VPS: https://www.digitalocean.com/pricing/droplets · https://www.hetzner.com/cloud/regular-performance/
- Términos de WhatsApp: https://www.whatsapp.com/legal/terms-of-service
