# Configuración

Zelly's Guard incluye cuatro archivos de configuración: `config.yml`, `database.yml`,
`integrations.yml` y `stones.yml`. Se fusionan al arrancar y de nuevo con `/zg reload`. Los
interruptores de módulos y los ajustes de almacenamiento surten efecto al reiniciar. Cuando
una clave o una sección completa está reservada para un comportamiento aún en desarrollo, la
tabla lo indica; esas claves actualmente no tienen efecto.

## config.yml

### General

| Clave | Por defecto | Notas |
|---|---|---|
| `language_file` | `en` | Código del idioma activo |
| `fallback_string` | `Unknown translation` | Texto mostrado cuando falta una traducción |
| `replace_translations` | `true` | Al actualizar, fusiona las claves de traducción nuevas mientras conserva las editadas |
| `dialogs` | `true` | Diálogos nativos de Paper para jugadores de Java |
| `bedrock_forms` | `true` | Formularios de Bedrock mediante Floodgate. Aún no se aplica; la compatibilidad con formularios se detecta directamente desde Floodgate |
| `colorblind_default` | `false` | Modo de visualización para daltonismo por defecto |

### Enlace con Nexus

| Clave | Por defecto | Notas |
|---|---|---|
| `nexus.follow_language` | `true` | Sigue el idioma seleccionado en Zelly's Nexus. Aún no se aplica |

### Módulos (requiere reinicio)

| Clave | Por defecto | Notas |
|---|---|---|
| `modules.integrations` | `true` | Detección de integraciones e informe de arranque |
| `modules.updater` | `true` | Reservado; aún no hay ningún módulo de actualizaciones conectado |
| `modules.debug` | `true` | Suite de diagnósticos |
| `modules.regions` | `true` | Motor de regiones y listener de protección |
| `modules.stones` | `true` | Piedras de protección |
| `modules.claims` | `true` | Herramienta de claims y gestión de claims |
| `modules.blacklist` | `true` | Aún no se aplica |
| `modules.locks` | `true` | Enlace y sincronización con BlockProt Reloaded |
| `modules.logging` | `true` | Registro de acciones sobre bloques |
| `modules.combat` | `true` | Aún no se aplica |
| `modules.pvp` | `true` | Interruptor personal de PvP |
| `modules.graves` | `true` | Ubicaciones de las tumbas de muerte |
| `modules.antixray` | `true` | Heurísticas anti-xray |

### Regiones

Reservado: el flujo actual de claims usa un comportamiento fijo (mínimo 10 bloques por lado,
altura completa del mundo), por lo que estas claves de ajuste aún no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `regions.max_per_player` | `3` | Máximo de regiones o claims por jugador |
| `regions.min_size` | `4` | Tamaño mínimo de claim en X y Z |
| `regions.max_size` | `500` | Tamaño máximo de claim en X y Z |
| `regions.default_auto_expand_vertical` | `true` | Expande los claims desde la bedrock hasta el cielo |
| `regions.entry_titles` | `true` | Títulos al entrar y salir de una región |
| `regions.visualizer_duration_seconds` | `15` | Duración de las partículas del límite |
| `regions.visualizer_particle` | `FLAME` | Tipo de partícula del límite |

### Combate

El módulo de combate está conectado pero aún no está activo; estas claves aún no tienen
efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `combat.tag_duration_seconds` | `15` | Duración del tag de combate |
| `combat.disable_elytra` | `true` | Bloquea el elytra mientras estás marcado por el tag |
| `combat.punish_disconnect` | `true` | Castiga las desconexiones en combate |
| `combat.punish_action` | `KILL` | `KILL` o `NONE` |
| `combat.actionbar_timer` | `true` | Cuenta atrás en la barra de acción |

### Tumbas

El ajuste de tumbas está reservado; las tumbas actualmente solo almacenan ubicaciones de
muerte, por lo que estas claves aún no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `graves.expiration_minutes` | `60` | Caducidad de la tumba |
| `graves.retain_xp_percent` | `80` | XP conservada en la tumba |
| `graves.give_compass` | `true` | Brújula que apunta a la ubicación de la muerte |
| `graves.hologram` | `true` | Holograma sobre la tumba |

### Bloqueos

El ajuste de bloqueos está reservado; el bloqueo en sí lo proporciona BlockProt Reloaded,
por lo que estas claves aún no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `locks.auto_lock_on_place` | `true` | Bloqueo automático dentro de tus propios claims |
| `locks.notify_owner_on_denied` | `true` | Notifica al propietario cuando se deniega el acceso |
| `locks.max_locks_per_player` | `50` | Máximo de bloques bloqueados por jugador |

### PvP

El estado de PvP se rastrea en memoria; estas claves de ajuste aún no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `pvp.default_enabled` | `true` | Estado de PvP por defecto para jugadores nuevos |
| `pvp.toggle_cooldown_seconds` | `30` | Enfriamiento del interruptor |

### Anti-xray

El informe anti-xray sigue en desarrollo; estas claves aún no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `antixray.alert_staff` | `true` | Alerta al staff sobre minería anormal |
| `antixray.suspicion_threshold` | `10` | Umbral de la tasa de minería de minerales |

### Registro

La canalización de registro sigue en desarrollo; estas claves aún no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `logging.retention_days` | `30` | Retención de registros |
| `logging.queue_batch_size` | `100` | Tamaño de lote del vaciado de la cola |

### Claims

| Clave | Por defecto | Notas |
|---|---|---|
| `claims.tool_material` | `GOLDEN_SHOVEL` | Material de la varita de claims. Aún no se aplica; cualquier pala dorada sirve como herramienta de claims |
| `claims.selection_corner_particle` | `HAPPY_VILLAGER` | Partícula de selección de esquinas. Aún no se aplica; la respuesta visual de las esquinas es un resaltado de bloque dorado |

## database.yml

Los ajustes de almacenamiento surten efecto al reiniciar.

| Clave | Por defecto | Notas |
|---|---|---|
| `storage.type` | `sqlite` | `sqlite` o `mysql` |
| `storage.sqlite.file` | `guard.db` | Nombre del archivo SQLite |
| `storage.mysql.host` | `localhost` | Host de MySQL |
| `storage.mysql.port` | `3306` | Puerto de MySQL |
| `storage.mysql.database` | `guard` | Base de datos de MySQL |
| `storage.mysql.user` | `guard` | Usuario de MySQL |
| `storage.mysql.password` | (vacía) | Contraseña de MySQL |
| `storage.mysql.pool_size` | `10` | Tamaño del pool de MySQL |

## integrations.yml

Estos interruptores aún no tienen efecto; la detección de integraciones se basa en que el
plugin esté presente en el servidor.

| Clave | Por defecto | Notas |
|---|---|---|
| `floodgate.enabled` | `true` | Interruptor de detección de Floodgate |
| `placeholderapi.enabled` | `true` | Interruptor de detección de PlaceholderAPI |

## stones.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `stone_block` | `COAL_ORE` | Bloque que crea un área protegida |
| `radius_x` | `10` | Bloques protegidos a lo largo de X por lado |
| `radius_y` | `10` | Bloques protegidos por encima y por debajo |
| `radius_z` | `10` | Bloques protegidos a lo largo de Z por lado |
| `max_per_player` | `5` | Piedras por jugador |

## Archivos de idioma

La carpeta `lang/` contiene `lang.yml` (la lista de idiomas incluidos habilitados) y los
archivos incluidos `translations_en.yml` y `translations_es.yml`, mantenidos con paridad
total de claves. Al arrancar y al recargar, los archivos incluidos se sincronizan en la
carpeta de datos; con `replace_translations: true`, las claves recién añadidas se fusionan
mientras que los textos editados se conservan.

La carpeta de datos del plugin contiene `config.yml`, `database.yml`, `integrations.yml`,
`stones.yml`, la carpeta `lang/` y el archivo de base de datos (`guard.db` por defecto).
