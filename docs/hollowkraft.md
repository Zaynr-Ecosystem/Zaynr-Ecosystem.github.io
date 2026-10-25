# HollowKraft

<div class="hk4-banner-container" markdown="1">

![HollowKraft 4](assets/images/HK4.png){ .hk4-banner }

</div>

**HollowKraft (HK4)** is the next edition of the **Vasijas de Hallownest** community server, designed for **Minecraft 26.x**. The project is **planned and in active development**.

!!! info "Status: planned, in active development"
    HollowKraft is undergoing active technical development and stabilization. When a feature is undecided, no final choice has been made yet.

## What is HollowKraft?

HollowKraft is a long-term community survival server focused on exploration, building, and shared player experiences. It is not an anarchy server or a seasonal festival server.

## Planned at a Glance

| Area | Current Plan |
|---|---|
| Server | Community survival world, with continuous 24/7 operation planned. |
| Difficulty | Hard. |
| Capacity | Target capacity of 50+ concurrent players. |
| Worlds | Two worlds managed via Zelly's Guard: a PvP world (semi-peaceful, featuring harmless pranks) and a peaceful pure building world. |
| Clans | Full clan system powered by Zelly's Nexus. Configurable clan tags in chat and player list. |
| Chat & Social | Global cross-world chat, join/quit notices, custom advancement messages, and death messages. No paid ranks at launch. |
| Economy | Planned for post-launch with "Geo" currency (inspired by Hollow Knight), item shops, and interactive skill progression. |
| Client Mod (Java) | Optional (Fabric 26.3). 100% controlled via in-game graphical interface (`K` key) and main menu toggle. Never mandatory. |
| Resource Pack | Optional opt-in resource pack for Java; final visual content is currently under design. |

## Platform Support: Java and Bedrock

HollowKraft supports both Java Edition and Bedrock Edition players in the same world using **Geyser** and **Floodgate**. No client modifications are ever mandatory to connect and play.

### Java Edition

Java Edition provides the primary desktop experience and supports both unmodified vanilla clients and the optional custom client mod.

#### Capabilities on Java
- **Standard Vanilla Compatibility:** Players can connect with any standard Minecraft Java Edition client on version 26.x.
- **Native Paper Dialogs:** Clean, responsive dialog interfaces for server navigation, claim configuration, and profile management.
- **Chest Inventory Fallback:** Standard inventory GUIs are available for players who prefer classic chest-style menus (`/zg gui`, `/zn gui`).
- **Full Support for the HollowKraft Client Mod:**
    - Custom cinematic dark start screen with server branding.
    - Stylized dark main menu with instant toggle switch to the vanilla Minecraft menu.
    - Floating dark theme for server dialog windows.
    - Unified in-game control hub opened with the `K` key.
    - Smooth client animations including hotbar cursor glide, chat line fading, smooth mouse-wheel scrolling, and container slot glow.
    - Accessibility options including a master motion reduction switch.

#### Limitations on Java
- **Mod Installation Requirements:** The optional visual client mod requires the Fabric Loader and Fabric API on Java 26.3. It cannot run on default vanilla launchers without Fabric.
- **Client-Side Scope:** The mod is strictly client-side and is not installed on the server. Playing without the mod is fully supported, but vanilla Java players will experience default vanilla menus, standard Paper Dialogs, and standard Minecraft interface animations.
- **Hardware Dependencies:** Client-side visual smoothing and particle effects require sufficient local GPU and CPU resources.

---

### Bedrock Edition

Bedrock Edition players can join the server directly through Geyser and Floodgate cross-play.

#### Capabilities on Bedrock
- **Cross-Platform Connectivity:** Players on Windows Bedrock, mobile devices (iOS, Android), and consoles (Xbox, PlayStation, Nintendo Switch) can join the exact same server world.
- **Native Floodgate Forms:** Server dialogs and configuration screens are automatically converted into native Bedrock modal forms, simple lists, and custom input windows.
- **Complete Gameplay Parity:** Full participation in survival mechanics, cross-world chat, clan creation and management (`/zn clans`), land claiming (`/zg claim`), container locking (`/zg lock`), and pranks (`/zn prank`).
- **No Third-Party Installations Needed:** Players can connect using the official Bedrock client without installing any external software or sideloaded modifications.

#### Limitations on Bedrock
- **No Fabric Mod Compatibility:** The HollowKraft Fabric client mod cannot run on Bedrock Edition. Fabric is exclusive to the Java Edition platform.
- **No Custom Client Menus or Loading Screens:** The stylized Java main menu, custom title screen artwork, and dark startup overlay cannot be displayed on Bedrock clients.
- **Standard Bedrock Interface Only:** Client-side visual effects such as smooth hotbar sliding, animated chat fading, slot illumination, and the `K` key client hub are unavailable on Bedrock.
- **Form-Based Navigation:** Navigation on Bedrock uses standard Floodgate dialog forms and container menus rather than client-rendered custom GUI layers.

---

## HollowKraft Client Mod (Fabric 26.3)

For Java Edition players, an **optional client mod** provides aesthetic improvements and visual polish without altering core vanilla mechanics.

### 100% Controlled via Graphical Interface

The mod is designed to be managed **entirely through graphical interfaces in-game**, eliminating any need for memorizing client commands:

- **`K` Key (In-Game Control Hub):** Opens the unified interactive panel containing server shortcuts and client controls:
    - **Home:** Server connection status, welcome message, and quick summary.
    - **Clans:** Clan home, member roster, profile, and social statistics (`/zn clans`).
    - **Protection:** Claim land (`/zg claim`), lock containers (`/zg lock`), grave history (`/zg graves`), combat mode (`/zg pvp`), regions, and protection stones (`/zg stone`).
    - **Utilities:** Virtual workbench (`/craft`), enderchest, trash bin, portable anvil, kits, and prank menu (`/prank`).
    - **Administration:** Interactive configuration for Nexus and Guard, system diagnostics, audit logs, and sanction history.
    - **Mod Settings:** Real-time visual and animation preferences.
- **Menu Mode Toggle:** Instantly switches between the stylized Hollow Knight main menu and the vanilla Minecraft menu with a single click.

### Visual Settings and Animations

Inside the **Mod Settings** tab of the in-game panel, players can configure:

- **Custom Splash Screen:** Cinematic dark loading overlay featuring custom artwork.
- **Stylized Dialogs:** Replaces standard Paper Dialogs with dark Hollow Knight-themed floating windows.
- **Container Glow:** Subtle ambient illumination when interacting with chests and inventories.
- **Fluid Animations:** Smooth GUI window transitions, fading chat message lines, and sliding hotbar selection cursor.
- **Smooth Scrolling:** Fluid inertia-based scrolling across menus and lists.
- **Reduced Motion:** Accessibility option to disable camera shakes and abrupt screen shifts.
- **Reset to Defaults:** One-click master action to restore all visual settings to factory defaults.

### Full Option List (Settings Panel, Key `K`)

The panel uses a black, gray and white palette and has four tabs. Every value is edited from the panel; nothing requires editing a file.

| Tab | Option | Values |
|---|---|---|
| General | Menu style | Hollow Knight or vanilla |
| General | Custom menu | on or off |
| General | Start screen (image and title) | on or off |
| General | Alpha notice | on or off |
| General | Reduce motion | on or off |
| General | Respect other mods | on or off |
| General | Direct server | local or online |
| Animations | Master switch | on or off |
| Animations | Smooth hand swapping | on or off |
| Animations | Slot glow | on or off |
| Animations | Dark dialogs | on or off |
| Animations | Immersive overlays | on or off |
| Transitions | Screen animation | on or off |
| Transitions | Fluid hotbar | on or off |
| Transitions | Animated chat | on or off |
| Transitions | Smooth scroll | on or off |
| Speed | Screen displacement | 0, 5, 10, 15, 20 |
| Speed | Screen duration (ms) | 120, 220, 320, 450 |
| Speed | Hotbar speed | 12, 24, 36, 48 |
| Speed | Chat fade (ms) | 90, 180, 300, 450 |
| Speed | Scroll speed | 8, 16, 24, 32 |
| Speed | Hand swap speed | 9, 18, 27, 36 |

Clicking a speed card moves to the next value and wraps around at the end.

---

## Frequently Asked Questions

### Launch and Availability

**When does HK4 launch?**
There is no fixed public launch date yet. The server will open once systems are fully developed, tested, and verified.

**Will the server run 24/7?**
Yes, the operational plan is continuous 24/7 uptime, aside from scheduled maintenance windows.

**How many players can join?**
The target capacity is 50+ concurrent players.

**What hardware do I need?**
The server and client mod are optimized to run on standard everyday hardware, with no high-end requirements.

### Platforms and Cross-Play

**Can Bedrock players join the server?**
Yes. Through Geyser and Floodgate, Bedrock players on phones, consoles, and Windows can join seamlessly.

**Is the Fabric mod required to play on Java?**
No. The client mod is 100% optional. Players without the mod can play normally using standard Java clients with server-provided Paper Dialogs and chat commands.

**Can Bedrock players use the custom main menu from the mod?**
No. Fabric client mods are exclusive to Java Edition. Bedrock players experience the server through native Bedrock menus and Floodgate forms.

### Gameplay and Worlds

**Is HK4 an anarchy server?**
No. HK4 is a regulated community survival world, not an anarchy or griefing server.

**Will there be two distinct worlds?**
Yes. Two worlds are planned and managed via Zelly's Guard:
1. **PvP World:** Semi-peaceful survival with regulated PvP and the harmless prank system (`/zn prank`).
2. **Peaceful World:** Pure cooperative building with player-versus-player damage disabled.

**Can I move items between worlds?**
An economy-based toll system is under consideration for carrying items across worlds; without paying the toll, players would start fresh with a clean inventory in the other world.

**Are my buildings and chests protected?**
Yes. Land claims are protected by Zelly's Guard, while individual blocks and containers are locked through BlockProt Reloaded 1.4.2.

**What difficulty will the server use?**
The server runs on Hard difficulty.

### Clans, Chat, and Economy

**Will there be clans or teams?**
Yes, powered by Zelly's Nexus. Players can form clans, set clan bases, and display configurable clan tags in chat and the tablist.

**Is chat global across both worlds?**
Yes, global chat connects players across both worlds.

**Do death messages display coordinates?**
The server supports configurable death coordinates, but they remain disabled by default to protect base privacy.

**Will there be an economy and shops?**
The economy will not be active at initial launch. It will be enabled in a later phase featuring "Geo" currency (inspired by Hollow Knight), shops, and interactive skill progression.

**Will there be paid ranks?**
No ranks will be available at launch. Any future ranks will remain strictly cosmetic, with zero pay-to-win advantages.

### Client Mod and Previous Editions

**Does the mod require typing console commands?**
No. The HollowKraft mod is managed entirely through its in-game interface (`K` key) and the main menu. Everything is in the GUI.

**What previous editions existed?**
The community previously ran three editions: HollowKraft 1 on Aternos, HollowKraft 2 on Shockbyte, and HollowKraft 3 on HolyHosting. HollowKraft 4 represents the most advanced custom iteration.

## Related

HollowKraft builds upon the ecosystem projects documented on this site: [Zelly's Guard](guard/index.md), [Zelly's Nexus](nexus/index.md), and [BlockProt Reloaded](blockprot/index.md).
