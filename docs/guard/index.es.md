# Zelly's Guard

Zelly's Guard es una suite de protección para servidores modernos de Paper y Folia
(Minecraft 26.x). Cubre protección regional, claims con pala dorada, piedras de protección,
registro de bloques, control de PvP, tumbas de muerte, heurísticas anti-xray e integración
de bloqueo de contenedores mediante BlockProt Reloaded.

!!! note "Sobre los nombres y las rutas de comandos"

    Todo en Zelly's Guard funciona bajo un único comando raíz, `/zg` (también
    disponible como `/guard` y `/zguard`); el plugin no registra comandos
    sueltos de nivel superior para sus módulos.

    Muchos nombres de módulos y funciones pueden parecerse a los de otros
    plugins. Esto es porque NO ENCONTRÉ OTRA FORMA DE LLAMARLOS, ¿okay? No son
    réplicas ni copias: son nombres parecidos pero originales, adaptados al
    plugin, porque estos plugins están pensados para vivir en el ecosistema de
    un servidor de comunidad, tanto para su uso ahí como para uso público
    (fuera del servidor).

## Propósito y filosofía

Guard existe para reemplazar el conjunto fragmentado de plugins de protección heredados con
un único motor, sin duplicar dominios que ya posee un proyecto hermano maduro. Su alcance es
la protección regional, los claims, el bloqueo de bloques, el registro, las mecánicas de
combate y el anti-xray; la economía, los minijuegos y las funciones de chat quedan
deliberadamente fuera de su alcance.

Principios de diseño:

- **Espacio de nombres unificado.** Todo es accesible bajo un único comando raíz, `/zg`
  (alias `/guard` y `/zguard`).
- **Subsistemas modulares.** Regiones, claims, piedras, bloqueos, registro, PvP, tumbas y
  anti-xray funcionan como módulos independientes que un administrador del servidor activa
  o desactiva.
- **Interfaces de diálogo nativas.** Los menús se renderizan como diálogos nativos de Paper
  en los clientes compatibles, con formularios de Bedrock mediante Floodgate.
- **Integrar, no duplicar.** El bloqueo de contenedores se delega a BlockProt Reloaded;
  donde ese plugin está presente, Guard detecta el enlace al arrancar y sincroniza las
  comprobaciones de construcción de regiones con sus eventos de bloqueo. Guard también se
  registra dentro de los menús de Zelly's Nexus cuando ambos plugins funcionan juntos.
- **Listo para Folia.** El plugin está orientado al modelo de hilos regionalizados de Folia
  además de a los servidores Paper normales.

## Estado de desarrollo

!!! info "Estado de desarrollo"
    Zelly's Guard está en desarrollo activo (0.1.0-alpha) para Paper y Folia 26.x sobre
    Java 25. Los claims, las piedras de protección, las regiones, las interfaces de diálogo,
    el interruptor de PvP, las tumbas y los enlaces con BlockProt Reloaded y Nexus funcionan
    hoy; las mecánicas de combate, el almacenamiento y la reversión del registro de bloques
    y los informes anti-xray siguen en desarrollo.

## Crear claims con la pala dorada

1. Haz clic derecho en un bloque mientras sostienes una pala dorada para iniciar una
   selección. La interacción en sí se cancela mientras la pala está en uso.
2. El primer clic guarda la primera esquina y la muestra; el segundo clic completa el claim.
   Un clic adicional reinicia la sesión y comienza una nueva selección.

Reglas de creación:

- Ambas esquinas deben estar en el mismo mundo.
- El claim se expande automáticamente desde la altura mínima hasta la máxima del mundo.
- Cada lado debe medir al menos 10 bloques.
- Se rechaza superponerse a una región existente en el mismo mundo.

Los claims nuevos se guardan con un nombre generado (`claim|<player>|<x>_<z>`) y prioridad 5.
La respuesta visual de las esquinas es un resaltado de bloque dorado, que se borra cuando
sales del juego o dejas de sostener una pala dorada.

Los claims se gestionan con `/zg claim` (`abandon`, `trust <player>`, `untrust <player>`,
`list`); la gestión actúa sobre el claim en el que estás de pie, emparejado por propiedad.

## Piedras de protección

Colocar el bloque de piedra configurado (`COAL_ORE` por defecto) crea un área protegida a su
alrededor con prioridad 10. Se rechaza superponerse al cuboide protegido de otro jugador, y
cada jugador puede mantener hasta el número configurado de piedras (5 por defecto). El
propietario de la piedra, o un jugador con `zguard.bypass`, puede romperla para liberar el
área; cualquier otra persona queda bloqueada.

## Flags de región

- `build` - colocación y rotura de bloques
- `interact` - interacciones con bloques
- `pvp` - daño entre jugadores
- `lock` - se responde para la interacción con el bloqueo de contenedores de BlockProt Reloaded

Los propietarios y miembros de una región pueden construir; a todos los demás se les deniega
con un mensaje traducido.

## Integraciones

- **Zelly's Nexus.** Cuando ambos plugins funcionan juntos, Guard registra una entrada de
  menú "Guard" (icono de escudo) en los menús de Nexus que abre el centro de usuario de Guard.
- **BlockProt Reloaded.** Se detecta al arrancar, con el enlace activo notificado; Guard
  cancela los eventos de bloqueo, menú de acceso y bloqueo automático de BlockProt cuando la
  interacción con los claims deniega la acción. `/zg lock` informa del estado del enlace o
  recomienda instalar BlockProt Reloaded cuando falta.
- **Informe de arranque.** La secuencia de arranque detecta Zelly's Nexus, Floodgate,
  PlaceholderAPI, LuckPerms y BlockProt Reloaded, e informa de cada uno como encontrado o no
  encontrado.
- **API para desarrolladores.** Un pequeño servicio de API expone la versión del plugin, si
  un módulo está habilitado, la apertura del centro de usuario y las comprobaciones de
  construcción/interacción para otros plugins.

## Referencia

- [Comandos](commands.md)
- [Configuración](configuration.md)
