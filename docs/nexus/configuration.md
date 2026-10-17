# Configuration

Global settings live in `config.yml` in the plugin data folder; per-module settings live
in `modules/<module>.yml`. `/zn reload` applies language and dialog changes immediately;
module toggles need a full server restart. Where a key is parsed but not yet consumed by
its module, the table marks it as not applied yet.

## config.yml

| Key | Default | Notes |
|---|---|---|
| `config-version` | `2` | Config schema version; upgraded automatically |
| `language` | `en` | Active translation: `en` or `es` |
| `dialogs` | `true` | Native Paper dialogs; `false` falls back to the chat interface |
| `commands.register-root-aliases` | `true` | Register the optional root shortcuts (`/spawn`, `/home`, `/login`, and more) |
| `commands.disabled-root-aliases` | `[kill, kick, time, weather, msg, gamemode]` | Root command names that are never registered |
| `updater.check-on-boot` | `true` | Run the update check on boot |

### Module toggles

| Key | Default |
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

Toggles take effect only after a full server restart. Unknown module names default to
enabled, and `debug` defaults to disabled.

## modules/auth.yml

| Key | Default | Notes |
|---|---|---|
| `session-hours` | `12` | Session memory duration |
| `max-accounts-per-ip` | `3` | Account limit per address |
| `min-password-length` | `4` | Minimum password length |
| `max-password-length` | `64` | Maximum password length |
| `max-failed-attempts` | `5` | Failed attempts before lockout |
| `lockout-seconds` | `60` | Lockout duration |
| `otp-expiry-seconds` | `300` | One-time password validity |
| `form-delay-ticks` | `20` | Delay before the auth form opens |
| `auto-login-bedrock` | `true` | Not applied yet |
| `auto-login-premium` | `false` | Not applied yet |
| `login-timeout-seconds` | `60` | Not applied yet |
| `security-effects.blindness` | `true` | Not applied yet |
| `security-effects.slowness` | `true` | Not applied yet |
| `security-effects.invulnerability` | `true` | Not applied yet |
| `security-effects.mute-chat` | `true` | Not applied yet |
| `allowed-commands` | `[/login, /register, /l, /reg]` | Not applied yet |
| `mojang.timeout-seconds` | `4` | Premium verification timeout |
| `mojang.cache-seconds` | `3600` | Premium verification cache |

## modules/antibot.yml

| Key | Default | Notes |
|---|---|---|
| `window-seconds` | `10` | Rate-limit window per address |
| `max-joins-per-window` | `4` | Connections allowed per window |
| `attack-mode.auto-enable` | `true` | Not applied yet |
| `attack-mode.threshold` | `8` | Not applied yet |
| `attack-mode.duration-seconds` | `60` | Not applied yet |
| `checks.require-ping` | `false` | Not applied yet |
| `checks.alert-staff` | `true` | Not applied yet |

## modules/toolkit.yml

| Key | Default | Notes |
|---|---|---|
| `near-radius` | `100` | Radius of the "near" player list |
| `burn-ticks` | `100` | Burn duration applied by the burn action |
| `tpa-timeout-seconds` | `120` | Teleport request timeout |
| `teleport.warmup-seconds` | `3` | Not applied yet |
| `teleport.cancel-on-move` | `true` | Not applied yet |
| `teleport.cancel-on-damage` | `true` | Not applied yet |
| `homes.default-max-homes` | `3` | Not applied yet |
| `homes.bed-sets-home` | `false` | Not applied yet |
| `spawn.on-first-join` | `true` | Not applied yet |
| `spawn.on-death` | `false` | Not applied yet |
| `back.save-on-death` | `true` | Not applied yet |
| `back.cooldown-seconds` | `10` | Not applied yet |
| `rtp.rtp-min` | `-1000` | Not applied yet; the range is changed at runtime with `/settpr` |
| `rtp.rtp-max` | `1000` | Not applied yet; the range is changed at runtime with `/settpr` |
| `rtp.cooldown-seconds` | `60` | Not applied yet |
| `rtp.avoid-water` | `true` | Not applied yet |
| `rtp.avoid-lava` | `true` | Not applied yet |
| `pranks.enabled` | `true` | Not applied yet |
| `pranks.level-1` to `pranks.level-6` | policy text | Not applied yet |

## modules/ban.yml

| Key | Default | Notes |
|---|---|---|
| `server-name` | `"the server"` | Name shown on the ban, kick and suspend screens |
| `default-suspend-duration` | `"7d"` | Duration applied by `/zn suspend` when none is given (`s`, `m`, `h`, `d`, `w` or `perm`) |
| `screens` | `true` | Render the ban, kick and suspend screens on login refusal and kicks |
| `date-format` | `"yyyy-MM-dd HH:mm"` | Date format used on the screens |
| `help-url` | docs site | Link shown on the screens |
| `appeal-url` | docs site | Link shown on the screens |
| `store-url` | docs site | Link shown on the screens |

## modules/join.yml

| Key | Default | Notes |
|---|---|---|
| `title-fade` | `10 / 80 / 10` ticks | Default title fade-in, stay and fade-out |
| `chat.enabled` | `true` | First-join, join and quit chat messages |
| `chat.public.<event>` / `chat.private.<event>` | entries | Public goes to every online player, private only to the player |
| `title.enabled` | `false` | Screen titles |
| `title.public.<event>` / `title.private.<event>` | entries | Title and subtitle entries |
| `actionbar.enabled` | `false` | Action-bar lines |
| `actionbar.public.<event>` / `actionbar.private.<event>` | entries | Single-line entries |
| `sound.enabled` | `false` | Join and quit sounds |
| `sound.public.<event>` / `sound.private.<event>` | entries | Sound entries |

`<event>` is `first-join`, `join` or `quit`. Every entry sets a `priority` and can set
an optional `permission`; message entries use `messages` (a list), title entries use
`title` and `subtitle`, and sound entries use `sound`, `volume` and `pitch`.
Placeholders: `<player>`, `<displayname>`, `<world>`, `<online>` and `<uniquejoins>`
(the counter kept in `join-stats.yml`).

## modules/chat.yml

### Channels

| Key | Default | Notes |
|---|---|---|
| `enabled` | `true` | Not applied yet; use `modules.chat.enabled` |
| `channels.default-channel` | `local` | Default channel for players |
| `channels.local-radius` | `100` | Radius of local chat |
| `channels.shout-prefix` | `!` | Prefix that sends a message to the whole server |
| `channels.shout-permission` | `zn.chat.shout` | Not applied yet; the permission is fixed at `zn.chat.shout` |

### Formatting

| Key | Default | Notes |
|---|---|---|
| `formatting.local-format` | gray `[L]` prefix/name/suffix: message | MiniMessage format for local chat |
| `formatting.global-format` | gold `[G]` prefix/name/suffix: message | MiniMessage format for global chat |
| `formatting.player-hover` | 6 lines (name, rank, ping, world, blank, hint) | Tooltip on player names |
| `formatting.player-click.action` | `SUGGEST_COMMAND` | Click action on player names |
| `formatting.player-click.value` | `/msg <player>` | Click action value |
| `formatting.groups.admin.priority` | `100` | Group priority |
| `formatting.groups.admin.permission` | `zn.chat.group.admin` | Group permission |
| `formatting.groups.admin.local-format` / `global-format` | admin formats | Group chat formats |
| `formatting.groups.admin.player-hover` | 6 lines | Group tooltip |
| `formatting.groups.admin.player-click.action` / `value` | `SUGGEST_COMMAND` / `/msg <player>` | Group click action |
| `formatting.groups.mod.priority` / `permission` | `80` / `zn.chat.group.mod` | Mod group |
| `formatting.groups.mod.local-format` / `global-format` | mod formats | Mod group formats |
| `formatting.groups.vip.priority` / `permission` | `50` / `zn.chat.group.vip` | VIP group |
| `formatting.groups.vip.local-format` / `global-format` | vip formats | VIP group formats |

### Placeholders

| Key | Default | Notes |
|---|---|---|
| `placeholders.item.enabled` | `true` | `[item]` and `[i]` |
| `placeholders.item.format` | aqua `[item_name x amount]` | Item placeholder format |
| `placeholders.inventory.enabled` | `true` | `[inv]` |
| `placeholders.inventory.format` | gold `[Inventory]` | Inventory placeholder format |
| `placeholders.inventory.hover` | Click to inspect inventory | Hover text |
| `placeholders.inventory.command` | `/zn inv see <player>` | Click command |
| `placeholders.enderchest.enabled` | `true` | `[ender]` |
| `placeholders.enderchest.format` | light purple `[EnderChest]` | Ender chest placeholder format |
| `placeholders.enderchest.hover` | Click to inspect ender chest | Hover text |
| `placeholders.enderchest.command` | `/zn inv endersee <player>` | Click command |

### Mentions

| Key | Default | Notes |
|---|---|---|
| `mentions.enabled` | `true` | Player mentions |
| `mentions.format` | yellow bold `@target` | Mention format |
| `mentions.sound.enabled` | `true` | Sound on mention |
| `mentions.sound.type` | `block.note_block.bell` | Sound type |
| `mentions.sound.volume` | `1.0` | Sound volume |
| `mentions.sound.pitch` | `1.5` | Sound pitch |
| `mentions.actionbar.enabled` | `true` | Action bar notification |
| `mentions.actionbar.message` | mentioned-you message | Notification text |

### Moderation

| Key | Default | Notes |
|---|---|---|
| `moderation.cooldown-seconds` | `1.5` | Chat cooldown |
| `moderation.cooldown-bypass-permission` | `zn.chat.bypass.cooldown` | Bypass permission |
| `moderation.anti-duplicate.enabled` | `true` | Block repeated messages |
| `moderation.anti-caps.enabled` | `true` | Block excessive caps |
| `moderation.anti-caps.min-message-length` | `6` | Minimum length for the caps check |
| `moderation.anti-caps.max-caps-percent` | `60` | Maximum share of capital letters |
| `moderation.swear-filter.enabled` | `false` | Swear filter |
| `moderation.swear-filter.block-message` | `false` | Block instead of censoring |
| `moderation.swear-filter.censor-replacement` | `****` | Censoring replacement |
| `moderation.swear-filter.blocked-words` | `[]` | Blocked word list |

### Announcements

| Key | Default | Notes |
|---|---|---|
| `announcements.enabled` | `false` | Scheduled announcements |
| `announcements.interval-seconds` | `180` | Interval between announcements |
| `announcements.prefix` | Nexus prefix | Announcement prefix |
| `announcements.messages` | 3 lines | Rotating messages |

## modules/clans.yml

| Key | Default | Notes |
|---|---|---|
| `invite-seconds` | `120` | Invitation validity |
| `naming.min-name-length` | `3` | Not applied yet |
| `naming.max-name-length` | `32` | Maximum clan name length |
| `naming.max-tag-length` | `6` | Not applied yet |
| `membership.max-members` | `10` | Not applied yet |
| `membership.creation-cost` | `0` | Not applied yet |
| `gameplay.friendly-fire-default` | `false` | Default friendly fire state |
| `gameplay.home-warmup-seconds` | `3` | Not applied yet |
| `gameplay.max-allies` | `3` | Not applied yet |
| `gameplay.max-rivals` | `5` | Not applied yet |

## modules/inventory.yml

The inventory module has no settings file in the data folder; it runs on these built-in
defaults, and none of them are applied yet.

| Key | Default | Notes |
|---|---|---|
| `rollback.save-on-death` | `true` | Not applied yet |
| `rollback.save-on-disconnect` | `true` | Not applied yet |
| `rollback.max-snapshots-per-player` | `20` | Not applied yet |
| `rollback.retention-days` | `7` | Not applied yet |
| `inspector.allow-modification` | `true` | Not applied yet |

## modules/itemedit.yml

| Key | Default | Notes |
|---|---|---|
| `lore-lines` | `8` | Maximum lore lines |
| `limits.max-name-length` | `64` | Not applied yet |
| `limits.max-lore-line-length` | `128` | Not applied yet |
| `formatting.allow-color-codes` | `true` | Not applied yet |
| `formatting.allow-minimessage` | `true` | Not applied yet |
| `economy.repair-cost` | `0` | Not applied yet |

## modules/tab.yml

| Key | Default | Notes |
|---|---|---|
| `tablist.enabled` | `true` | Not applied yet; use `modules.tab.enabled` |
| `tablist.update-interval-ticks` | `20` | Not applied yet |
| `tablist.colorize-ping` | `true` | Not applied yet |
| `tablist.header` | 2 lines | Not applied yet; the header comes from translation keys |
| `tablist.footer` | 2 lines | Not applied yet; the footer comes from translation keys |
| `bossbar.duration-ticks` | `200` | Join boss bar duration |
| `bossbar.color` | `BLUE` | Join boss bar color |
| `bossbar.overlay` | `PROGRESS` | Join boss bar overlay |

## Data layout

Everything lives under the plugin data folder `plugins/ZellysNexus/`:

- `config.yml`: global settings, copied from the jar on first run.
- `modules/`: per-module settings; the templates for `auth`, `antibot`, `toolkit`,
  `ban`, `join`, `chat`, `inventory`, `clans`, `itemedit`, and `tab` are copied on
  first start when missing.
- Module data files: `auth.yml`, `antibot.yml`, `clans.yml`, `ban-audit.yml`,
  `join-stats.yml`, `spawn.yml`, `homes.yml`, `warps.yml`, `jails.yml`, `kits.yml`,
  `mail.yml`, `jailed.yml`, `lastseen.yml`, `nicknames.yml`, and `items.yml`.
- `debug/`: dated diagnostic reports written by the debug module.
- No database is used: every store is a UTF-8 YAML file.

## Language files

Translations ship inside the jar and are not data-folder files. `language` selects `en`
or `es`; a key missing in the active language falls back to English, and a language that
fails to load falls back to English entirely. `/zn reload` applies language changes
immediately.
