# Comandos y permisos

BlockProt Reloaded registra un único comando raíz:

- `/blockprot`, con el alias `/bp`

Cuando `use_menus` está activado, los subcomandos adicionales de CLI se desactivan para
los jugadores: solo disponen de `/bp user`, más `/bp admin` cuando poseen algún permiso
de administración, mientras que la consola conserva acceso a todos los subcomandos. Los
comandos exclusivos para jugadores se indican más abajo; los comandos de administración
imprimen listados de texto cuando se ejecutan desde la consola.

## Comandos de menú

| Comando | Permiso | Descripción |
|---|---|---|
| `/bp user` | `blockprot.user` | Abre el menú de usuario (formulario de Bedrock, diálogo o menú de cofre). Solo jugadores |
| `/bp admin` | cualquier permiso de administración | Abre el menú de administración (formulario de Bedrock, diálogo o menú de cofre). Solo jugadores |

## Comandos de jugador

| Comando | Permiso | Descripción |
|---|---|---|
| `/bp help` | | Imprime el texto de ayuda; los administradores reciben el bloque de ayuda de administración |
| `/bp about` | `blockprot.user` | Versión del plugin, edición, autor, mantenedor y el rastreador de incidencias |
| `/bp settings` | `blockprot.user` | Ajustes personales: preferencias, sonidos e interruptores de avisos. Solo jugadores |
| `/bp friends [addall <player>]` | `blockprot.user` | Abre el menú de amigos por defecto, o añade a un jugador como amigo en todos los bloques que poseas |
| `/bp stats` | `blockprot.user` | Estadísticas de bloques protegidos y lista de ubicaciones. Solo jugadores |
| `/bp transferall <player>` | `blockprot.user` | Transfiere la propiedad de todos los bloques bloqueables que poseas a otro jugador. Solo jugadores |
| `/bp disablehints` | `blockprot.user` | Desactiva los mensajes de aviso de protección para ti. Solo jugadores |

## Comandos de administración

Con `admin_tiers.enabled: false` (el valor por defecto), `blockprot.user.admin` otorga
todos los comandos de administración. Con los niveles activados, cada comando requiere
su nivel mínimo o superior.

| Comando | Nivel mínimo | Descripción |
|---|---|---|
| `/bp info [player]` | T1 | Inspecciona todos los bloques que posee un jugador, esté conectado o no |
| `/bp logs [here\|player <player>] [page]` | T1 | Inspector del registro de auditoría de acceso con filtros y paginación (7 entradas por página) |
| `/bp unlock <player>` | T2 | Lista los bloques protegidos de un jugador; el clic derecho elimina la protección de un bloque |
| `/bp lockables` | T2 | Navegador interactivo de todos los materiales conocidos, con estado de bloqueable que se puede activar o desactivar. Solo jugadores |
| `/bp protdel [world] [confirm\|undo]` | T3 | Elimina en masa las protecciones de un mundo, con soporte de deshacer para el último lote borrado |
| `/bp debug <run\|placeDebugChest\|placeDebugShulker\|clearSearchHistory>` | T3 | Conjunto de diagnóstico y banco de pruebas manual |
| `/bp reload` | Owner | Crea una copia de seguridad y recarga configuraciones, bloques y traducciones |
| `/bp update` | Owner | Comprueba las versiones de GitHub en busca de actualizaciones |
| `/bp integrations` | Owner | Lista el estado de todas las integraciones de terceros |
| `/bp recommended <blocks\|config\|all\|undo> [force]` | Owner | Aplica o revierte la configuración inicial recomendada |
| `/bp tiers [setrole] <player> <role>` | Owner | Abre la interfaz de gestión de niveles, o establece el rol de un jugador (`owner`, `t3`, `t2`, `t1`, `custom`, `user`, `none`) |

## Permisos

| Nodo | Por defecto | Significado |
|---|---|---|
| `blockprot.user` | true | Funciones estándar de jugador: bloqueo, amigos, ajustes, estadísticas, transferencia, el menú de usuario |
| `blockprot.user.admin` | op | Todas las funciones de administración; también puede romper bloques protegidos que pertenecen a otros |
| `blockprot.user.admin.t1` | false | Nivel 1 Moderador: comandos de inspección, teletransporte desde estadísticas, registros de auditoría |
| `blockprot.user.admin.t2` | false | Nivel 2 Ayudante: desbloqueo, romper bloques protegidos, bypass de contenedores, navegador de bloqueables |
| `blockprot.user.admin.t3` | false | Nivel 3 Admin: eliminación de protecciones de un mundo, editor de configuración, diagnóstico |
| `blockprot.user.admin.owner` | op | Nivel 4 Owner: control total, recarga, actualización, perfiles recomendados, asignación de roles |
| `blockprot.user.admin.custom` | false | Rol de personal personalizado con permisos de acción granulares desde `admins.yml` |
| `blockprot.lockmax` | false | Exime al jugador del límite de bloques bloqueados |
| `blockprot.locklimit.<N>` | false | Sustituye el límite de bloques bloqueados por un número concreto; prevalece el valor concedido más alto |
| `blockprot.blocks.tp` | op | Teletransporta a un bloque protegido desde la vista de estadísticas |
| `blockprot.debug` | op | Ejecuta el diagnóstico mediante `/bp debug` |

## Niveles de personal

La jerarquía de personal de cuatro niveles es opcional mediante `admin_tiers.enabled`.
Cada acción de administración requiere un nivel mínimo:

| Acción | Nivel mínimo |
|---|---|
| INFO, TELEPORT, LOGS | T1 |
| BREAK, UNLOCK, LOCKABLES, CONTAINER_BYPASS | T2 |
| PROTDEL, CONFIG, DEBUG | T3 |
| RELOAD, UPDATE, INTEGRATIONS, RECOMMENDED, SETROLE | Owner |

Reglas de resolución: `blockprot.user.admin` está limitado a T2 cuando los niveles están
activados; los operadores del servidor se resuelven como Owner; la consola omite todas
las comprobaciones; los administradores personalizados usan el nodo granular
`blockprot.user.admin.action.<name>`; las asignaciones de nivel persisten en
`admins.yml`; y la entrada `/bp admin` aparece para cualquiera que posea algún permiso
de administración.
