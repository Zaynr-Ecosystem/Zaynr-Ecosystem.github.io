# Módulos

Zelly's Nexus es modular: cada función es un módulo que puede activarse o desactivarse
de forma independiente, y a todos los módulos se accede mediante un único comando raíz,
`/zn` (alias `/nexus`).

- **La lista de módulos.** Trece módulos activables se encuentran bajo `modules` en
  `config.yml`: `auth`, `antibot`, `toolkit`, `ban`, `join`, `chat`, `inventory`,
  `clans`, `itemedit`, `tab`, `integrations`, `updater` y `debug`. Todos están activados
  por defecto excepto `debug`.
- **Dónde se guarda la configuración.** La configuración global está en `config.yml`; la
  configuración por módulo está en `modules/<module>.yml`, en la carpeta de datos del
  plugin. Las plantillas de diez módulos vienen en el jar y se copian en el primer
  arranque cuando faltan: `auth`, `antibot`, `toolkit`, `ban`, `join`, `chat`,
  `inventory`, `clans`, `itemedit` y `tab`.
- **Activar o desactivar requiere reinicio.** Cambiar cualquier valor de
  `modules.<id>.enabled` surte efecto solo tras un reinicio completo del servidor;
  `/zn reload` detecta el cambio, se lo indica al emisor y registra una advertencia.
- **Informe de arranque.** Al activarse, el plugin carga los módulos en un orden fijo
  (translation, auth, antibot, toolkit, ban, join, chat, inventory, clans, itemedit,
  tab, integrations, updater, debug). Cada módulo termina en LOADED, DISABLED o FAILED,
  y el informe de arranque imprime las integraciones detectadas, el estado de cada
  módulo y un resumen de una línea.
- **Rutas y alias.** A cada módulo se accede como `/zn <module>` con un alias corto:
  `a`, `ab`, `tools`, `c`, `inv`, `clan`, `ie`, `t`, `int`, `dbg`. Los atajos de raíz
  opcionales (`/spawn`, `/home`, `/login` y más) se controlan con
  `commands.register-root-aliases` y `commands.disabled-root-aliases`. Cinco raíces de
  módulo se registran siempre que su módulo esté activado, independientemente de esos
  ajustes: `/auth`, `/zantibot`, `/clan`, `/inventory` y `/itemedit`.
- **Orden en el menú.** El menú de usuario lista los módulos en un orden fijo: auth,
  toolkit, chat, inventory, clans, itemedit, tab, integrations, debug. Los botones
  también dependen de qué módulos estén activados y de los permisos.
- **Barrera de inicio de sesión.** Mientras el módulo auth está cargado, los jugadores
  sin autenticar no pueden moverse, romper ni colocar bloques, interactuar, usar el
  chat, soltar ni recoger objetos, recibir daño ni hacer clic en inventarios, ni
  ejecutar ningún comando excepto `/zn`, `/zn menu`, `/zn help`, `/zn auth` y los alias
  raíz de auth registrados. Si el módulo auth falla al cargar, se rechazan las entradas
  hasta el siguiente reinicio.
- **Traducciones.** `language` acepta `en` o `es`; las claves que faltan recurren al
  inglés, y un idioma que no se carga recurre por completo al inglés.
- **API pública.** El plugin registra `NexusApi` como servicio de Bukkit, y expone la
  versión, el idioma, el estado de los diálogos y el registro de entradas de menú y
  subcomandos personalizados para otros plugins.

## auth

Ruta `/zn auth` (alias `a`); orden en el menú 10; activado por defecto.

- Registro, inicio y cierre de sesión con límites configurables de longitud de contraseña.
- Memoria de sesión, contraseñas de un solo uso, TOTP, PIN, correo de recuperación,
  captcha y flujos de código de verificación.
- Una barrera de inicio de sesión para jugadores sin autenticar con las restricciones
  indicadas arriba.
- Verificación de cuentas premium de Mojang con tiempo de espera y caché.
- Herramientas administrativas de cuentas: eliminar cuenta, marcar
  premium/cracked/freemium, registros de auth, purga e inicio de sesión forzado.
- Las credenciales se ocultan en el registro del servidor.

Comandos: `/auth`, `/register` (`/reg`), `/login` (`/l`), `/logout`,
`/changepassword` (`/changepw`), `/email`, `/totp`, `/pin`, más las acciones
`unregister`, `otp`, `remember`, `captcha`, `verification`, `form`, `menu`, `delacc`,
`premium`, `cracked`, `freemium`, `getlogs`, `admin` y `antibot`.

Permisos: `zn.auth.player` (todos), `zn.auth.admin` (operadores).
Almacenamiento: `auth.yml`.

## antibot

Ruta `/zn antibot` (alias `ab`); activado por defecto. Sin entrada en el menú raíz; su
menú se abre desde el comando.

- Limitación de la tasa de conexiones por dirección dentro de una ventana de tiempo.
- Modo pánico que bloquea toda conexión nueva, una lista de direcciones bloqueadas y un
  informe de estado.
- Una comprobación de permiso de staff para cada acción.

Comandos: `/zantibot` (`/antibot`), `menu`, `status`, `panic <on|off>`, `list`,
`add`/`block <address>`, `remove`/`unblock <address>`.

Permisos: `zn.antibot.admin` (operadores); el nodo heredado `zn.antibot` lo concede.
Almacenamiento: `antibot.yml`.

## toolkit

Ruta `/zn toolkit` (alias `tools`); orden en el menú 30; activado por defecto.

- Registra seis dominios de comandos: teletransporte, jugador, servidor, moderación,
  kits y objetos, más sus listeners y su almacén de datos.
- Expone `/zn prank` como ruta directa adicional.
- Guarda homes, warps, spawn, cárceles, kits, correo, datos de último acceso y apodos en
  archivos YAML.
- El rango de teletransporte aleatorio se puede cambiar en tiempo de ejecución con
  `/settpr`.

La lista completa de comandos está en la página [Comandos](commands.md).

Permisos: por acción `zn.<domain>.<action>` (dominios: teleport, player, server,
moderation, kit, items), también aceptado como `zn.toolkit.<action>`; `zn.admin` y
`zn.toolkit.admin` conceden todas las acciones, y se aceptan varios nodos heredados.
Almacenamiento: `spawn.yml`, `homes.yml`, `warps.yml`, `jails.yml`, `kits.yml`,
`mail.yml`, `jailed.yml`, `lastseen.yml`, `nicknames.yml`.

## ban

Activado por defecto; sin ruta de comando propia: las acciones de ban, ban por IP,
expulsión, suspensión y retirada de la suspensión del toolkit se ejecutan sobre él.

- Bans permanentes, temporales y por IP, además de suspensiones, con una pantalla de
  rechazo de inicio de sesión para jugadores baneados o suspendidos y una pantalla de
  expulsión, construidas a partir de `modules/ban.yml` (nombre del servidor, formato de
  fecha y enlaces).
- Las suspensiones usan `default-suspend-duration` cuando no se indica ninguna duración;
  `/zn suspend` sin motivo abre el diálogo de suspensión para el staff en línea.
- Las acciones de ban se registran en `ban-audit.yml`.
- Con `modules.ban.enabled: false`, esas acciones responden que el módulo está
  desactivado.

Comandos: ninguno propio; las acciones están en el toolkit (`/ban`, `/tempban`, `/unban`,
`/banip`, `/tempbanip`, `/unbanip`, `/suspend` y `/unsuspend`).

Permisos: los nodos del toolkit `zn.moderation.*`.
Almacenamiento: `ban-audit.yml`.

## join

Activado por defecto; sin ruta de comando: reacciona a las entradas, primeras entradas y
salidas.

- Cuatro canales independientes: mensajes de chat, títulos de pantalla, líneas de barra
  de acción y sonidos, cada uno con variantes pública (todos) y privada (el jugador).
- Cada entrada establece una prioridad y puede llevar un permiso opcional, de modo que
  distintos grupos pueden recibir mensajes distintos.
- Las primeras entradas se detectan automáticamente; los títulos comparten los tiempos
  de `title-fade` a menos que una entrada los sobrescriba.
- Marcadores: `<player>`, `<displayname>`, `<world>`, `<online>` y `<uniquejoins>` (el
  contador que se guarda en `join-stats.yml`).

Comandos: ninguno.

Permisos: ninguno propio; los valores de `permission` por entrada son opcionales y los
define el servidor.
Almacenamiento: `join-stats.yml`.

## chat

Ruta `/zn chat` (alias `c`); orden en el menú 40; activado por defecto.

- Canales locales y globales: un prefijo de shout envía a todo el servidor, un radio
  local limita el resto; activación del shout y ocultación del chat por jugador.
- Formatos MiniMessage para el chat local y global con anulaciones por grupo (admin,
  mod, vip) elegidas por prioridad y permiso.
- Tooltips al pasar el cursor y acciones de clic en los nombres de los jugadores.
- Marcadores interactivos: `[item]`/`[i]`, `[inv]` y `[ender]`.
- Menciones a jugadores con un sonido opcional y notificación en la barra de acción.
- Moderación: enfriamiento con permiso de omisión, anti-duplicados, anti-mayúsculas y un
  filtro de palabrotas con palabras bloqueadas.
- Anuncios programados, desactivados por defecto.

Comandos: `/zn chat` (menú), `/zn chat shout`, `/zn chat toggle` (raíces opcionales
`/chattoggle`, `/hidechat`), `clear`, `mute`.

Permisos: `zn.chat.shout`, `zn.chat.admin.clear`, `zn.chat.admin.mute`,
`zn.chat.color`, `zn.chat.minimessage`, `zn.chat.bypass.cooldown`,
`zn.chat.bypass.mute` y `zn.chat.bypass.clear` (operadores); `zn.chat.toggle` (todos).
Almacenamiento: ninguno; el estado de toggle y mute se mantiene en memoria.

## inventory

Ruta `/zn inventory` (alias `inv`); orden en el menú 50; activado por defecto.

- Inspección en vivo del inventario y el cofre de ender de otro jugador, con un modo de
  modificación opcional.
- Equivalentes de clear, clone y give, incluidos los del cofre de ender, un comando de
  reversión que restaura una instantánea de muerte y una purga de instantáneas de muerte
  de jugadores desconectados.
- Las instantáneas de muerte se capturan mediante un listener de muerte.

Comandos: `/inventory`, `/invsee`, `/endersee` (`/ecsee`), `/clearinventory` (`/ci`),
`enderclear`, `clone`, `enderclone`, `give`, `endergive`, `/invrollback`, `reload`.

Permisos: `zn.inventory.see`, `zn.inventory.clear`, `zn.inventory.clone`,
`zn.inventory.give`, `zn.inventory.rollback`, `zn.inventory.admin` (operadores).
Almacenamiento: ninguno; las instantáneas se mantienen en memoria.

## clans

Ruta `/zn clans` (alias `clan`); orden en el menú 60; activado por defecto.

- Creación y ciclo de vida del clan: disolución, invitación, aceptación, expulsión,
  salida, cambio de nombre, descripción, rangos, home y home-set.
- Diplomacia y guerra: aliados, rivales, guerras, rivalidades y fuego amigo (personal,
  de clan y global).
- Herramientas de comunidad: boletín, estadísticas, lista de miembros, lista, consulta,
  reagrupación, confianza, silencio, estandarte, bajas, más eliminados, coordenadas,
  signos vitales, perfil, idioma, ayuda y menú.

Comandos: 39 acciones, todas solo para jugadores; la lista completa está en la página
[Comandos](commands.md).

Permisos: `zn.clans.player` (todos); las acciones administrativas (`verify`, `ban`,
`unban`, `globalff`) además requieren `zn.admin`.
Almacenamiento: `clans.yml`.

## itemedit

Ruta `/zn itemedit` (alias `ie`); orden en el menú 70; activado por defecto.

- Edita el objeto de la mano principal: renombrado, líneas de lore, encantamientos,
  marca de irrompible, modificadores de atributos, custom model data y flags del objeto.
- Muestra información del objeto, importa datos de objetos en Base64, guarda objetos
  bajo claves y gestiona objetos de servidor.
- Se abre un editor basado en diálogos cuando los diálogos están activados.

Comandos: `/itemedit` (`/ie`), `/rename`, `/lore`, `enchant`, `unbreakable`,
`attribute`, `custommodeldata`, `flags`, `info`, `import`, `storage`, `serveritem`.

Permisos: `zn.itemedit.admin` (operadores); el nodo heredado `zellysnexus.itemedit` lo
concede.
Almacenamiento: `items.yml`.

## tab

Ruta `/zn tab` (alias `t`); orden en el menú 80; activado por defecto.

- Renderiza el encabezado y el pie de la tab list, fija el nombre del jugador en la
  lista y muestra una boss bar al entrar cuyo color, superposición y duración provienen
  de los ajustes de tab.
- Activación por jugador, información y una recarga de la tab list para todos los
  jugadores en línea.

Comandos: `menu`, `info`, `reload`, `toggle`.

Permisos: `menu`, `info` y `toggle` no requieren permiso; `reload` requiere
`zn.admin.reload` (operadores).
Almacenamiento: ninguno.

## integrations

Ruta `/zn integrations` (alias `int`); orden en el menú 90; activado por defecto.

- Informa de si se encontraron plugins conocidos al arrancar: PlaceholderAPI, LuckPerms,
  Geyser-Spigot, Floodgate y BlockProt o BlockProtReloaded.
- Busca el grupo principal y el prefijo de un jugador en LuckPerms, e informa de si un
  jugador entró a través de Floodgate.

Comandos: `menu`, `perms <player>`, `bedrock <player>`.

Permisos: `zn.admin.integrations` (operadores).
Almacenamiento: ninguno; no se incluye ningún archivo de configuración para este módulo.

## updater

Sin ruta de comando; el módulo no tiene comandos visibles para el usuario. Activado por
defecto, pero se carga solo cuando `updater.check-on-boot` es true.

Comprueba de forma asíncrona el repositorio de GitHub en busca de una etiqueta más
nueva al arrancar y registra uno de tres mensajes traducidos: actualización disponible
(con versión y URL), al día o comprobación fallida.

## debug

Ruta `/zn debug` (alias `dbg`); orden en el menú 100; desactivado por defecto (actívalo
con `modules.debug.enabled` y reinicia).

- Ejecuta autopruebas de un área o de todas las áreas e informa de líneas de aprobado o
  fallido con un resumen; cada área tiene un tiempo límite de 10 segundos.
- Las 16 áreas son: environment, configuration, translation, persistence, storage,
  listeners, commands_permissions, user_interface, utilities, player_simulation, auth,
  clans, files, toolkit, threads y world.
- Escribe un informe con fecha en la carpeta de datos del plugin, bajo `debug/`.

Comandos: `/zn debug [area]`, `/zn debug menu`.

Permisos: `zn.debug` (operadores).
Almacenamiento: `debug/debug-<date>.log`.
