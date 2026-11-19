---
titulo: "Tu bot de WhatsApp con Evolution API (código abierto)"
bloque: WhatsApp
tiempo: "2 a 3 horas para probarlo en tu compu. En un servidor (VPS): medio día más"
para: Equipos con alguien técnico que quieren todo propio y sin pagar plataforma
necesitas: s2-claude-code, s3-herramientas-base, s9-api-anthropic, w1-opciones
resultado: Evolution API corriendo en tu compu con Docker, un WhatsApp secundario conectado por QR y un bot mínimo que contesta con tu cerebro. Y sabés qué hace falta para pasarlo a un servidor y al modo oficial.
---

Evolution API es un programa **gratis y de código abierto** que conecta WhatsApp con bots y sistemas (n8n, Chatwoot, Typebot y otros). Lo instalás vos, en tu compu o en un servidor alquilado, y no le pagás a ninguna plataforma. Tiene **dos modos**: uno no oficial que se conecta por QR (rápido, con riesgo de bloqueo) y uno **oficial** que usa la API de Meta.
Ejemplo: Denvet tiene a alguien que maneja sistemas y quiere que el bot de pedidos viva en su propio servidor, sin depender de un proveedor. Lo prueba hoy en una compu con un chip secundario y, si le sirve, lo pasa al modo oficial.

> **Ojo:** el modo QR (se llama **Baileys**) imita WhatsApp Web y **no es oficial**. Los términos de WhatsApp prohíben el acceso automatizado: si lo detecta, suspende el número y perdés sus chats. Probalo solo con un número que no te importe perder. Para el número del negocio, usá el **modo Cloud API** (Paso 7), que es oficial.

> **Tip:** palabras que vas a ver en esta página:
> - **Docker:** un programa que corre otros programas dentro de "cajas" (contenedores) que traen todo lo que necesitan. Instalás Docker una vez y después levantás Evolution API con un solo comando, sin instalar bases de datos a mano. [Qué es Docker, en la web oficial](https://docs.docker.com/get-started/docker-overview/).
> - **Servidor o VPS:** una compu alquilada en internet, prendida todo el día.
> - **Instancia:** cada número de WhatsApp conectado a Evolution API.
> - **Webhook:** la dirección a la que Evolution API le avisa a tu bot cada mensaje nuevo.
> - **Manager:** el panel web de Evolution API, para crear instancias y ver el QR.
> - **`.env`:** un archivo de tu compu donde van las claves. No se sube a GitHub.

## Dónde correrlo
| | En tu compu (para probar) | En un servidor VPS (para usarlo de verdad) |
|---|---|---|
| Para qué | Probar hoy, sin pagar nada | Que el bot conteste las 24 horas |
| Qué necesitás | Docker Desktop | Un VPS con Linux, Docker y un dominio con HTTPS |
| Si apagás la compu | El bot se apaga | Sigue andando |
| Costo (nov 2026) | 0 | Desde unos 11 a 12 USD por mes un VPS de 2 GB ([DigitalOcean](https://www.digitalocean.com/pricing/droplets): 12 USD; [Hetzner](https://www.hetzner.com/cloud/regular-performance/): 9,99 EUR) |

## Cuánto cuesta (nov 2026)
- **Evolution API:** gratis, licencia Apache 2.0 con condiciones de marca ([GitHub oficial](https://github.com/evolution-foundation/evolution-api)). Desde la versión 2.4.0 pide **activar la instancia** una vez, con tu mail y teléfono: la licencia comunitaria es gratis, sin límites de mensajes ([licencia](https://docs.evolutionfoundation.com.br/licensing)).
- **Docker Desktop:** gratis para uso personal y para empresas de menos de 250 empleados **y** menos de 10 millones de dólares de facturación anual ([licencia de Docker](https://docs.docker.com/subscription/desktop-license/)).
- **Servidor:** el VPS de la tabla de arriba, si lo pasás a producción.
- **Claude para el bot:** por uso. Con Claude Haiku, del orden de 1 a 2 USD cada 1.000 mensajes ([Stack y costos](#r-stack-y-costos)).
- **Meta:** solo en el modo Cloud API, por mensaje ([cómo se cobra](#w1-opciones)). En modo QR, Meta no cobra.

## Pros y contras
| A favor | En contra |
|---|---|
| El programa es gratis y es tuyo. | Lo instalás y lo mantenés vos. Si se cae a las 3 de la mañana, se cae tu atención. |
| Dos modos: QR para probar, Cloud API oficial para producción. | En modo QR, **riesgo alto** de bloqueo del número. |
| Muchas integraciones listas (n8n, Chatwoot, Typebot, OpenAI). | Necesita base de datos (PostgreSQL) y Redis: Docker lo resuelve, pero hay más piezas que pueden fallar. |
| Muchas instancias (números) en el mismo servidor. | La documentación oficial está en portugués y cambió de sitio en 2026. |

## Antes de empezar
- [ ] Claude Code instalado ([Instalá Claude Code](#s2-claude-code)) y Node.js ([Herramientas base](#s3-herramientas-base)).
- [ ] Clave de API de Anthropic con crédito ([API de Anthropic](#s9-api-anthropic)).
- [ ] Un **número secundario** con WhatsApp en un celular (chip nuevo). **Nunca** el número principal del negocio.
- [ ] Tu cerebro con `agente/prompt-del-agente.md` y `agente/conocimiento-publico.md` ([la práctica del agente](#p3-agente-preguntas), Pasos 1 a 4). Si no los tenés, sirve `bot/instrucciones-del-bot.md` de [Cierre: tu bot de WhatsApp](#d7-whatsapp).
- [ ] Unos 5 GB libres en el disco para Docker.
- [ ] En Windows: permisos de administrador para instalar Docker Desktop.

## Paso 1 · Instalá Docker Desktop
1. Entrá a [docs.docker.com/get-started/get-docker](https://docs.docker.com/get-started/get-docker/) y descargá **Docker Desktop** para tu sistema.

<div data-os="mac">

2. Elegí la versión según tu chip. Para saberlo: menú **Apple › Acerca de esta Mac**. Si dice "Apple M…", bajá **Apple Silicon**; si dice "Intel", bajá **Intel chip**.
3. Abrí el archivo `.dmg` y arrastrá Docker a **Aplicaciones**. Abrilo desde **Aplicaciones** y aceptá los permisos que pide.

</div>
<div data-os="win">

2. Abrí el instalador. Dejá tildada la opción de usar **WSL 2** (el "Linux dentro de Windows" que Docker necesita) y seguí.
3. Si te pide reiniciar, reiniciá. Abrí **Docker Desktop** desde el menú Inicio.

</div>

4. Docker Desktop te pide aceptar sus términos y, opcionalmente, iniciar sesión: podés saltear el inicio de sesión.
5. Abrí una terminal nueva (en Mac, **Terminal**; en Windows, **PowerShell**) y escribí:

```bash
docker --version
```

**Tenés que ver:** algo como `Docker version 2X.X.X`, y en Docker Desktop, abajo a la izquierda, que el motor está corriendo (**Engine running**).

> **Ojo:** verificá en pantalla los nombres de las opciones del instalador: Docker los cambia entre versiones.

## Paso 2 · Que Claude Code arme Evolution API
1. Creá la carpeta y abrí Claude Code ahí:

<div data-os="mac">

```bash
mkdir -p ~/Documents/evolution-api
cd ~/Documents/evolution-api
claude
```

</div>
<div data-os="win">

```powershell
New-Item -ItemType Directory -Force $HOME\Documents\evolution-api
cd $HOME\Documents\evolution-api
claude
```

</div>

2. Pegá:

```prompt
Quiero correr Evolution API en mi compu con Docker Desktop, para probar. Antes de hacer nada, leé el README oficial (https://github.com/evolution-foundation/evolution-api), su docker-compose.yaml y .env.example, la guía de Docker (https://docs.evolutionfoundation.com.br/evolution-api/install/docker.md) y la página de releases. Después:
1. Armá en esta carpeta un docker-compose.yml con Evolution API, PostgreSQL y Redis, basado en el oficial. Usá la última versión estable (no una "rc") y escribí el número de versión en la imagen, no "latest".
2. Armá el .env desde el .env.example con lo mínimo: base de datos, Redis, SERVER_URL=http://localhost:8080 y una AUTHENTICATION_API_KEY larga generada al azar. No me muestres la clave: decime en qué línea está.
3. Que el puerto 8080 solo se abra en mi compu (127.0.0.1).
4. Explicame en castellano, como a alguien que no programa, qué es cada servicio y si la versión que elegiste pide activar la licencia.
5. Decime el comando para arrancarlo y cómo abrir el Manager. No lo arranques todavía.
```

3. Cuando Claude termine, arrancalo en la terminal (o pedile a Claude que lo haga):

```bash
docker compose up -d
```

**Tenés que ver:** al abrir `http://localhost:8080` en el navegador, un mensaje de bienvenida de Evolution API. Y el Manager en `http://localhost:8080/manager`.

> **Ojo:** desde la versión 2.4.0, la primera vez que abrís el Manager te pide activar la instancia con tu mail y teléfono (gratis). Verificá la dirección del Manager en lo que te dijo Claude: puede cambiar según la versión.

## Paso 3 · Creá la instancia y escaneá el QR
1. En el Manager, iniciá sesión con la dirección `http://localhost:8080` y tu `AUTHENTICATION_API_KEY` (está en el `.env`: abrilo vos, no se la pegues a Claude).
2. Creá una instancia nueva: nombre `prueba`, conexión **Baileys** (la de QR).
3. Abrí la instancia y tocá para conectar. Aparece un QR.
4. En el celular del número secundario, abrí WhatsApp:
   - **iPhone:** **Configuración › Dispositivos vinculados › Vincular un dispositivo**.
   - **Android:** tres puntos **⋮ › Dispositivos vinculados › Vincular un dispositivo**.
5. Apuntá la cámara al QR.

> **Ojo:** verificá los nombres de los botones del Manager en pantalla. Si preferís, pedile a Claude Code: "Creá la instancia prueba con POST /instance/create (qrcode true, integración Baileys) y mostrame el QR de GET /instance/connect/prueba como imagen", leyendo la clave del `.env` sin mostrarla.

**Tenés que ver:** la instancia `prueba` como conectada (**open** o **connected**) y Evolution API entre los **Dispositivos vinculados** del celular.

## Paso 4 · El bot mínimo, en tu compu
Un programita en tu compu (el "puente") recibe cada mensaje de Evolution API, le pregunta a Claude con tu cerebro y contesta. Como los dos corren en tu compu, no hace falta publicar nada.

1. En la terminal, creá la carpeta del puente y abrí el archivo de claves:

<div data-os="mac">

```bash
mkdir -p ~/Documents/evolution-api/puente-bot
cd ~/Documents/evolution-api/puente-bot
touch .env
open -e .env
```

</div>
<div data-os="win">

```powershell
New-Item -ItemType Directory -Force $HOME\Documents\evolution-api\puente-bot
cd $HOME\Documents\evolution-api\puente-bot
notepad .env
```

Si el Bloc de notas pregunta si querés crear el archivo, tocá **Sí**.

</div>

2. Escribí estas líneas con tus valores (la clave de Anthropic y la `AUTHENTICATION_API_KEY` del `.env` de Evolution), guardá y cerrá:

```text
ANTHROPIC_API_KEY=[TU-CLAVE-DE-ANTHROPIC]
EVOLUTION_API_KEY=[TU-AUTHENTICATION-API-KEY]
EVOLUTION_URL=http://localhost:8080
EVOLUTION_INSTANCIA=prueba
```

3. Volvé a Claude Code (en la carpeta `evolution-api`) y pegá. Cambiá `[RUTA-DE-TU-CEREBRO]` por la carpeta de tu cerebro (por ejemplo `~/Documents/cerebro-fondus`):

```prompt
En la carpeta puente-bot armá un servidor chico en Node.js (puerto 3001, comando npm start) que haga de bot de WhatsApp con Evolution API. Leé las claves de puente-bot/.env sin mostrarlas y confirmá que .env está en el .gitignore. Antes de escribir código, leé en https://docs.evolutionfoundation.com.br/evolution-api/configuration/webhooks.md el formato del evento MESSAGES_UPSERT y en https://docs.evolutionfoundation.com.br/evolution-api/send-text-message.md cómo mandar texto.
- POST /webhook: responde 200 enseguida. Procesa solo MESSAGES_UPSERT. Ignora los mensajes propios (fromMe en true), los grupos (terminan en @g.us), los estados y los repetidos (por id).
- Si es texto, arma la respuesta con Claude Haiku usando como instrucciones [RUTA-DE-TU-CEREBRO]/agente/prompt-del-agente.md y [RUTA-DE-TU-CEREBRO]/agente/conocimiento-publico.md (o bot/instrucciones-del-bot.md si no existen), con memoria de los últimos 10 mensajes de cada chat. Si es audio o foto, pide que lo escriban.
- Contesta con POST EVOLUTION_URL/message/sendText/EVOLUTION_INSTANCIA y el encabezado apikey, esperando entre 3 y 8 segundos al azar.
- Si la respuesta dice que hay que derivar a una persona, lo escribe en la consola con el motivo.
Después configurá el webhook de la instancia con POST /webhook/set/prueba: url http://host.docker.internal:3001/webhook (así Docker llega a mi compu), evento MESSAGES_UPSERT, habilitado. Explicame qué hiciste y cómo lo arranco.
```

4. Arrancá el puente con `npm start` dentro de `puente-bot` (en Windows, si da error de scripts, `npm.cmd start`). Dejá esa terminal abierta.

**Tenés que ver:** en la terminal del puente, un mensaje de que escucha en el puerto 3001, y Claude confirmando que el webhook quedó configurado.

## Paso 5 · Probá desde otro celular
1. Desde otro teléfono, escribile al número secundario 3 preguntas de tus casos de prueba.
2. Pedí hablar con una persona.

**Tenés que ver:** las respuestas con tu cerebro en WhatsApp y, en la terminal del puente, cada mensaje que llegó y el aviso de derivación.

## Paso 6 · Pasalo a un servidor (después del taller)
En tu compu, el bot se apaga cuando cerrás la tapa. Para que conteste las 24 horas:

1. Alquilá un VPS con Ubuntu y al menos 2 GB de memoria (ver la tabla de **Dónde correrlo**).
2. Apuntá un subdominio (por ejemplo `wa.[TU-DOMINIO]`) a la IP del VPS.
3. Pedile a Claude Code que te guíe, con este prompt:

```prompt
Quiero pasar mi Evolution API de prueba a un VPS con Ubuntu. Guiame paso a paso, como a alguien que no programa, siguiendo la documentación oficial (https://docs.evolutionfoundation.com.br/evolution-api/install/docker.md y https://docs.evolutionfoundation.com.br/evolution-api/install/nginx.md): instalar Docker, copiar mi docker-compose.yml, generar claves nuevas (no reutilices las de prueba), HTTPS con Nginx y Let's Encrypt para wa.[TU-DOMINIO], firewall con solo los puertos 22, 80 y 443 abiertos, y copias de seguridad de la base de datos. Para el bot, proponeme la opción más simple entre: (a) sumar una ruta /evolution al Worker de Cloudflare de mi práctica del agente, o (b) un flujo de n8n con un Webhook, un nodo de Claude y un HTTP Request a /message/sendText. Antes de cada comando, decime qué hace.
```

> **Tip:** si usás n8n instalado en tu propio servidor, existe un nodo comunitario oficial: en n8n, **Settings › Community Nodes › Install** y el paquete `n8n-nodes-evolution-api`. En n8n Cloud no hace falta: alcanza con el nodo **HTTP Request**.

**Tenés que ver:** `https://wa.[TU-DOMINIO]` abre con candado y el bot contesta con tu compu apagada.

## Paso 7 · El modo oficial (Cloud API de Meta)
Para el número del negocio, Evolution API puede usar la API oficial de Meta en vez del QR. Necesitás lo mismo que la API oficial directa: una app en Meta for Developers con WhatsApp, el **Phone number ID**, el **ID de la cuenta de WhatsApp Business** y un **token permanente** de un usuario del sistema ([De Telegram a WhatsApp en 5 pasos](#w1-opciones), pasos 1 y 5).

1. En el servidor (con HTTPS, no en tu compu), pedile a Claude Code que cree una instancia con la integración **WHATSAPP-BUSINESS**: `POST /instance/create` con `instanceName`, `token`, `number` (el Phone number ID), `businessId` y `qrcode` en `false`. Los valores los cargás vos en el `.env` del servidor.
2. En el `.env` de Evolution, poné un verify token inventado en `WA_BUSINESS_TOKEN_WEBHOOK` y reiniciá.
3. En tu app de Meta, en **WhatsApp › Configuration**, poné como webhook `https://wa.[TU-DOMINIO]/webhook/meta`, el mismo verify token, **Verify and save**, y suscribite a **messages**.
4. Cargá un método de pago en Meta.

> **Ojo:** verificá estos pasos en la [guía oficial de Cloud API de Evolution](https://docs.evolutionfoundation.com.br/evolution-api/integrations/cloudapi.md) antes de hacerlos: la escribieron para la v2 y puede cambiar.

**Tenés que ver:** el webhook verificado en Meta y el bot contestando en el número oficial.

## Riesgos (leelos antes de prenderlo)
- **Modo QR (Baileys): riesgo alto de bloqueo.** Solo con un número secundario, solo para contestar a quien te escribió, nada de envíos masivos ni en frío.
- **El servidor es tuyo:** actualizaciones, copias de seguridad, seguridad y caídas. Si no hay nadie técnico en el equipo, mirá [dlastcrm](#w2-bot-dlastcrm) o [Zernio](#w4-zernio).
- **Las claves:** con la `AUTHENTICATION_API_KEY`, cualquiera maneja tus números. Nunca en el chat, nunca en GitHub, y el puerto 8080 cerrado al público (el acceso, solo por HTTPS).
- **Cambios de versión:** desde la 2.4.0 la instancia se activa contra el servidor de licencias de Evolution Foundation. Leé las notas de cada versión antes de actualizar.

## Cómo sé que funcionó
Desde un celular que no sea el del número conectado, mandá:

```text
Hola, ¿qué horario tienen? Y quiero hablar con una persona.
```

Tiene que contestar el horario que está en tu cerebro, avisar que te pasa con alguien y dejar el aviso de derivación en la terminal del puente. Y no tiene que contestarse a sí mismo.

## Si algo falla
| Te pasa | Hacé esto |
|---|---|
| `docker` no se reconoce como comando | Abrí Docker Desktop y esperá a que diga que el motor está corriendo. Cerrá la terminal y abrí una nueva. |
| En Windows, Docker pide WSL o virtualización | Seguí el aviso de Docker Desktop para instalar WSL 2 y reiniciá. Si dice que la virtualización está apagada, hay que activarla en la BIOS: pedí ayuda a la mesa. |
| La API responde 503 "service not activated" | Es una versión 2.4.0 o posterior: activá la instancia desde el Manager con tu mail y teléfono. |
| El QR no aparece o vence | Volvé a tocar conectar. El QR dura pocos segundos: escanealo rápido. |
| El bot no recibe nada | Revisá que el puente esté corriendo y que el webhook apunte a `http://host.docker.internal:3001/webhook`. Pedile a Claude Code que lo consulte con GET /webhook/find/prueba. |
| El bot se contesta a sí mismo | Falta ignorar `fromMe`. Pará el puente con **Ctrl + C**, pedile a Claude Code que lo arregle y volvé a arrancarlo. |
| WhatsApp avisa que el número está restringido | Desconectá la instancia. No reconectes ese número: pasá al modo oficial con otro. |

## Para seguir solo
- **Chatwoot para el equipo:** Evolution API se integra con Chatwoot, una bandeja de atención de código abierto, para que varias personas contesten desde el mismo número.
- **Más números en el mismo servidor:** cada instancia es un número. Un mismo VPS puede atender varios negocios.
- **Medí antes de decidir:** si después de un mes el bot contesta bien, pasalo al modo Cloud API oficial o a [dlastcrm](#w2-bot-dlastcrm). El prompt y el conocimiento pasan tal cual.

## Fuentes (consultadas el 18/11/2026)
- Evolution API, GitHub oficial (README, docker-compose, .env.example, releases): https://github.com/evolution-foundation/evolution-api
- Evolution API, documentación oficial (Docker, webhooks, crear instancia, enviar texto, Cloud API, n8n): https://docs.evolutionfoundation.com.br/evolution-api/index.md
- Evolution API, licencia comunitaria: https://docs.evolutionfoundation.com.br/licensing
- Docker Desktop, descarga y licencia: https://docs.docker.com/get-started/get-docker/ · https://docs.docker.com/subscription/desktop-license/
- Precios de VPS: https://www.digitalocean.com/pricing/droplets · https://www.hetzner.com/cloud/regular-performance/
- Términos de servicio de WhatsApp: https://www.whatsapp.com/legal/terms-of-service
