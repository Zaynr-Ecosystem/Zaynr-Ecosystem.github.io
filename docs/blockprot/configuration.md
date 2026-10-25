# Configuration

BlockProt Reloaded keeps its configuration in the plugin data folder:

| File | Contents |
|---|---|
| `config.yml` | Main settings: language, locking behavior, entities, expiry, notifications, maintenance |
| `integrations.yml` | Centralized third-party integration settings with a master toggle per plugin |
| `blocks.yml` | Lockable block lists (empty by default; configure through the `/bp lockables` GUI or edit directly) |
| `worlds.yml` | Per-world block lists, active when `per_worlds_config: true` |
| `mysql/mysql.yml` | Optional MySQL/MariaDB index settings |
| `admins.yml` | Staff tier assignments (created when tiers are assigned) |
| `lang/` | `lang.yml` plus 25 bundled translations |

All lockable lists default to empty; `/bp recommended blocks` applies a ready-made
starting selection. Most changes apply with `/bp reload` (which creates a safety backup
first) or automatically when files are edited externally.

## config.yml

### Language

| Key | Default | Notes |
|---|---|---|
| `language_file` | `translations_en.yml` | Active language file |
| `fallback_string` | `Unknown translation` | Text shown when a translation key is missing |
| `replace_translations` | `true` | Automatically add missing keys to translation files on update |

### Worlds

| Key | Default | Notes |
|---|---|---|
| `excluded_worlds` | `[]` | Worlds where the plugin is entirely disabled |
| `per_worlds_config` | `false` | Read separate per-world block configuration from `worlds.yml` |

### Players and friends

| Key | Default | Notes |
|---|---|---|
| `bedrock_username_prefixes` | `[".", "*", "_"]` | Prefixes used to detect Bedrock players through Geyser/Floodgate |
| `lock_on_place_by_default` | `true` | Lock blocks automatically when a player places them |
| `public_is_friend_by_default` | `false` | Treat public blocks as friends by default |
| `player_max_locked_block_count` | `-1` | Cap on locked blocks per player; `-1` is unlimited |
| `lock_hint_cooldown_in_seconds` | `10` | Cooldown between lock hint messages |
| `friend_search_similarity` | `0.5` | Similarity threshold when searching friends by name (0.0 to 1.0) |
| `disable_friend_functionality` | `false` | Globally disable the friends system |

### Blocks and locking behavior

| Key | Default | Notes |
|---|---|---|
| `modern_family_blocks` | `false` | Output format of `blocks.yml` when modified through `/bp lockables` (`false` flat names, `true` family expressions). Never reads or modifies the file on startup; auto-disables when all lockable lists are empty |
| `redstone_disallowed_by_default` | `false` | Disallow redstone interaction with locked blocks by default |
| `simplified_hopper_logic` | `false` | Simpler hopper checks, trading precision for performance |
| `protect_locked_blocks_from_explosions` | `true` | Locked blocks survive explosions |
| `block_protected_block_piston_movement` | `true` | Pistons cannot move locked blocks |
| `clear_protection_on_shulker_break` | `false` | Clear a shulker box's protection when it is broken |
| `allow_break_protected_blocks` | `false` | Allow breaking protected blocks you do not own (protection data stays) |
| `respect_spawn_protection` | `true` | Respect vanilla spawn protection |
| `block_lock_effects` | `true` | Particle effects when interacting with locked blocks |
| `block_lock_sounds` | `true` | Sounds when interacting with locked blocks |
| `use_menus` | `false` | Consolidate menus into `/bp user` and `/bp admin`; when false, each feature keeps its own subcommand |
| `use_dialogs` | `false` | Native Paper Dialogs instead of inventories, anvils, and chat. Requires Paper 1.21.7 or later; auto-disabled with a warning when the dialog API is unavailable |
| `timed_access_max_duration_days` | `90` | Maximum duration of a timed access grant |

### Entity protection

| Key | Default | Notes |
|---|---|---|
| `entity_protection.enabled` | `false` | Protect animals, villagers, and other entities |
| `entity_protection.auto_protect_on_tame` | `true` | Protect entities automatically when tamed |
| `entity_protection.menu_item` | `STICK` | Item used to open the entity protection menu |
| `entity_protection.villager_locate_seconds` | `6` | Seconds of the villager locate indicator |
| `villager_workstation_protection.enabled` | `true` | Protect workstations belonging to protected villagers |
| `villager_workstation_protection.radius` | `2` | Horizontal radius around the workstation |
| `villager_workstation_protection.vertical_radius` | `1` | Vertical radius around the workstation |

### Expiry

Per-block manual expiry (setting an expiration time on one specific block) is planned
for a future release and is not available yet; world-level default expiry is configured
below.

| Key | Default | Notes |
|---|---|---|
| `world_expiry.enabled` | `false` | Global expiry of inactive block protections |
| `world_expiry.check_interval_minutes` | `10` | Interval between expiration checks |
| `world_expiry.worlds` | `{}` | World-specific expiry times |

### Raid detection

| Key | Default | Notes |
|---|---|---|
| `raid_detection.enabled` | `false` | Protect locked blocks and entities from raids |

### Notifications

| Key | Default | Notes |
|---|---|---|
| `notify_op_of_updates` | `false` | Notify operators when an update is available |
| `owner_notifications.enabled` | `true` | Allow owners to receive notifications about their blocks |
| `owner_notifications.notify_on_open` | `true` | Notify when someone opens the owner's block |
| `owner_notifications.notify_on_take` | `true` | Notify when someone takes items from the owner's block |
| `owner_notifications.notify_on_place` | `true` | Notify when someone places items in the owner's block |

### Maintenance

| Key | Default | Notes |
|---|---|---|
| `inactivity_cleanup_days` | `-1` | Days of inactivity before a player's protections are removed; `-1` disables it |
| `auto_reload_configs` | `true` | Reload configuration when files change externally |
| `auto_reload_delay_seconds` | `2` | Quiet period (0 to 5) batching rapid saves into a single reload |
| `enable_session_log` | `true` | Session logging |
| `enable_backups` | `true` | Automatic database backups |
| `admin_tiers.enabled` | `false` | When false, `blockprot.user.admin` grants all admin capabilities; when true, permissions split into t1, t2, t3, owner, and custom tiers |

### Action bar

| Key | Default | Notes |
|---|---|---|
| `action_bar.duration_seconds` | `6` | Duration of temporary action bar alerts |

## integrations.yml

All external integrations are configured from this single file; the old per-integration
files are no longer read and can be removed safely. Each integration has a master
`enabled` toggle.

| Key | Default | Notes |
|---|---|---|
| `worldguard.enabled` | `true` | WorldGuard integration |
| `worldguard.enable_flag_functionality` | `true` | Enables the `allow-blockprot` region flag; when off, WorldGuard is detected but never consulted |
| `lands.enabled` | `true` | Lands integration |
| `lands.allow_protecting_containers_in_wilderness` | `true` | Allow protecting containers in unclaimed wilderness |
| `lands.require_protect_for_friends_flag` | `false` | Register the "Require 'Protect containers' for friends" role flag |
| `towny.enabled` | `true` | Towny integration |
| `towny.cleanup_plots_after_unclaim` | `true` | Clean protections when a plot is cleared, unclaimed, or ruined |
| `towny.restrict_access_to_residents` | `false` | Restrict block access to town residents only |
| `towny.allow_mayor_to_see_block_info` | `false` | Allow mayors to use the block info view |
| `towny.bypass_protection_in_ruined_towns` | `true` | Allow bypassing protections in ruined towns |
| `claimchunk.enabled` | `true` | ClaimChunk integration |
| `claimchunk.restrict_access_to_chunk_owner` | `false` | Fully restrict access to the chunk owner (otherwise only locking is restricted) |
| `worldedit.enabled` | `true` | WorldEdit integration |
| `worldedit.paste_autolock.enabled` | `false` | Auto-lock protectable blocks after a `//paste` |
| `worldedit.paste_autolock.radius` | `24` | Radius around the paste origin to scan |
| `worldedit.paste_autolock.max_blocks_per_paste` | `5000` | Safety limit per paste |
| `worldedit.paste_autolock.delay_ticks` | `20` | Delay before the scan starts |
| `placeholderapi.enabled` | `true` | PlaceholderAPI integration |
| `viaversion.enabled` | `true` | ViaVersion client version detection |
| `residence.enabled` | `true` | Residence integration |
| `residence.restrict_access_to_residence_owner` | `false` | Fully restrict access to the residence owner |
| `griefprevention.enabled` | `true` | GriefPrevention integration |
| `griefprevention.restrict_access_to_claim_owner` | `false` | Fully restrict access to the claim owner |
| `geyser.enabled` | `true` | Geyser integration: Bedrock player detection and Bedrock forms |
| `floodgate.enabled` | `true` | Floodgate integration |
| `floodgate.auto_detect_prefix` | `true` | Detect the Bedrock username prefix from Floodgate automatically |

## blocks.yml

Lockable lists are empty by default. Entries accept flat material names (`CHEST`) or
family expressions such as `[*-CHEST]` (all chest variants), `[*-FURNACE *-CHEST]`
(combined families), or `[*]`. The file is never modified on startup or reload; only
GUI toggles write to it.

| Key | Default | Notes |
|---|---|---|
| `lockable_tile_entities` | `[]` | Containers and workstations |
| `lockable_shulker_boxes` | `[]` | Shulker box variants |
| `lockable_blocks` | `[]` | General lockable blocks |
| `lockable_doors` | `[]` | Doors and trapdoors |
| `lockable_entities` | `[]` | Lockable entities |
| `protectable_entities` | `[VILLAGER]` | Entities eligible for entity protection |
| `auto_drop_to_inventory.enabled` | `true` | Return blocks to the inventory when unprotecting |
| `auto_drop_to_inventory.blocks` | `[]` | Blocks affected by the auto-drop behavior |

## worlds.yml

Active when `config.yml` has `per_worlds_config: true`. Each listed world takes
absolute, self-contained control of its lists: `blocks.yml` is never consulted for that
world once it has an entry, even for a category the entry leaves empty. Lists here always
use the compact family-expression syntax regardless of `modern_family_blocks`. A world
with `enabled: false` cannot have any locked blocks. Worlds auto-populate with empty
lists on first scan, and the per-world editor is reachable from `/bp lockables` (map
button) when the option is on.

## mysql/mysql.yml

Protection data always lives in NBT/PDC on the blocks themselves; MySQL is an optional
index that mirrors block locations and trust lists into a shared database for searching
and auditing on large servers. Changes apply with `/bp reload`.

| Key | Default | Notes |
|---|---|---|
| `mysql.enabled` | `false` | Mirror protection data into the MySQL index |
| `mysql.host` | `127.0.0.1` | Database host |
| `mysql.port` | `3306` | Database port |
| `mysql.database` | `blockprot` | Database name |
| `mysql.username` | `blockprot` | Database user |
| `mysql.password` | (empty) | Database password |
| `mysql.jdbc_url` | (empty) | Full JDBC URL; when set, host, port, and database are ignored |
| `mysql.pool.maximum_pool_size` | `10` | Maximum HikariCP connections |
| `mysql.pool.minimum_idle` | `2` | Minimum idle connections kept alive |
| `mysql.pool.connection_timeout_ms` | `10000` | Connection attempt timeout |

## Language files

The `lang/` folder ships `lang.yml` plus 25 translations: Arabic, Czech, German,
English, Spanish, Finnish, French, Hebrew, Hungarian, Indonesian, Italian, Japanese,
Korean, Dutch, Polish, Brazilian Portuguese, Romanian, Russian, Slovak, Swedish, Thai,
Turkish, Ukrainian, Simplified Chinese, and Traditional Chinese. English and Spanish are
the reference files; missing keys fall back to English, and `replace_translations: true`
keeps translated texts while adding new keys.
