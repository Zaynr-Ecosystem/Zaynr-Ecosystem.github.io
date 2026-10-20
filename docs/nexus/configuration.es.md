# Configuración

La configuración global está en `config.yml`. Cada módulo tiene su propia carpeta,
`modules/<module>/config.yml`, y empieza con `enabled: false`. `/zn reload` aplica los
cambios de idioma y de renderizador de inmediato; los interruptores de módulos necesitan
un reinicio completo del servidor. Cuando una clave se procesa pero su módulo aún no la
usa, la tabla la marca como aún sin aplicar. Los hubs de jugador son `/zn user` y
`/zn admin`; cada pantalla usa el renderizador que eligen `use_dialogs` y
`bedrock_forms`.

## config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `config-version` | `3` | Versión del esquema; se actualiza automáticamente |
| `language` | `en` | Traducción activa: `en` o `es` |
| `use_dialogs` | `false` | Los jugadores de Java ven diálogos de Paper en lugar de inventarios. Requiere una build de Paper con la API de diálogos |
| `bedrock_forms` | `true` | Los jugadores de Bedrock ven formularios de Floodgate cuando Floodgate está instalado |
| `setup_notice` | `true` | Los administradores ven el aviso de primera configuración hasta que se aplica la configuración recomendada o esta clave es `false` |
| `apply_recommended_on_start` | `false` | Aplica `recommended all` en el siguiente arranque y luego vuelve a `false` |
| `admin_tiers.enabled` | `false` | Separa las capacidades de administración por nivel. En `false`, `zn.admin` concede todas |
| `commands.register-root-aliases` | `true` | Registra los atajos de raíz opcionales (`/spawn`, `/home`, `/login` y más) |
| `commands.disabled-root-aliases` | `[kill, kick, time, weather, msg, gamemode]` | Comandos de raíz que nunca se registran |
| `updater.check-on-boot` | `true` | Comprueba actualizaciones al arrancar |
| `recommended_config_applied` | ausente | Marca que se escribe cuando `recommended config` termina bien |
| `recommended_modules_applied` | ausente | Marca que se escribe cuando `recommended modules` termina bien |
| `recommended_<module>_applied` | ausente | Marca que se escribe cuando `recommended <module>` termina bien |

Los inventarios son el renderizador por defecto. `use_dialogs: true` cambia a los
jugadores de Java a diálogos; los de Bedrock reciben formularios cuando Floodgate está
presente y `bedrock_forms` es `true`. Las claves antiguas `dialogs` y `gui-mode` se
migran a `use_dialogs` y se eliminan en el primer arranque de esta versión.

### Interruptores de módulos

| Clave | Por defecto |
|---|---|
| `enabled` en `modules/auth/config.yml` | `false` |
| `enabled` en `modules/antibot/config.yml` | `false` |
| `enabled` en `modules/toolkit/config.yml` | `false` |
| `enabled` en `modules/ban/config.yml` | `false` |
| `enabled` en `modules/join/config.yml` | `false` |
| `enabled` en `modules/chat/config.yml` | `false` |
| `enabled` en `modules/inventory/config.yml` | `false` |
| `enabled` en `modules/clans/config.yml` | `false` |
| `enabled` en `modules/itemedit/config.yml` | `false` |
| `enabled` en `modules/tab/config.yml` | `false` |
| `enabled` en `modules/integrations/config.yml` | `false` |
| `enabled` en `modules/updater/config.yml` | `false` |
| `enabled` en `modules/debug/config.yml` | `false` |

Los interruptores solo se aplican tras un reinicio completo. Un módulo desactivado
sigue registrando sus comandos; al usarlos, el plugin explica que está desactivado y
muestra las dos salidas (editar su carpeta o ejecutar `/zn recommended <module>`).

## modules/auth/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `session-hours` | `12` | Duración de la sesión recordada |
| `max-accounts-per-ip` | `3` | Cuentas permitidas por dirección |
| `min-password-length` | `4` | Longitud mínima de contraseña |
| `max-password-length` | `64` | Longitud máxima de contraseña |
| `max-failed-attempts` | `5` | Intentos fallidos antes del bloqueo |
| `lockout-seconds` | `60` | Duración del bloqueo |
| `otp-expiry-seconds` | `300` | Validez de las contraseñas de un solo uso |
| `form-delay-ticks` | `20` | Retardo antes de abrir el formulario de acceso |
| `auto-login-bedrock` | `true` | Aún sin aplicar |
| `auto-login-premium` | `false` | Aún sin aplicar |
| `login-timeout-seconds` | `60` | Aún sin aplicar |
| `security-effects.blindness` | `true` | Aún sin aplicar |
| `security-effects.slowness` | `true` | Aún sin aplicar |
| `security-effects.invulnerability` | `true` | Aún sin aplicar |
| `security-effects.mute-chat` | `true` | Aún sin aplicar |
| `allowed-commands` | `[/login, /register, /l, /reg]` | Aún sin aplicar |
| `mojang.timeout-seconds` | `4` | Tiempo máximo de verificación premium |
| `mojang.cache-seconds` | `3600` | Caché de verificación premium |

## modules/antibot/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `window-seconds` | `10` | Ventana del límite por dirección |
| `max-joins-per-window` | `4` | Conexiones permitidas por ventana |
| `attack-mode.auto-enable` | `true` | Aún sin aplicar |
| `attack-mode.threshold` | `8` | Aún sin aplicar |
| `attack-mode.duration-seconds` | `60` | Aún sin aplicar |
| `checks.require-ping` | `false` | Aún sin aplicar |
| `checks.alert-staff` | `true` | Aún sin aplicar |

## modules/toolkit/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `near-radius` | `100` | Radio de la lista de jugadores cercanos |
| `burn-ticks` | `100` | Duración del efecto de quemadura |
| `tpa-timeout-seconds` | `120` | Tiempo máximo de una solicitud de teletransporte |
| `teleport.warmup-seconds` | `3` | Aún sin aplicar |
| `teleport.cancel-on-move` | `true` | Aún sin aplicar |
| `teleport.cancel-on-damage` | `true` | Aún sin aplicar |
| `homes.default-max-homes` | `3` | Aún sin aplicar |
| `spawn.on-first-join` | `true` | Aún sin aplicar |
| `spawn.on-death` | `false` | Aún sin aplicar |
| `back.save-on-death` | `true` | Aún sin aplicar |
| `back.cooldown-seconds` | `10` | Aún sin aplicar |
| `rtp.rtp-min` | `-1000` | Aún sin aplicar; el rango se cambia con `/settpr` |
| `rtp.rtp-max` | `1000` | Aún sin aplicar; el rango se cambia con `/settpr` |
| `rtp.cooldown-seconds` | `60` | Aún sin aplicar |

## modules/ban/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `server-name` | `"the server"` | Nombre que aparece en las pantallas de sanción |
| `default-suspend-duration` | `"7d"` | Duración de `/zn suspend` cuando no se indica (`s`, `m`, `h`, `d`, `w` o `perm`) |
| `screens` | `true` | Muestra las pantallas de expulsión y sanción |
| `date-format` | `"yyyy-MM-dd HH:mm"` | Formato de fecha de las pantallas |
| `help-url` | sitio de documentación | Enlace de ayuda |
| `appeal-url` | sitio de documentación | Enlace de apelación |
| `store-url` | sitio de documentación | Enlace de tienda |

## modules/join/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `title-fade.fade-in` | `10` | Entrada del título, en ticks |
| `title-fade.stay` | `80` | Permanencia del título, en ticks |
| `title-fade.fade-out` | `10` | Salida del título, en ticks |
| `chat.enabled` | `true` | Mensajes de primera entrada, entrada y salida |
| `chat.public.first-join` | 1 entrada | Lista pública para `first-join` |
| `chat.public.join` | 1 entrada | Lista pública para `join` |
| `chat.public.quit` | 1 entrada | Lista pública para `quit` |
| `chat.private.first-join` | `[]` | Lista privada para `first-join` |
| `chat.private.join` | `[]` | Lista privada para `join` |
| `chat.private.quit` | `[]` | Lista privada para `quit` |
| `title.enabled` | `false` | Títulos en pantalla |
| `title.public.first-join` | `[]` | Título público para `first-join` |
| `title.public.join` | `[]` | Título público para `join` |
| `title.public.quit` | `[]` | Título público para `quit` |
| `title.private.first-join` | `[]` | Título privado para `first-join` |
| `title.private.join` | `[]` | Título privado para `join` |
| `title.private.quit` | `[]` | Título privado para `quit` |
| `actionbar.enabled` | `false` | Líneas de action bar |
| `actionbar.public.first-join` | `[]` | Action bar pública para `first-join` |
| `actionbar.public.join` | `[]` | Action bar pública para `join` |
| `actionbar.public.quit` | `[]` | Action bar pública para `quit` |
| `actionbar.private.first-join` | `[]` | Action bar privada para `first-join` |
| `actionbar.private.join` | `[]` | Action bar privada para `join` |
| `actionbar.private.quit` | `[]` | Action bar privada para `quit` |
| `sound.enabled` | `false` | Sonidos de entrada y salida |
| `sound.public.first-join` | `[]` | Sonido público para `first-join` |
| `sound.public.join` | `[]` | Sonido público para `join` |
| `sound.public.quit` | `[]` | Sonido público para `quit` |
| `sound.private.first-join` | `[]` | Sonido privado para `first-join` |
| `sound.private.join` | `[]` | Sonido privado para `join` |
| `sound.private.quit` | `[]` | Sonido privado para `quit` |

`<event>` es `first-join`, `join` o `quit`. Cada entrada define `priority` y puede
definir `permission`; los mensajes usan `messages` (lista), los títulos usan `title` y
`subtitle`, y los sonidos usan `sound`, `volume` y `pitch`. Marcadores: `<player>`,
`<displayname>`, `<world>`, `<online>` y `<uniquejoins>` (el contador de
`join-stats.yml`).

## modules/chat/config.yml

### Canales

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `channels.default-channel` | `local` | Canal por defecto |
| `channels.local-radius` | `100` | Radio del chat local |
| `channels.shout-prefix` | `!` | Prefijo que envía al servidor entero |
| `channels.shout-permission` | `zn.chat.shout` | Aún sin aplicar; el permiso es fijo |

### Formato

| Clave | Por defecto | Notas |
|---|---|---|
| `formatting.local-format` | gris `[L]` prefijo/nombre/sufijo: mensaje | Formato MiniMessage local |
| `formatting.global-format` | dorado `[G]` prefijo/nombre/sufijo: mensaje | Formato MiniMessage global |
| `formatting.player-hover` | 6 líneas | Información al pasar el ratón |
| `formatting.player-click.action` | `SUGGEST_COMMAND` | Acción al hacer clic |
| `formatting.player-click.value` | `/msg <player>` | Valor de la acción |
| `formatting.groups.admin.priority` | `100` | Prioridad del grupo |
| `formatting.groups.admin.permission` | `zn.chat.group.admin` | Permiso del grupo |
| `formatting.groups.admin.local-format` | formato local de admin | Formato local |
| `formatting.groups.admin.global-format` | formato global de admin | Formato global |
| `formatting.groups.admin.player-hover` | 6 líneas | Información del grupo |
| `formatting.groups.admin.player-click.action` | `SUGGEST_COMMAND` | Acción del grupo |
| `formatting.groups.admin.player-click.value` | `/msg <player> ` | Valor de la acción |
| `formatting.groups.mod.priority` | `80` | Prioridad del grupo |
| `formatting.groups.mod.permission` | `zn.chat.group.mod` | Permiso del grupo |
| `formatting.groups.mod.local-format` | formato local de mod | Formato local |
| `formatting.groups.mod.global-format` | formato global de mod | Formato global |
| `formatting.groups.vip.priority` | `50` | Prioridad del grupo |
| `formatting.groups.vip.permission` | `zn.chat.group.vip` | Permiso del grupo |
| `formatting.groups.vip.local-format` | formato local de vip | Formato local |
| `formatting.groups.vip.global-format` | formato global de vip | Formato global |

### Marcadores

| Clave | Por defecto | Notas |
|---|---|---|
| `placeholders.item.enabled` | `true` | `[item]` y `[i]` |
| `placeholders.inventory.enabled` | `true` | `[inv]` |
| `placeholders.inventory.format` | dorado `[Inventory]` | Formato del marcador |
| `placeholders.inventory.hover` | Texto al pasar el ratón | Texto de ayuda |
| `placeholders.inventory.command` | `/zn inv see <player>` | Comando al hacer clic |
| `placeholders.enderchest.enabled` | `true` | `[ender]` |
| `placeholders.enderchest.format` | lila `[EnderChest]` | Formato del marcador |
| `placeholders.enderchest.hover` | Texto al pasar el ratón | Texto de ayuda |
| `placeholders.enderchest.command` | `/zn inv endersee <player>` | Comando al hacer clic |

### Menciones

| Clave | Por defecto | Notas |
|---|---|---|
| `mentions.enabled` | `true` | Menciones de jugadores |
| `mentions.format` | amarillo negrita `@target` | Formato de mención |
| `mentions.sound.enabled` | `true` | Sonido al mencionar |
| `mentions.sound.type` | `block.note_block.bell` | Sonido |
| `mentions.sound.volume` | `1.0` | Volumen |
| `mentions.sound.pitch` | `1.5` | Tono |
| `mentions.actionbar.enabled` | `true` | Aviso en action bar |
| `mentions.actionbar.message` | mensaje de mención | Texto del aviso |

### Moderación

| Clave | Por defecto | Notas |
|---|---|---|
| `moderation.cooldown-seconds` | `1.5` | Enfriamiento del chat |
| `moderation.cooldown-bypass-permission` | `zn.chat.bypass.cooldown` | Permiso para saltarlo |
| `moderation.anti-duplicate.enabled` | `true` | Bloquea mensajes repetidos |
| `moderation.anti-caps.enabled` | `true` | Bloquea mayúsculas excesivas |
| `moderation.anti-caps.min-message-length` | `6` | Longitud mínima para revisar mayúsculas |
| `moderation.anti-caps.max-caps-percent` | `60` | Porcentaje máximo de mayúsculas |
| `moderation.swear-filter.enabled` | `false` | Filtro de palabras |
| `moderation.swear-filter.block-message` | `false` | Bloquear en lugar de censurar |
| `moderation.swear-filter.censor-replacement` | `****` | Texto de censura |
| `moderation.swear-filter.blocked-words` | `[]` | Lista de palabras bloqueadas |

### Anuncios

| Clave | Por defecto | Notas |
|---|---|---|
| `announcements.enabled` | `false` | Anuncios programados |
| `announcements.interval-seconds` | `180` | Intervalo entre anuncios |
| `announcements.prefix` | prefijo Nexus | Prefijo del anuncio |
| `announcements.messages` | 3 líneas | Mensajes rotativos |

## modules/clans/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `invite-seconds` | `120` | Validez de la invitación |
| `naming.min-name-length` | `3` | Aún sin aplicar |
| `naming.max-name-length` | `32` | Longitud máxima del nombre |
| `naming.max-tag-length` | `6` | Aún sin aplicar |
| `membership.max-members` | `10` | Aún sin aplicar |
| `membership.creation-cost` | `0` | Aún sin aplicar |
| `gameplay.friendly-fire-default` | `false` | Fuego amigo por defecto |
| `gameplay.home-warmup-seconds` | `3` | Aún sin aplicar |
| `gameplay.max-allies` | `3` | Aún sin aplicar |
| `gameplay.max-rivals` | `5` | Aún sin aplicar |

## modules/inventory/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `rollback.save-on-death` | `true` | Aún sin aplicar |
| `rollback.save-on-disconnect` | `true` | Aún sin aplicar |
| `rollback.max-snapshots-per-player` | `20` | Aún sin aplicar |
| `rollback.retention-days` | `7` | Aún sin aplicar |
| `inspector.allow-modification` | `true` | Aún sin aplicar |

## modules/itemedit/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `lore-lines` | `8` | Líneas máximas de lore |
| `limits.max-name-length` | `64` | Aún sin aplicar |
| `limits.max-lore-line-length` | `128` | Aún sin aplicar |
| `formatting.allow-color-codes` | `true` | Aún sin aplicar |
| `formatting.allow-minimessage` | `true` | Aún sin aplicar |
| `economy.repair-cost` | `0` | Aún sin aplicar |

## modules/tab/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `tablist.enabled` | `true` | Aún sin aplicar |
| `tablist.update-interval-ticks` | `20` | Aún sin aplicar |
| `tablist.colorize-ping` | `true` | Aún sin aplicar |
| `tablist.header` | 2 líneas | Aún sin aplicar |
| `tablist.footer` | 2 líneas | Aún sin aplicar |
| `bossbar.duration-ticks` | `200` | Duración de la barra de entrada |
| `bossbar.color` | `BLUE` | Color de la barra |
| `bossbar.overlay` | `PROGRESS` | Estilo de la barra |

## modules/debug/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |

## modules/integrations/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |

## modules/updater/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio; la comprobación la controla `updater.check-on-boot` |

## Distribución de datos

Todo vive en `plugins/ZellysNexus/`:

- `config.yml`: configuración global, copiada del jar en el primer arranque.
- `modules/<module>/config.yml`: una carpeta por módulo, copiada si falta. Las carpetas
  son `auth`, `antibot`, `toolkit`, `ban`, `join`, `chat`, `inventory`, `clans`,
  `itemedit`, `tab`, `integrations`, `updater` y `debug`.
- Los datos de cada módulo viven en su carpeta: `modules/join/join-stats.yml`,
  `modules/ban/ban-audit.yml`, `modules/auth/auth.yml`, `modules/clans/clans.yml`,
  `modules/itemedit/items.yml`, `modules/antibot/antibot.yml` y, en
  `modules/toolkit/`: `spawn.yml`, `homes.yml`, `warps.yml`, `jails.yml`, `kits.yml`,
  `mail.yml`, `jailed.yml`, `lastseen.yml` y `nicknames.yml`.
- El primer arranque de esta versión copia el archivo antiguo de la raíz a su carpeta,
  verifica el tamaño y renombra el original a `<name>.migrated`. Nunca sobrescribe un
  archivo nuevo; si existen los dos, avisa y usa el nuevo.
- `debug/`: informes de diagnóstico con fecha.
- No se usa base de datos: todo es YAML UTF-8.

## Archivos de idioma

Las traducciones viajan dentro del jar; no son archivos de la carpeta de datos.
`language` elige `en` o `es`; una clave ausente cae a inglés y un idioma que no carga
cae a inglés por completo. `/zn reload` aplica el idioma de inmediato.
