# BlockProt Reloaded

BlockProt Reloaded es un plugin avanzado de protección de bloques y entidades para
servidores de Minecraft Java Edition que ejecutan software compatible con Bukkit,
optimizado principalmente para la familia de servidores Paper. Los jugadores protegen
cofres, hornos, barriles, puertas, trampillas, marcos de objetos, vehículos y mesas de
trabajo mediante menús de cofre o diálogos nativos de Paper, sin escribir comandos.

Es un fork de [spnda/BlockProt](https://github.com/spnda/BlockProt) (GPL-3.0),
mantenido en solitario por Zar. Versión actual: 1.4.1-hotfix.2.

## Propósito y filosofía

BlockProt Reloaded existe porque las mejores ideas vienen de la comunidad que usa el
plugin; la fragmentación en múltiples forks no ayuda a nadie, y cada mejora pertenece a
un solo lugar, compartida con todos. El fork conserva el modelo de almacenamiento NBT
original y añade las funciones descritas en esta página.

Su alcance es la protección granular de contenedores, mesas de trabajo, puertas,
carteles y entidades; el control de acceso mediante listas de amigos y niveles de
permiso de amigos; las notificaciones al propietario; la expiración por mundo y la
limpieza por inactividad; un registro de auditoría en SQLite; y herramientas de
diagnóstico para administradores. Fuera de alcance: mods independientes para
Fabric/Forge/NeoForge, compilación contra APIs inestables, sobrescribir la configuración
del usuario en las actualizaciones, texto para jugadores escrito directamente en el
código y refactorizaciones no solicitadas.

## Cómo funciona el bloqueo

- Agáchate y haz clic derecho sobre cualquier bloque bloqueable para abrir su menú de
  bloqueo: un interruptor de bloqueo o desbloqueo, ajustes de redstone y tolvas, gestión
  de amigos, un nombre visible personalizado, transferencia de propiedad y (para bloques
  de mesa de trabajo) un localizador del aldeano vinculado.
- Los bloques se bloquean automáticamente al colocarlos por defecto; los cofres dobles
  combinan su estado de bloqueo, y la lista de amigos del propietario se copia a los
  nuevos bloqueos.
- Los amigos se pueden añadir por bloque o como lista por defecto para todos los bloques
  que poseas, con cuatro niveles de permiso: Básico (depositar y retirar), Operador
  (también ajustes del bloque), Administrador total (también gestión de amigos) y
  Personalizado.
- El nivel Personalizado activa o desactiva habilidades individuales por amigo: abrir
  contenedor, depositar objetos, retirar objetos, gestionar amigos, abrir el menú de
  ajustes, configurar ajustes del bloque, cambiar el nombre del bloque, inspeccionar el
  contenido, ver el registro de auditoría y acceso a redstone.
- Un registro de auditoría de acceso por bloque registra cuándo los amigos abren bloques
  o toman, colocan o se les deniegan objetos, y los propietarios pueden recibir
  notificaciones de esos eventos.
- Las cajas de shulker llevan sus datos de protección dentro del objeto soltado, y los
  bloques bloqueados están protegidos contra explosiones, el movimiento de pistones y la
  interacción no deseada con redstone y tolvas.
- Los marcos de objetos, los botes con cofre, las vagonetas con almacenamiento y las
  vagonetas con tolva se protegen con la misma interacción de agacharse y hacer clic
  derecho; los marcos montados sobre contenedores bloqueados se vinculan automáticamente
  al contenedor. Los aldeanos cuyo puesto de trabajo apunta a una mesa de trabajo
  protegida heredan su protección.
- La expiración por mundo y la limpieza por inactividad eliminan protecciones obsoletas,
  y la eliminación de las protecciones de un mundo puede borrarlas con soporte de
  deshacer.

## Interfaces

Tres motores de presentación, elegidos automáticamente para cada jugador:

- **Menús de inventario de cofre** - las pantallas clásicas, con protección frente a
  clics y paginación.
- **Diálogos nativos de Paper** (`use_dialogs: true`) - diálogos modales en Paper 1.21.7
  o posterior, con una paleta pastel; se desactivan automáticamente con una advertencia
  cuando la API de diálogos no está disponible.
- **Formularios de Bedrock** - formularios nativos adaptados al táctil para jugadores
  que se conectan a través de Geyser y Floodgate.

## Ediciones y plataforma

| Edición | Rama | Minecraft | Java |
|---|---|---|---|
| BlockProt Reloaded | `main` | 1.21.7 y posteriores | 21 |
| BlockProt Reloaded Legacy | `BlockProt-Reloaded-Legacy` | 1.20.5 a 1.21.6 | 21 |
| BlockProt Legacy | `BlockProt-Legacy` | 1.18.2 a 1.20.4 | 17 |

Las ediciones Legacy solo reciben correcciones de errores y compatibilidad, nunca
funciones nuevas; los diálogos nativos de Paper solo existen en BlockProt Reloaded, y
las ediciones Legacy usan menús de inventario de cofre. Todas las ediciones mantienen el
nombre de plugin `BlockProtReloaded`, por lo que todas comparten una carpeta de datos y
un conjunto de permisos. La lista completa de compilaciones publicadas, edición por
edición, está en la página de [Versiones](../releases.md).

- Compatibles y probados: Paper, Purpur y Folia (rango declarado de 1.21.7 a 26.3).
- Reconocidos pero no probados: Pufferfish, Leaf, Leaves y Gale.
- Spigot estándar arranca con una advertencia de no ser compatible; CraftBukkit estándar
  es rechazado.
- El software de servidor híbrido (Mohist, Magma, CatServer, Arclight) está fuera de
  alcance.

## Almacenamiento

El NBT basado en archivos en cada bloque protegido es la principal fuente de verdad. Las
preferencias del jugador y los datos de amigos viven en el contenedor de datos
persistentes del jugador. SQLite almacena el registro de auditoría por bloque y la caché
de jugadores desconectados, y un índice opcional de MySQL/MariaDB replica las ubicaciones
de los bloques y las listas de confianza para servidores grandes. Las actualizaciones
del plugin nunca sobrescriben los archivos de configuración existentes del
administrador.

## Integraciones

| Plugin | Comportamiento |
|---|---|
| WorldGuard | Evalúa las flags de región y la flag personalizada `allow-blockprot` |
| Towny | Respeta los límites de pueblos y parcelas; limpia los unclaims; bypass opcional en pueblos en ruinas |
| Lands | Respeta los permisos de claim y las opciones de protección de tierras salvajes |
| ClaimChunk | Restringe el bloqueo y el acceso a contenedores a los propietarios del chunk |
| GriefPrevention | Respeta la propiedad del claim |
| Residence | Restringe el bloqueo y la interacción con contenedores a los propietarios de residencias |
| WorldEdit | Bloqueo automático opcional para estructuras recién pegadas |
| PlaceholderAPI | Expone recuentos de bloques y placeholders de amigos por defecto |
| ViaVersion | Detección de la versión de protocolo del cliente |
| Geyser / Floodgate | Resolución de nombres de Bedrock y formularios nativos de Bedrock |

Las integraciones se configuran de forma centralizada en `integrations.yml`, y cada una
tiene un interruptor `enabled`. Se publica una API para desarrolladores a través de
JitPack, con métodos de consulta documentados (`BlockProtAPI`) y cinco eventos
cancelables para otros plugins.

## Licencia

Con licencia GNU General Public License v3.0, basada en BlockProt de spnda, con los
avisos de copyright originales conservados según lo exige la GPL v3.

## Referencia

- [Comandos y permisos](commands.md)
- [Configuración](configuration.md)
