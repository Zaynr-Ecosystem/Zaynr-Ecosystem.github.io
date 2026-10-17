# Configuration

Zelly's Guard ships four configuration files: `config.yml`, `database.yml`,
`integrations.yml`, and `stones.yml`. They are merged on startup and again on
`/zg reload`. Module toggles and storage settings take effect on restart. Where a key or
a whole section is reserved for behavior still in development, the table says so; those
keys currently have no effect.

## config.yml

### General

| Key | Default | Notes |
|---|---|---|
| `language_file` | `en` | Active language code |
| `fallback_string` | `Unknown translation` | Text shown when a translation is missing |
| `replace_translations` | `true` | On update, merge new translation keys while keeping edited ones |
| `dialogs` | `true` | Native Paper dialogs for Java players |
| `bedrock_forms` | `true` | Bedrock forms through Floodgate. Not applied yet; form support is detected from Floodgate directly |
| `colorblind_default` | `false` | Default colorblind display mode |

### Nexus link

| Key | Default | Notes |
|---|---|---|
| `nexus.follow_language` | `true` | Follow the language selected in Zelly's Nexus. Not applied yet |

### Modules (restart required)

| Key | Default | Notes |
|---|---|---|
| `modules.integrations` | `true` | Integration detection and boot report |
| `modules.updater` | `true` | Reserved; no updater module is wired yet |
| `modules.debug` | `true` | Diagnostics suite |
| `modules.regions` | `true` | Region engine and protection listener |
| `modules.stones` | `true` | Protection stones |
| `modules.claims` | `true` | Claim tool and claim management |
| `modules.blacklist` | `true` | Not applied yet |
| `modules.locks` | `true` | BlockProt Reloaded link and sync |
| `modules.logging` | `true` | Block action logging |
| `modules.combat` | `true` | Not applied yet |
| `modules.pvp` | `true` | Personal PvP toggle |
| `modules.graves` | `true` | Death grave locations |
| `modules.antixray` | `true` | Anti-xray heuristics |

### Regions

Reserved: the current claim flow uses fixed behavior (minimum 10 blocks per side, full
world height), so these tuning keys have no effect yet.

| Key | Default | Notes |
|---|---|---|
| `regions.max_per_player` | `3` | Maximum regions or claims per player |
| `regions.min_size` | `4` | Minimum claim size in X and Z |
| `regions.max_size` | `500` | Maximum claim size in X and Z |
| `regions.default_auto_expand_vertical` | `true` | Expand claims from bedrock to sky |
| `regions.entry_titles` | `true` | Titles on region enter and leave |
| `regions.visualizer_duration_seconds` | `15` | Boundary particle duration |
| `regions.visualizer_particle` | `FLAME` | Boundary particle type |

### Combat

The combat module is wired but not active yet; these keys have no effect yet.

| Key | Default | Notes |
|---|---|---|
| `combat.tag_duration_seconds` | `15` | Combat tag duration |
| `combat.disable_elytra` | `true` | Block elytra while tagged |
| `combat.punish_disconnect` | `true` | Punish combat disconnects |
| `combat.punish_action` | `KILL` | `KILL` or `NONE` |
| `combat.actionbar_timer` | `true` | Countdown in the action bar |

### Graves

Grave tuning is reserved; graves currently store death locations only, so these keys
have no effect yet.

| Key | Default | Notes |
|---|---|---|
| `graves.expiration_minutes` | `60` | Grave expiry |
| `graves.retain_xp_percent` | `80` | XP preserved in the grave |
| `graves.give_compass` | `true` | Compass pointing to the death location |
| `graves.hologram` | `true` | Hologram above the grave |

### Locks

Lock tuning is reserved; locking itself is provided by BlockProt Reloaded, so these keys
have no effect yet.

| Key | Default | Notes |
|---|---|---|
| `locks.auto_lock_on_place` | `true` | Auto-lock inside own claims |
| `locks.notify_owner_on_denied` | `true` | Notify the owner on denied access |
| `locks.max_locks_per_player` | `50` | Maximum locked blocks per player |

### PvP

The PvP state is tracked in memory; these tuning keys have no effect yet.

| Key | Default | Notes |
|---|---|---|
| `pvp.default_enabled` | `true` | Default PvP state for new players |
| `pvp.toggle_cooldown_seconds` | `30` | Toggle cooldown |

### Anti-xray

The anti-xray report is still in development; these keys have no effect yet.

| Key | Default | Notes |
|---|---|---|
| `antixray.alert_staff` | `true` | Alert staff on abnormal mining |
| `antixray.suspicion_threshold` | `10` | Ore-mining rate threshold |

### Logging

The logging pipeline is still in development; these keys have no effect yet.

| Key | Default | Notes |
|---|---|---|
| `logging.retention_days` | `30` | Log retention |
| `logging.queue_batch_size` | `100` | Queue flush batch size |

### Claims

| Key | Default | Notes |
|---|---|---|
| `claims.tool_material` | `GOLDEN_SHOVEL` | Claim wand material. Not applied yet; any golden shovel works as the claim tool |
| `claims.selection_corner_particle` | `HAPPY_VILLAGER` | Corner selection particle. Not applied yet; corner feedback is a gold block highlight |

## database.yml

Storage settings take effect on restart.

| Key | Default | Notes |
|---|---|---|
| `storage.type` | `sqlite` | `sqlite` or `mysql` |
| `storage.sqlite.file` | `guard.db` | SQLite file name |
| `storage.mysql.host` | `localhost` | MySQL host |
| `storage.mysql.port` | `3306` | MySQL port |
| `storage.mysql.database` | `guard` | MySQL database |
| `storage.mysql.user` | `guard` | MySQL user |
| `storage.mysql.password` | (empty) | MySQL password |
| `storage.mysql.pool_size` | `10` | MySQL pool size |

## integrations.yml

These toggles have no effect yet; integration detection is based on the plugin being
present on the server.

| Key | Default | Notes |
|---|---|---|
| `floodgate.enabled` | `true` | Floodgate detection toggle |
| `placeholderapi.enabled` | `true` | PlaceholderAPI detection toggle |

## stones.yml

| Key | Default | Notes |
|---|---|---|
| `stone_block` | `COAL_ORE` | Block that creates a protected area |
| `radius_x` | `10` | Protected blocks along X per side |
| `radius_y` | `10` | Protected blocks above and below |
| `radius_z` | `10` | Protected blocks along Z per side |
| `max_per_player` | `5` | Stones per player |

## Language files

The `lang/` folder holds `lang.yml` (the list of enabled bundled languages) and the
bundled `translations_en.yml` and `translations_es.yml`, kept at full key parity. On
startup and on reload the bundled files are synchronized into the data folder; with
`replace_translations: true`, newly added keys are merged while edited texts are
preserved.

The plugin data folder contains `config.yml`, `database.yml`, `integrations.yml`,
`stones.yml`, the `lang/` folder, and the database file (`guard.db` by default).
