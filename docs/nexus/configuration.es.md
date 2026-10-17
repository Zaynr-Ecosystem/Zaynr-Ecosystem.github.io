# Configuración

La configuración global está en `config.yml`, en la carpeta de datos del plugin; la
configuración por módulo está en `modules/<module>.yml`. `/zn reload` aplica los cambios
de idioma y de diálogos de inmediato; los interruptores de módulos necesitan un reinicio
completo del servidor. Cuando una clave se procesa pero su módulo aún no la usa, la
tabla la marca como aún sin aplicar.

## config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `config-version` | `2` | Versión del esquema de configuración; se actualiza automáticamente |
| `language` | `en` | Traducción activa: `en` o `es` |
| `dialogs` | `true` | Diálogos nativos de Paper; `false` recurre a la interfaz de chat |
| `commands.register-root-aliases` | `true` | Registra los atajos de raíz opcionales (`/spawn`, `/home`, `/login` y más) |
| `commands.disabled-root-aliases` | `[kill, kick, time, weather, msg, gamemode]` | Nombres de comandos raíz que nunca se registran |
| `updater.check-on-boot` | `true` | Ejecuta la comprobación de actualizaciones al arrancar |

### Interruptores de módulos

| Clave | Por defecto |
|---|---|
| `modules.auth.enabled` | `true` |
| `modules.antibot.enabled` | `true` |
| `modules.toolkit.enabled` | `true` |
| `modules.ban.enabled` | `true` |
| `modules.join.enabled` | `true` |
| `modules.chat.enabled` | `true` |
| `modules.inventory.enabled` | `true` |
| `modules.clans.enabled` | `true` |
| `modules.itemedit.enabled` | `true` |
| `modules.tab.enabled` | `true` |
| `modules.integrations.enabled` | `true` |
| `modules.updater.enabled` | `true` |
| `modules.debug.enabled` | `false` |

Los interruptores surten efecto solo tras un reinicio completo del servidor. Los nombres
de módulos desconocidos quedan activados por defecto, y `debug` queda desactivado por
defecto.

## modules/auth.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `session-hours` | `12` | Duración de la memoria de sesión |
| `max-accounts-per-ip` | `3` | Límite de cuentas por dirección |
| `min-password-length` | `4` | Longitud mínima de la contraseña |
| `max-password-length` | `64` | Longitud máxima de la contraseña |
| `max-failed-attempts` | `5` | Intentos fallidos antes del bloqueo |
| `lockout-seconds` | `60` | Duración del bloqueo |
| `otp-expiry-seconds` | `300` | Validez de la contraseña de un solo uso |
| `form-delay-ticks` | `20` | Retardo antes de que se abra el formulario de auth |
| `auto-login-bedrock` | `true` | Aún sin aplicar |
| `auto-login-premium` | `false` | Aún sin aplicar |
| `login-timeout-seconds` | `60` | Aún sin aplicar |
| `security-effects.blindness` | `true` | Aún sin aplicar |
| `security-effects.slowness` | `true` | Aún sin aplicar |
| `security-effects.invulnerability` | `true` | Aún sin aplicar |
| `security-effects.mute-chat` | `true` | Aún sin aplicar |
| `allowed-commands` | `[/login, /register, /l, /reg]` | Aún sin aplicar |
| `mojang.timeout-seconds` | `4` | Tiempo de espera de la verificación premium |
| `mojang.cache-seconds` | `3600` | Caché de la verificación premium |

## modules/antibot.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `window-seconds` | `10` | Ventana del límite de tasa por dirección |
| `max-joins-per-window` | `4` | Conexiones permitidas por ventana |
| `attack-mode.auto-enable` | `true` | Aún sin aplicar |
| `attack-mode.threshold` | `8` | Aún sin aplicar |
| `attack-mode.duration-seconds` | `60` | Aún sin aplicar |
| `checks.require-ping` | `false` | Aún sin aplicar |
| `checks.alert-staff` | `true` | Aún sin aplicar |

## modules/toolkit.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `near-radius` | `100` | Radio de la lista de jugadores "near" |
| `burn-ticks` | `100` | Duración de la quemadura aplicada por la acción burn |
| `tpa-timeout-seconds` | `120` | Tiempo de espera de las solicitudes de teletransporte |
| `teleport.warmup-seconds` | `3` | Aún sin aplicar |
| `teleport.cancel-on-move` | `true` | Aún sin aplicar |
| `teleport.cancel-on-damage` | `true` | Aún sin aplicar |
| `homes.default-max-homes` | `3` | Aún sin aplicar |
| `homes.bed-sets-home` | `false` | Aún sin aplicar |
| `spawn.on-first-join` | `true` | Aún sin aplicar |
| `spawn.on-death` | `false` | Aún sin aplicar |
| `back.save-on-death` | `true` | Aún sin aplicar |
| `back.cooldown-seconds` | `10` | Aún sin aplicar |
| `rtp.rtp-min` | `-1000` | Aún sin aplicar; el rango se cambia en tiempo de ejecución con `/settpr` |
| `rtp.rtp-max` | `1000` | Aún sin aplicar; el rango se cambia en tiempo de ejecución con `/settpr` |
| `rtp.cooldown-seconds` | `60` | Aún sin aplicar |
| `rtp.avoid-water` | `true` | Aún sin aplicar |
| `rtp.avoid-lava` | `true` | Aún sin aplicar |
| `pranks.enabled` | `true` | Aún sin aplicar |
| `pranks.level-1` a `pranks.level-6` | texto de política | Aún sin aplicar |

## modules/ban.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `server-name` | `"the server"` | Nombre que se muestra en las pantallas de ban, expulsión y suspensión |
| `default-suspend-duration` | `"7d"` | Duración aplicada por `/zn suspend` cuando no se indica ninguna (`s`, `m`, `h`, `d`, `w` o `perm`) |
| `screens` | `true` | Muestra las pantallas de ban, expulsión y suspensión al rechazar el inicio de sesión y en las expulsiones |
| `date-format` | `"yyyy-MM-dd HH:mm"` | Formato de fecha usado en las pantallas |
| `help-url` | sitio de documentación | Enlace mostrado en las pantallas |
| `appeal-url` | sitio de documentación | Enlace mostrado en las pantallas |
| `store-url` | sitio de documentación | Enlace mostrado en las pantallas |

## modules/join.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `title-fade` | `10 / 80 / 10` ticks | Entrada, permanencia y salida por defecto de los títulos |
| `chat.enabled` | `true` | Mensajes de chat de primera entrada, entrada y salida |
| `chat.public.<event>` / `chat.private.<event>` | entradas | El público llega a todos los jugadores en línea, el privado solo al jugador |
| `title.enabled` | `false` | Títulos de pantalla |
| `title.public.<event>` / `title.private.<event>` | entradas | Entradas de título y subtítulo |
| `actionbar.enabled` | `false` | Líneas de la barra de acción |
| `actionbar.public.<event>` / `actionbar.private.<event>` | entradas | Entradas de una sola línea |
| `sound.enabled` | `false` | Sonidos de entrada y salida |
| `sound.public.<event>` / `sound.private.<event>` | entradas | Entradas de sonido |

`<event>` es `first-join`, `join` o `quit`. Cada entrada establece una `priority` y
puede establecer una `permission` opcional; las entradas de mensaje usan `messages` (una
lista), las de título usan `title` y `subtitle`, y las de sonido usan `sound`, `volume`
y `pitch`. Marcadores: `<player>`, `<displayname>`, `<world>`, `<online>` y
`<uniquejoins>` (el contador que se guarda en `join-stats.yml`).

## modules/chat.yml

### Canales

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `true` | Aún sin aplicar; usa `modules.chat.enabled` |
| `channels.default-channel` | `local` | Canal por defecto para los jugadores |
| `channels.local-radius` | `100` | Radio del chat local |
| `channels.shout-prefix` | `!` | Prefijo que envía un mensaje a todo el servidor |
| `channels.shout-permission` | `zn.chat.shout` | Aún sin aplicar; el permiso está fijado en `zn.chat.shout` |

### Formato

| Clave | Por defecto | Notas |
|---|---|---|
| `formatting.local-format` | prefijo/nombre/sufijo en gris `[L]`: mensaje | Formato MiniMessage para el chat local |
| `formatting.global-format` | prefijo/nombre/sufijo en dorado `[G]`: mensaje | Formato MiniMessage para el chat global |
| `formatting.player-hover` | 6 líneas (nombre, rango, ping, mundo, en blanco, sugerencia) | Tooltip en los nombres de los jugadores |
| `formatting.player-click.action` | `SUGGEST_COMMAND` | Acción de clic en los nombres de los jugadores |
| `formatting.player-click.value` | `/msg <player>` | Valor de la acción de clic |
| `formatting.groups.admin.priority` | `100` | Prioridad del grupo |
| `formatting.groups.admin.permission` | `zn.chat.group.admin` | Permiso del grupo |
| `formatting.groups.admin.local-format` / `global-format` | formatos de admin | Formatos de chat del grupo |
| `formatting.groups.admin.player-hover` | 6 líneas | Tooltip del grupo |
| `formatting.groups.admin.player-click.action` / `value` | `SUGGEST_COMMAND` / `/msg <player>` | Acción de clic del grupo |
| `formatting.groups.mod.priority` / `permission` | `80` / `zn.chat.group.mod` | Grupo mod |
| `formatting.groups.mod.local-format` / `global-format` | formatos de mod | Formatos del grupo mod |
| `formatting.groups.vip.priority` / `permission` | `50` / `zn.chat.group.vip` | Grupo VIP |
| `formatting.groups.vip.local-format` / `global-format` | formatos de VIP | Formatos del grupo VIP |

### Marcadores

| Clave | Por defecto | Notas |
|---|---|---|
| `placeholders.item.enabled` | `true` | `[item]` y `[i]` |
| `placeholders.item.format` | aqua `[item_name x amount]` | Formato del marcador de objeto |
| `placeholders.inventory.enabled` | `true` | `[inv]` |
| `placeholders.inventory.format` | dorado `[Inventory]` | Formato del marcador de inventario |
| `placeholders.inventory.hover` | Haz clic para inspeccionar el inventario | Texto al pasar el cursor |
| `placeholders.inventory.command` | `/zn inv see <player>` | Comando de clic |
| `placeholders.enderchest.enabled` | `true` | `[ender]` |
| `placeholders.enderchest.format` | lila claro `[EnderChest]` | Formato del marcador del cofre de ender |
| `placeholders.enderchest.hover` | Haz clic para inspeccionar el cofre de ender | Texto al pasar el cursor |
| `placeholders.enderchest.command` | `/zn inv endersee <player>` | Comando de clic |

### Menciones

| Clave | Por defecto | Notas |
|---|---|---|
| `mentions.enabled` | `true` | Menciones a jugadores |
| `mentions.format` | amarillo en negrita `@target` | Formato de mención |
| `mentions.sound.enabled` | `true` | Sonido al mencionar |
| `mentions.sound.type` | `block.note_block.bell` | Tipo de sonido |
| `mentions.sound.volume` | `1.0` | Volumen del sonido |
| `mentions.sound.pitch` | `1.5` | Tono del sonido |
| `mentions.actionbar.enabled` | `true` | Notificación en la barra de acción |
| `mentions.actionbar.message` | mensaje de mención | Texto de la notificación |

### Moderación

| Clave | Por defecto | Notas |
|---|---|---|
| `moderation.cooldown-seconds` | `1.5` | Enfriamiento del chat |
| `moderation.cooldown-bypass-permission` | `zn.chat.bypass.cooldown` | Permiso de omisión |
| `moderation.anti-duplicate.enabled` | `true` | Bloquea los mensajes repetidos |
| `moderation.anti-caps.enabled` | `true` | Bloquea el exceso de mayúsculas |
| `moderation.anti-caps.min-message-length` | `6` | Longitud mínima para la comprobación de mayúsculas |
| `moderation.anti-caps.max-caps-percent` | `60` | Porcentaje máximo de mayúsculas |
| `moderation.swear-filter.enabled` | `false` | Filtro de palabrotas |
| `moderation.swear-filter.block-message` | `false` | Bloquea en lugar de censurar |
| `moderation.swear-filter.censor-replacement` | `****` | Reemplazo al censurar |
| `moderation.swear-filter.blocked-words` | `[]` | Lista de palabras bloqueadas |

### Anuncios

| Clave | Por defecto | Notas |
|---|---|---|
| `announcements.enabled` | `false` | Anuncios programados |
| `announcements.interval-seconds` | `180` | Intervalo entre anuncios |
| `announcements.prefix` | prefijo de Nexus | Prefijo del anuncio |
| `announcements.messages` | 3 líneas | Mensajes rotativos |

## modules/clans.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `invite-seconds` | `120` | Validez de la invitación |
| `naming.min-name-length` | `3` | Aún sin aplicar |
| `naming.max-name-length` | `32` | Longitud máxima del nombre del clan |
| `naming.max-tag-length` | `6` | Aún sin aplicar |
| `membership.max-members` | `10` | Aún sin aplicar |
| `membership.creation-cost` | `0` | Aún sin aplicar |
| `gameplay.friendly-fire-default` | `false` | Estado por defecto del fuego amigo |
| `gameplay.home-warmup-seconds` | `3` | Aún sin aplicar |
| `gameplay.max-allies` | `3` | Aún sin aplicar |
| `gameplay.max-rivals` | `5` | Aún sin aplicar |

## modules/inventory.yml

El módulo inventory no tiene archivo de configuración en la carpeta de datos; funciona
con estos valores por defecto integrados, y ninguno de ellos se aplica aún.

| Clave | Por defecto | Notas |
|---|---|---|
| `rollback.save-on-death` | `true` | Aún sin aplicar |
| `rollback.save-on-disconnect` | `true` | Aún sin aplicar |
| `rollback.max-snapshots-per-player` | `20` | Aún sin aplicar |
| `rollback.retention-days` | `7` | Aún sin aplicar |
| `inspector.allow-modification` | `true` | Aún sin aplicar |

## modules/itemedit.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `lore-lines` | `8` | Líneas máximas de lore |
| `limits.max-name-length` | `64` | Aún sin aplicar |
| `limits.max-lore-line-length` | `128` | Aún sin aplicar |
| `formatting.allow-color-codes` | `true` | Aún sin aplicar |
| `formatting.allow-minimessage` | `true` | Aún sin aplicar |
| `economy.repair-cost` | `0` | Aún sin aplicar |

## modules/tab.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `tablist.enabled` | `true` | Aún sin aplicar; usa `modules.tab.enabled` |
| `tablist.update-interval-ticks` | `20` | Aún sin aplicar |
| `tablist.colorize-ping` | `true` | Aún sin aplicar |
| `tablist.header` | 2 líneas | Aún sin aplicar; el encabezado proviene de claves de traducción |
| `tablist.footer` | 2 líneas | Aún sin aplicar; el pie proviene de claves de traducción |
| `bossbar.duration-ticks` | `200` | Duración de la boss bar al entrar |
| `bossbar.color` | `BLUE` | Color de la boss bar al entrar |
| `bossbar.overlay` | `PROGRESS` | Superposición de la boss bar al entrar |

## Estructura de datos

Todo se encuentra bajo la carpeta de datos del plugin `plugins/ZellysNexus/`:

- `config.yml`: configuración global, copiada del jar en la primera ejecución.
- `modules/`: configuración por módulo; las plantillas de `auth`, `antibot`, `toolkit`,
  `ban`, `join`, `chat`, `inventory`, `clans`, `itemedit` y `tab` se copian en el primer
  arranque cuando faltan.
- Archivos de datos de los módulos: `auth.yml`, `antibot.yml`, `clans.yml`,
  `ban-audit.yml`, `join-stats.yml`, `spawn.yml`, `homes.yml`, `warps.yml`, `jails.yml`,
  `kits.yml`, `mail.yml`, `jailed.yml`, `lastseen.yml`, `nicknames.yml` y `items.yml`.
- `debug/`: informes de diagnóstico con fecha escritos por el módulo debug.
- No se usa ninguna base de datos: cada almacén es un archivo YAML en UTF-8.

## Archivos de idioma

Las traducciones vienen dentro del jar y no son archivos de la carpeta de datos.
`language` selecciona `en` o `es`; una clave que falta en el idioma activo recurre al
inglés, y un idioma que no carga recurre por completo al inglés. `/zn reload` aplica los
cambios de idioma de inmediato.
