# Configuration

Global settings live in `config.yml`. Every module owns one folder,
`modules/<module>/config.yml`, and starts with `enabled: false`. `/zn reload` applies
language and renderer changes immediately; module switches need a full server restart.
Where a key is parsed but not yet consumed by its module, the table marks it as not
applied yet. The player hubs are `/zn user` and `/zn admin`; every screen in them uses
the renderer chosen by `use_dialogs` and `bedrock_forms`.

## config.yml

| Key | Default | Notes |
|---|---|---|
| `config-version` | `3` | Config schema version; upgraded automatically |
| `language` | `en` | Active translation: `en` or `es` |
| `use_dialogs` | `false` | Java players see Paper dialogs instead of chest inventories. Requires a Paper build with the Dialog API |
| `bedrock_forms` | `true` | Bedrock players see Floodgate forms when Floodgate is installed |
| `setup_notice` | `true` | Admins see the first-start notice until the recommended setup is applied or this key is false |
| `apply_recommended_on_start` | `false` | Apply `recommended all` on the next start, then reset to false |
| `admin_tiers.enabled` | `false` | Segment admin capabilities by tier. False means `zn.admin` grants every admin capability |
| `commands.register-root-aliases` | `true` | Register the optional root shortcuts (`/spawn`, `/home`, `/login`, and more) |
| `commands.disabled-root-aliases` | `[kill, kick, time, weather, msg, gamemode]` | Root command names that are never registered |
| `updater.check-on-boot` | `true` | Run the update check on boot |
| `recommended_config_applied` | absent | Marker written after `recommended config` succeeds |
| `recommended_modules_applied` | absent | Marker written after `recommended modules` succeeds |
| `recommended_<module>_applied` | absent | Marker written after `recommended <module>` succeeds |

Inventories are the default renderer. `use_dialogs: true` switches Java players to
dialogs; Bedrock players always get forms when Floodgate is present and
`bedrock_forms` is true. The old `dialogs` and `gui-mode` keys are migrated to
`use_dialogs` and removed on the first start of this version.

### Module switches

| Key | Default |
|---|---|
| `enabled` in `modules/auth/config.yml` | `false` |
| `enabled` in `modules/antibot/config.yml` | `false` |
| `enabled` in `modules/toolkit/config.yml` | `false` |
| `enabled` in `modules/ban/config.yml` | `false` |
| `enabled` in `modules/join/config.yml` | `false` |
| `enabled` in `modules/chat/config.yml` | `false` |
| `enabled` in `modules/inventory/config.yml` | `false` |
| `enabled` in `modules/clans/config.yml` | `false` |
| `enabled` in `modules/itemedit/config.yml` | `false` |
| `enabled` in `modules/tab/config.yml` | `false` |
| `enabled` in `modules/integrations/config.yml` | `false` |
| `enabled` in `modules/updater/config.yml` | `false` |
| `enabled` in `modules/debug/config.yml` | `false` |

Switches take effect only after a full server restart. A disabled module still
registers its commands; using one explains that the module is disabled and shows both
ways out (edit its folder or run `/zn recommended <module>`).

## modules/auth/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
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

## modules/antibot/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `window-seconds` | `10` | Rate-limit window per address |
| `max-joins-per-window` | `4` | Connections allowed per window |
| `attack-mode.auto-enable` | `true` | Not applied yet |
| `attack-mode.threshold` | `8` | Not applied yet |
| `attack-mode.duration-seconds` | `60` | Not applied yet |
| `checks.require-ping` | `false` | Not applied yet |
| `checks.alert-staff` | `true` | Not applied yet |

## modules/toolkit/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `near-radius` | `100` | Radius of the "near" player list |
| `burn-ticks` | `100` | Burn duration applied by the burn action |
| `tpa-timeout-seconds` | `120` | Teleport request timeout |
| `teleport.warmup-seconds` | `3` | Not applied yet |
| `teleport.cancel-on-move` | `true` | Not applied yet |
| `teleport.cancel-on-damage` | `true` | Not applied yet |
| `homes.default-max-homes` | `3` | Not applied yet |
| `spawn.on-first-join` | `true` | Not applied yet |
| `spawn.on-death` | `false` | Not applied yet |
| `back.save-on-death` | `true` | Not applied yet |
| `back.cooldown-seconds` | `10` | Not applied yet |
| `rtp.rtp-min` | `-1000` | Not applied yet; the range is changed at runtime with `/settpr` |
| `rtp.rtp-max` | `1000` | Not applied yet; the range is changed at runtime with `/settpr` |
| `rtp.cooldown-seconds` | `60` | Not applied yet |

## modules/ban/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `server-name` | `"the server"` | Name shown on the ban, kick and suspend screens |
| `default-suspend-duration` | `"7d"` | Duration applied by `/zn suspend` when none is given (`s`, `m`, `h`, `d`, `w` or `perm`) |
| `screens` | `true` | Render the ban, kick and suspend screens on login refusal and kicks |
| `date-format` | `"yyyy-MM-dd HH:mm"` | Date format used on the screens |
| `help-url` | docs site | Link shown on the screens |
| `appeal-url` | docs site | Link shown on the screens |
| `store-url` | docs site | Link shown on the screens |

## modules/join/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `title-fade.fade-in` | `10` | Title fade-in in ticks |
| `title-fade.stay` | `80` | Title stay in ticks |
| `title-fade.fade-out` | `10` | Title fade-out in ticks |
| `chat.enabled` | `true` | First-join, join and quit chat messages |
| `chat.public.first-join` | 1 entry | Public chat message list for `first-join` |
| `chat.public.join` | 1 entry | Public chat message list for `join` |
| `chat.public.quit` | 1 entry | Public chat message list for `quit` |
| `chat.private.first-join` | `[]` | Private chat message list for `first-join` |
| `chat.private.join` | `[]` | Private chat message list for `join` |
| `chat.private.quit` | `[]` | Private chat message list for `quit` |
| `title.enabled` | `false` | Screen titles |
| `title.public.first-join` | `[]` | Public title list for `first-join` |
| `title.public.join` | `[]` | Public title list for `join` |
| `title.public.quit` | `[]` | Public title list for `quit` |
| `title.private.first-join` | `[]` | Private title list for `first-join` |
| `title.private.join` | `[]` | Private title list for `join` |
| `title.private.quit` | `[]` | Private title list for `quit` |
| `actionbar.enabled` | `false` | Action-bar lines |
| `actionbar.public.first-join` | `[]` | Public action-bar list for `first-join` |
| `actionbar.public.join` | `[]` | Public action-bar list for `join` |
| `actionbar.public.quit` | `[]` | Public action-bar list for `quit` |
| `actionbar.private.first-join` | `[]` | Private action-bar list for `first-join` |
| `actionbar.private.join` | `[]` | Private action-bar list for `join` |
| `actionbar.private.quit` | `[]` | Private action-bar list for `quit` |
| `sound.enabled` | `false` | Join and quit sounds |
| `sound.public.first-join` | `[]` | Public sound list for `first-join` |
| `sound.public.join` | `[]` | Public sound list for `join` |
| `sound.public.quit` | `[]` | Public sound list for `quit` |
| `sound.private.first-join` | `[]` | Private sound list for `first-join` |
| `sound.private.join` | `[]` | Private sound list for `join` |
| `sound.private.quit` | `[]` | Private sound list for `quit` |

`<event>` is `first-join`, `join` or `quit`. Every entry sets a `priority` and can set
an optional `permission`; message entries use `messages` (a list), title entries use
`title` and `subtitle`, and sound entries use `sound`, `volume` and `pitch`.
Placeholders: `<player>`, `<displayname>`, `<world>`, `<online>` and `<uniquejoins>`
(the counter kept in `join-stats.yml`).

## modules/chat/config.yml

### Channels

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
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
| `formatting.groups.admin.global-format` | admin global format | Admin global chat format |
| `formatting.groups.admin.player-click.value` | `/msg <player> ` | Admin click action value |
| `formatting.groups.mod.permission` | `zn.chat.group.mod` | Mod group permission |
| `formatting.groups.mod.global-format` | mod global format | Mod global chat format |
| `formatting.groups.vip.permission` | `zn.chat.group.vip` | VIP group permission |
| `formatting.groups.vip.global-format` | vip global format | VIP global chat format |

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

## modules/clans/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
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

## modules/inventory/config.yml

The inventory module uses `modules/inventory/config.yml`; none of these keys are
applied yet.

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `rollback.save-on-death` | `true` | Not applied yet |
| `rollback.save-on-disconnect` | `true` | Not applied yet |
| `rollback.max-snapshots-per-player` | `20` | Not applied yet |
| `rollback.retention-days` | `7` | Not applied yet |
| `inspector.allow-modification` | `true` | Not applied yet |

## modules/itemedit/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `lore-lines` | `8` | Maximum lore lines |
| `limits.max-name-length` | `64` | Not applied yet |
| `limits.max-lore-line-length` | `128` | Not applied yet |
| `formatting.allow-color-codes` | `true` | Not applied yet |
| `formatting.allow-minimessage` | `true` | Not applied yet |
| `economy.repair-cost` | `0` | Not applied yet |

## modules/tab/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart |
| `tablist.enabled` | `true` | Not applied yet; use `modules.tab.enabled` |
| `tablist.update-interval-ticks` | `20` | Not applied yet |
| `tablist.colorize-ping` | `true` | Not applied yet |
| `tablist.header` | 2 lines | Not applied yet; the header comes from translation keys |
| `tablist.footer` | 2 lines | Not applied yet; the footer comes from translation keys |
| `bossbar.duration-ticks` | `200` | Join boss bar duration |
| `bossbar.color` | `BLUE` | Join boss bar color |
| `bossbar.overlay` | `PROGRESS` | Join boss bar overlay |

## modules/debug/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart. Hidden commands stay registered |

## modules/integrations/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart. Integration detection runs at boot |

## modules/updater/config.yml

| Key | Default | Notes |
|---|---|---|
| `enabled` | `false` | Module switch; requires a restart. The update check is controlled by `updater.check-on-boot` |

## Data layout

Everything lives under the plugin data folder `plugins/ZellysNexus/`:

- `config.yml`: global settings, copied from the jar on first run.
- `modules/<module>/config.yml`: one folder per module, copied on first start when
  missing. The folders are `auth`, `antibot`, `toolkit`, `ban`, `join`, `chat`,
  `inventory`, `clans`, `itemedit`, `tab`, `integrations`, `updater` and `debug`.
- Module data files now live in the same folder as their module: `modules/join/join-stats.yml`,
  `modules/ban/ban-audit.yml`, `modules/auth/auth.yml`, `modules/clans/clans.yml`,
  `modules/itemedit/items.yml`, `modules/antibot/antibot.yml`, and under
  `modules/toolkit/`: `spawn.yml`, `homes.yml`, `warps.yml`, `jails.yml`, `kits.yml`,
  `mail.yml`, `jailed.yml`, `lastseen.yml` and `nicknames.yml`.
- The first start of this version copies a legacy root data file into its module
  folder, verifies the size, and renames the old file to `<name>.migrated`. It never
  overwrites an existing new file; when both exist, it warns and uses the new one.
- `debug/`: dated diagnostic reports written by the debug module.
- No database is used: every store is a UTF-8 YAML file.

## Language files

Translations ship inside the jar and are not data-folder files. `language` selects `en`
or `es`; a key missing in the active language falls back to English, and a language that
fails to load falls back to English entirely. `/zn reload` applies language changes
immediately.
