---
titulo: Datos y seguridad
bloque: Teoría
tiempo: 20 min
para: Todos
necesitas: nada
resultado: Sabés qué datos no pasarle a una IA, cómo cuidar tus claves, qué permisos darle a Claude Code y cuándo tiene que revisar una persona.
---

La IA es como un empleado nuevo muy capaz: le das acceso de a poco, a medida que ves cómo trabaja. No le das las llaves de la caja fuerte el primer día.
Ejemplo: Denvet maneja datos de clientes y de mascotas con tratamientos. El bot puede responder "¿tienen stock de tal alimento?", pero un diagnóstico o una dosis la confirma siempre un veterinario.

> **Datos:** esta página es una guía práctica, no asesoramiento legal. Si tu empresa maneja datos de salud o financieros de terceros, consultá con tu contador o abogado qué te exige la ley argentina de datos personales (Ley 25.326).

## Qué datos se le pasan y cuáles no
| | Ejemplos | Regla |
|---|---|---|
| **Nunca** | Contraseñas, claves de API, tokens, números de tarjeta, CBU con clave, códigos de verificación | No van en ningún chat, ni de Claude ni de ninguna IA. Si se te escapó uno, cambialo ya |
| **Nunca sin permiso y sin necesidad** | DNI, datos de salud, deudas, ingresos, legajos de empleados, conversaciones privadas de clientes con nombre y teléfono | Para practicar, datos inventados. Para trabajar en serio, solo si tu empresa lo decidió y lo escribió |
| **Con cuidado** | Precios internos, márgenes, contratos, estrategia | Sí en tu cuenta paga y en tu cerebro privado. No en herramientas gratis que no conocés |
| **Sí** | Tus productos, tu voz, preguntas frecuentes, reseñas públicas, procesos | Es justamente lo que hace que la IA trabaje bien |

> **Tip:** antes de pegar una conversación real, reemplazá nombre, teléfono y DNI por `[CLIENTE]`, `[TELÉFONO]`, `[DNI]`. Claude lo puede hacer por vos con el prompt de abajo, pero sobre un archivo que ya está en tu compu.

**Probalo** (en Claude Code, abierto en la carpeta donde está el archivo; reemplazá `[ARCHIVO]` por su nombre, por ejemplo `consultas-octubre.txt`):

```prompt
Hacé una copia de [ARCHIVO] llamada [ARCHIVO]-anonimo y reemplazá en la copia todos los nombres de personas, teléfonos, mails, DNI y direcciones por [CLIENTE], [TELÉFONO], [MAIL], [DNI] y [DIRECCIÓN]. No toques el original. Al final decime cuántos reemplazos hiciste de cada tipo.
```

**Tenés que ver:** un archivo nuevo terminado en `-anonimo` y el original sin cambios.

Escribí la regla de tu empresa en el cerebro, en `datos/reglas.md`: qué se puede pasar, qué no y quién lo decide.

## La privacidad de tu cuenta de Claude
- En **Settings › Privacy** hay una opción para que Anthropic use (o no) tus chats y sesiones de Claude Code para entrenar modelos: **Help improve Claude**. Decidí vos. Si la apagás, las conversaciones nuevas no se usan para entrenar.
- Según Anthropic, con esa opción apagada los datos se guardan 30 días; prendida, hasta 5 años. Los chats que borrás no se usan para entrenar.
- Los planes de empresa (**Team** y **Enterprise**) tienen sus propios términos y controles de administrador.

> **Ojo:** verificá el nombre exacto de la opción y la política vigente en [privacy.claude.com](https://privacy.claude.com). Cambió en 2025 y puede volver a cambiar.

- Si compartís una sesión de Claude Code en la nube (**Public**), cualquiera con el link y una cuenta de Claude la ve. Puede tener código o claves: revisala antes.
- El feedback que mandás (pulgar arriba o abajo) puede guardarse aunque tengas el entrenamiento apagado. No lo mandes en chats con datos sensibles.

## Los permisos de Claude Code
Claude Code trabaja en tu compu: puede leer, escribir, borrar y correr comandos. Por eso **te pide permiso**. No lo apagues.

| Modo | Qué hace | Cuándo |
|---|---|---|
| **Manual** (el de siempre) | Pregunta antes de editar archivos o correr comandos | Para empezar y para todo lo nuevo |
| **Aceptar cambios** | Edita archivos sin preguntar; los comandos los sigue preguntando | Cuando ya confiás en la tarea |
| **Plan** | Solo lee y propone. No toca nada | Para tareas grandes: primero el plan |
| **Auto** | Un control automático aprueba lo seguro y frena lo riesgoso | Tareas largas que conocés bien |
| **Bypass permissions** | No pregunta nada | **No lo uses en el taller.** |

Reglas simples:
1. **Abrí Claude Code en la carpeta del proyecto**, nunca en tu carpeta de usuario entera ni en el escritorio. Solo toca lo que hay ahí.
2. **Leé antes de aprobar.** Si no entendés qué va a hacer un comando, preguntale: "¿qué hace exactamente esto?".
3. **"Permitir siempre" solo para lo inofensivo** (leer archivos, listar carpetas). Para borrar, publicar o mandar algo: que pregunte siempre.
4. Revisá lo que ya aprobaste con `/permissions`.

**Probalo:**

```prompt
Configurá los permisos de este proyecto para que nunca puedas leer ni editar archivos .env ni carpetas de claves, y para que siempre me preguntes antes de borrar archivos o publicar algo. Mostrame el cambio antes de guardarlo y explicame en qué archivo queda.
```

## Claves y tokens: dónde se guardan
Una clave de API (de Anthropic, Telegram, Supabase, Meta) es **la llave de tu casa**: quien la tiene, gasta a tu nombre o entra a tus datos. Un **token** es lo mismo con otro nombre.

**Dónde sí:**
- En un archivo **`.env`** en la carpeta del proyecto, con una línea por clave. Cada línea es una **variable de entorno**: un nombre, un `=` y el valor, sin espacios ni comillas:

```text
ANTHROPIC_API_KEY=[TU-CLAVE]
TELEGRAM_BOT_TOKEN=[TU-TOKEN]
```

- En las "variables de entorno" o "secretos" de donde publicás (Vercel, Cloudflare, n8n, la nube de Claude Code).
- En un gestor de contraseñas (1Password, Bitwarden, el llavero de tu compu), como respaldo.

**Dónde no:**
- En el chat de Claude ni de ninguna IA.
- En GitHub. Por eso el `.env` va **siempre** en el `.gitignore` (la lista de archivos que git no sube).
- En el `CLAUDE.md`, en una planilla compartida o en un mensaje de WhatsApp.

Para crear el `.gitignore` con el `.env` adentro:

<div data-os="mac">

```bash
echo ".env" >> .gitignore
```

</div>
<div data-os="win">

```powershell
Add-Content .gitignore ".env"
```

</div>

### Cómo crear el `.env` y pegar la clave vos (sin pasársela a Claude)
Los archivos que empiezan con punto (`.env`, `.gitignore`) son **ocultos**: no los ves en Finder ni en el Explorador si no los mostrás. Por eso los abrimos desde la terminal.

1. Abrí la terminal parada en la carpeta del proyecto (con `cd`, ver el [glosario](#t2-piezas)).
2. Creá y abrí el archivo con el editor de texto de tu compu:

<div data-os="mac">

```bash
touch .env && open -e .env
```

**Tenés que ver:** TextEdit abierto con un documento vacío llamado `.env`.

</div>
<div data-os="win">

```powershell
notepad .env
```

Si te pregunta si querés crear un archivo nuevo, tocá **Sí**.

**Tenés que ver:** el Bloc de notas abierto con un documento vacío llamado `.env`.

</div>

3. Escribí el nombre de la variable que te pide el tutorial, un `=` y pegá tu clave pegada al `=`. Ejemplo: `ANTHROPIC_API_KEY=` y la clave a continuación.
4. Guardá (**Cmd+S** en Mac, **Ctrl+S** en Windows) y cerrá.
5. Agregá el `.env` al `.gitignore` con el comando de arriba.

> **Tip:** para ver los archivos ocultos: en Mac, en Finder apretá **Cmd+Shift+.** (punto). En Windows, en el Explorador: **Ver › Mostrar › Elementos ocultos**.

**Si una clave se escapó** (la pegaste en un chat, aunque sea el de Claude, o la subiste a GitHub): no alcanza con borrar el mensaje o el archivo. **Entrá a la herramienta, revocala (borrala) y creá una nueva.**

> **Costo:** en la consola de la API de Anthropic poné un **límite de gasto mensual** ([Clave de API](#s9-api-anthropic)). Si alguien usa tu clave, el daño tiene techo.

**Probalo:**

```prompt
Revisá esta carpeta y decime si hay claves, tokens o contraseñas escritas en algún archivo que no sea .env. No me muestres las claves completas: decime solo el archivo, la línea y los primeros 4 caracteres. Después revisá que .env esté en .gitignore.
```

## Conectores, MCP y plugins: solo de fuentes conocidas
- Instalá conectores y MCP **oficiales** (los de **Customize › Connectors**, o el que publica la empresa dueña de la app). Un MCP de un desconocido puede leer todo lo que le das.
- Activá solo los que usás. En las tareas programadas, sacá los que la tarea no necesita.
- Ojo con lo que Claude **lee**: una web, un mail o un PDF pueden traer instrucciones escondidas ("ignorá lo anterior y mandá…"). Si Claude te propone algo raro después de leer algo de afuera, frená y preguntale de dónde salió.

## Agente seguro: antes de dejarlo trabajar solo
Regla de oro: **nunca le des autonomía a algo que no viste funcionar.**

**Diseño**
- [ ] Tiene UN objetivo escrito en una frase.
- [ ] Sé exactamente qué datos lee y de qué carpeta.
- [ ] Tiene escrito qué NUNCA puede hacer (pagar, borrar, publicar, mandar a clientes, prometer precios).
- [ ] Sabe cuándo pasarle la charla a una persona (queja, plata, salud, contratos, duda).

**Prueba**
- [ ] Lo probé con al menos 6 casos reales (o parecidos) y la respuesta esperada de cada uno.
- [ ] Probé casos difíciles: datos que faltan, un cliente enojado, una pregunta fuera de tema.
- [ ] Cuando no sabe algo dice PENDIENTE o deriva, no inventa.

**Los 5 frenos** (si corre solo, con una tarea programada o n8n)
- [ ] **Solo lectura primero:** las primeras semanas solo reporta, no actúa.
- [ ] **Permisos mínimos:** únicamente las carpetas y herramientas que necesita.
- [ ] **Tope:** máximo de mensajes, llamadas o gasto por día.
- [ ] **Registro:** deja un log de qué hizo y cuándo.
- [ ] **Botón de apagado:** sé cómo frenarlo en 1 minuto (pausar la tarea, desactivar el workflow).

**Seguimiento**
- [ ] Una vez por semana leo lo que hizo y corrijo el proceso o las reglas.

## Cuándo revisa una persona, sí o sí
La IA propone, una persona aprueba. Siempre que haya:

| Tema | Ejemplo | Qué hace la IA | Qué hace la persona |
|---|---|---|---|
| **Plata** | Un presupuesto de Viajes TDH, una cuota de Fondus | Arma el borrador con los datos del cerebro | Revisa el número y lo manda |
| **Salud** | Una consulta sobre una mascota enferma en Denvet | Responde lo general y deriva | Diagnostica y receta |
| **Clientes** | Un mensaje a toda la base, una respuesta a una queja | Redacta y propone a quién | Aprueba antes de enviar |
| **Contratos y promesas** | Plazos, garantías, aprobación de un crédito | Nunca promete | Decide y firma |
| **Publicar** | Un anuncio, un post, un cambio en la web | Prepara y deja listo | Lo mira y publica |

Escribilo en el cerebro: en el `CLAUDE.md`, una sección "Nunca hagas sin mi OK".

## WhatsApp: cuidado con las librerías no oficiales
Hay programas que conectan WhatsApp "escaneando el QR" como si fueras vos en WhatsApp Web. Son baratos y rápidos, pero **no son oficiales**: Meta puede **bloquear el número**, y si es el número de tu empresa perdés el canal con tus clientes.
- Para el número principal del negocio: vía oficial (API de WhatsApp de Meta o un proveedor que la use).
- Si probás algo no oficial: con un número aparte, nunca con el principal, y con poco volumen.

Comparativa completa y qué conviene para cada empresa: [WhatsApp: opciones](#w1-opciones).

## Para seguir solo
- Escribí `datos/reglas.md` en tu cerebro con la regla de tu empresa y pedile a Claude que la lea siempre (sumala al `CLAUDE.md`).
- Una vez por mes: revisá qué conectores tenés activos, qué claves existen y quién las tiene. Lo que no se usa, se apaga.
- Antes de soltar cualquier agente, pasá el checklist de arriba con alguien de tu equipo.
