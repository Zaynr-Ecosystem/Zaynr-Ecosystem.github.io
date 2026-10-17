# Configuración

BlockProt Reloaded guarda su configuración en la carpeta de datos del plugin:

| Archivo | Contenido |
|---|---|
| `config.yml` | Ajustes principales: idioma, comportamiento de bloqueo, entidades, expiración, notificaciones, mantenimiento |
| `integrations.yml` | Ajustes de integración centralizados para plugins de terceros, con un interruptor maestro por plugin |
| `blocks.yml` | Listas de bloques bloqueables (vacías por defecto; se configuran desde la GUI de `/bp lockables` o se editan directamente) |
| `worlds.yml` | Listas de bloques por mundo, activas cuando `per_worlds_config: true` |
| `mysql/mysql.yml` | Ajustes opcionales del índice MySQL/MariaDB |
| `admins.yml` | Asignaciones de nivel del personal (se crea cuando se asignan niveles) |
| `lang/` | `lang.yml` más 25 traducciones incluidas |

Todas las listas de bloqueables están vacías por defecto; `/bp recommended blocks`
aplica una selección inicial ya preparada. La mayoría de los cambios se aplican con
`/bp reload` (que antes crea una copia de seguridad) o automáticamente cuando los
archivos se editan desde fuera.

## config.yml

### Idioma

| Clave | Por defecto | Notas |
|---|---|---|
| `language_file` | `translations_en.yml` | Archivo de idioma activo |
| `fallback_string` | `Unknown translation` | Texto mostrado cuando falta una clave de traducción |
| `replace_translations` | `true` | Añadir automáticamente las claves que falten a los archivos de traducción al actualizar |

### Mundos

| Clave | Por defecto | Notas |
|---|---|---|
| `excluded_worlds` | `[]` | Mundos donde el plugin está totalmente desactivado |
| `per_worlds_config` | `false` | Leer desde `worlds.yml` una configuración de bloques separada por mundo |

### Jugadores y amigos

| Clave | Por defecto | Notas |
|---|---|---|
| `bedrock_username_prefixes` | `[".", "*", "_"]` | Prefijos usados para detectar jugadores de Bedrock a través de Geyser/Floodgate |
| `lock_on_place_by_default` | `true` | Bloquear los bloques automáticamente cuando un jugador los coloca |
| `public_is_friend_by_default` | `false` | Tratar los bloques públicos como amigos por defecto |
| `player_max_locked_block_count` | `-1` | Límite de bloques bloqueados por jugador; `-1` es ilimitado |
| `lock_hint_cooldown_in_seconds` | `10` | Tiempo de espera entre mensajes de aviso de bloqueo |
| `friend_search_similarity` | `0.5` | Umbral de similitud al buscar amigos por nombre (0.0 a 1.0) |
| `disable_friend_functionality` | `false` | Desactivar globalmente el sistema de amigos |

### Bloques y comportamiento de bloqueo

| Clave | Por defecto | Notas |
|---|---|---|
| `modern_family_blocks` | `false` | Formato de salida de `blocks.yml` cuando se modifica desde `/bp lockables` (`false` nombres planos, `true` expresiones de familia). Nunca lee ni modifica el archivo al arrancar; se desactiva automáticamente cuando todas las listas de bloqueables están vacías |
| `redstone_disallowed_by_default` | `false` | Prohibir por defecto la interacción de redstone con los bloques bloqueados |
| `simplified_hopper_logic` | `false` | Comprobaciones de tolvas más simples, sacrificando precisión por rendimiento |
| `protect_locked_blocks_from_explosions` | `true` | Los bloques bloqueados sobreviven a las explosiones |
| `block_protected_block_piston_movement` | `true` | Los pistones no pueden mover bloques bloqueados |
| `clear_protection_on_shulker_break` | `false` | Borrar la protección de una caja de shulker cuando se rompe |
| `allow_break_protected_blocks` | `false` | Permitir romper bloques protegidos que no te pertenecen (los datos de protección se conservan) |
| `respect_spawn_protection` | `true` | Respetar la protección de spawn vanilla |
| `block_lock_effects` | `true` | Efectos de partículas al interactuar con bloques bloqueados |
| `block_lock_sounds` | `true` | Sonidos al interactuar con bloques bloqueados |
| `use_menus` | `false` | Consolidar los menús en `/bp user` y `/bp admin`; cuando es false, cada función conserva su propio subcomando |
| `use_dialogs` | `false` | Diálogos nativos de Paper en lugar de inventarios, yunques y chat. Requiere Paper 1.21.7 o posterior; se desactiva automáticamente con una advertencia cuando la API de diálogos no está disponible |
| `timed_access_max_duration_days` | `90` | Duración máxima de una concesión de acceso temporizado |

### Protección de entidades

| Clave | Por defecto | Notas |
|---|---|---|
| `entity_protection.enabled` | `false` | Proteger animales, aldeanos y otras entidades |
| `entity_protection.auto_protect_on_tame` | `true` | Proteger las entidades automáticamente al domesticarlas |
| `entity_protection.menu_item` | `STICK` | Objeto usado para abrir el menú de protección de entidades |
| `entity_protection.villager_locate_seconds` | `6` | Segundos que dura el indicador de localización del aldeano |
| `villager_workstation_protection.enabled` | `true` | Proteger las mesas de trabajo que pertenecen a aldeanos protegidos |
| `villager_workstation_protection.radius` | `2` | Radio horizontal alrededor de la mesa de trabajo |
| `villager_workstation_protection.vertical_radius` | `1` | Radio vertical alrededor de la mesa de trabajo |

### Expiración

La expiración manual por bloque (establecer una hora de expiración en un bloque
concreto) está prevista para una versión futura y todavía no está disponible; la
expiración por defecto a nivel de mundo se configura más abajo.

| Clave | Por defecto | Notas |
|---|---|---|
| `world_expiry.enabled` | `false` | Expiración global de las protecciones de bloques inactivas |
| `world_expiry.check_interval_minutes` | `10` | Intervalo entre comprobaciones de expiración |
| `world_expiry.worlds` | `{}` | Tiempos de expiración específicos por mundo |

### Detección de raids

| Clave | Por defecto | Notas |
|---|---|---|
| `raid_detection.enabled` | `false` | Proteger los bloques bloqueados y las entidades de las raids |

### Notificaciones

| Clave | Por defecto | Notas |
|---|---|---|
| `notify_op_of_updates` | `false` | Notificar a los operadores cuando haya una actualización disponible |
| `owner_notifications.enabled` | `true` | Permitir que los propietarios reciban notificaciones sobre sus bloques |
| `owner_notifications.notify_on_open` | `true` | Notificar cuando alguien abre el bloque del propietario |
| `owner_notifications.notify_on_take` | `true` | Notificar cuando alguien toma objetos del bloque del propietario |
| `owner_notifications.notify_on_place` | `true` | Notificar cuando alguien coloca objetos en el bloque del propietario |

### Mantenimiento

| Clave | Por defecto | Notas |
|---|---|---|
| `inactivity_cleanup_days` | `-1` | Días de inactividad antes de eliminar las protecciones de un jugador; `-1` lo desactiva |
| `auto_reload_configs` | `true` | Recargar la configuración cuando los archivos cambian desde fuera |
| `auto_reload_delay_seconds` | `2` | Periodo de espera (0 a 5) que agrupa guardados rápidos en una sola recarga |
| `enable_session_log` | `true` | Registro de sesiones |
| `enable_backups` | `true` | Copias de seguridad automáticas de la base de datos |
| `admin_tiers.enabled` | `false` | Cuando es false, `blockprot.user.admin` otorga todas las capacidades de administración; cuando es true, los permisos se dividen en los niveles t1, t2, t3, owner y custom |

### Barra de acción

| Clave | Por defecto | Notas |
|---|---|---|
| `action_bar.duration_seconds` | `6` | Duración de las alertas temporales en la barra de acción |

## integrations.yml

Todas las integraciones externas se configuran desde este único archivo; los antiguos
archivos por integración ya no se leen y se pueden eliminar sin problema. Cada
integración tiene un interruptor maestro `enabled`.

| Clave | Por defecto | Notas |
|---|---|---|
| `worldguard.enabled` | `true` | Integración con WorldGuard |
| `worldguard.enable_flag_functionality` | `true` | Activa la flag de región `allow-blockprot`; cuando está desactivada, WorldGuard se detecta pero nunca se consulta |
| `lands.enabled` | `true` | Integración con Lands |
| `lands.allow_protecting_containers_in_wilderness` | `true` | Permitir proteger contenedores en tierras salvajes sin reclamar |
| `lands.require_protect_for_friends_flag` | `false` | Registrar la flag de rol "Require 'Protect containers' for friends" |
| `towny.enabled` | `true` | Integración con Towny |
| `towny.cleanup_plots_after_unclaim` | `true` | Limpiar las protecciones cuando una parcela se vacía, se libera o queda en ruinas |
| `towny.restrict_access_to_residents` | `false` | Restringir el acceso a los bloques únicamente a los residentes del pueblo |
| `towny.allow_mayor_to_see_block_info` | `false` | Permitir a los alcaldes usar la vista de información del bloque |
| `towny.bypass_protection_in_ruined_towns` | `true` | Permitir el bypass de las protecciones en pueblos en ruinas |
| `claimchunk.enabled` | `true` | Integración con ClaimChunk |
| `claimchunk.restrict_access_to_chunk_owner` | `false` | Restringir completamente el acceso al propietario del chunk (de lo contrario, solo se restringe el bloqueo) |
| `worldedit.enabled` | `true` | Integración con WorldEdit |
| `worldedit.paste_autolock.enabled` | `false` | Bloquear automáticamente los bloques protegibles después de un `//paste` |
| `worldedit.paste_autolock.radius` | `24` | Radio alrededor del origen del pegado que se escanea |
| `worldedit.paste_autolock.max_blocks_per_paste` | `5000` | Límite de seguridad por pegado |
| `worldedit.paste_autolock.delay_ticks` | `20` | Retardo antes de que comience el escaneo |
| `placeholderapi.enabled` | `true` | Integración con PlaceholderAPI |
| `viaversion.enabled` | `true` | Detección de la versión del cliente de ViaVersion |
| `residence.enabled` | `true` | Integración con Residence |
| `residence.restrict_access_to_residence_owner` | `false` | Restringir completamente el acceso al propietario de la residencia |
| `griefprevention.enabled` | `true` | Integración con GriefPrevention |
| `griefprevention.restrict_access_to_claim_owner` | `false` | Restringir completamente el acceso al propietario del claim |
| `geyser.enabled` | `true` | Integración con Geyser: detección de jugadores de Bedrock y formularios de Bedrock |
| `floodgate.enabled` | `true` | Integración con Floodgate |
| `floodgate.auto_detect_prefix` | `true` | Detectar automáticamente el prefijo de nombre de usuario de Bedrock desde Floodgate |

## blocks.yml

Las listas de bloqueables están vacías por defecto. Las entradas aceptan nombres de
material planos (`CHEST`) o expresiones de familia como `[*-CHEST]` (todas las variantes
de cofre), `[*-FURNACE *-CHEST]` (familias combinadas) o `[*]`. El archivo nunca se
modifica al arrancar ni al recargar; solo los interruptores de la GUI escriben en él.

| Clave | Por defecto | Notas |
|---|---|---|
| `lockable_tile_entities` | `[]` | Contenedores y mesas de trabajo |
| `lockable_shulker_boxes` | `[]` | Variantes de cajas de shulker |
| `lockable_blocks` | `[]` | Bloques bloqueables generales |
| `lockable_doors` | `[]` | Puertas y trampillas |
| `lockable_entities` | `[]` | Entidades bloqueables |
| `protectable_entities` | `[VILLAGER]` | Entidades aptas para la protección de entidades |
| `auto_drop_to_inventory.enabled` | `true` | Devolver los bloques al inventario al quitar la protección |
| `auto_drop_to_inventory.blocks` | `[]` | Bloques afectados por el comportamiento de devolución automática |

## worlds.yml

Activo cuando `config.yml` tiene `per_worlds_config: true`. Cada mundo listado toma el
control absoluto e independiente de sus listas: `blocks.yml` nunca se consulta para ese
mundo una vez que tiene una entrada, ni siquiera para una categoría que la entrada deja
vacía. Las listas de aquí usan siempre la sintaxis compacta de expresiones de familia,
independientemente de `modern_family_blocks`. Un mundo con `enabled: false` no puede
tener ningún bloque bloqueado. Los mundos se rellenan automáticamente con listas vacías
en el primer escaneo, y el editor por mundo es accesible desde `/bp lockables` (botón de
mapa) cuando la opción está activada.

## mysql/mysql.yml

Los datos de protección siempre viven en NBT/PDC en los propios bloques; MySQL es un
índice opcional que replica las ubicaciones de los bloques y las listas de confianza en
una base de datos compartida para búsquedas y auditoría en servidores grandes. Los
cambios se aplican con `/bp reload`.

| Clave | Por defecto | Notas |
|---|---|---|
| `mysql.enabled` | `false` | Replicar los datos de protección en el índice MySQL |
| `mysql.host` | `127.0.0.1` | Host de la base de datos |
| `mysql.port` | `3306` | Puerto de la base de datos |
| `mysql.database` | `blockprot` | Nombre de la base de datos |
| `mysql.username` | `blockprot` | Usuario de la base de datos |
| `mysql.password` | (vacío) | Contraseña de la base de datos |
| `mysql.jdbc_url` | (vacío) | URL JDBC completa; cuando se establece, se ignoran host, puerto y base de datos |
| `mysql.pool.maximum_pool_size` | `10` | Conexiones máximas de HikariCP |
| `mysql.pool.minimum_idle` | `2` | Conexiones inactivas mínimas que se mantienen abiertas |
| `mysql.pool.connection_timeout_ms` | `10000` | Tiempo máximo de espera de un intento de conexión |

## Archivos de idioma

La carpeta `lang/` incluye `lang.yml` más 25 traducciones: árabe, checo, alemán, inglés,
español, finés, francés, hebreo, húngaro, indonesio, italiano, japonés, coreano,
neerlandés, polaco, portugués de Brasil, rumano, ruso, eslovaco, sueco, tailandés,
turco, ucraniano, chino simplificado y chino tradicional. El inglés y el español son los
archivos de referencia; las claves que faltan recurren al inglés, y
`replace_translations: true` conserva los textos traducidos mientras añade las claves
nuevas.
