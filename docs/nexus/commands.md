# Commands

Every feature of Zelly's Nexus is reached through one root command, `/zn <module> <action>`.
Each module also has a short alias. `/zn user` opens the player hub, `/zn admin` opens the
admin hub (tier t1 and above), and `/zn recommended` applies the recommended setup.
Every screen is a Paper dialog (chest inventory menus no longer exist) and Bedrock players get Floodgate forms when Floodgate is installed. Without dialogs, every function stays available through its own command.
`/zn help` lists the modules the sender can use.

| Module | Route | Alias |
|---|---|---|
| Core / Config | `/zn config` | `cfg` |
| Core / Admin | `/zn admin` | |
| Auth | `/zn auth` | `a` |
| Antibot | `/zn antibot` | `ab` |
| Ban | `/zn ban` | `b` |
| Toolkit (teleportation, player, server, moderation, kits, items) | `/zn toolkit` | `tools` |
| Chat | `/zn chat` | `c` |
| Inventory | `/zn inventory` | `inv` |
| Clans | `/zn clans` | `clan` |
| ItemEdit | `/zn itemedit` | `ie` |
| Join | `/zn join` | `j` |
| Tab | `/zn tab` | `t` |
| Integrations | `/zn integrations` | `int` |
| Updater | `/zn updater` | `up` |
| Debug | `/zn debug` | `dbg` |

A module appears only when `enabled: true` in its own
`modules/<module>/config.yml`. Every module starts disabled; a disabled module still
registers its commands and answers with a message that names it and shows both ways out
(edit its folder or run `/zn recommended <module>`).

Angle brackets mark a required argument and square brackets mark an optional one.

## Root aliases

Most actions can also be run as a direct root command, for example `/spawn` instead of
`/zn toolkit spawn`. These aliases are optional and are controlled in `config.yml`:

- `commands.register-root-aliases` turns every optional root alias on or off. The default
  is `true`.
- `commands.disabled-root-aliases` lists root command names that are never registered. The
  default list is `kill`, `kick`, `time`, `weather`, `msg` and `gamemode`. These names
  collide with vanilla commands, so the vanilla versions keep working. Remove a name from
  the list to let Zelly's Nexus replace the vanilla command. The `/zn` route is unaffected
  and always works.

`/zn` is always registered. `/auth`, `/zantibot`, `/clan`, `/inventory` and `/itemedit`
are registered whenever their module is enabled, whatever these two settings say. Root
aliases follow the same permission, console and login rules as the `/zn` route.

## Permissions

Every table lists the node and its default. "Everyone" means the node is granted to all
players by default and "Operators" means it is granted to operators only.

Teleportation, Player, Server, Moderation, Kits and Items actions use the node
`zn.<domain>.<action>`, where the domain is `teleport`, `player`, `server`, `moderation`,
`kit` or `items`. The following nodes are also accepted for these actions:

- `zn.admin` and `zn.toolkit.admin` grant every action of these domains.
- `zn.toolkit.<action>` grants a single action, for example `zn.toolkit.heal`.
- `zn.toolkit.mod` is accepted for `socialspy` and for the moderation actions `kick`,
  `kickall`, `kill`, `mute`, `unmute`, `jail`, `unjail`, `togglejail`, `jails`,
  `jailedplayers`, `burn`, `extinguish`, `lightning` and `whois`.
- `zn.moderation.mute` is also accepted for `unmute`, and `zn.moderation.jail` for
  `unjail`, `togglejail`, `jails` and `jailedplayers`.
- `zn.teleport.home` is also accepted for `sethome`, `delhome`, `homes` and `renamehome`;
  `zn.teleport.warp` for `warps` and `warpinfo`; `zn.teleport.tpa` for `tpahere`,
  `tpaccept`, `tpdeny`, `tpacancel` and `tptoggle`; and `zn.teleport.rtp` or
  `zn.toolkit.rtp` for `tpr`.

Other legacy nodes: `zellysnexus.itemedit` grants `zn.itemedit.admin`, and `zn.antibot`
grants `zn.antibot.admin`.

`zn.admin` is also checked by `/zn reload` and by the administrative Clans actions. The
plugin does not declare it, so it is held by operators and by anyone it is granted to
explicitly.

### Admin tiers

With `admin_tiers.enabled: false` (the default) `zn.admin` grants every admin capability.
With it set to `true`, the admin chain is `zn.admin.t1` (everyday moderation),
`zn.admin.t2` (actions on other players and their items), `zn.admin.t3` (world and server
settings) and `zn.admin.owner` (reload, stop and restart, recommended, permissions and
integrations). Each tier also satisfies the lower ones. `zn.admin.custom` is opt-in for
granular action nodes. Every click re-checks its node at click time in the inventory, the
dialog and the Bedrock form; the admin hub lists only what the viewer's tier allows.

## Console

The Console column states whether the console can run the command. "Yes (target required)"
means the console must name a target player. Commands marked "No" must be run by a player.

## Login gate

When the Auth module is enabled, a player who has not logged in is gated. Movement, block
breaking and placing, interaction, chat, item drops and pickups, damage and inventory
clicks are blocked. The only commands that work are `/zn`, `/zn menu`, `/zn help`,
`/zn auth` (and `/zn a`) and the Auth root aliases that are registered; `/zn` and
`/zn menu` open the login form instead of the menu, or show the login message when dialogs
are off. Every other command is cancelled and the player is asked to log in. Inside
`/zn auth`, only `login`, `register`, `captcha`, `form` and `menu` work before login.
`/zn antibot` is not open before login.

If the Auth module is enabled but fails to load, no player can join: every join is refused
with a translated message until the module loads again after a restart.

The arguments of `/login`, `/l`, `/register`, `/reg`, `/changepassword`, `/changepw`,
`/email`, `/pin` and `/totp`, and of the `login`, `register`, `changepassword`,
`unregister`, `email`, `pin`, `totp` and `otp` actions of `/auth` and `/zn auth`, are
replaced with `***` in the server log.

## Core

These commands belong to the root command and are always available.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/zn` | `[menu]` | Opens the player hub. | none | Everyone | Yes (module list) |
| `/zn user` | none | Opens the player hub in every renderer. | none | Everyone | No |
| `/zn admin` | none | Opens the admin hub with the sections the viewer's tier allows. | `zn.admin` | Operators | No |
| `/zn menu` | none | Opens the player hub. The renderer is always the dialog. | none | Everyone | No |
| `/zn recommended` | `<all\|config\|modules\|<module>> [force]` or `undo <same targets>` | Applies or undoes the recommended values. `all` is `config` plus `modules`; a module name applies only that module. A second run without `force` does nothing and says so. | `zn.admin.owner` | Operators | Yes |
| `/zn help` | none | Lists the modules the sender can use. | none | Everyone | Yes |
| `/zn reload` | none | Reloads `config.yml`. Language and renderer changes apply at once; a module switch needs a restart. | `zn.admin` | Operators | Yes |

## Auth

Route: `/zn auth` (alias `a`). All Auth commands are player-only. The module permission is
`zn.auth.player`, which everyone holds by default. Administrative actions also need
`zn.auth.admin`, which operators hold by default. Before login only `login`, `register`,
`captcha`, `form` and `menu` work. The root aliases `/auth`, `/login`, `/l`, `/register`,
`/reg`, `/changepassword`, `/changepw`, `/logout`, `/pin`, `/totp` and `/email` run the
matching action; only `/auth` is always registered.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/auth` | `[action]` | Opens the Auth menu, or runs an action below. | `zn.auth.player` | Everyone | No |
| `/register`, `/reg` | `<password>` | Registers an account. | `zn.auth.player` | Everyone | No |
| `/login`, `/l` | `<password>` | Logs in. | `zn.auth.player` | Everyone | No |
| `/logout` | none | Logs out of the current session. | `zn.auth.player` | Everyone | No |
| none | `<password>` | Unregisters the account. | `zn.auth.player` | Everyone | No |
| `/changepassword`, `/changepw` | `<old> <new>` | Changes the password. | `zn.auth.player` | Everyone | No |
| `/email` | `add <email>`, `change <email>`, `recover`, `recover <code> <newPassword>` | Manages the recovery email; `recover` issues a code, then resets the password with it. | `zn.auth.player` | Everyone | No |
| `/totp` | `setup`, `confirm <code>`, `disable` | Manages two-factor codes. | `zn.auth.player` | Everyone | No |
| none | `generate`, `verify <code>` | Generates and verifies a one-time code. | `zn.auth.player` | Everyone | No |
| `/pin` | `set <pin>`, `verify <pin>`, `reset` | Manages the secondary PIN. | `zn.auth.player` | Everyone | No |
| none | `<on\|off>` | Turns remembering the session on or off. | `zn.auth.player` | Everyone | No |
| none | `[answer]` | Issues a captcha challenge, or answers it. | `zn.auth.player` | Everyone | No |
| none | `[code]` | Issues a verification code, or confirms it. | `zn.auth.player` | Everyone | No |
| none | none | Opens the login and register form when dialogs are enabled. | `zn.auth.player` | Everyone | No |
| none | none | Opens the Auth menu. | `zn.auth.player` | Everyone | No |
| none | `<player>` | Deletes the account of an online player. | `zn.auth.admin` | Operators | No |
| none | `<player>` | Marks an online player as premium. | `zn.auth.admin` | Operators | No |
| none | `<player>` | Marks an online player as cracked. | `zn.auth.admin` | Operators | No |
| none | `<player>` | Marks an online player as freemium. | `zn.auth.admin` | Operators | No |
| none | `<player>` | Shows the authentication log of an online player. | `zn.auth.admin` | Operators | No |
| none | `reload`, `purge [days]`, `forcelogin <player>` | Reloads auth data, purges inactive accounts (30 days by default) or logs an online player in. | `zn.auth.admin` | Operators | No |
| none | `[action]` | Runs an Antibot action; requires the Antibot permission. | `zn.antibot.admin` | Operators | No |

## Antibot

Route: `/zn antibot` (alias `ab`). Root aliases: `/zantibot` is always registered and
`/antibot` is optional. Permission: `zn.antibot.admin`, held by operators by default;
`zn.antibot` grants it. The commands work from the console and are not available before
login.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/zantibot`, `/antibot` | `[action]` | Opens the Antibot menu for players, or prints the usage. | `zn.antibot.admin` | Operators | Yes |
| none | none | Opens the Antibot menu. | `zn.antibot.admin` | Operators | Yes |
| none | none | Shows the connection rate, blocked count and panic state. | `zn.antibot.admin` | Operators | Yes |
| none | `<on\|off>` | Turns panic mode on or off; panic mode blocks every new connection. | `zn.antibot.admin` | Operators | Yes |
| none | none | Lists the blocked addresses. | `zn.antibot.admin` | Operators | Yes |
| none | `<address>` | Adds an address to the block list. | `zn.antibot.admin` | Operators | Yes |
| none | `<address>` | Removes an address from the block list. | `zn.antibot.admin` | Operators | Yes |

## Toolkit

The toolkit groups six command domains: Teleportation, Player, Server, Moderation, Kits
and Items. Every action is run as `/zn toolkit <action>`, and most are also available as
an optional root alias with the same name.

### Teleportation

Every command is also available as an optional root alias with the same name, and `/rtp`
is an additional alias of `/tpr`. The nodes `zn.teleport.sethome`, `zn.teleport.delhome`,
`zn.teleport.homes`, `zn.teleport.renamehome`, `zn.teleport.warps`, `zn.teleport.warpinfo`,
`zn.teleport.tpahere`, `zn.teleport.tpaccept`, `zn.teleport.tpdeny`, `zn.teleport.tpacancel`
and `zn.teleport.tptoggle` are declared for operators, but those actions are open to
everyone through `zn.teleport.home`, `zn.teleport.warp` and `zn.teleport.tpa`.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/spawn` | none | Teleports to the server spawn. | `zn.teleport.spawn` | Everyone | No |
| `/setspawn` | none | Sets the server spawn to the current position. | `zn.teleport.setspawn` | Operators | No |
| `/home` | `[name]` | Teleports to a home; the name defaults to `home`. | `zn.teleport.home` | Everyone | No |
| `/sethome` | `[name]` | Saves the current position as a home; the name defaults to `home`. | `zn.teleport.sethome` | Everyone | No |
| `/delhome` | `<name>` | Deletes a home. | `zn.teleport.delhome` | Everyone | No |
| `/homes` | none | Lists the saved homes. | `zn.teleport.homes` | Everyone | No |
| `/renamehome` | `<home> <newName>` | Renames a home. | `zn.teleport.renamehome` | Everyone | No |
| `/warp` | `[name]` | Teleports to a warp, or lists the warps when no name is given. | `zn.teleport.warp` | Everyone | No |
| `/setwarp` | `<name>` | Creates a warp at the current position. | `zn.teleport.setwarp` | Operators | No |
| `/delwarp` | `<name>` | Deletes a warp. | `zn.teleport.delwarp` | Operators | No |
| `/warps` | none | Lists the warps. | `zn.teleport.warps` | Everyone | Yes |
| `/warpinfo` | `<name>` | Shows the coordinates and world of a warp. | `zn.teleport.warpinfo` | Everyone | Yes |
| `/tpa` | `<player>` | Sends a teleport request to a player. | `zn.teleport.tpa` | Everyone | No |
| `/tpahere` | `<player>` | Asks a player to teleport to you. | `zn.teleport.tpahere` | Everyone | No |
| `/tpaccept` | none | Accepts the pending teleport request. | `zn.teleport.tpaccept` | Everyone | No |
| `/tpdeny` | none | Denies the pending teleport request. | `zn.teleport.tpdeny` | Everyone | No |
| `/tpacancel` | none | Cancels the requests you sent. | `zn.teleport.tpacancel` | Everyone | No |
| `/tpaall` | none | Sends a teleport request to every online player that accepts requests. | `zn.teleport.tpaall` | Operators | No |
| `/tptoggle` | none | Toggles whether you receive teleport requests. | `zn.teleport.tptoggle` | Everyone | No |
| `/tpr`, `/rtp` | none | Teleports to a random location within the configured range. | `zn.teleport.tpr` | Operators | No |
| `/settpr` | `<min> <max>` | Sets the random teleport range until the next restart. The range is not saved; `rtp-min` and `rtp-max` in `modules/toolkit.yml` apply again on the next start. | `zn.teleport.settpr` | Operators | Yes |
| `/back` | none | Returns to the last saved location. | `zn.teleport.back` | Operators | No |
| `/top` | none | Teleports to the highest block at the current position. | `zn.teleport.top` | Operators | No |
| `/bottom` | none | Teleports to the bottom of the world at the current position. | `zn.teleport.bottom` | Operators | No |
| `/jump` | none | Teleports to the block you are looking at, up to 32 blocks away. | `zn.teleport.jump` | Operators | No |
| `/tpo` | `<player>` | Teleports to a player without a request. | `zn.teleport.tpo` | Operators | No |
| `/tphere` | `<player>` | Teleports a player to you. | `zn.teleport.tphere` | Operators | No |
| `/tpall` | none | Teleports every online player to you. | `zn.teleport.tpall` | Operators | No |
| `/tppos` | `<x> <y> <z>` | Teleports to coordinates in the current world. | `zn.teleport.tppos` | Operators | No |
| `/tp` | `<player>` | Teleports you to an online player. | `zn.teleport.tp` | Operators | No |
| `/tpohere` | `<player>` | Teleports an online player to your location. | `zn.teleport.tpohere` | Operators | No |
| `/tpoffline` | `<player>` | Teleports you to the player's last logout location. Not implemented yet: the command currently only sends the confirmation message and does not move the player. | `zn.teleport.tpoffline` | Operators | No |
| `/tpauto` | none | Toggles automatic acceptance of your teleport requests. | `zn.teleport.tpauto` | Operators | No |
| `/world` | `<world>` | Teleports you to the spawn of a world. | `zn.teleport.world` | Operators | No |

### Player

Every command is also available as an optional root alias with the same name. Additional
aliases: `/wb` for `/workbench`, `/ec` for `/enderchest` and `/r` for `/reply`. `/msg` and
`/gamemode` are in the default disabled list.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/heal` | `[player]` | Restores health to full. | `zn.player.heal` | Operators | Yes (target required) |
| `/feed` | `[player]` | Restores the food level to full. | `zn.player.feed` | Operators | Yes (target required) |
| `/fly` | `[player]` | Toggles flight. | `zn.player.fly` | Operators | Yes (target required) |
| `/god` | `[player]` | Toggles god mode. | `zn.player.god` | Operators | Yes (target required) |
| `/speed` | `<1-10> [player]` | Sets walk and fly speed. | `zn.player.speed` | Operators | Yes (target required) |
| `/workbench`, `/wb` | none | Opens a crafting table. | `zn.player.workbench` | Operators | No |
| `/enderchest`, `/ec` | none | Opens your ender chest. | `zn.player.enderchest` | Operators | No |
| `/disposal` | none | Opens a disposal inventory. | `zn.player.disposal` | Operators | No |
| `/hat` | none | Places the held item on your head. | `zn.player.hat` | Operators | No |
| `/zn prank` | `[player] [level]` | Executes a prank on a player (levels 1-5, 5.5 or 6), or opens the prank menu. | `zn.player.prank` | Operators | Yes (with target) |
| `/ping` | `[player]` | Shows the latency of a player. | `zn.player.ping` | Everyone | Yes (target required) |
| `/near` | none | Lists players within the configured radius. | `zn.player.near` | Everyone | No |
| `/msg` | `<player> <text>` | Sends a private message. | `zn.player.msg` | Everyone | Yes |
| `/reply`, `/r` | `<text>` | Replies to the last private message. | `zn.player.reply` | Everyone | No |
| `/msgtoggle` | none | Toggles receiving private messages. | `zn.player.msgtoggle` | Everyone | No |
| `/socialspy` | none | Toggles viewing the private messages of others. | `zn.player.socialspy` | Operators | No |
| `/nick` | `[name]` | Sets the display name, or resets it when no name is given. | `zn.player.nick` | Everyone | No |
| `/realname` | `<nick>` | Shows the real name behind a nickname. | `zn.player.realname` | Everyone | Yes |
| `/suicide` | none | Kills yourself. | `zn.player.suicide` | Everyone | No |
| `/mail` | `read \| clear \| send <player> <text>` | Reads or clears your mail, or sends mail to an online player. | `zn.player.mail` | Everyone | Yes (send only) |
| `/getpos` | none | Shows your coordinates and world. | `zn.player.getpos` | Everyone | No |
| `/seen` | `<player>` | Shows how long ago a player was last online. | `zn.player.seen` | Everyone | Yes |
| `/helpop` | `<text>` | Sends a message to online staff. | `zn.player.helpop` | Everyone | Yes |
| `/more` | none | Fills the held stack to its maximum size. | `zn.player.more` | Operators | No |
| `/repair` | none | Restores the durability of the held item. | `zn.player.repair` | Operators | No |
| `/unlimited` | none | Toggles unlimited block placement. | `zn.player.unlimited` | Operators | No |
| `/gamemode` | `<survival\|creative\|adventure\|spectator> [player]` | Sets the game mode. | `zn.player.gamemode` | Operators | Yes (target required) |
| `/afk` | none | Toggles your AFK state. | `zn.player.afk` | Everyone | No |
| `/playtime` | `[player]` | Shows how long a player has played. | `zn.player.playtime` | Everyone | Yes (target required) |
| `/ptime` | `<day\|night\|reset>` | Sets your personal time (`day` is 1000 ticks and `night` is 13000). | `zn.player.ptime` | Operators | No |
| `/pweather` | `<clear\|rain\|reset>` | Sets your personal weather. | `zn.player.pweather` | Operators | No |

### Server

Every command is also available as an optional root alias with the same name. `/time` and
`/weather` are in the default disabled list.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/time` | `<day\|noon\|night\|midnight\|ticks> [world]` | Sets the world time. | `zn.server.time` | Operators | Yes |
| `/weather` | `<clear\|rain\|thunder> [world]` | Sets the weather. | `zn.server.weather` | Operators | Yes |
| `/thunder` | `[world]` | Toggles thunder. | `zn.server.thunder` | Operators | Yes |
| `/broadcast` | `<text>` | Broadcasts a message to all players. | `zn.server.broadcast` | Operators | Yes |
| `/motd` | none | Shows the server message of the day. | `zn.server.motd` | Everyone | Yes |
| `/rules` | none | Shows the server rules. | `zn.server.rules` | Everyone | Yes |
| `/powertool` | `<command\|clear\|list\|toggle>` | Binds a command to the held item, clears the binding, lists the bindings or toggles powertools. | `zn.items.powertool` | Operators | No |
| `/gc` | none | Shows used and total memory and the server TPS. | `zn.server.gc` | Operators | Yes |

### Moderation

Every command is also available as an optional root alias with the same name, and `/ext`
is an additional alias of `/extinguish`. `/kill` and `/kick` are in the default disabled
list. See the Permissions overview for the legacy nodes accepted here. The ban, IP ban,
kick, suspend and unsuspend actions need the ban module: with `modules.ban.enabled:
false` they reply that it is disabled, and their screens and settings come from
`modules/ban.yml`.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/kick` | `<player> [reason]` | Kicks a player. | `zn.moderation.kick` | Operators | Yes |
| `/kickall` | none | Kicks every online player except the sender. | `zn.moderation.kickall` | Operators | Yes |
| `/kill` | `[player]` | Kills a player, or yourself. | `zn.moderation.kill` | Operators | Yes (target required) |
| `/vanish` | none | Toggles invisibility from other players. | `zn.moderation.vanish` | Operators | No |
| `/mute` | `<player>` | Mutes a player in chat. | `zn.moderation.mute` | Operators | Yes |
| `/unmute` | `<player>` | Unmutes a player. | `zn.moderation.unmute` | Operators | Yes |
| `/jail` | `<player> [jail]` | Jails a player in the named jail, or in the first defined jail. | `zn.moderation.jail` | Operators | Yes |
| `/togglejail` | `<player> [jail]` | Jails a player, or releases a player who is already jailed. | `zn.moderation.togglejail` | Operators | Yes |
| `/unjail` | `<player>` | Releases a jailed player. | `zn.moderation.unjail` | Operators | Yes |
| `/setjail` | `<name>` | Creates a jail at the current position. | `zn.moderation.setjail` | Operators | No |
| `/deljail` | `<name>` | Deletes a jail. | `zn.moderation.deljail` | Operators | Yes |
| `/jails` | none | Lists the jails. | `zn.moderation.jails` | Operators | Yes |
| `/jailedplayers` | none | Lists the jailed players. | `zn.moderation.jailedplayers` | Operators | Yes |
| `/sudo` | `<player> <command>` | Makes a player run a command. | `zn.moderation.sudo` | Operators | Yes |
| `/burn` | `<player>` | Sets a player on fire for the configured duration. | `zn.moderation.burn` | Operators | Yes |
| `/extinguish`, `/ext` | `[player]` | Extinguishes a player. | `zn.moderation.extinguish` | Operators | Yes (target required) |
| `/lightning` | `[player]` | Strikes lightning at a player, or at the block you are looking at. | `zn.moderation.lightning` | Operators | Yes (target required) |
| `/whois` | `[player]` | Shows the address, UUID and game mode of a player. | `zn.moderation.whois` | Operators | Yes (target required) |
| `/ban` | `<player> [reason]` | Permanently bans a player. | `zn.moderation.ban` | Operators | Yes |
| `/suspend` | `<player>` | Opens the interactive suspension dialog with reason and duration. | `zn.moderation.ban` | Operators | No |
| `/unsuspend` | `<player>` | Unsuspends a previously suspended player. | `zn.moderation.ban` | Operators | Yes |
| `/tempban` | `<player> <minutes> [reason]` | Bans a player for the given number of minutes. | `zn.moderation.tempban` | Operators | Yes |
| `/unban` | `<player>` | Lifts a player ban. | `zn.moderation.unban` | Operators | Yes |
| `/banip` | `<ip\|player> [reason]` | Permanently bans an IP address. | `zn.moderation.banip` | Operators | Yes |
| `/tempbanip` | `<ip\|player> <minutes> [reason]` | Bans an IP address for the given number of minutes. | `zn.moderation.tempbanip` | Operators | Yes |
| `/unbanip` | `<ip>` | Lifts an IP ban. | `zn.moderation.unbanip` | Operators | Yes |
| `/suspend` | `<player> [duration] [reason]` | Suspends a player; without a reason it opens the suspend dialog for online staff. | `zn.moderation.suspend` | Operators | Yes |
| `/unsuspend` | `<player>` | Lifts a suspension. | `zn.moderation.unsuspend` | Operators | Yes |
| `/nuke` | `[player]` | Spawns five primed TNT above the target, or above yourself. | `zn.moderation.nuke` | Operators | Yes (target required) |

### Kits

Every command is also available as an optional root alias with the same name.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/kit` | `[name]` | Gives a kit, or lists the kits when no name is given. | `zn.kit.kit` | Everyone | Yes (list only) |
| `/kits` | none | Lists the kits. | `zn.kit.kits` | Everyone | Yes |
| `/showkit` | `<name>` | Shows the item count of a kit. | `zn.kit.showkit` | Everyone | Yes |
| `/createkit` | `<name> [cooldownSeconds]` | Creates a kit from your inventory with an optional cooldown in seconds. | `zn.kit.createkit` | Operators | No |
| `/delkit` | `<name>` | Deletes a kit. | `zn.kit.delkit` | Operators | Yes |
| `/kitreset` | `<player> [kit]` | Resets the cooldown of one kit, or of every kit, for a player. | `zn.kit.kitreset` | Operators | Yes |

### Additional toolkit actions

The toolkit also registers the actions below, reached the same way
(`/zn toolkit <action>`). They follow the same permission scheme, so the node is
`zn.<domain>.<action>`.

| Action | Description | Permission | Default | Console |
|---|---|---|---|---|
| `compass` | Shows your bearing and facing direction. | `zn.player.compass` | Everyone | No |
| `customtext` | Prints the given text: customtext <text>. | `zn.player.customtext` | Operators | Yes |
| `depth` | Shows your depth relative to sea level. | `zn.player.depth` | Everyone | No |
| `exp` | Shows a player's level and total experience, and grants experience when an amount is given. | `zn.player.exp` | Operators | Yes |
| `gma` | Sets the game mode to adventure. | `zn.player.gma` | Operators | Yes |
| `gmc` | Sets the game mode to creative. | `zn.player.gmc` | Operators | Yes |
| `gmsp` | Sets the game mode to spectator. | `zn.player.gmsp` | Operators | Yes |
| `gms` | Sets the game mode to survival. | `zn.player.gms` | Operators | Yes |
| `help` | Lists the toolkit actions. | `zn.player.help` | Everyone | Yes |
| `ice` | Traps a player in ice. | `zn.player.ice` | Operators | No |
| `ignore` | Toggles ignoring an online player. | `zn.player.ignore` | Operators | No |
| `info` | Shows the online player count. | `zn.player.info` | Everyone | Yes |
| `list` | Lists the online players. | `zn.player.list` | Everyone | Yes |
| `me` | Broadcasts an emote message. | `zn.player.me` | Operators | Yes |
| `potion` | Applies a potion effect: potion <effect> [duration] [amplifier] [player]. | `zn.player.potion` | Operators | Yes |
| `rest` | Resets your time-since-rest statistic (the phantom timer). | `zn.player.rest` | Operators | No |
| `rtoggle` | Sets or clears a reply lock with a player; not applied yet. | `zn.player.rtoggle` | Operators | No |
| `rules` | Shows the server rules. | `zn.player.rules` | Operators | Yes |
| `antioch` | Spawns a primed TNT where you are looking, with the Holy Grail message. | `zn.server.antioch` | Operators | No |
| `backup` | Saves players and all worlds. | `zn.server.backup` | Operators | Yes |
| `beezooka` | Fires the Beezooka. | `zn.server.beezooka` | Operators | No |
| `bigtree` | Grows a big tree where you are looking. | `zn.server.bigtree` | Operators | No |
| `broadcastworld` | Sends a message to the players of one world: broadcastworld <world> <text>. | `zn.server.broadcastworld` | Operators | Yes |
| `fireball` | Launches a fireball. | `zn.server.fireball` | Operators | No |
| `firework` | Launches a firework. | `zn.server.firework` | Operators | No |
| `kittycannon` | Fires the kitty cannon. | `zn.server.kittycannon` | Operators | No |
| `spawnmob` | Spawns a mob (up to 50) at your position: spawnmob <mob> [amount]. | `zn.server.spawnmob` | Operators | No |
| `tree` | Grows a tree where you are looking; an optional argument chooses the tree type. | `zn.server.tree` | Operators | No |
| `removeentities` | Removes dropped items and mobs. | `zn.moderation.removeentities` | Operators | Yes |
| `anvil` | Opens an anvil. | `zn.items.anvil` | Operators | No |
| `book` | Unlocks a written book (restores its generation to original). | `zn.items.book` | Operators | No |
| `break` | Breaks the block you are looking at. | `zn.items.break` | Operators | No |
| `cartographytable` | Opens a cartography table. | `zn.items.cartographytable` | Operators | No |
| `clearinventory` | Clears the inventory of a player; defaults to yourself. | `zn.items.clearinventory` | Operators | Yes |
| `condense` | Condenses items into their block form. | `zn.items.condense` | Operators | No |
| `editsign` | Rewrites a line of the sign you are looking at: editsign <1-4> <text>. | `zn.items.editsign` | Operators | No |
| `give` | Gives items to an online player: give <player> <material> [amount]. | `zn.items.give` | Operators | Yes |
| `grindstone` | Opens a grindstone. | `zn.items.grindstone` | Operators | No |
| `item` | Gives an item by material name: item <material> [amount]. | `zn.items.item` | Operators | No |
| `itemdb` | Shows the material and amount of the item in your main hand. | `zn.items.itemdb` | Everyone | No |
| `itemlore` | Updates the lore of the held item. | `zn.items.itemlore` | Operators | No |
| `itemname` | Sets the name of the held item. | `zn.items.itemname` | Operators | No |
| `loom` | Opens a loom. | `zn.items.loom` | Operators | No |
| `powertoollist` | Lists the powertool bindings. | `zn.items.powertoollist` | Operators | No |
| `powertooltoggle` | Toggles powertools on or off. | `zn.items.powertooltoggle` | Operators | No |
| `recipe` | Shows the recipe header for the held item or a named material. Not implemented yet: only the header is sent. | `zn.items.recipe` | Everyone | No |
| `skull` | Gives you a player head of the target player, or of yourself. | `zn.items.skull` | Operators | No |
| `smithingtable` | Opens a smithing table. | `zn.items.smithingtable` | Operators | No |
| `spawner` | Changes the type of the spawner you are looking at: spawner <mob>. | `zn.items.spawner` | Operators | No |
| `stonecutter` | Opens a stonecutter. | `zn.items.stonecutter` | Operators | No |

## Clans

Route: `/zn clans` (alias `clan`). Root aliases: `/clan` is always registered and `/clans`
is optional. All Clans commands are player-only. The module permission is `zn.clans.player`,
held by everyone by default. Administrative actions also need `zn.admin`. Running the
command without an action opens the clan menu when dialogs are enabled.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/clan create` | `<name>` | Creates a clan. | `zn.clans.player` | Everyone | No |
| `/clan disband` | none | Disbands your clan. | `zn.clans.player` | Everyone | No |
| `/clan invite` | `<player>` | Invites an online player. | `zn.clans.player` | Everyone | No |
| `/clan accept` | none | Accepts a clan invitation. | `zn.clans.player` | Everyone | No |
| `/clan kick` | `<player>` | Removes a member. | `zn.clans.player` | Everyone | No |
| `/clan leave` | none | Leaves your clan. | `zn.clans.player` | Everyone | No |
| `/clan ally` | `<add\|remove> <clan>` | Adds or removes an alliance. | `zn.clans.player` | Everyone | No |
| `/clan rival` | `<add\|remove> <clan>` | Adds or removes a rivalry. | `zn.clans.player` | Everyone | No |
| `/clan war` | `<start\|end> <clan>` | Starts or ends a war. | `zn.clans.player` | Everyone | No |
| `/clan rank` | `create <rank> \| delete <rank> \| set <player> <rank> \| list` | Manages clan ranks. | `zn.clans.player` | Everyone | No |
| `/clan home` | none | Teleports to the clan home. | `zn.clans.player` | Everyone | No |
| `/clan home-set` | none | Sets the clan home at the current position. | `zn.clans.player` | Everyone | No |
| `/clan description` | `<text>` | Sets the clan description. | `zn.clans.player` | Everyone | No |
| `/clan verify` | `<clan>` | Marks a clan as verified. | `zn.clans.player` and `zn.admin` | Operators | No |
| `/clan ban` | `<player>` | Bans a player from clans. | `zn.clans.player` and `zn.admin` | Operators | No |
| `/clan unban` | `<player>` | Lifts a clan ban. | `zn.clans.player` and `zn.admin` | Operators | No |
| `/clan ff` | `<on\|off>` | Turns your personal friendly fire on or off. | `zn.clans.player` | Everyone | No |
| `/clan clanff` | `<on\|off>` | Turns friendly fire inside the clan on or off. | `zn.clans.player` | Everyone | No |
| `/clan globalff` | `<on\|off>` | Turns global friendly fire on or off. | `zn.clans.player` and `zn.admin` | Operators | No |
| `/clan bb` | `[text]` | Posts to the clan bulletin board, or shows it when no text is given. | `zn.clans.player` | Everyone | No |
| `/clan stats` | `<clan>` | Shows the statistics of a clan. | `zn.clans.player` | Everyone | No |
| `/clan roster` | `<clan>` | Shows the members of a clan. | `zn.clans.player` | Everyone | No |
| `/clan list` | none | Lists the clans. | `zn.clans.player` | Everyone | No |
| `/clan lookup` | `<player>` | Shows the clan of an online player. | `zn.clans.player` | Everyone | No |
| `/clan regroup` | none | Teleports online clan members to you. | `zn.clans.player` | Everyone | No |
| `/clan trust` | `<player>` | Trusts a player. | `zn.clans.player` | Everyone | No |
| `/clan untrust` | `<player>` | Removes the trust of a player. | `zn.clans.player` | Everyone | No |
| `/clan mute` | `<player>` | Mutes a clan member. | `zn.clans.player` | Everyone | No |
| `/clan setbanner` | `<banner>` | Sets the clan banner. | `zn.clans.player` | Everyone | No |
| `/clan kills` | none | Shows your clan kills. | `zn.clans.player` | Everyone | No |
| `/clan mostkilled` | none | Shows who your clan has killed most. | `zn.clans.player` | Everyone | No |
| `/clan coords` | none | Shows the coordinates of online clan members. | `zn.clans.player` | Everyone | No |
| `/clan vitals` | none | Shows the health and food of online clan members. | `zn.clans.player` | Everyone | No |
| `/clan rivalries` | none | Lists your clan rivals. | `zn.clans.player` | Everyone | No |
| `/clan profile` | `[clan]` | Shows the profile of a clan; defaults to your own. | `zn.clans.player` | Everyone | No |
| `/clan rename` | `<name>` | Renames your clan. | `zn.clans.player` | Everyone | No |
| `/clan locale` | `<locale>` | Sets the clan language. | `zn.clans.player` | Everyone | No |
| `/clan help` | none | Lists the clan subcommands. | `zn.clans.player` | Everyone | No |
| `/clan menu` | none | Opens the clan menu. | `zn.clans.player` | Everyone | No |

## Chat

Route: `/zn chat` (alias `c`). All Chat commands are player-only. The root aliases
`/shout`, `/chattoggle` and `/hidechat` are optional. While typing in chat, `[item]`,
`[inv]` and `[ender]` are replaced by the held item and by clickable inventory and ender
chest links.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| none | none | Opens the Chat menu when dialogs are enabled. | none | Everyone | No |
| `/shout` | `[on\|off]` | Toggles, or sets, chatting to the whole server instead of nearby players. | `zn.chat.shout` | Operators | No |
| `/chattoggle`, `/hidechat` | none | Toggles hiding chat messages for yourself. | none | Everyone | No |
| none | none | Clears the chat for every player. | `zn.chat.admin.clear` | Operators | No |
| none | `<player>` | Mutes a player in chat. | `zn.chat.admin.mute` | Operators | No |

## Inventory

Route: `/zn inventory` (alias `inv`). Root aliases: `/inventory` is always registered;
`/invsee`, `/endersee`, `/ecsee`, `/clearinventory`, `/ci` and `/invrollback` are optional.
All Inventory commands are player-only. The `/zn inventory` and `/inventory` routes need
`zn.inventory.see` to be entered, in addition to the node of the action. The optional root
aliases need only the node of their own action. All nodes are held by operators by default.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/inventory` | none | Opens the Inventory menu when dialogs are enabled. | `zn.inventory.see` | Operators | No |
| `/invsee` | `<player>` | Opens the inventory of an online player. | `zn.inventory.see` | Operators | No |
| `/endersee`, `/ecsee` | `<player>` | Opens the ender chest of an online player. | `zn.inventory.see` | Operators | No |
| `/clearinventory`, `/ci` | `[player]` | Clears the inventory of an online player; defaults to yourself. | `zn.inventory.clear` | Operators | No |
| none | `<player>` | Clears the ender chest of an online player. | `zn.inventory.clear` | Operators | No |
| none | `<source> <target>` | Copies the inventory of one online player to another. | `zn.inventory.clone` | Operators | No |
| none | `<source> <target>` | Copies the ender chest of one online player to another. | `zn.inventory.clone` | Operators | No |
| none | `<player> <material> [amount]` | Gives items to an online player. | `zn.inventory.give` | Operators | No |
| none | `<player> <material> [amount]` | Adds items to the ender chest of an online player. | `zn.inventory.give` | Operators | No |
| `/invrollback` | `[player]` | Restores the last death backup of the player. Without a player it opens the backup browser when dialogs are enabled, and restores the caller's own backup when dialogs are off. | `zn.inventory.rollback` | Operators | No |
| none | none | Discards the death backups of players who are offline. | `zn.inventory.admin` | Operators | No |

## ItemEdit

Route: `/zn itemedit` (alias `ie`). Root aliases: `/itemedit` is always registered; `/ie`,
`/rename` and `/lore` are optional. All ItemEdit commands are player-only and need
`zn.itemedit.admin`, held by operators by default; the legacy node `zellysnexus.itemedit`
grants it. Most actions edit the item in the main hand.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| `/itemedit`, `/ie` | none | Opens the item editor when dialogs are enabled. Running `/zn itemedit` without an action does the same. | `zn.itemedit.admin` | Operators | No |
| `/rename` | `<name>` | Renames the held item. | `zn.itemedit.admin` | Operators | No |
| `/lore` | `add <text> \| set <line> <text> \| clear` | Adds, replaces or clears lore lines; line numbers start at 0 and the line limit is configurable. | `zn.itemedit.admin` | Operators | No |
| none | `<enchantment> <level>` | Adds an enchantment to the held item. | `zn.itemedit.admin` | Operators | No |
| none | `[true\|false]` | Toggles, or sets, the unbreakable flag. | `zn.itemedit.admin` | Operators | No |
| none | `add <attribute> <amount> [slot] [operation] \| remove <attribute>` | Adds or removes an attribute modifier. | `zn.itemedit.admin` | Operators | No |
| none | `<number>` | Sets the custom model data. | `zn.itemedit.admin` | Operators | No |
| none | `add <flag> \| remove <flag> \| clear` | Adds, removes or clears item flags. | `zn.itemedit.admin` | Operators | No |
| none | none | Shows the type, model data, flags and enchantments of the held item. | `zn.itemedit.admin` | Operators | No |
| none | `<data>` | Adds an item from its Base64-encoded form to your inventory. | `zn.itemedit.admin` | Operators | No |
| none | `list \| save <key> \| get <key> \| delete <key>` | Saves the held item under a key, gives a saved item, deletes it or lists the keys. | `zn.itemedit.admin` | Operators | No |
| none | `create <key> \| give <key> [player] [amount]` | Saves the held item as a server item, or gives a server item to yourself or another online player. | `zn.itemedit.admin` | Operators | No |

## Tab

Route: `/zn tab` (alias `t`). No root aliases exist for this module. All Tab commands are
player-only.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| none | none | Opens the Tab menu when dialogs are enabled. Running `/zn tab` without an action does the same. | none | Everyone | No |
| none | none | Shows the number of teams and online players. | none | Everyone | No |
| none | none | Reloads the tab list for every online player. | `zn.admin.reload` | Operators | No |
| none | none | Toggles the custom tab list for yourself. | none | Everyone | No |

## Integrations

Route: `/zn integrations` (alias `int`). No root aliases exist for this module. All
Integrations commands are player-only and need `zn.admin.integrations`, held by operators
by default.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| none | none | Opens the Integrations menu when dialogs are enabled. Running `/zn integrations` without an action does the same. | `zn.admin.integrations` | Operators | No |
| none | `<player>` | Shows the LuckPerms primary group and prefix of an online player. | `zn.admin.integrations` | Operators | No |
| none | `<player>` | Reports whether an online player joined through Floodgate. | `zn.admin.integrations` | Operators | No |

## Debug

Route: `/zn debug` (alias `dbg`). The Debug module is disabled by default; enable it with
`modules.debug.enabled` in `config.yml` and restart the server. No root aliases exist for
this module. Each run saves a dated report under the plugin data folder.

| Command | Syntax | Description | Permission | Default | Console |
|---|---|---|---|---|---|
| none | `[area]` | Runs the self-tests of an area, or of every area when none is given. | `zn.debug` | Operators | Yes |
| none | none | Opens the diagnostics menu for players when dialogs are enabled. | `zn.debug` | Operators | Yes |
