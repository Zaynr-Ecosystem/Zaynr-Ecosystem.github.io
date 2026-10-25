# Configuration

Zelly's Guard reads `config.yml` plus one folder per module that already has its own
file: `modules/database/config.yml` and `modules/stones/config.yml`. Everything else is
still in `config.yml` and is documented in its own section below. Files are merged on
startup and again on `/zg reload`; module switches and storage settings take effect on
restart. Where a key is reserved for behavior still in development, the table says so.
The player hubs are `/zg user` and `/zg admin`; `/zg recommended` applies the recommended
setup.

## config.yml

### General

| Key | Default | Notes |
|---|---|---|
| `config-version` | `3` | Config schema version; upgraded automatically |
| `language_file` | `en` | Active language code |
| `fallback_string` | `Unknown translation` | Text shown when a translation is missing |
| `replace_translations` | `true` | On update, merge new translation keys while keeping edited ones |
| `bedrock_forms` | `true` | Bedrock players see Floodgate forms when Floodgate is installed |
| `setup_notice` | `true` | Admins see the first-start notice until the recommended setup is applied or this key is false |
| `apply_recommended_on_start` | `false` | Apply `recommended all` on the next start, then reset to false |
| `admin_tiers.enabled` | `false` | Segment admin capabilities by tier. False means `zguard.admin` grants every admin capability |
| `blockprot_recommendation` | `true` | Show the recommendation to install BlockProt Reloaded when it is absent. It never controls the link when BlockProt is present |
| `colorblind_default` | `false` | Default colorblind display mode |

Paper dialogs are the native menu interface for Java players; chest inventory menus have been retired. On servers without Paper Dialog API support, menu commands show a notice and every function remains fully usable through its command. Bedrock players receive Floodgate forms when Floodgate is present and `bedrock_forms` is true. Legacy `dialogs`, `gui-mode`, and `use_dialogs` keys are automatically purged from `config.yml`.

### Nexus link

| Key | Default | Notes |
|---|---|---|
| `nexus.follow_language` | `true` | Follow the language selected in Zelly's Nexus. Not applied yet |

### Modules (restart required)

Every module starts disabled; enable the ones the server uses.

| Key | Default | Notes |
|---|---|---|
| `modules.integrations` | `false` | Integration detection and boot report |
| `modules.updater` | `false` | Reserved; no updater module is wired yet |
| `modules.debug` | `false` | Diagnostics suite |
| `modules.regions` | `false` | Region engine and protection listener |
| `modules.stones` | `false` | Protection stones. `enabled` in `modules/stones/config.yml` also turns it on |
| `modules.claims` | `false` | Claim tool and claim management |
| `modules.blacklist` | `false` | Not applied yet |
| `modules.locks` | `false` | BlockProt Reloaded link and sync |
| `modules.logging` | `false` | Block action logging |
| `modules.combat` | `false` | Not applied yet |
| `modules.pvp` | `false` | Personal PvP toggle |
| `modules.graves` | `false` | Death grave locations |
| `modules.antixray` | `false` | Anti-xray heuristics |

A disabled module still registers its commands; using one explains that the module is
disabled and shows both ways out (edit its folder or run `/zg recommended <module>`).

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

## modules/database/config.yml

Storage settings take effect on restart. A legacy root `database.yml` is copied here,
verified, and renamed to `database.yml.migrated`.

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

## modules/stones/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `stone_block` | `COAL_ORE` | Block that creates a protected area |
| `radius_x` | `10` | Protected blocks along X per side |
| `radius_y` | `10` | Protected blocks above and below |
| `radius_z` | `10` | Protected blocks along Z per side |
| `max_per_player` | `5` | Stones per player |

## BlockProt Reloaded

Guard works without BlockProt Reloaded, but it cannot protect individual blocks on its
own. When the plugin named `BlockProtReloaded` (or `BlockProt`) is installed and enabled,
Guard links to it and `/zg lock` reports that it is active. When it is absent, `/zg lock`
and the locks screen show a recommendation controlled by `blockprot_recommendation`, and
the console logs the same hint when the key is true. The user and admin hubs do not open
BlockProt's own menu.

## Language files

The `lang/` folder holds `lang.yml` (the list of enabled bundled languages) and the
bundled `translations_en.yml` and `translations_es.yml`, kept at full key parity. On
startup and on reload the bundled files are synchronized into the data folder; with
`replace_translations: true`, newly added keys are merged while edited texts are
preserved.

The plugin data folder contains `config.yml`, `modules/database/config.yml`,
`modules/stones/config.yml`, the `lang/` folder, and the database file (`guard.db` by
default).
