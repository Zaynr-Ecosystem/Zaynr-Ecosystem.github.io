# Zelly's Guard

Zelly's Guard is a protection suite for modern Paper and Folia servers (Minecraft 26.x).
It covers regional protection, golden shovel claims, protection stones, block logging,
PvP control, death graves, anti-xray heuristics, and container-lock integration through
BlockProt Reloaded.

!!! note "About names and command routes"

    Everything in Zelly's Guard runs under a single root command, `/zg` (also
    reachable as `/guard` and `/zguard`); the plugin registers no separate
    top-level commands for its modules.

    Many module and function names may look similar to those of other plugins.
    This is because I could not find another way to call them, okay? They are
    not replicated or copied: they are similar names, but original, adapted to
    the plugin, because these plugins are meant to live in the ecosystem of a
    community server, both there and for public use (outside the server).

## Purpose and philosophy

Guard exists to replace the fragmented set of legacy protection plugins with a single
engine, without duplicating domains that a mature sibling project already owns. Its scope
is regional protection, claiming, block locking, logging, combat mechanics, and anti-xray;
economy, minigames, and chat features are deliberately out of scope.

Design principles:

- **Unified namespace.** Everything is reachable under one root command, `/zg`
  (aliases `/guard` and `/zguard`).
- **Modular subsystems.** Regions, claims, stones, locks, logging, PvP, graves, and
  anti-xray run as independent modules that a server admin enables or disables.
- **Native dialog interfaces.** Menus are rendered as native Paper dialogs on supported
  clients, with Bedrock forms through Floodgate.
- **Integrate, do not duplicate.** Container locking is delegated to BlockProt Reloaded;
  where that plugin is present, Guard detects the link on boot and synchronizes region
  build checks with its lock events. Guard also registers itself inside Zelly's Nexus
  menus when both plugins run together.
- **Folia-ready.** The plugin targets Folia's regionized threading model alongside
  regular Paper servers.

## Development status

!!! info "Development status"
    Zelly's Guard is under active development (0.1.0-alpha) for Paper and Folia 26.x on
    Java 25. Claims, protection stones, regions, the dialog interfaces, PvP toggling,
    graves, and the BlockProt Reloaded and Nexus links work today; combat mechanics,
    block logging storage and rollback, and anti-xray reports are still being built out.

## Claiming with the golden shovel

1. Right-click a block while holding a golden shovel to start a selection. The
   interaction itself is cancelled while the shovel is in use.
2. The first click stores the first corner and shows it; the second click completes the
   claim. A further click resets the session and starts a new selection.

Creation rules:

- Both corners must be in the same world.
- The claim expands automatically from the world minimum to the world maximum height.
- Each side must be at least 10 blocks long.
- Overlapping an existing region in the same world is rejected.

New claims are stored with a generated name (`claim|<player>|<x>_<z>`) and priority 5.
Corner feedback is a gold block highlight, cleared when you quit or stop holding a golden
shovel.

Claims are managed with `/zg claim` (`abandon`, `trust <player>`, `untrust <player>`,
`list`); management acts on the claim you are standing in, matched by ownership.

## Protection stones

Placing the configured stone block (`COAL_ORE` by default) creates a protected area
around it with priority 10. Overlapping another player's protected cuboid is rejected,
and each player can keep up to the configured number of stones (5 by default). The owner
of the stone, or a player with `zguard.bypass`, can break it to free the area; anyone
else is blocked.

## Region flags

- `build` - block placement and breaking
- `interact` - block interactions
- `pvp` - player-versus-player damage
- `lock` - answered for the BlockProt Reloaded container-lock interplay

Owners and members of a region may build; everyone else is denied with a translated
message.

## Integrations

- **Zelly's Nexus.** When both plugins run together, Guard registers a "Guard" menu entry
  (shield icon) in the Nexus menus that opens the Guard user hub.
- **BlockProt Reloaded.** Detected on boot, with the active link reported; Guard cancels
  BlockProt lock, access-menu, and auto-lock events when the claim interplay denies the
  action. `/zg lock` reports the link status or recommends installing BlockProt Reloaded
  when it is missing.
- **Boot report.** The boot sequence detects Zelly's Nexus, Floodgate, PlaceholderAPI,
  LuckPerms, and BlockProt Reloaded, and reports each one as found or not found.
- **Developer API.** A small API service exposes the plugin version, whether a module is
  enabled, opening the user hub, and build/interact checks for other plugins.

## Reference

- [Commands](commands.md)
- [Configuration](configuration.md)
