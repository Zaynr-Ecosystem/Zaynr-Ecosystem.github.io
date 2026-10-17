# Modules

Zelly's Nexus is modular: every feature is a module that can be enabled or disabled
independently, and all modules are reached through one root command, `/zn` (alias
`/nexus`).

- **The module list.** Thirteen toggles live under `modules` in `config.yml`: `auth`,
  `antibot`, `toolkit`, `ban`, `join`, `chat`, `inventory`, `clans`, `itemedit`, `tab`,
  `integrations`, `updater`, and `debug`. All default to enabled except `debug`.
- **Where settings live.** Global settings are in `config.yml`; per-module settings are in
  `modules/<module>.yml` in the plugin data folder. Templates for ten modules ship in
  the jar and are copied on first start when missing: `auth`, `antibot`, `toolkit`,
  `ban`, `join`, `chat`, `inventory`, `clans`, `itemedit`, and `tab`.
- **Toggling needs a restart.** Changing any `modules.<id>.enabled` value takes effect
  only after a full server restart; `/zn reload` detects the change, tells the sender,
  and logs a warning.
- **Boot report.** On enable, the plugin loads modules in a fixed order (translation,
  auth, antibot, toolkit, ban, join, chat, inventory, clans, itemedit, tab, integrations,
  updater, debug). Each module ends up LOADED, DISABLED, or FAILED, and the boot report
  prints the
  detected integrations, every module state, and a one-line summary.
- **Routes and aliases.** Every module is reached as `/zn <module>` with a short alias:
  `a`, `ab`, `tools`, `c`, `inv`, `clan`, `ie`, `t`, `int`, `dbg`. Optional root
  shortcuts (`/spawn`, `/home`, `/login`, and more) are controlled by
  `commands.register-root-aliases` and `commands.disabled-root-aliases`. Five module
  roots are always registered when their module is enabled, regardless of those settings:
  `/auth`, `/zantibot`, `/clan`, `/inventory`, and `/itemedit`.
- **Menu order.** The user menu lists modules in a fixed order: auth, toolkit, chat,
  inventory, clans, itemedit, tab, integrations, debug. Buttons are also gated on the
  module toggles and on permissions.
- **Login gate.** While the auth module is loaded, unauthenticated players are blocked
  from movement, block breaking and placing, interaction, chat, item drops and pickups,
  damage, and inventory clicks, and from every command except `/zn`, `/zn menu`,
  `/zn help`, `/zn auth`, and the registered auth root aliases. If the auth module fails
  to load, joins are refused until the next restart.
- **Translations.** `language` accepts `en` or `es`; missing keys fall back to English,
  and a language that fails to load falls back to English entirely.
- **Public API.** The plugin registers `NexusApi` as a Bukkit service, exposing the
  version, language, dialog state, and registration of custom menu entries and
  subcommands for other plugins.

## auth

Route `/zn auth` (alias `a`); menu order 10; enabled by default.

- Registration, login, and logout with configurable password length limits.
- Session memory, one-time passwords, TOTP, PIN, recovery email, captcha, and
  verification-code flows.
- A login gate for unauthenticated players with the restrictions listed above.
- Mojang premium-account verification with a timeout and cache.
- Administrative account tools: delete account, mark premium/cracked/freemium, auth
  logs, purge, and forced login.
- Credentials are masked in the server log.

Commands: `/auth`, `/register` (`/reg`), `/login` (`/l`), `/logout`,
`/changepassword` (`/changepw`), `/email`, `/totp`, `/pin`, plus the actions
`unregister`, `otp`, `remember`, `captcha`, `verification`, `form`, `menu`, `delacc`,
`premium`, `cracked`, `freemium`, `getlogs`, `admin`, and `antibot`.

Permissions: `zn.auth.player` (everyone), `zn.auth.admin` (operators).
Storage: `auth.yml`.

## antibot

Route `/zn antibot` (alias `ab`); enabled by default. No root-menu entry; its menu opens
from the command.

- Connection rate throttling per address within a time window.
- Panic mode that blocks every new connection, an address block list, and status
  reporting.
- A staff permission gate for every action.

Commands: `/zantibot` (`/antibot`), `menu`, `status`, `panic <on|off>`, `list`,
`add`/`block <address>`, `remove`/`unblock <address>`.

Permissions: `zn.antibot.admin` (operators); the legacy `zn.antibot` node grants it.
Storage: `antibot.yml`.

## toolkit

Route `/zn toolkit` (alias `tools`); menu order 30; enabled by default.

- Registers six command domains: teleportation, player, server, moderation, kits, and
  items, plus their listeners and data store.
- Exposes `/zn prank` as an additional direct route.
- Keeps homes, warps, spawn, jails, kits, mail, last-seen data, and nicknames in YAML
  files.
- The random teleport range can be changed at runtime with `/settpr`.

The full command list lives on the [Commands](commands.md) page.

Permissions: per action `zn.<domain>.<action>` (domains: teleport, player, server,
moderation, kit, items), also accepted as `zn.toolkit.<action>`; `zn.admin` and
`zn.toolkit.admin` grant every action, and several legacy nodes are accepted.
Storage: `spawn.yml`, `homes.yml`, `warps.yml`, `jails.yml`, `kits.yml`, `mail.yml`,
`jailed.yml`, `lastseen.yml`, `nicknames.yml`.

## ban

Enabled by default; no command route of its own: the toolkit's ban, IP ban, kick,
suspend and unsuspend actions run on it.

- Permanent, temporary and IP bans, plus suspensions, with a login-refusal screen for
  banned or suspended players and a screen on kick, built from `modules/ban.yml`
  (server name, date format and links).
- Suspensions use `default-suspend-duration` when no duration is given; `/zn suspend`
  without a reason opens the suspend dialog for online staff.
- Ban actions are recorded to `ban-audit.yml`.
- With `modules.ban.enabled: false`, those actions reply that the module is disabled.

Commands: none of its own; the actions live in the toolkit (`/ban`, `/tempban`,
`/unban`, `/banip`, `/tempbanip`, `/unbanip`, `/suspend` and `/unsuspend`).

Permissions: the toolkit nodes `zn.moderation.*`.
Storage: `ban-audit.yml`.

## join

Enabled by default; no command route: it reacts to joins, first joins and quits.

- Four independent channels: chat messages, screen titles, action-bar lines and
  sounds, each with public (everyone) and private (the player) variants.
- Every entry sets a priority and can carry an optional permission, so different
  groups can receive different messages.
- First joins are detected automatically; titles share the `title-fade` timings unless
  an entry overrides them.
- Placeholders: `<player>`, `<displayname>`, `<world>`, `<online>` and `<uniquejoins>`
  (the counter kept in `join-stats.yml`).

Commands: none.

Permissions: none of its own; the per-entry `permission` values are optional and
defined by the server.
Storage: `join-stats.yml`.

## chat

Route `/zn chat` (alias `c`); menu order 40; enabled by default.

- Local and global channels: a shout prefix sends to the whole server, a local radius
  limits the rest; per-player shout toggle and chat hiding.
- MiniMessage formats for local and global chat with per-group overrides (admin, mod,
  vip) chosen by priority and permission.
- Hover tooltips and click actions on player names.
- Interactive placeholders: `[item]`/`[i]`, `[inv]`, and `[ender]`.
- Player mentions with an optional sound and action-bar notification.
- Moderation: cooldown with bypass permission, anti-duplicate, anti-caps, and a swear
  filter with blocked words.
- Scheduled announcements, disabled by default.

Commands: `/zn chat` (menu), `/zn chat shout`, `/zn chat toggle` (optional roots
`/chattoggle`, `/hidechat`), `clear`, `mute`.

Permissions: `zn.chat.shout`, `zn.chat.admin.clear`, `zn.chat.admin.mute`,
`zn.chat.color`, `zn.chat.minimessage`, `zn.chat.bypass.cooldown`,
`zn.chat.bypass.mute`, and `zn.chat.bypass.clear` (operators); `zn.chat.toggle`
(everyone).
Storage: none; toggle and mute state is kept in memory.

## inventory

Route `/zn inventory` (alias `inv`); menu order 50; enabled by default.

- Live inspection of another player's inventory and ender chest, with an optional
  modification mode.
- Clear, clone, give, and ender-chest equivalents, a rollback command that restores a
  death snapshot, and a purge of offline death snapshots.
- Death snapshots are captured through a death listener.

Commands: `/inventory`, `/invsee`, `/endersee` (`/ecsee`), `/clearinventory` (`/ci`),
`enderclear`, `clone`, `enderclone`, `give`, `endergive`, `/invrollback`, `reload`.

Permissions: `zn.inventory.see`, `zn.inventory.clear`, `zn.inventory.clone`,
`zn.inventory.give`, `zn.inventory.rollback`, `zn.inventory.admin` (operators).
Storage: none; snapshots are held in memory.

## clans

Route `/zn clans` (alias `clan`); menu order 60; enabled by default.

- Clan creation and lifecycle: disband, invite, accept, kick, leave, rename,
  description, ranks, home, and home-set.
- Diplomacy and warfare: allies, rivals, wars, rivalries, and friendly fire (personal,
  clan, and global).
- Community tools: bulletin board, stats, roster, list, lookup, regroup, trust, mute,
  banner, kills, most-killed, coords, vitals, profile, locale, help, and menu.

Commands: 39 actions, all player-only; the full list lives on the
[Commands](commands.md) page.

Permissions: `zn.clans.player` (everyone); the administrative actions (`verify`, `ban`,
`unban`, `globalff`) additionally need `zn.admin`.
Storage: `clans.yml`.

## itemedit

Route `/zn itemedit` (alias `ie`); menu order 70; enabled by default.

- Edits the item in the main hand: rename, lore lines, enchantments, unbreakable flag,
  attribute modifiers, custom model data, and item flags.
- Shows item info, imports Base64 item data, stores items under keys, and manages server
  items.
- A dialog-based editor opens when dialogs are enabled.

Commands: `/itemedit` (`/ie`), `/rename`, `/lore`, `enchant`, `unbreakable`,
`attribute`, `custommodeldata`, `flags`, `info`, `import`, `storage`, `serveritem`.

Permissions: `zn.itemedit.admin` (operators); the legacy `zellysnexus.itemedit` node
grants it.
Storage: `items.yml`.

## tab

Route `/zn tab` (alias `t`); menu order 80; enabled by default.

- Renders the tab-list header and footer, sets the player list name, and shows a boss bar
  on join whose color, overlay, and duration come from the tab settings.
- Per-player toggle, info, and a reload of the tab list for every online player.

Commands: `menu`, `info`, `reload`, `toggle`.

Permissions: `menu`, `info`, and `toggle` require no permission; `reload` requires
`zn.admin.reload` (operators).
Storage: none.

## integrations

Route `/zn integrations` (alias `int`); menu order 90; enabled by default.

- Reports whether known plugins were found at boot: PlaceholderAPI, LuckPerms,
  Geyser-Spigot, Floodgate, and BlockProt or BlockProtReloaded.
- Looks up the LuckPerms primary group and prefix of a player, and reports whether a
  player joined through Floodgate.

Commands: `menu`, `perms <player>`, `bedrock <player>`.

Permissions: `zn.admin.integrations` (operators).
Storage: none; no module settings file is shipped for this module.

## updater

No command route; the module has no user-facing commands. Enabled by default but loads
only when `updater.check-on-boot` is true.

Asynchronously checks the GitHub repository for a newer tag on boot and logs one of
three translated messages: update available (with version and URL), up to date, or check
failed.

## debug

Route `/zn debug` (alias `dbg`); menu order 100; disabled by default (enable with
`modules.debug.enabled` and restart).

- Runs self-tests of one area or of all areas and reports pass/fail lines with a summary;
  each area has a 10-second timeout.
- The 16 areas are: environment, configuration, translation, persistence, storage,
  listeners, commands_permissions, user_interface, utilities, player_simulation, auth,
  clans, files, toolkit, threads, and world.
- Writes a dated report to the plugin data folder under `debug/`.

Commands: `/zn debug [area]`, `/zn debug menu`.

Permissions: `zn.debug` (operators).
Storage: `debug/debug-<date>.log`.
