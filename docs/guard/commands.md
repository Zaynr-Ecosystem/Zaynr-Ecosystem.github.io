# Commands

All Zelly's Guard operations run under a single root command:

- `/zg`, with aliases `/guard` and `/zguard`

With no arguments, a player opens the user protection hub; the console receives a usage
line. Unknown subcommands return a translated error, player-only subcommands are blocked
from the console, and tab completion only suggests subcommands the sender is allowed
to use.

## Command reference

| Command | Aliases | Permission | Player only | Description |
|---|---|---|---|---|
| `/zg user` | | `zguard.user` | yes | Opens the player hub in the configured renderer |
| `/zg admin` | | `zguard.admin.t1` | yes | Opens the admin hub with the sections the viewer's tier allows |
| `/zg config` | `cfg` | `zguard.admin.owner` | yes | Opens the interactive global and modular configuration editor |
| `/zg recommended` | | `zguard.admin.owner` | no | `<all\|config\|modules\|<module>> [force]` applies the recommended values; `undo <target>` restores them |
| `/zg help` | | `zguard.user` | no | Lists every subcommand the sender can use |
| `/zg reload` | | `zguard.admin.owner` | no | Reloads configuration and translations, reporting the elapsed time |
| `/zg about` | | `zguard.user` | no | About dialog for players when dialogs are on; otherwise version and tagline lines |
| `/zg info` | | `zguard.user` | no | Version, tagline, and platform lines |
| `/zg settings` | | `zguard.user` | yes | Opens the personal settings dialog |
| `/zg prank` | | `zguard.admin.t1` | no | Opens the prank menu; `/zg prank <player> <level>` sends a prank |
| `/zg claim` | `/zg claims` | `zguard.user` | yes | Claim management: `abandon`, `trust <player>`, `untrust <player>`, `list` |
| `/zg region` | `/zg rg` | `zguard.user` | no | Region inspection: `info`, `list` |
| `/zg stone` | `/zg ps`, `/zg stones` | `zguard.user` | yes | `info` shows your protection stone limit |
| `/zg lock` | | `zguard.user` | yes | Reports the BlockProt Reloaded link status, or recommends installing it |
| `/zg pvp` | | `zguard.user` | yes | Toggles your personal PvP state |
| `/zg graves` | `/zg grave` | `zguard.user` | yes | Lists your stored grave coordinates |
| `/zg log` | `/zg logs` | `zguard.admin.t1` | no | Action logging: `inspect`, `lookup`, `rollback` |
| `/zg antixray` | `/zg xray` | `zguard.admin.t1` | no | Prints the mining suspicion report line |
| `/zg debug` | | `zguard.admin.t3` | no | Runs the diagnostics suite |

## Admin tiers

With `admin_tiers.enabled: false` (the default) `zguard.admin` grants every admin
capability. With it set to `true`, the chain is `zguard.admin.t1` (everyday moderation),
`zguard.admin.t2` (actions on other players and their items), `zguard.admin.t3` (world and
server settings) and `zguard.admin.owner` (reload, recommended, permissions and
integrations). Each tier also satisfies the lower ones; `zguard.admin.custom` is opt-in.
Every click re-checks its node at click time in the inventory, the dialog and the Bedrock
form.

## Command details

### `/zg claim`

Management always acts on the claim the player is standing in, matched by ownership.

- `abandon` - abandons the claim you are standing in.
- `trust <player>` - grants build trust to a player in that claim.
- `untrust <player>` - revokes that trust.
- `list` - lists all claims you own.

### `/zg region`

- `info` - shows the regions at your current location (requires being in game).
- `list` - lists regions you own; staff with `zguard.admin.t1` see all regions.

### `/zg prank`

- `/zg prank` - opens the prank menu.
- `/zg prank <player> <level>` - sends the prank text for a level to an online player.
  Accepted levels are `1` through `5`, `5.5` and `6`; `5.5` and `6` both send the
level 6 text.

### `/zg stone`

- `info` - shows your protection stone limit.

### `/zg log`

- `inspect`, `lookup`, `rollback` - block action logging commands. The logging pipeline
  and the rollback engine are still in development.

### `/zg debug`

- `/zg debug` - runs every diagnostic group.
- `/zg debug <group>` - runs a single group.
- `/zg debug run [group]` - runs all groups, or one group.

The diagnostics suite covers core, environment, configuration, localization, storage,
persistence, listeners, commands and permissions, the user interface, utilities, player
simulation, and one group per feature subsystem.

## Permissions

| Node | Default | Inherits |
|---|---|---|
| `zguard.user` | everyone | - |
| `zguard.admin.t1` | operators | `zguard.user` |
| `zguard.admin.t2` | operators | `zguard.admin.t1` |
| `zguard.admin.t3` | operators | `zguard.admin.t2` |
| `zguard.admin.owner` | operators | `zguard.admin.t3` |
| `zguard.admin.custom` | nobody | `zguard.user` |
| `zguard.bypass` | operators | `zguard.user` |

The admin tiers inherit downward: tier 2 includes tier 1, tier 3 includes tier 2, and the
owner tier includes tier 3. `zguard.bypass` skips region protection checks, protection
stone ownership checks, and the build/interact checks exposed to other plugins.
