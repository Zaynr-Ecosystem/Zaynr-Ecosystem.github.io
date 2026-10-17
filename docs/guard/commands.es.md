# Comandos

Todas las operaciones de Zelly's Guard se ejecutan bajo un único comando raíz:

- `/zg`, con los alias `/guard` y `/zguard`

Sin argumentos, un jugador abre el centro de protección de usuario; la consola recibe una
línea de uso. Los subcomandos desconocidos devuelven un error traducido, los subcomandos
exclusivos de jugadores se bloquean desde la consola y el autocompletado solo sugiere los
subcomandos que el emisor tiene permitido usar.

## Referencia de comandos

| Comando | Alias | Permiso | Solo jugadores | Descripción |
|---|---|---|---|---|
| `/zg admin` | | `zguard.admin.t1` | sí | Abre el diálogo del centro de administración |
| `/zg help` | | `zguard.user` | no | Enumera todos los subcomandos que el emisor puede usar |
| `/zg reload` | | `zguard.admin.owner` | no | Recarga la configuración y las traducciones, informando del tiempo transcurrido |
| `/zg about` | | `zguard.user` | no | Diálogo de información para jugadores cuando los diálogos están activos; de lo contrario, líneas de versión y lema |
| `/zg info` | | `zguard.user` | no | Líneas de versión, lema y plataforma |
| `/zg settings` | | `zguard.user` | sí | Abre el diálogo de ajustes personales |
| `/zg prank` | | `zguard.admin.t1` | no | Abre el menú de bromas; `/zg prank <player> <level>` envía una broma |
| `/zg claim` | `/zg claims` | `zguard.user` | sí | Gestión de claims: `abandon`, `trust <player>`, `untrust <player>`, `list` |
| `/zg region` | `/zg rg` | `zguard.user` | no | Inspección de regiones: `info`, `list` |
| `/zg stone` | `/zg ps` | `zguard.user` | sí | `info` muestra tu límite de piedras de protección |
| `/zg lock` | | `zguard.user` | sí | Informa del estado del enlace con BlockProt Reloaded o recomienda instalarlo |
| `/zg pvp` | | `zguard.user` | sí | Alterna tu estado personal de PvP |
| `/zg graves` | `/zg grave` | `zguard.user` | sí | Enumera las coordenadas de tus tumbas almacenadas |
| `/zg log` | `/zg logs` | `zguard.admin.t1` | no | Registro de acciones: `inspect`, `lookup`, `rollback` |
| `/zg antixray` | `/zg xray` | `zguard.admin.t1` | no | Imprime la línea del informe de sospecha de minería |
| `/zg debug` | | `zguard.admin.t3` | no | Ejecuta la suite de diagnósticos |

## Detalles de los comandos

### `/zg claim`

La gestión siempre actúa sobre el claim en el que está de pie el jugador, emparejado por
propiedad.

- `abandon` - abandona el claim en el que estás de pie.
- `trust <player>` - concede permiso de construcción a un jugador en ese claim.
- `untrust <player>` - revoca ese permiso.
- `list` - enumera todos los claims que posees.

### `/zg region`

- `info` - muestra las regiones en tu ubicación actual (requiere estar en el juego).
- `list` - enumera las regiones que posees; el staff con `zguard.admin.t1` ve todas las regiones.

### `/zg prank`

- `/zg prank` - abre el menú de bromas.
- `/zg prank <player> <level>` - envía el texto de la broma de un nivel a un jugador en línea. Los niveles aceptados son del `1` al `5`, `5.5` y `6`; `5.5` y `6` envían el texto del nivel 6.

### `/zg stone`

- `info` - muestra tu límite de piedras de protección.

### `/zg log`

- `inspect`, `lookup`, `rollback` - comandos de registro de acciones sobre bloques. La
  canalización de registro y el motor de reversión siguen en desarrollo.

### `/zg debug`

- `/zg debug` - ejecuta todos los grupos de diagnóstico.
- `/zg debug <group>` - ejecuta un solo grupo.
- `/zg debug run [group]` - ejecuta todos los grupos, o un solo grupo.

La suite de diagnósticos cubre el núcleo, el entorno, la configuración, la localización, el
almacenamiento, la persistencia, los listeners, los comandos y permisos, la interfaz de
usuario, las utilidades, la simulación de jugadores y un grupo por cada subsistema de
funciones.

## Permisos

| Nodo | Por defecto | Hereda |
|---|---|---|
| `zguard.user` | todos | - |
| `zguard.admin.t1` | operadores | `zguard.user` |
| `zguard.admin.t2` | operadores | `zguard.admin.t1` |
| `zguard.admin.t3` | operadores | `zguard.admin.t2` |
| `zguard.admin.owner` | operadores | `zguard.admin.t3` |
| `zguard.admin.custom` | nadie | `zguard.user` |
| `zguard.bypass` | operadores | `zguard.user` |

Los niveles de administración heredan hacia abajo: el nivel 2 incluye el nivel 1, el nivel 3
incluye el nivel 2 y el nivel de propietario incluye el nivel 3. `zguard.bypass` omite las
comprobaciones de protección de regiones, las comprobaciones de propiedad de las piedras de
protección y las comprobaciones de construcción/interacción expuestas a otros plugins.
