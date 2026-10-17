# Comandos

Se accede a todas las funciones de Zelly's Nexus mediante un único comando raíz, `/zn <module> <action>`. Cada módulo también tiene un alias corto. Ejecutar `/zn` o `/zn menu` abre el diálogo de navegación para los jugadores cuando los diálogos están habilitados en `config.yml`, y en caso contrario imprime la lista de módulos. `/zn help` lista los módulos que el remitente puede usar.

| Módulo | Ruta | Alias |
|---|---|---|
| Auth | `/zn auth` | `a` |
| Antibot | `/zn antibot` | `ab` |
| Toolkit (teletransporte, jugador, servidor, moderación, kits, ítems) | `/zn toolkit` | `tools` |
| Chat | `/zn chat` | `c` |
| Inventory | `/zn inventory` | `inv` |
| Clans | `/zn clans` | `clan` |
| ItemEdit | `/zn itemedit` | `ie` |
| Tab | `/zn tab` | `t` |
| Integrations | `/zn integrations` | `int` |
| Debug | `/zn debug` | `dbg` |

Un módulo aparece solo cuando está habilitado bajo `modules` en `config.yml`. Todos los módulos están habilitados por defecto excepto Debug.

Los paréntesis angulares marcan un argumento obligatorio y los corchetes marcan uno opcional.

## Alias raíz

La mayoría de las acciones también se pueden ejecutar como un comando raíz directo, por ejemplo `/spawn` en lugar de `/zn toolkit spawn`. Estos alias son opcionales y se controlan en `config.yml`:

- `commands.register-root-aliases` activa o desactiva todos los alias raíz opcionales. El valor por defecto es `true`.
- `commands.disabled-root-aliases` lista los nombres de comandos raíz que nunca se registran. La lista por defecto es `kill`, `kick`, `time`, `weather`, `msg` y `gamemode`. Estos nombres entran en conflicto con los comandos vanilla, por lo que las versiones vanilla siguen funcionando. Elimina un nombre de la lista para que Zelly's Nexus reemplace el comando vanilla. La ruta `/zn` no se ve afectada y siempre funciona.

`/zn` siempre está registrado. `/auth`, `/zantibot`, `/clan`, `/inventory` y `/itemedit` se registran siempre que su módulo esté habilitado, sin importar lo que digan estas dos opciones. Los alias raíz siguen las mismas reglas de permisos, consola e inicio de sesión que la ruta `/zn`.

## Permisos

Cada tabla lista el nodo y su valor por defecto. "Todos" significa que el nodo se concede a todos los jugadores por defecto y "Operadores" significa que se concede solo a los operadores.

Las acciones de Teletransporte, Jugador, Servidor, Moderación, Kits e Ítems usan el nodo `zn.<domain>.<action>`, donde el dominio es `teleport`, `player`, `server`, `moderation`, `kit` o `items`. Para estas acciones también se aceptan los siguientes nodos:

- `zn.admin` y `zn.toolkit.admin` conceden todas las acciones de estos dominios.
- `zn.toolkit.<action>` concede una sola acción, por ejemplo `zn.toolkit.heal`.
- `zn.toolkit.mod` se acepta para `socialspy` y para las acciones de moderación `kick`, `kickall`, `kill`, `mute`, `unmute`, `jail`, `unjail`, `togglejail`, `jails`, `jailedplayers`, `burn`, `extinguish`, `lightning` y `whois`.
- `zn.moderation.mute` también se acepta para `unmute`, y `zn.moderation.jail` para `unjail`, `togglejail`, `jails` y `jailedplayers`.
- `zn.teleport.home` también se acepta para `sethome`, `delhome`, `homes` y `renamehome`; `zn.teleport.warp` para `warps` y `warpinfo`; `zn.teleport.tpa` para `tpahere`, `tpaccept`, `tpdeny`, `tpacancel` y `tptoggle`; y `zn.teleport.rtp` o `zn.toolkit.rtp` para `tpr`.

Otros nodos heredados: `zellysnexus.itemedit` concede `zn.itemedit.admin`, y `zn.antibot` concede `zn.antibot.admin`.

`zn.admin` también lo comprueban `/zn reload` y las acciones administrativas de Clans. El plugin no lo declara, por lo que lo tienen los operadores y cualquier persona a la que se le conceda explícitamente.

## Consola

La columna Consola indica si la consola puede ejecutar el comando. "Sí (objetivo obligatorio)" significa que la consola debe indicar un jugador objetivo. Los comandos marcados con "No" deben ser ejecutados por un jugador.

## Bloqueo previo al inicio de sesión

Cuando el módulo Auth está habilitado, un jugador que no ha iniciado sesión queda bloqueado. Se bloquean el movimiento, romper y colocar bloques, la interacción, el chat, soltar y recoger ítems, el daño y los clics en el inventario. Los únicos comandos que funcionan son `/zn`, `/zn menu`, `/zn help`, `/zn auth` (y `/zn a`) y los alias raíz de Auth que estén registrados; `/zn` y `/zn menu` abren el formulario de inicio de sesión en lugar del menú, o muestran el mensaje de inicio de sesión cuando los diálogos están desactivados. Todos los demás comandos se cancelan y se le pide al jugador que inicie sesión. Dentro de `/zn auth`, antes de iniciar sesión solo funcionan `login`, `register`, `captcha`, `form` y `menu`. `/zn antibot` no está disponible antes de iniciar sesión.

Si el módulo Auth está habilitado pero no se carga, ningún jugador puede entrar: se rechaza cada conexión con un mensaje traducido hasta que el módulo vuelva a cargarse tras un reinicio.

Los argumentos de `/login`, `/l`, `/register`, `/reg`, `/changepassword`, `/changepw`, `/email`, `/pin` y `/totp`, y de las acciones `login`, `register`, `changepassword`, `unregister`, `email`, `pin`, `totp` y `otp` de `/auth` y `/zn auth`, se reemplazan por `***` en el registro del servidor.

## Núcleo

Estos comandos pertenecen al comando raíz y están siempre disponibles.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/zn` | `[menu]` | Abre el diálogo de navegación para los jugadores cuando los diálogos están habilitados, y en caso contrario lista los módulos disponibles. | Ninguno | Todos | Sí (lista de módulos) |
| Ninguno | Ninguno | Lista los módulos que el remitente puede usar. | Ninguno | Todos | Sí |
| Ninguno | Ninguno | Recarga `config.yml`. El idioma se aplica de inmediato a todos los mensajes de los comandos, al bloqueo previo al inicio de sesión y a todos los menús que se abran después; un diálogo que ya esté abierto, y el encabezado y el pie de la tablist hasta la siguiente conexión o `/zn tab reload`, mantienen el texto antiguo. La opción de diálogos se aplica de inmediato. Cambiar la habilitación de un módulo necesita un reinicio del servidor; se informa al remitente y se registra una advertencia. | `zn.admin` | Operadores | Sí |

## Auth

Ruta: `/zn auth` (alias `a`). Todos los comandos de Auth son solo para jugadores. El permiso del módulo es `zn.auth.player`, que todos tienen por defecto. Las acciones administrativas también necesitan `zn.auth.admin`, que los operadores tienen por defecto. Antes de iniciar sesión solo funcionan `login`, `register`, `captcha`, `form` y `menu`. Los alias raíz `/auth`, `/login`, `/l`, `/register`, `/reg`, `/changepassword`, `/changepw`, `/logout`, `/pin`, `/totp` y `/email` ejecutan la acción correspondiente; solo `/auth` está siempre registrado.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/auth` | `[action]` | Abre el menú de Auth, o ejecuta una de las acciones siguientes. | `zn.auth.player` | Todos | No |
| `/register`, `/reg` | `<password>` | Registra una cuenta. | `zn.auth.player` | Todos | No |
| `/login`, `/l` | `<password>` | Inicia sesión. | `zn.auth.player` | Todos | No |
| `/logout` | Ninguno | Cierra la sesión actual. | `zn.auth.player` | Todos | No |
| Ninguno | `<password>` | Elimina el registro de la cuenta. | `zn.auth.player` | Todos | No |
| `/changepassword`, `/changepw` | `<old> <new>` | Cambia la contraseña. | `zn.auth.player` | Todos | No |
| `/email` | `add <email>`, `change <email>`, `recover`, `recover <code> <newPassword>` | Gestiona el correo de recuperación; `recover` emite un código y después restablece la contraseña con él. | `zn.auth.player` | Todos | No |
| `/totp` | `setup`, `confirm <code>`, `disable` | Gestiona los códigos de doble factor. | `zn.auth.player` | Todos | No |
| Ninguno | `generate`, `verify <code>` | Genera y verifica un código de un solo uso. | `zn.auth.player` | Todos | No |
| `/pin` | `set <pin>`, `verify <pin>`, `reset` | Gestiona el PIN secundario. | `zn.auth.player` | Todos | No |
| Ninguno | `<on\|off>` | Activa o desactiva recordar la sesión. | `zn.auth.player` | Todos | No |
| Ninguno | `[answer]` | Emite un desafío de captcha, o lo responde. | `zn.auth.player` | Todos | No |
| Ninguno | `[code]` | Emite un código de verificación, o lo confirma. | `zn.auth.player` | Todos | No |
| Ninguno | Ninguno | Abre el formulario de inicio de sesión y registro cuando los diálogos están habilitados. | `zn.auth.player` | Todos | No |
| Ninguno | Ninguno | Abre el menú de Auth. | `zn.auth.player` | Todos | No |
| Ninguno | `<player>` | Elimina la cuenta de un jugador en línea. | `zn.auth.admin` | Operadores | No |
| Ninguno | `<player>` | Marca a un jugador en línea como premium. | `zn.auth.admin` | Operadores | No |
| Ninguno | `<player>` | Marca a un jugador en línea como cracked. | `zn.auth.admin` | Operadores | No |
| Ninguno | `<player>` | Marca a un jugador en línea como freemium. | `zn.auth.admin` | Operadores | No |
| Ninguno | `<player>` | Muestra el registro de autenticación de un jugador en línea. | `zn.auth.admin` | Operadores | No |
| Ninguno | `reload`, `purge [days]`, `forcelogin <player>` | Recarga los datos de auth, purga las cuentas inactivas (30 días por defecto) o hace que un jugador en línea inicie sesión. | `zn.auth.admin` | Operadores | No |
| Ninguno | `[action]` | Ejecuta una acción de Antibot; requiere el permiso de Antibot. | `zn.antibot.admin` | Operadores | No |

## Antibot

Ruta: `/zn antibot` (alias `ab`). Alias raíz: `/zantibot` está siempre registrado y `/antibot` es opcional. Permiso: `zn.antibot.admin`, que los operadores tienen por defecto; `zn.antibot` lo concede. Los comandos funcionan desde la consola y no están disponibles antes de iniciar sesión.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/zantibot`, `/antibot` | `[action]` | Abre el menú de Antibot para los jugadores, o imprime el uso. | `zn.antibot.admin` | Operadores | Sí |
| Ninguno | Ninguno | Abre el menú de Antibot. | `zn.antibot.admin` | Operadores | Sí |
| Ninguno | Ninguno | Muestra la tasa de conexiones, el número de bloqueos y el estado de pánico. | `zn.antibot.admin` | Operadores | Sí |
| Ninguno | `<on\|off>` | Activa o desactiva el modo pánico; el modo pánico bloquea cada conexión nueva. | `zn.antibot.admin` | Operadores | Sí |
| Ninguno | Ninguno | Lista las direcciones bloqueadas. | `zn.antibot.admin` | Operadores | Sí |
| Ninguno | `<address>` | Añade una dirección a la lista de bloqueo. | `zn.antibot.admin` | Operadores | Sí |
| Ninguno | `<address>` | Elimina una dirección de la lista de bloqueo. | `zn.antibot.admin` | Operadores | Sí |

## Toolkit

El Toolkit agrupa seis dominios de comandos: Teletransporte, Jugador, Servidor, Moderación, Kits e Ítems. Cada acción se ejecuta como `/zn toolkit <action>`, y la mayoría también están disponibles como un alias raíz opcional con el mismo nombre.

### Teletransporte

Cada comando también está disponible como un alias raíz opcional con el mismo nombre, y `/rtp` es un alias adicional de `/tpr`. Los nodos `zn.teleport.sethome`, `zn.teleport.delhome`, `zn.teleport.homes`, `zn.teleport.renamehome`, `zn.teleport.warps`, `zn.teleport.warpinfo`, `zn.teleport.tpahere`, `zn.teleport.tpaccept`, `zn.teleport.tpdeny`, `zn.teleport.tpacancel` y `zn.teleport.tptoggle` están declarados para operadores, pero esas acciones están abiertas a todos mediante `zn.teleport.home`, `zn.teleport.warp` y `zn.teleport.tpa`.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/spawn` | Ninguno | Te teletransporta al spawn del servidor. | `zn.teleport.spawn` | Todos | No |
| `/setspawn` | Ninguno | Establece el spawn del servidor en la posición actual. | `zn.teleport.setspawn` | Operadores | No |
| `/home` | `[name]` | Te teletransporta a un home; el nombre por defecto es `home`. | `zn.teleport.home` | Todos | No |
| `/sethome` | `[name]` | Guarda la posición actual como un home; el nombre por defecto es `home`. | `zn.teleport.sethome` | Todos | No |
| `/delhome` | `<name>` | Elimina un home. | `zn.teleport.delhome` | Todos | No |
| `/homes` | Ninguno | Lista los homes guardados. | `zn.teleport.homes` | Todos | No |
| `/renamehome` | `<home> <newName>` | Cambia el nombre de un home. | `zn.teleport.renamehome` | Todos | No |
| `/warp` | `[name]` | Te teletransporta a un warp, o lista los warps cuando no se indica un nombre. | `zn.teleport.warp` | Todos | No |
| `/setwarp` | `<name>` | Crea un warp en la posición actual. | `zn.teleport.setwarp` | Operadores | No |
| `/delwarp` | `<name>` | Elimina un warp. | `zn.teleport.delwarp` | Operadores | No |
| `/warps` | Ninguno | Lista los warps. | `zn.teleport.warps` | Todos | Sí |
| `/warpinfo` | `<name>` | Muestra las coordenadas y el mundo de un warp. | `zn.teleport.warpinfo` | Todos | Sí |
| `/tpa` | `<player>` | Envía una solicitud de teletransporte a un jugador. | `zn.teleport.tpa` | Todos | No |
| `/tpahere` | `<player>` | Pide a un jugador que se teletransporte hacia ti. | `zn.teleport.tpahere` | Todos | No |
| `/tpaccept` | Ninguno | Acepta la solicitud de teletransporte pendiente. | `zn.teleport.tpaccept` | Todos | No |
| `/tpdeny` | Ninguno | Rechaza la solicitud de teletransporte pendiente. | `zn.teleport.tpdeny` | Todos | No |
| `/tpacancel` | Ninguno | Cancela las solicitudes que hayas enviado. | `zn.teleport.tpacancel` | Todos | No |
| `/tpaall` | Ninguno | Envía una solicitud de teletransporte a todos los jugadores en línea que acepten solicitudes. | `zn.teleport.tpaall` | Operadores | No |
| `/tptoggle` | Ninguno | Activa o desactiva la recepción de solicitudes de teletransporte. | `zn.teleport.tptoggle` | Todos | No |
| `/tpr`, `/rtp` | Ninguno | Te teletransporta a una ubicación aleatoria dentro del rango configurado. | `zn.teleport.tpr` | Operadores | No |
| `/settpr` | `<min> <max>` | Establece el rango de teletransporte aleatorio hasta el siguiente reinicio. El rango no se guarda; `rtp-min` y `rtp-max` de `modules/toolkit.yml` vuelven a aplicarse en el siguiente arranque. | `zn.teleport.settpr` | Operadores | Sí |
| `/back` | Ninguno | Regresa a la última ubicación guardada. | `zn.teleport.back` | Operadores | No |
| `/top` | Ninguno | Te teletransporta al bloque más alto en la posición actual. | `zn.teleport.top` | Operadores | No |
| `/bottom` | Ninguno | Te teletransporta al fondo del mundo en la posición actual. | `zn.teleport.bottom` | Operadores | No |
| `/jump` | Ninguno | Te teletransporta al bloque que estás mirando, hasta 32 bloques de distancia. | `zn.teleport.jump` | Operadores | No |
| `/tpo` | `<player>` | Te teletransporta a un jugador sin solicitud. | `zn.teleport.tpo` | Operadores | No |
| `/tphere` | `<player>` | Teletransporta a un jugador hacia ti. | `zn.teleport.tphere` | Operadores | No |
| `/tpall` | Ninguno | Teletransporta a todos los jugadores en línea hacia ti. | `zn.teleport.tpall` | Operadores | No |
| `/tppos` | `<x> <y> <z>` | Te teletransporta a unas coordenadas en el mundo actual. | `zn.teleport.tppos` | Operadores | No |
| `/tp` | `<player>` | Te teletransporta a un jugador en línea. | `zn.teleport.tp` | Operadores | No |
| `/tpohere` | `<player>` | Teletransporta a un jugador en línea a tu ubicación. | `zn.teleport.tpohere` | Operadores | No |
| `/tpoffline` | `<player>` | Te teletransporta a la última ubicación de desconexión del jugador. Aún no implementado: actualmente el comando solo envía el mensaje de confirmación y no mueve al jugador. | `zn.teleport.tpoffline` | Operadores | No |
| `/tpauto` | Ninguno | Activa o desactiva la aceptación automática de tus solicitudes de teletransporte. | `zn.teleport.tpauto` | Operadores | No |
| `/world` | `<world>` | Te teletransporta al spawn de un mundo. | `zn.teleport.world` | Operadores | No |

### Jugador

Cada comando también está disponible como un alias raíz opcional con el mismo nombre. Alias adicionales: `/wb` para `/workbench`, `/ec` para `/enderchest` y `/r` para `/reply`. `/msg` y `/gamemode` están en la lista de deshabilitados por defecto.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/heal` | `[player]` | Restaura la salud al máximo. | `zn.player.heal` | Operadores | Sí (objetivo obligatorio) |
| `/feed` | `[player]` | Restaura el nivel de comida al máximo. | `zn.player.feed` | Operadores | Sí (objetivo obligatorio) |
| `/fly` | `[player]` | Activa o desactiva el vuelo. | `zn.player.fly` | Operadores | Sí (objetivo obligatorio) |
| `/god` | `[player]` | Activa o desactiva el modo dios. | `zn.player.god` | Operadores | Sí (objetivo obligatorio) |
| `/speed` | `<1-10> [player]` | Establece la velocidad de caminar y de volar. | `zn.player.speed` | Operadores | Sí (objetivo obligatorio) |
| `/workbench`, `/wb` | Ninguno | Abre una mesa de trabajo. | `zn.player.workbench` | Operadores | No |
| `/enderchest`, `/ec` | Ninguno | Abre tu cofre de ender. | `zn.player.enderchest` | Operadores | No |
| `/disposal` | Ninguno | Abre un inventario de eliminación. | `zn.player.disposal` | Operadores | No |
| `/hat` | Ninguno | Coloca el ítem en la mano sobre tu cabeza. | `zn.player.hat` | Operadores | No |
| `/zn prank` | `[player] [level]` | Ejecuta una broma a un jugador (niveles 1-5, 5.5 o 6), o abre el menú de bromas. | `zn.player.prank` | Operadores | Sí (con objetivo) |
| `/ping` | `[player]` | Muestra la latencia de un jugador. | `zn.player.ping` | Todos | Sí (objetivo obligatorio) |
| `/near` | Ninguno | Lista los jugadores dentro del radio configurado. | `zn.player.near` | Todos | No |
| `/msg` | `<player> <text>` | Envía un mensaje privado. | `zn.player.msg` | Todos | Sí |
| `/reply`, `/r` | `<text>` | Responde al último mensaje privado. | `zn.player.reply` | Todos | No |
| `/msgtoggle` | Ninguno | Activa o desactiva la recepción de mensajes privados. | `zn.player.msgtoggle` | Todos | No |
| `/socialspy` | Ninguno | Activa o desactiva la visualización de los mensajes privados de otros. | `zn.player.socialspy` | Operadores | No |
| `/nick` | `[name]` | Establece el nombre visible, o lo restablece cuando no se indica un nombre. | `zn.player.nick` | Todos | No |
| `/realname` | `<nick>` | Muestra el nombre real detrás de un apodo. | `zn.player.realname` | Todos | Sí |
| `/suicide` | Ninguno | Te mata a ti mismo. | `zn.player.suicide` | Todos | No |
| `/mail` | `read \| clear \| send <player> <text>` | Lee o borra tu correo, o envía correo a un jugador en línea. | `zn.player.mail` | Todos | Sí (solo envío) |
| `/getpos` | Ninguno | Muestra tus coordenadas y tu mundo. | `zn.player.getpos` | Todos | No |
| `/seen` | `<player>` | Muestra cuánto tiempo ha pasado desde la última vez que un jugador estuvo en línea. | `zn.player.seen` | Todos | Sí |
| `/helpop` | `<text>` | Envía un mensaje al personal en línea. | `zn.player.helpop` | Todos | Sí |
| `/more` | Ninguno | Rellena la pila de la mano hasta su tamaño máximo. | `zn.player.more` | Operadores | No |
| `/repair` | Ninguno | Restaura la durabilidad del ítem en la mano. | `zn.player.repair` | Operadores | No |
| `/unlimited` | Ninguno | Activa o desactiva la colocación ilimitada de bloques. | `zn.player.unlimited` | Operadores | No |
| `/gamemode` | `<survival\|creative\|adventure\|spectator> [player]` | Establece el modo de juego. | `zn.player.gamemode` | Operadores | Sí (objetivo obligatorio) |
| `/afk` | Ninguno | Activa o desactiva tu estado AFK. | `zn.player.afk` | Todos | No |
| `/playtime` | `[player]` | Muestra cuánto tiempo ha jugado un jugador. | `zn.player.playtime` | Todos | Sí (objetivo obligatorio) |
| `/ptime` | `<day\|night\|reset>` | Establece tu hora personal (`day` son 1000 ticks y `night` son 13000). | `zn.player.ptime` | Operadores | No |
| `/pweather` | `<clear\|rain\|reset>` | Establece tu clima personal. | `zn.player.pweather` | Operadores | No |

### Servidor

Cada comando también está disponible como un alias raíz opcional con el mismo nombre. `/time` y `/weather` están en la lista de deshabilitados por defecto.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/time` | `<day\|noon\|night\|midnight\|ticks> [world]` | Establece la hora del mundo. | `zn.server.time` | Operadores | Sí |
| `/weather` | `<clear\|rain\|thunder> [world]` | Establece el clima. | `zn.server.weather` | Operadores | Sí |
| `/thunder` | `[world]` | Activa o desactiva los truenos. | `zn.server.thunder` | Operadores | Sí |
| `/broadcast` | `<text>` | Difunde un mensaje a todos los jugadores. | `zn.server.broadcast` | Operadores | Sí |
| `/motd` | Ninguno | Muestra el mensaje del día del servidor. | `zn.server.motd` | Todos | Sí |
| `/rules` | Ninguno | Muestra las reglas del servidor. | `zn.server.rules` | Todos | Sí |
| `/powertool` | `<command\|clear\|list\|toggle>` | Vincula un comando al ítem en la mano, borra la vinculación, lista las vinculaciones o activa y desactiva los powertools. | `zn.items.powertool` | Operadores | No |
| `/gc` | Ninguno | Muestra la memoria usada y total y los TPS del servidor. | `zn.server.gc` | Operadores | Sí |

### Moderación

Cada comando también está disponible como un alias raíz opcional con el mismo nombre, y `/ext` es un alias adicional de `/extinguish`. `/kill` y `/kick` están en la lista de deshabilitados por defecto. Consulta el resumen de Permisos para ver los nodos heredados que se aceptan aquí. Las acciones de ban, ban de IP, expulsión, suspensión y reactivación necesitan el módulo ban: con `modules.ban.enabled: false` responden que está deshabilitado, y sus pantallas y ajustes provienen de `modules/ban.yml`.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/kick` | `<player> [reason]` | Expulsa a un jugador. | `zn.moderation.kick` | Operadores | Sí |
| `/kickall` | Ninguno | Expulsa a todos los jugadores en línea excepto al remitente. | `zn.moderation.kickall` | Operadores | Sí |
| `/kill` | `[player]` | Mata a un jugador, o a ti mismo. | `zn.moderation.kill` | Operadores | Sí (objetivo obligatorio) |
| `/vanish` | Ninguno | Activa o desactiva la invisibilidad ante los demás jugadores. | `zn.moderation.vanish` | Operadores | No |
| `/mute` | `<player>` | Silencia a un jugador en el chat. | `zn.moderation.mute` | Operadores | Sí |
| `/unmute` | `<player>` | Quita el silencio a un jugador. | `zn.moderation.unmute` | Operadores | Sí |
| `/jail` | `<player> [jail]` | Encarcela a un jugador en la cárcel indicada, o en la primera cárcel definida. | `zn.moderation.jail` | Operadores | Sí |
| `/togglejail` | `<player> [jail]` | Encarcela a un jugador, o libera a un jugador que ya está encarcelado. | `zn.moderation.togglejail` | Operadores | Sí |
| `/unjail` | `<player>` | Libera a un jugador encarcelado. | `zn.moderation.unjail` | Operadores | Sí |
| `/setjail` | `<name>` | Crea una cárcel en la posición actual. | `zn.moderation.setjail` | Operadores | No |
| `/deljail` | `<name>` | Elimina una cárcel. | `zn.moderation.deljail` | Operadores | Sí |
| `/jails` | Ninguno | Lista las cárceles. | `zn.moderation.jails` | Operadores | Sí |
| `/jailedplayers` | Ninguno | Lista los jugadores encarcelados. | `zn.moderation.jailedplayers` | Operadores | Sí |
| `/sudo` | `<player> <command>` | Hace que un jugador ejecute un comando. | `zn.moderation.sudo` | Operadores | Sí |
| `/burn` | `<player>` | Prende fuego a un jugador durante la duración configurada. | `zn.moderation.burn` | Operadores | Sí |
| `/extinguish`, `/ext` | `[player]` | Apaga el fuego de un jugador. | `zn.moderation.extinguish` | Operadores | Sí (objetivo obligatorio) |
| `/lightning` | `[player]` | Lanza un rayo sobre un jugador, o sobre el bloque que estás mirando. | `zn.moderation.lightning` | Operadores | Sí (objetivo obligatorio) |
| `/whois` | `[player]` | Muestra la dirección, el UUID y el modo de juego de un jugador. | `zn.moderation.whois` | Operadores | Sí (objetivo obligatorio) |
| `/ban` | `<player> [reason]` | Banea a un jugador de forma permanente. | `zn.moderation.ban` | Operadores | Sí |
| `/tempban` | `<player> <minutes> [reason]` | Banea a un jugador durante el número de minutos indicado. | `zn.moderation.tempban` | Operadores | Sí |
| `/unban` | `<player>` | Levanta el ban de un jugador. | `zn.moderation.unban` | Operadores | Sí |
| `/banip` | `<ip\|player> [reason]` | Banea una dirección IP de forma permanente. | `zn.moderation.banip` | Operadores | Sí |
| `/tempbanip` | `<ip\|player> <minutes> [reason]` | Banea una dirección IP durante el número de minutos indicado. | `zn.moderation.tempbanip` | Operadores | Sí |
| `/unbanip` | `<ip>` | Levanta el ban de una IP. | `zn.moderation.unbanip` | Operadores | Sí |
| `/suspend` | `<player> [duration] [reason]` | Suspende a un jugador; sin un motivo abre el diálogo de suspensión para el personal en línea. | `zn.moderation.suspend` | Operadores | Sí |
| `/unsuspend` | `<player>` | Levanta la suspensión. | `zn.moderation.unsuspend` | Operadores | Sí |
| `/nuke` | `[player]` | Genera cinco TNT activadas sobre el objetivo, o sobre ti mismo. | `zn.moderation.nuke` | Operadores | Sí (objetivo obligatorio) |

### Kits

Cada comando también está disponible como un alias raíz opcional con el mismo nombre.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/kit` | `[name]` | Da un kit, o lista los kits cuando no se indica un nombre. | `zn.kit.kit` | Todos | Sí (solo listado) |
| `/kits` | Ninguno | Lista los kits. | `zn.kit.kits` | Todos | Sí |
| `/showkit` | `<name>` | Muestra la cantidad de ítems de un kit. | `zn.kit.showkit` | Todos | Sí |
| `/createkit` | `<name> [cooldownSeconds]` | Crea un kit a partir de tu inventario con un tiempo de espera opcional en segundos. | `zn.kit.createkit` | Operadores | No |
| `/delkit` | `<name>` | Elimina un kit. | `zn.kit.delkit` | Operadores | Sí |
| `/kitreset` | `<player> [kit]` | Restablece el tiempo de espera de un kit, o de todos los kits, para un jugador. | `zn.kit.kitreset` | Operadores | Sí |

### Acciones adicionales del toolkit

El Toolkit también registra las acciones siguientes, a las que se llega de la misma forma (`/zn toolkit <action>`). Siguen el mismo esquema de permisos, por lo que el nodo es `zn.<domain>.<action>`.

| Acción | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|
| `compass` | Muestra tu orientación y la dirección hacia la que miras. | `zn.player.compass` | Todos | No |
| `customtext` | Imprime el texto indicado: customtext <text>. | `zn.player.customtext` | Operadores | Sí |
| `depth` | Muestra tu profundidad respecto al nivel del mar. | `zn.player.depth` | Todos | No |
| `exp` | Muestra el nivel y la experiencia total de un jugador, y otorga experiencia cuando se indica una cantidad. | `zn.player.exp` | Operadores | Sí |
| `gma` | Establece el modo de juego en aventura. | `zn.player.gma` | Operadores | Sí |
| `gmc` | Establece el modo de juego en creativo. | `zn.player.gmc` | Operadores | Sí |
| `gmsp` | Establece el modo de juego en espectador. | `zn.player.gmsp` | Operadores | Sí |
| `gms` | Establece el modo de juego en supervivencia. | `zn.player.gms` | Operadores | Sí |
| `help` | Lista las acciones del toolkit. | `zn.player.help` | Todos | Sí |
| `ice` | Atrapa a un jugador en hielo. | `zn.player.ice` | Operadores | No |
| `ignore` | Activa o desactiva ignorar a un jugador en línea. | `zn.player.ignore` | Operadores | No |
| `info` | Muestra el número de jugadores en línea. | `zn.player.info` | Todos | Sí |
| `list` | Lista los jugadores en línea. | `zn.player.list` | Todos | Sí |
| `me` | Difunde un mensaje de emote. | `zn.player.me` | Operadores | Sí |
| `potion` | Aplica un efecto de poción: potion <effect> [duration] [amplifier] [player]. | `zn.player.potion` | Operadores | Sí |
| `rest` | Restablece tu estadística de tiempo desde el último descanso (el temporizador de los fantasmas). | `zn.player.rest` | Operadores | No |
| `rtoggle` | Establece o elimina un bloqueo de respuesta con un jugador; aún no aplicado. | `zn.player.rtoggle` | Operadores | No |
| `rules` | Muestra las reglas del servidor. | `zn.player.rules` | Operadores | Sí |
| `antioch` | Genera una TNT activada donde estás mirando, con el mensaje del Santo Grial. | `zn.server.antioch` | Operadores | No |
| `backup` | Guarda a los jugadores y a todos los mundos. | `zn.server.backup` | Operadores | Sí |
| `beezooka` | Dispara la Beezooka. | `zn.server.beezooka` | Operadores | No |
| `bigtree` | Hace crecer un árbol grande donde estás mirando. | `zn.server.bigtree` | Operadores | No |
| `broadcastworld` | Envía un mensaje a los jugadores de un mundo: broadcastworld <world> <text>. | `zn.server.broadcastworld` | Operadores | Sí |
| `fireball` | Lanza una bola de fuego. | `zn.server.fireball` | Operadores | No |
| `firework` | Lanza un fuego artificial. | `zn.server.firework` | Operadores | No |
| `kittycannon` | Dispara el cañón de gatitos. | `zn.server.kittycannon` | Operadores | No |
| `spawnmob` | Genera un mob (hasta 50) en tu posición: spawnmob <mob> [amount]. | `zn.server.spawnmob` | Operadores | No |
| `tree` | Hace crecer un árbol donde estás mirando; un argumento opcional elige el tipo de árbol. | `zn.server.tree` | Operadores | No |
| `removeentities` | Elimina los ítems tirados y los mobs. | `zn.moderation.removeentities` | Operadores | Sí |
| `anvil` | Abre un yunque. | `zn.items.anvil` | Operadores | No |
| `book` | Desbloquea un libro escrito (restaura su generación a la original). | `zn.items.book` | Operadores | No |
| `break` | Rompe el bloque que estás mirando. | `zn.items.break` | Operadores | No |
| `cartographytable` | Abre una mesa de cartografía. | `zn.items.cartographytable` | Operadores | No |
| `clearinventory` | Borra el inventario de un jugador; por defecto, el tuyo propio. | `zn.items.clearinventory` | Operadores | Sí |
| `condense` | Condensa los ítems en su forma de bloque. | `zn.items.condense` | Operadores | No |
| `editsign` | Reescribe una línea del cartel que estás mirando: editsign <1-4> <text>. | `zn.items.editsign` | Operadores | No |
| `give` | Da ítems a un jugador en línea: give <player> <material> [amount]. | `zn.items.give` | Operadores | Sí |
| `grindstone` | Abre una piedra de afilar. | `zn.items.grindstone` | Operadores | No |
| `item` | Da un ítem por nombre de material: item <material> [amount]. | `zn.items.item` | Operadores | No |
| `itemdb` | Muestra el material y la cantidad del ítem de tu mano principal. | `zn.items.itemdb` | Todos | No |
| `itemlore` | Actualiza el lore del ítem en la mano. | `zn.items.itemlore` | Operadores | No |
| `itemname` | Establece el nombre del ítem en la mano. | `zn.items.itemname` | Operadores | No |
| `loom` | Abre un telar. | `zn.items.loom` | Operadores | No |
| `powertoollist` | Lista las vinculaciones de powertools. | `zn.items.powertoollist` | Operadores | No |
| `powertooltoggle` | Activa o desactiva los powertools. | `zn.items.powertooltoggle` | Operadores | No |
| `recipe` | Muestra el encabezado de la receta del ítem en la mano o de un material indicado. Aún no implementado: solo se envía el encabezado. | `zn.items.recipe` | Todos | No |
| `skull` | Te da una cabeza de jugador del jugador objetivo, o de ti mismo. | `zn.items.skull` | Operadores | No |
| `smithingtable` | Abre una mesa de herrería. | `zn.items.smithingtable` | Operadores | No |
| `spawner` | Cambia el tipo del spawner que estás mirando: spawner <mob>. | `zn.items.spawner` | Operadores | No |
| `stonecutter` | Abre un cortapiedras. | `zn.items.stonecutter` | Operadores | No |

## Clans

Ruta: `/zn clans` (alias `clan`). Alias raíz: `/clan` está siempre registrado y `/clans` es opcional. Todos los comandos de Clans son solo para jugadores. El permiso del módulo es `zn.clans.player`, que todos tienen por defecto. Las acciones administrativas también necesitan `zn.admin`. Ejecutar el comando sin una acción abre el menú de clanes cuando los diálogos están habilitados.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/clan create` | `<name>` | Crea un clan. | `zn.clans.player` | Todos | No |
| `/clan disband` | Ninguno | Disuelve tu clan. | `zn.clans.player` | Todos | No |
| `/clan invite` | `<player>` | Invita a un jugador en línea. | `zn.clans.player` | Todos | No |
| `/clan accept` | Ninguno | Acepta una invitación de clan. | `zn.clans.player` | Todos | No |
| `/clan kick` | `<player>` | Elimina a un miembro. | `zn.clans.player` | Todos | No |
| `/clan leave` | Ninguno | Abandona tu clan. | `zn.clans.player` | Todos | No |
| `/clan ally` | `<add\|remove> <clan>` | Añade o elimina una alianza. | `zn.clans.player` | Todos | No |
| `/clan rival` | `<add\|remove> <clan>` | Añade o elimina una rivalidad. | `zn.clans.player` | Todos | No |
| `/clan war` | `<start\|end> <clan>` | Inicia o termina una guerra. | `zn.clans.player` | Todos | No |
| `/clan rank` | `create <rank> \| delete <rank> \| set <player> <rank> \| list` | Gestiona los rangos del clan. | `zn.clans.player` | Todos | No |
| `/clan home` | Ninguno | Te teletransporta al home del clan. | `zn.clans.player` | Todos | No |
| `/clan home-set` | Ninguno | Establece el home del clan en la posición actual. | `zn.clans.player` | Todos | No |
| `/clan description` | `<text>` | Establece la descripción del clan. | `zn.clans.player` | Todos | No |
| `/clan verify` | `<clan>` | Marca un clan como verificado. | `zn.clans.player` y `zn.admin` | Operadores | No |
| `/clan ban` | `<player>` | Banea a un jugador de los clanes. | `zn.clans.player` y `zn.admin` | Operadores | No |
| `/clan unban` | `<player>` | Levanta un ban de clanes. | `zn.clans.player` y `zn.admin` | Operadores | No |
| `/clan ff` | `<on\|off>` | Activa o desactiva tu fuego amigo personal. | `zn.clans.player` | Todos | No |
| `/clan clanff` | `<on\|off>` | Activa o desactiva el fuego amigo dentro del clan. | `zn.clans.player` | Todos | No |
| `/clan globalff` | `<on\|off>` | Activa o desactiva el fuego amigo global. | `zn.clans.player` y `zn.admin` | Operadores | No |
| `/clan bb` | `[text]` | Publica en el tablón de anuncios del clan, o lo muestra cuando no se indica texto. | `zn.clans.player` | Todos | No |
| `/clan stats` | `<clan>` | Muestra las estadísticas de un clan. | `zn.clans.player` | Todos | No |
| `/clan roster` | `<clan>` | Muestra los miembros de un clan. | `zn.clans.player` | Todos | No |
| `/clan list` | Ninguno | Lista los clanes. | `zn.clans.player` | Todos | No |
| `/clan lookup` | `<player>` | Muestra el clan de un jugador en línea. | `zn.clans.player` | Todos | No |
| `/clan regroup` | Ninguno | Teletransporta hacia ti a los miembros del clan que están en línea. | `zn.clans.player` | Todos | No |
| `/clan trust` | `<player>` | Confía en un jugador. | `zn.clans.player` | Todos | No |
| `/clan untrust` | `<player>` | Elimina la confianza de un jugador. | `zn.clans.player` | Todos | No |
| `/clan mute` | `<player>` | Silencia a un miembro del clan. | `zn.clans.player` | Todos | No |
| `/clan setbanner` | `<banner>` | Establece el estandarte del clan. | `zn.clans.player` | Todos | No |
| `/clan kills` | Ninguno | Muestra los asesinatos de tu clan. | `zn.clans.player` | Todos | No |
| `/clan mostkilled` | Ninguno | Muestra a quién ha matado más tu clan. | `zn.clans.player` | Todos | No |
| `/clan coords` | Ninguno | Muestra las coordenadas de los miembros del clan que están en línea. | `zn.clans.player` | Todos | No |
| `/clan vitals` | Ninguno | Muestra la salud y la comida de los miembros del clan que están en línea. | `zn.clans.player` | Todos | No |
| `/clan rivalries` | Ninguno | Lista los rivales de tu clan. | `zn.clans.player` | Todos | No |
| `/clan profile` | `[clan]` | Muestra el perfil de un clan; por defecto, el tuyo propio. | `zn.clans.player` | Todos | No |
| `/clan rename` | `<name>` | Cambia el nombre de tu clan. | `zn.clans.player` | Todos | No |
| `/clan locale` | `<locale>` | Establece el idioma del clan. | `zn.clans.player` | Todos | No |
| `/clan help` | Ninguno | Lista los subcomandos del clan. | `zn.clans.player` | Todos | No |
| `/clan menu` | Ninguno | Abre el menú de clanes. | `zn.clans.player` | Todos | No |

## Chat

Ruta: `/zn chat` (alias `c`). Todos los comandos de Chat son solo para jugadores. Los alias raíz `/shout`, `/chattoggle` y `/hidechat` son opcionales. Mientras escribes en el chat, `[item]`, `[inv]` y `[ender]` se reemplazan por el ítem en la mano y por enlaces clicables al inventario y al cofre de ender.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| Ninguno | Ninguno | Abre el menú de Chat cuando los diálogos están habilitados. | Ninguno | Todos | No |
| `/shout` | `[on\|off]` | Activa o desactiva, o establece, el chat para todo el servidor en lugar de para los jugadores cercanos. | `zn.chat.shout` | Operadores | No |
| `/chattoggle`, `/hidechat` | Ninguno | Activa o desactiva ocultar los mensajes del chat para ti. | Ninguno | Todos | No |
| Ninguno | Ninguno | Borra el chat para todos los jugadores. | `zn.chat.admin.clear` | Operadores | No |
| Ninguno | `<player>` | Silencia a un jugador en el chat. | `zn.chat.admin.mute` | Operadores | No |

## Inventory

Ruta: `/zn inventory` (alias `inv`). Alias raíz: `/inventory` está siempre registrado; `/invsee`, `/endersee`, `/ecsee`, `/clearinventory`, `/ci` y `/invrollback` son opcionales. Todos los comandos de Inventory son solo para jugadores. Las rutas `/zn inventory` y `/inventory` necesitan `zn.inventory.see` para poder entrar, además del nodo de la acción. Los alias raíz opcionales solo necesitan el nodo de su propia acción. Todos los nodos los tienen los operadores por defecto.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/inventory` | Ninguno | Abre el menú de Inventory cuando los diálogos están habilitados. | `zn.inventory.see` | Operadores | No |
| `/invsee` | `<player>` | Abre el inventario de un jugador en línea. | `zn.inventory.see` | Operadores | No |
| `/endersee`, `/ecsee` | `<player>` | Abre el cofre de ender de un jugador en línea. | `zn.inventory.see` | Operadores | No |
| `/clearinventory`, `/ci` | `[player]` | Borra el inventario de un jugador en línea; por defecto, el tuyo propio. | `zn.inventory.clear` | Operadores | No |
| Ninguno | `<player>` | Borra el cofre de ender de un jugador en línea. | `zn.inventory.clear` | Operadores | No |
| Ninguno | `<source> <target>` | Copia el inventario de un jugador en línea a otro. | `zn.inventory.clone` | Operadores | No |
| Ninguno | `<source> <target>` | Copia el cofre de ender de un jugador en línea a otro. | `zn.inventory.clone` | Operadores | No |
| Ninguno | `<player> <material> [amount]` | Da ítems a un jugador en línea. | `zn.inventory.give` | Operadores | No |
| Ninguno | `<player> <material> [amount]` | Añade ítems al cofre de ender de un jugador en línea. | `zn.inventory.give` | Operadores | No |
| `/invrollback` | `[player]` | Restaura la última copia de seguridad al morir del jugador. Sin un jugador, abre el explorador de copias de seguridad cuando los diálogos están habilitados, y restaura la copia del propio remitente cuando los diálogos están desactivados. | `zn.inventory.rollback` | Operadores | No |
| Ninguno | Ninguno | Descarta las copias de seguridad al morir de los jugadores que están desconectados. | `zn.inventory.admin` | Operadores | No |

## ItemEdit

Ruta: `/zn itemedit` (alias `ie`). Alias raíz: `/itemedit` está siempre registrado; `/ie`, `/rename` y `/lore` son opcionales. Todos los comandos de ItemEdit son solo para jugadores y necesitan `zn.itemedit.admin`, que los operadores tienen por defecto; el nodo heredado `zellysnexus.itemedit` lo concede. La mayoría de las acciones editan el ítem de la mano principal.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| `/itemedit`, `/ie` | Ninguno | Abre el editor de ítems cuando los diálogos están habilitados. Ejecutar `/zn itemedit` sin una acción hace lo mismo. | `zn.itemedit.admin` | Operadores | No |
| `/rename` | `<name>` | Cambia el nombre del ítem en la mano. | `zn.itemedit.admin` | Operadores | No |
| `/lore` | `add <text> \| set <line> <text> \| clear` | Añade, reemplaza o borra líneas de lore; los números de línea empiezan en 0 y el límite de líneas es configurable. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `<enchantment> <level>` | Añade un encantamiento al ítem en la mano. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `[true\|false]` | Activa o desactiva, o establece, el indicador de irrompible. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `add <attribute> <amount> [slot] [operation] \| remove <attribute>` | Añade o elimina un modificador de atributo. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `<number>` | Establece los datos de modelo personalizados. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `add <flag> \| remove <flag> \| clear` | Añade, elimina o borra indicadores de ítem. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | Ninguno | Muestra el tipo, los datos de modelo, los indicadores y los encantamientos del ítem en la mano. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `<data>` | Añade un ítem a tu inventario desde su forma codificada en Base64. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `list \| save <key> \| get <key> \| delete <key>` | Guarda el ítem en la mano bajo una clave, da un ítem guardado, lo elimina o lista las claves. | `zn.itemedit.admin` | Operadores | No |
| Ninguno | `create <key> \| give <key> [player] [amount]` | Guarda el ítem en la mano como un ítem del servidor, o da un ítem del servidor a ti mismo o a otro jugador en línea. | `zn.itemedit.admin` | Operadores | No |

## Tab

Ruta: `/zn tab` (alias `t`). No existen alias raíz para este módulo. Todos los comandos de Tab son solo para jugadores.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| Ninguno | Ninguno | Abre el menú de Tab cuando los diálogos están habilitados. Ejecutar `/zn tab` sin una acción hace lo mismo. | Ninguno | Todos | No |
| Ninguno | Ninguno | Muestra el número de equipos y de jugadores en línea. | Ninguno | Todos | No |
| Ninguno | Ninguno | Recarga la tablist para todos los jugadores en línea. | `zn.admin.reload` | Operadores | No |
| Ninguno | Ninguno | Activa o desactiva la tablist personalizada para ti. | Ninguno | Todos | No |

## Integrations

Ruta: `/zn integrations` (alias `int`). No existen alias raíz para este módulo. Todos los comandos de Integrations son solo para jugadores y necesitan `zn.admin.integrations`, que los operadores tienen por defecto.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| Ninguno | Ninguno | Abre el menú de Integrations cuando los diálogos están habilitados. Ejecutar `/zn integrations` sin una acción hace lo mismo. | `zn.admin.integrations` | Operadores | No |
| Ninguno | `<player>` | Muestra el grupo principal y el prefijo de LuckPerms de un jugador en línea. | `zn.admin.integrations` | Operadores | No |
| Ninguno | `<player>` | Informa de si un jugador en línea entró a través de Floodgate. | `zn.admin.integrations` | Operadores | No |

## Debug

Ruta: `/zn debug` (alias `dbg`). El módulo Debug está deshabilitado por defecto; habilítalo con `modules.debug.enabled` en `config.yml` y reinicia el servidor. No existen alias raíz para este módulo. Cada ejecución guarda un informe con fecha en la carpeta de datos del plugin.

| Comando | Sintaxis | Descripción | Permiso | Por defecto | Consola |
|---|---|---|---|---|---|
| Ninguno | `[area]` | Ejecuta las autopruebas de un área, o de todas las áreas cuando no se indica ninguna. | `zn.debug` | Operadores | Sí |
| Ninguno | Ninguno | Abre el menú de diagnósticos para los jugadores cuando los diálogos están habilitados. | `zn.debug` | Operadores | Sí |
