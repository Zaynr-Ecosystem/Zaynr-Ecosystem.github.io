# Zelly's Nexus

The modular core of the ecosystem: one plugin for the everyday player services and staff
tooling of a Paper server, reached through a single root command, `/zn` (alias `/nexus`).

!!! note "About names and command routes"

    Everything in Zelly's Nexus runs under a single root command, `/zn`; the
    optional root shortcuts (`/spawn`, `/login`, and the rest) can be turned
    off in `config.yml`, and the `/zn` route always works. See
    [Commands](commands.md) for the details.

    Many module and function names may look similar to those of other plugins.
    This is because I could not find another way to call them, okay? They are
    not replicated or copied: they are similar names, but original, adapted to
    the plugin, because these plugins are meant to live in the ecosystem of a
    community server, both there and for public use (outside the server).

!!! info "Development status"
    Zelly's Nexus is under active development. Modules, commands and screens grow release
    by release, and the project name itself is not final.

## Purpose and philosophy

Zelly's Nexus exists to consolidate the services that a modern server would otherwise
assemble from a dozen separate plugins - authentication, a player and staff toolkit,
clans, chat channels, inventory tools, an item editor and the tab list - into one cohesive
core with a single namespace, a single configuration layout, and one consistent interface.

The design principles behind it:

- **Modular by construction.** Every feature is a module that can be enabled or disabled
  on its own, with its own settings file and its own lifecycle state in the boot report.
  Nothing is all-or-nothing.
- **One route, optional shortcuts.** Everything lives under `/zn <module> <action>`.
  Classic root commands such as `/spawn`, `/home` or `/login` are optional aliases that
  can be turned on or off, so the plugin can coexist with an existing command layout.
- **Modern interfaces first.** Menus are rendered as native Paper dialogs, with chat
  prompts and classic inventory menus as the fallback when dialogs are off. The dialog
  approach follows the same design direction used in BlockProt Reloaded, another project
  in this ecosystem.
- **Built for current Paper.** Java 25, Paper and Folia 26.x, with region-safe task
  routing for Folia servers. No support for older Minecraft versions or for Spigot.
- **Localized from the start.** English and Spanish ship inside the jar, with a safe
  English fallback for any missing key.

## Modules

Thirteen modules make up the plugin: `auth`, `antibot`, `toolkit`, `ban`, `join`,
`chat`, `inventory`, `clans`, `itemedit`, `tab`, `integrations`, `updater` and `debug`.
Every module except Debug is enabled by default.

The [Modules](modules.md) page describes what each one does, its commands, its permissions
and its storage.

## Interfaces

- **Dialogs.** With `dialogs: true` in `config.yml`, menus open as native Paper dialog
  screens: the module menu and per-module menus such as the clan menu or the item editor.
  With dialogs off, the flows fall back to chat prompts.
- **Login gate.** While the auth module is loaded, players who have not logged in cannot
  move, build, interact, chat, drop or pick up items, take damage, click inventories, or
  run any command except the auth entry points.
- **Bedrock players.** Geyser and Floodgate are detected, and the integrations module can
  report whether a player joined through Floodgate.

## Commands

Every command, its syntax, its permission node and its console behavior is listed on the
[Commands](commands.md) page. Running `/zn` or `/zn menu` opens the module menu; `/zn help`
lists the modules the sender can use.

## Configuration

Global settings live in `config.yml`; per-module settings live in `modules/<module>.yml`.
The [Configuration](configuration.md) page lists every key with its default and marks the
keys that are parsed but not applied yet.

## Integrations

At boot the plugin reports which known plugins it found: PlaceholderAPI, LuckPerms,
Geyser-Spigot, Floodgate, and BlockProt or BlockProtReloaded. A public API service,
`NexusApi`, is registered with the server, exposing the plugin version, the active
language, the dialog state, and the ability for other plugins to register custom menu
entries and subcommands.

## License

Zelly's Nexus is distributed under the PolyForm Noncommercial License 1.0.0, plus
project-specific additional terms: no commercial use, no closed derivatives, and forks
must stay linked to this repository or be removed. The full license text is linked on the
[About](../about.md) page.
