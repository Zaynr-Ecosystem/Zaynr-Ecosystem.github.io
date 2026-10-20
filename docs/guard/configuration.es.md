# Configuración

Zelly's Guard lee `config.yml` y una carpeta por cada módulo que ya tiene archivo propio:
`modules/database/config.yml` y `modules/stones/config.yml`. El resto sigue en
`config.yml` y se documenta en su sección. Los archivos se combinan al arrancar y de
nuevo con `/zg reload`; los interruptores de módulos y el almacenamiento se aplican tras
un reinicio. Cuando una clave está reservada para comportamiento aún en desarrollo, la
tabla lo indica. Los hubs de jugador son `/zg user` y `/zg admin`; `/zg recommended`
aplica la configuración recomendada.

## config.yml

### General

| Clave | Por defecto | Notas |
|---|---|---|
| `config-version` | `3` | Versión del esquema de configuración; se actualiza sola |
| `language_file` | `en` | Código del idioma activo |
| `fallback_string` | `Unknown translation` | Texto cuando falta una traducción |
| `replace_translations` | `true` | Al actualizar, añade claves nuevas y conserva las editadas |
| `use_dialogs` | `false` | Los jugadores de Java ven diálogos de Paper en lugar de inventarios. Requiere una build de Paper con la API de diálogos |
| `bedrock_forms` | `true` | Los jugadores de Bedrock ven formularios de Floodgate cuando está instalado |
| `setup_notice` | `true` | Los administradores ven el aviso de primera configuración hasta aplicar la recomendada o poner esta clave en `false` |
| `apply_recommended_on_start` | `false` | Aplica `recommended all` en el siguiente arranque y vuelve a `false` |
| `admin_tiers.enabled` | `false` | Separa las capacidades de administración por nivel. En `false`, `zguard.admin` concede todas |
| `blockprot_recommendation` | `true` | Muestra la recomendación de instalar BlockProt Reloaded cuando falta. Nunca controla el enlace cuando está presente |
| `colorblind_default` | `false` | Modo daltónico por defecto |

Los inventarios son el renderizador por defecto. `use_dialogs: true` cambia a los
jugadores de Java a diálogos; los de Bedrock reciben formularios cuando Floodgate está
presente y `bedrock_forms` es `true`. Las claves antiguas `dialogs` y `gui-mode` se migran
a `use_dialogs` y se eliminan.

### Enlace con Nexus

| Clave | Por defecto | Notas |
|---|---|---|
| `nexus.follow_language` | `true` | Sigue el idioma elegido en Zelly's Nexus. Aún sin aplicar |

### Módulos (requiere reinicio)

Todos los módulos empiezan desactivados; activa los que use el servidor.

| Clave | Por defecto | Notas |
|---|---|---|
| `modules.integrations` | `false` | Detección de integraciones e informe de arranque |
| `modules.updater` | `false` | Reservado; no hay módulo de actualizaciones |
| `modules.debug` | `false` | Suite de diagnóstico |
| `modules.regions` | `false` | Motor de regiones y listener de protección |
| `modules.stones` | `false` | Piedras de protección. `enabled` en `modules/stones/config.yml` también lo activa |
| `modules.claims` | `false` | Herramienta y gestión de claims |
| `modules.blacklist` | `false` | Aún sin aplicar |
| `modules.locks` | `false` | Enlace y sincronización con BlockProt Reloaded |
| `modules.logging` | `false` | Registro de acciones |
| `modules.combat` | `false` | Aún sin aplicar |
| `modules.pvp` | `false` | Alternador personal de PvP |
| `modules.graves` | `false` | Ubicaciones de tumbas |
| `modules.antixray` | `false` | Heurísticas anti-xray |

Un módulo desactivado sigue registrando sus comandos; al usarlos, explica que está
desactivado y muestra las dos salidas (editar su carpeta o ejecutar
`/zg recommended <module>`).

### Regiones

Reservado: el flujo actual de claims usa comportamiento fijo (mínimo 10 bloques por lado,
altura completa), así que estas claves aún no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `regions.max_per_player` | `3` | Máximo de regiones o claims por jugador |
| `regions.min_size` | `4` | Tamaño mínimo en X y Z |
| `regions.max_size` | `500` | Tamaño máximo en X y Z |
| `regions.default_auto_expand_vertical` | `true` | Expande de bedrock al cielo |
| `regions.entry_titles` | `true` | Títulos al entrar y salir |
| `regions.visualizer_duration_seconds` | `15` | Duración de las partículas |
| `regions.visualizer_particle` | `FLAME` | Tipo de partícula |

### Combate

El módulo está conectado pero aún no activo; estas claves no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `combat.tag_duration_seconds` | `15` | Duración de la marca de combate |
| `combat.disable_elytra` | `true` | Bloquea élitros durante el combate |
| `combat.punish_disconnect` | `true` | Castiga desconexiones en combate |
| `combat.punish_action` | `KILL` | `KILL` o `NONE` |
| `combat.actionbar_timer` | `true` | Cuenta atrás en la action bar |

### Tumbas

Ajustes reservados; las tumbas solo guardan ubicaciones, así que estas claves no tienen
efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `graves.expiration_minutes` | `60` | Caducidad de la tumba |
| `graves.retain_xp_percent` | `80` | XP conservada |
| `graves.give_compass` | `true` | Brújula hacia la tumba |
| `graves.hologram` | `true` | Holograma sobre la tumba |

### Candados

Ajustes reservados; los candados los aporta BlockProt Reloaded, así que estas claves no
tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `locks.auto_lock_on_place` | `true` | Cierra al colocar dentro del claim |
| `locks.notify_owner_on_denied` | `true` | Avisa al dueño si se deniega el acceso |
| `locks.max_locks_per_player` | `50` | Máximo de bloques cerrados por jugador |

### PvP

El estado se guarda en memoria; estas claves no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `pvp.default_enabled` | `true` | PvP por defecto para jugadores nuevos |
| `pvp.toggle_cooldown_seconds` | `30` | Enfriamiento del alternador |

### Anti-xray

El informe sigue en desarrollo; estas claves no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `antixray.alert_staff` | `true` | Avisa al staff de minería anómala |
| `antixray.suspicion_threshold` | `10` | Umbral de sospecha |

### Registro

El registro sigue en desarrollo; estas claves no tienen efecto.

| Clave | Por defecto | Notas |
|---|---|---|
| `logging.retention_days` | `30` | Retención |
| `logging.queue_batch_size` | `100` | Tamaño del lote |

### Claims

| Clave | Por defecto | Notas |
|---|---|---|
| `claims.tool_material` | `GOLDEN_SHOVEL` | Material de la herramienta. Aún sin aplicar; cualquier pala dorada sirve |
| `claims.selection_corner_particle` | `HAPPY_VILLAGER` | Partícula de esquina. Aún sin aplicar; la señal es un bloque dorado |

## modules/database/config.yml

El almacenamiento se aplica tras un reinicio. Un `database.yml` antiguo en la raíz se
copia aquí, se verifica y se renombra a `database.yml.migrated`.

| Clave | Por defecto | Notas |
|---|---|---|
| `storage.type` | `sqlite` | `sqlite` o `mysql` |
| `storage.sqlite.file` | `guard.db` | Archivo SQLite |
| `storage.mysql.host` | `localhost` | Host MySQL |
| `storage.mysql.port` | `3306` | Puerto MySQL |
| `storage.mysql.database` | `guard` | Base de datos |
| `storage.mysql.user` | `guard` | Usuario |
| `storage.mysql.password` | (vacío) | Contraseña |
| `storage.mysql.pool_size` | `10` | Tamaño del pool |

## modules/stones/config.yml

| Clave | Por defecto | Notas |
|---|---|---|
| `enabled` | `false` | Interruptor del módulo; requiere reinicio |
| `stone_block` | `COAL_ORE` | Bloque que crea el área protegida |
| `radius_x` | `10` | Bloques protegidos en X por lado |
| `radius_y` | `10` | Bloques arriba y abajo |
| `radius_z` | `10` | Bloques protegidos en Z por lado |
| `max_per_player` | `5` | Piedras por jugador |

## BlockProt Reloaded

Guard funciona sin BlockProt Reloaded, pero por sí solo no puede proteger bloques
individuales. Cuando el plugin llamado `BlockProtReloaded` (o `BlockProt`) está instalado
y activo, Guard se enlaza con él y `/zg lock` informa de que está activo. Cuando falta,
`/zg lock` y la pantalla de bloqueos muestran una recomendación controlada por
`blockprot_recommendation`, y la consola registra el mismo aviso cuando la clave es true.
Los hubs de jugador y de administración no abren el menú propio de BlockProt.

## Archivos de idioma

La carpeta `lang/` contiene `lang.yml` (la lista de idiomas incluidos activos) y los
archivos `translations_en.yml` y `translations_es.yml`, con paridad completa de claves.
Al arrancar y al recargar, los archivos incluidos se sincronizan en la carpeta de datos;
con `replace_translations: true`, las claves nuevas se añaden y los textos editados se
conservan.

La carpeta de datos contiene `config.yml`, `modules/database/config.yml`,
`modules/stones/config.yml`, la carpeta `lang/` y el archivo de base de datos
(`guard.db` por defecto).
