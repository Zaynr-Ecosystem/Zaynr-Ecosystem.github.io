# Commands and permissions

BlockProt Reloaded registers one root command:

- `/blockprot`, with alias `/bp`

When `use_menus` is enabled, the extra CLI subcommands are switched off for players:
they get only `/bp user`, plus `/bp admin` when they hold any admin permission, while
the console keeps access to every subcommand. Player-only commands are marked below;
admin commands print textual listings when run from the console.

## Menu commands

| Command | Permission | Description |
|---|---|---|
| `/bp user` | `blockprot.user` | Opens the user menu (Bedrock form, dialog, or chest menu). Player only |
| `/bp admin` | any admin permission | Opens the admin menu (Bedrock form, dialog, or chest menu). Player only |

## Player commands

| Command | Permission | Description |
|---|---|---|
| `/bp help` | | Prints the help text; admins get the admin help block |
| `/bp about` | `blockprot.user` | Plugin version, edition, author, maintainer, and the issue tracker |
| `/bp settings` | `blockprot.user` | Personal settings: preferences, sounds, and hint toggles. Player only |
| `/bp friends [addall <player>]` | `blockprot.user` | Opens the default friends menu, or adds a player as a friend on every block you own |
| `/bp stats` | `blockprot.user` | Protected-block statistics and location list. Player only |
| `/bp transferall <player>` | `blockprot.user` | Transfers ownership of every lockable block you own to another player. Player only |
| `/bp disablehints` | `blockprot.user` | Disables protection hint messages for yourself. Player only |

## Admin commands

With `admin_tiers.enabled: false` (the default), `blockprot.user.admin` grants all
admin commands. With tiers enabled, each command requires its minimum tier or higher.

| Command | Minimum tier | Description |
|---|---|---|
| `/bp info [player]` | T1 | Inspects all blocks owned by a player, online or offline |
| `/bp logs [here\|player <player>] [page]` | T1 | Access audit log inspector with filters and pagination (7 entries per page) |
| `/bp unlock <player>` | T2 | Lists a player's protected blocks; right-click removes a block's protection |
| `/bp lockables` | T2 | Interactive browser of all known materials with toggleable lockable status. Player only |
| `/bp protdel [world] [confirm\|undo]` | T3 | Bulk-deletes protections in a world, with undo support for the latest erase batch |
| `/bp debug <run\|placeDebugChest\|placeDebugShulker\|clearSearchHistory>` | T3 | Diagnostics suite and manual test bench |
| `/bp reload` | Owner | Creates a safety backup and reloads configs, blocks, and translations |
| `/bp update` | Owner | Checks GitHub releases for updates |
| `/bp integrations` | Owner | Lists the status of all third-party integrations |
| `/bp recommended <blocks\|config\|all\|undo> [force]` | Owner | Applies or reverts the recommended starting configuration |
| `/bp tiers [setrole] <player> <role>` | Owner | Opens the tier management UI, or sets a player's role (`owner`, `t3`, `t2`, `t1`, `custom`, `user`, `none`) |

## Permissions

| Node | Default | Meaning |
|---|---|---|
| `blockprot.user` | true | Standard player features: locking, friends, settings, statistics, transfer, the user menu |
| `blockprot.user.admin` | op | All admin features; can also break protected blocks owned by others |
| `blockprot.user.admin.t1` | false | Tier 1 Moderator: inspection commands, statistics teleport, audit logs |
| `blockprot.user.admin.t2` | false | Tier 2 Helper: unlock, break protected blocks, container bypass, lockables browser |
| `blockprot.user.admin.t3` | false | Tier 3 Admin: world protection deletion, config editor, diagnostics |
| `blockprot.user.admin.owner` | op | Tier 4 Owner: full control, reload, update, recommended profiles, role assignments |
| `blockprot.user.admin.custom` | false | Custom staff role with granular action permissions from `admins.yml` |
| `blockprot.lockmax` | false | Exempts the player from the locked-block cap |
| `blockprot.locklimit.<N>` | false | Overrides the locked-block cap with a specific number; the highest granted value wins |
| `blockprot.blocks.tp` | op | Teleports to a protected block from the statistics view |
| `blockprot.debug` | op | Runs diagnostics through `/bp debug` |

## Staff tiers

The four-tier staff hierarchy is opt-in through `admin_tiers.enabled`. Each admin
action requires a minimum tier:

| Action | Minimum tier |
|---|---|
| INFO, TELEPORT, LOGS | T1 |
| BREAK, UNLOCK, LOCKABLES, CONTAINER_BYPASS | T2 |
| PROTDEL, CONFIG, DEBUG | T3 |
| RELOAD, UPDATE, INTEGRATIONS, RECOMMENDED, SETROLE | Owner |

Resolution rules: `blockprot.user.admin` is capped at T2 when tiers are enabled; server
operators resolve as Owner; the console bypasses all checks; custom admins use the
granular node `blockprot.user.admin.action.<name>`; tier assignments persist in
`admins.yml`; and the `/bp admin` entry appears for anyone holding any admin permission.
