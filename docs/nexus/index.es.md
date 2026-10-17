# Zelly's Nexus

El núcleo modular del ecosistema: un solo plugin para los servicios diarios de los
jugadores y las herramientas de staff de un servidor Paper, al que se accede mediante un
único comando raíz, `/zn` (alias `/nexus`).

!!! note "Sobre los nombres y las rutas de comandos"

    Todo en Zelly's Nexus funciona bajo un único comando raíz, `/zn`; los
    atajos de raíz opcionales (`/spawn`, `/login` y el resto) se pueden
    desactivar en `config.yml`, y la ruta `/zn` siempre funciona. Consulta
    [Comandos](commands.md) para los detalles.

    Muchos nombres de módulos y funciones pueden parecerse a los de otros
    plugins. Esto es porque NO ENCONTRÉ OTRA FORMA DE LLAMARLOS, ¿okay? No son
    réplicas ni copias: son nombres parecidos pero originales, adaptados al
    plugin, porque estos plugins están pensados para vivir en el ecosistema de
    un servidor de comunidad, tanto para su uso ahí como para uso público
    (fuera del servidor).

!!! info "Estado de desarrollo"
    Zelly's Nexus está en desarrollo activo. Los módulos, los comandos y las pantallas
    crecen versión a versión, y el nombre del proyecto en sí aún no es definitivo.

## Propósito y filosofía

Zelly's Nexus existe para consolidar en un único núcleo cohesivo los servicios que un
servidor moderno ensamblaría de otro modo a partir de una docena de plugins separados -
autenticación, un conjunto de herramientas para jugadores y staff, clanes, canales de
chat, herramientas de inventario, un editor de objetos y la tab list -, con un único
espacio de nombres, una única estructura de configuración y una interfaz consistente.

Los principios de diseño que hay detrás:

- **Modular por construcción.** Cada función es un módulo que puede activarse o
  desactivarse por su cuenta, con su propio archivo de configuración y su propio estado
  de ciclo de vida en el informe de arranque. Nada es todo o nada.
- **Una ruta, atajos opcionales.** Todo vive bajo `/zn <module> <action>`. Los comandos
  raíz clásicos como `/spawn`, `/home` o `/login` son alias opcionales que pueden
  activarse o desactivarse, de modo que el plugin puede convivir con un conjunto de
  comandos ya existente.
- **Interfaces modernas primero.** Los menús se renderizan como diálogos nativos de
  Paper, con indicaciones en el chat y menús de inventario clásicos como respaldo cuando
  los diálogos están desactivados. El enfoque de diálogos sigue la misma dirección de
  diseño que se usa en BlockProt Reloaded, otro proyecto de este ecosistema.
- **Construido para el Paper actual.** Java 25, Paper y Folia 26.x, con enrutamiento de
  tareas seguro por región para servidores Folia. Sin soporte para versiones antiguas de
  Minecraft ni para Spigot.
- **Localizado desde el principio.** El inglés y el español vienen dentro del jar, con un
  respaldo seguro en inglés para cualquier clave que falte.

## Módulos

El plugin se compone de trece módulos: `auth`, `antibot`, `toolkit`, `ban`, `join`,
`chat`, `inventory`, `clans`, `itemedit`, `tab`, `integrations`, `updater` y `debug`.
Todos los módulos excepto Debug están activados por defecto.

La página [Módulos](modules.md) describe qué hace cada uno, sus comandos, sus permisos y
su almacenamiento.

## Interfaces

- **Diálogos.** Con `dialogs: true` en `config.yml`, los menús se abren como pantallas de
  diálogo nativas de Paper: el menú de módulos y los menús por módulo, como el menú de
  clanes o el editor de objetos. Con los diálogos desactivados, los flujos recurren a
  las indicaciones en el chat.
- **Barrera de inicio de sesión.** Mientras el módulo auth está cargado, los jugadores
  que no han iniciado sesión no pueden moverse, construir, interactuar, usar el chat,
  soltar o recoger objetos, recibir daño, hacer clic en inventarios, ni ejecutar ningún
  comando excepto los puntos de entrada de auth.
- **Jugadores Bedrock.** Se detectan Geyser y Floodgate, y el módulo integrations puede
  informar de si un jugador entró a través de Floodgate.

## Comandos

Todos los comandos, con su sintaxis, su nodo de permisos y su comportamiento en consola,
están en la página [Comandos](commands.md). Ejecutar `/zn` o `/zn menu` abre el menú de
módulos; `/zn help` lista los módulos que el emisor puede usar.

## Configuración

La configuración global está en `config.yml`; la configuración por módulo está en
`modules/<module>.yml`. La página [Configuración](configuration.md) lista cada clave con
su valor por defecto y marca las claves que se procesan pero aún no se aplican.

## Integraciones

Al arrancar, el plugin informa de qué plugins conocidos ha encontrado: PlaceholderAPI,
LuckPerms, Geyser-Spigot, Floodgate y BlockProt o BlockProtReloaded. Se registra en el
servidor un servicio de API pública, `NexusApi`, que expone la versión del plugin, el
idioma activo, el estado de los diálogos y la posibilidad de que otros plugins registren
entradas de menú y subcomandos personalizados.

## Licencia

Zelly's Nexus se distribuye bajo la PolyForm Noncommercial License 1.0.0, más términos
adicionales específicos del proyecto: sin uso comercial, sin derivados cerrados, y los
forks deben permanecer vinculados a este repositorio o ser eliminados. El texto completo
de la licencia está enlazado en la página [Acerca de](../about.md).
