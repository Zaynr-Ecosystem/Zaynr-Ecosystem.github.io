# BlockProt Reloaded

BlockProt Reloaded is an advanced block and entity protection plugin for Minecraft Java
Edition servers running Bukkit-compatible software, primarily optimized for the Paper
server family. Players protect chests, furnaces, barrels, doors, trapdoors, item frames,
vehicles, and workstations through chest menus or native Paper Dialogs, without typing
commands.

It is a fork of [spnda/BlockProt](https://github.com/spnda/BlockProt) (GPL-3.0),
maintained as a solo project by Zar. Current release: 1.4.1-hotfix.2.

## Purpose and philosophy

BlockProt Reloaded exists because the best ideas come from the community that uses the
plugin; fragmentation into multiple forks helps nobody, and every improvement belongs in
one place, shared with everyone. The fork keeps the original NBT storage model and adds
the features described on this page.

Its scope is granular protection for containers, workstations, doors, signs, and
entities; access control through friend lists and friend permission levels; owner
notifications; world expiry and inactivity cleanup; an SQLite audit log; and
administrator diagnostic tools. Out of scope: standalone Fabric/Forge/NeoForge mods,
compilation against unstable APIs, overwriting user configuration on updates, hardcoded
player-facing text, and unsolicited refactors.

## How locking works

- Sneak and right-click any lockable block to open its lock menu: a lock or unlock
  toggle, redstone and hopper settings, friend management, a custom display name,
  ownership transfer, and (for workstation blocks) a locator for the linked villager.
- Blocks are locked automatically on placement by default; double chests merge their
  lock state, and the owner's friend list is copied to new locks.
- Friends can be added per block or as a default list for every block you own, with
  four permission levels: Basic (deposit and take), Operator (also block settings),
  Full Manager (also friend management), and Custom.
- The Custom level toggles individual abilities per friend: open container, deposit
  items, withdraw items, manage friends, open the settings menu, configure block
  settings, change the block name, inspect contents, view the audit log, and redstone
  access.
- A per-block access audit log records when friends open blocks or take, place, or are
  denied items, and owners can receive notifications for those events.
- Shulker boxes carry their protection data inside the dropped item, and locked blocks
  are protected from explosions, piston movement, and unwanted redstone and hopper
  interaction.
- Item frames, chest boats, storage minecarts, and hopper minecarts are protected with
  the same sneak and right-click interaction; frames mounted on locked containers link
  to the container automatically. Villagers whose job site points to a protected
  workstation inherit its protection.
- World expiry and inactivity cleanup remove stale protections, and world protection
  deletion can erase a world's protections with undo support.

## Interfaces

Three presentation engines, chosen automatically per player:

- **Chest inventory menus** - the classic screens, with click protection and pagination.
- **Native Paper Dialogs** (`use_dialogs: true`) - modal dialogs on Paper 1.21.7 or
  later, with a pastel palette; automatically disabled with a warning when the dialog
  API is unavailable.
- **Bedrock forms** - native touch-friendly forms for players joining through Geyser
  and Floodgate.

## Editions and platform

| Edition | Branch | Minecraft | Java |
|---|---|---|---|
| BlockProt Reloaded | `main` | 1.21.7 and newer | 21 |
| BlockProt Reloaded Legacy | `BlockProt-Reloaded-Legacy` | 1.20.5 to 1.21.6 | 21 |
| BlockProt Legacy | `BlockProt-Legacy` | 1.18.2 to 1.20.4 | 17 |

Legacy editions receive bug fixes and compatibility only, never new features; native
Paper Dialogs exist only in BlockProt Reloaded, and legacy editions use chest inventory
menus. Every edition keeps the plugin name `BlockProtReloaded`, so all editions share
one data folder and permission set. The full list of published builds, edition by
edition, is on the [Releases](../releases.md) page.

- Supported and tested: Paper, Purpur, and Folia (declared range 1.21.7 through 26.3).
- Recognized but not tested: Pufferfish, Leaf, Leaves, and Gale.
- Plain Spigot starts with an unsupported warning; plain CraftBukkit is refused.
- Hybrid server software (Mohist, Magma, CatServer, Arclight) is out of scope.

## Storage

File-based NBT on each protected block is the primary source of truth. Player
preferences and friend data live in the player's persistent data container. SQLite
stores the per-block audit log and the offline player cache, and an optional
MySQL/MariaDB index mirrors block locations and trust lists for large servers. Plugin
updates never overwrite existing administrator configuration files.

## Integrations

| Plugin | Behavior |
|---|---|
| WorldGuard | Evaluates region flags and the `allow-blockprot` custom flag |
| Towny | Respects town and plot boundaries; cleans unclaims; optional ruined-town bypass |
| Lands | Honors claim permissions and wilderness protection options |
| ClaimChunk | Restricts locking and container access to chunk owners |
| GriefPrevention | Honors claim ownership |
| Residence | Restricts locking and container interaction to residence owners |
| WorldEdit | Optional auto-lock for newly pasted structures |
| PlaceholderAPI | Exposes block counts and default friend placeholders |
| ViaVersion | Client protocol version detection |
| Geyser / Floodgate | Bedrock name resolution and native Bedrock forms |

Integrations are configured centrally in `integrations.yml`, and each one has an
`enabled` toggle. A developer API is published through JitPack with documented query
methods (`BlockProtAPI`) and five cancellable events for other plugins.

## License

Licensed under the GNU General Public License v3.0, based on BlockProt by spnda, with
the original copyright notices preserved as required by GPL v3.

## Reference

- [Commands and permissions](commands.md)
- [Configuration](configuration.md)
