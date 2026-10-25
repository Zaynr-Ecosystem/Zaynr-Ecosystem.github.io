# HollowKraft

<div class="hk4-banner-container" markdown="1">

![HollowKraft 4 - Vasijas de Hallownest](assets/images/HK4.png){ .hk4-banner }

</div>

**HollowKraft (HK4)** es la siguiente edición del servidor de la comunidad **Vasijas de Hallownest**, para **Minecraft 26.x**. El proyecto está **planificado y en desarrollo activo**.

!!! info "Estado: planificado, en desarrollo activo"
    HollowKraft está en fase de desarrollo y estabilización técnica. Cuando un punto sigue abierto, no se ha tomado una decisión final.

## ¿Qué es HollowKraft?

HollowKraft es un servidor de supervivencia comunitaria a largo plazo donde los jugadores exploran, construyen y conviven. No es un servidor de anarquía ni un servidor de festivales con eventos estresantes.

## Planificado de un vistazo

| Área | Plan actual |
|---|---|
| Servidor | Mundo de supervivencia comunitario, con operación continua 24/7 planificada. |
| Dificultad | Difícil (*Hard*). |
| Capacidad | Objetivo de 50+ jugadores simultáneos. |
| Mundos | Dos mundos planificados y gestionados desde Zelly's Guard: un mundo PvP (semipacífico, con sistema de bromas) y un mundo pacífico de construcción pura. |
| Clanes | Sistema integral mediante Zelly's Nexus. Etiquetas de clan configurables en el chat y en la lista de jugadores. |
| Chat y social | Chat global en ambos mundos, mensajes de entrada y salida, logros con mensajes personalizados y avisos de muerte. Sin rangos de pago al lanzamiento. |
| Economía | Planificada para una etapa posterior al lanzamiento con la moneda "Geo" inspirada en Hollow Knight, tienda y progresión interactiva de habilidades. |
| Mod de cliente (Java) | Opcional (Fabric 26.3). Control 100% mediante interfaz gráfica in-game en tecla `K` y menú principal conmutador. Nunca obligatorio. |
| Pack de recursos | Opcional y opt-in para Java; el contenido visual definitivo se encuentra en desarrollo. |

## Compatibilidad de Plataformas: Java y Bedrock

HollowKraft permite la entrada conjunta de jugadores de Java Edition y de Bedrock Edition en el mismo mundo mediante **Geyser** y **Floodgate**. Ninguna modificación de cliente es obligatoria para conectarse y jugar.

### Java Edition

Java Edition ofrece la experiencia completa de escritorio y es compatible tanto con clientes estándar sin modificar como con el mod opcional de cliente.

#### Capacidades en Java
- **Compatibilidad Vanilla Total:** Los usuarios pueden conectarse utilizando cualquier cliente oficial o alternativo de Minecraft Java Edition en versión 26.x.
- **Diálogos Nativos de Paper:** Menús interactivos fluidos y modernos para la gestión de parcelas, configuración de clanes y perfiles de usuario.
- **Menús Clásicos en Cofres:** Soporte alternativo de interfaces de inventario para quienes prefieren la navegación tradicional (`/zg gui`, `/zn gui`).
- **Soporte para el Mod Opcional de Fabric:**
    - Pantalla de carga oscura cinemática con identidad visual del servidor.
    - Menú principal estilizado con conmutador instantáneo al menú vanilla con un solo clic.
    - Tema visual oscuro para ventanas de diálogo de Paper.
    - Centro de control unificado dentro del juego mediante la tecla `K`.
    - Animaciones suaves de interfaz, incluyendo deslizamiento de selector en barra rápida, desvanecimiento de líneas de chat, desplazamiento fluido de listas e iluminación de ranuras de inventario.
    - Ajustes de accesibilidad con interruptor general para reducir movimiento.

#### Limitaciones en Java
- **Requisitos de Instalación del Mod:** El mod de cliente requiere tener instalado el cargador Fabric y la API de Fabric para Java 26.3. No puede ejecutarse en el lanzador vanilla sin Fabric instalado.
- **Ámbito Exclusivo de Cliente:** El mod actúa únicamente del lado del cliente y no se instala en el servidor. Jugar sin el mod está admitido al 100%, pero el jugador verá los menús predeterminados vanilla, los diálogos normales y las animaciones estándar de Minecraft.
- **Rendimiento de Hardware:** Los efectos visuales de suavizado y partículas dependen de la capacidad del procesador y la tarjeta gráfica del equipo.

---

### Bedrock Edition

Los jugadores de Bedrock Edition acceden al servidor directamente mediante la integración de Geyser y Floodgate.

#### Capacidades en Bedrock
- **Conectividad Multiplataforma:** Jugadores desde Windows Bedrock, dispositivos móviles (iOS, Android) y consolas (Xbox, PlayStation, Nintendo Switch) acceden al mismo mundo común.
- **Formularios Nativos de Floodgate:** Todos los diálogos y menús del servidor se transforman en formularios modales, listas de opciones y paneles de entrada nativos de Bedrock.
- **Acceso Total a las Funciones de Juego:** Participación en la supervivencia, chat global entre mundos, protección de parcelas (`/zg claim`), bloqueo de cofres (`/zg lock`), creación y gestión de clanes (`/zn clans`) y bromas inofensivas (`/zn prank`).
- **Sin Necesidad de Software Externo:** Se conecta de manera directa desde la versión oficial de Bedrock sin instalar mods ni clientes modificados.

#### Limitaciones en Bedrock
- **Incompatibilidad con Mods de Fabric:** El mod de cliente de HollowKraft para Fabric no se puede instalar en Bedrock Edition. Fabric es una tecnología exclusiva de Java Edition.
- **Sin Menús Personalizados de Cliente:** El menú principal temático, la pantalla de inicio personalizada y las transiciones oscuras de carga no están disponibles en Bedrock.
- **Interfaz Exclusiva de Bedrock:** Efectos de interfaz del mod como el deslizamiento continuo de la hotbar, el desvanecimiento de chat, el brillo de ranuras y el panel `K` de cliente no se muestran en Bedrock.
- **Navegación por Formularios:** La interacción en Bedrock se realiza mediante los formularios de Floodgate y los menús tradicionales en cofre, no a través de pantallas gráficas personalizadas de cliente Java.

---

## Mod de Cliente HollowKraft (Fabric 26.3)

Para los jugadores de Java, se desarrolla un **mod de cliente opcional** que mejora la estética y la experiencia visual del servidor sin alterar la jugabilidad vanilla.

### Control 100% desde la Interfaz Gráfica

El mod está diseñado para gestionarse **exclusivamente desde la interfaz del juego**, eliminando la necesidad de memorizar comandos de cliente:

- **Tecla `K` (Centro de Control In-Game):** Abre el panel interactivo unificado que agrupa todas las funciones del servidor y del cliente:
    - **Inicio:** Estado de conexión, bienvenida y resumen del servidor.
    - **Clanes:** Base del clan, lista de miembros, perfil e información social (`/zn clans`).
    - **Protección:** Reclamar terrenos (`/zg claim`), bloquear cofres (`/zg lock`), tumbas (`/zg graves`), modo combate (`/zg pvp`), regiones y piedras de protección (`/zg stone`).
    - **Utilidades:** Mesa de crafteo virtual (`/craft`), enderchest, basurero, yunque, kits y menú de bromas (`/prank`).
    - **Administración:** Configuración interactiva de Nexus y Guard, diagnósticos de salud y gestión de sanciones.
    - **Ajustes del Mod:** Configuración gráfica en tiempo real.
- **Conmutador de Menú:** Permite alternar al instante entre el menú principal estilizado de Hollow Knight y el menú vanilla de Minecraft con un solo clic.

### Opciones Visuales y Animaciones Disponibles

Dentro de la pestaña **Ajustes Mod** del panel in-game, los jugadores pueden activar o desactivar libremente:

- **Pantalla de Carga Oscura:** Carga cinematográfica con logotipo personalizado estilo Dedsafio.
- **Diálogos Estilizados:** Reemplaza los menús estándar de Paper Dialogs por ventanas oscuras integradas con la temática de Hollow Knight.
- **Brillo en Contenedores (*Container Glow*):** Resplandor visual elegante al abrir cofres e interfaces de almacenamiento.
- **Animaciones Fluidas:** Apertura y cierre de paneles GUI con transiciones suaves, desvanecimiento gradual de líneas de chat y deslizamiento continuo del selector de la barra rápida (*hotbar*).
- **Desplazamiento Suave (*Smooth Scroll*):** Inercia y desplazamiento fluido en listas y paneles con rueda de ratón.
- **Reducción de Movimiento:** Opción de accesibilidad para desactivar sacudidas y animaciones bruscas.
- **Restablecer Ajustes:** Botón maestro para restaurar todas las opciones visuales a los valores de fábrica.

### Lista completa de opciones (panel de ajustes, tecla `K`)

El panel usa una paleta negra, gris y blanca y tiene cuatro pestañas. Todos los valores se editan desde el panel; nada exige editar un archivo.

| Pestaña | Opción | Valores |
|---|---|---|
| General | Estilo de menú | Hollow Knight o vanilla |
| General | Menú personalizado | activado o desactivado |
| General | Pantalla de inicio (imagen y título) | activado o desactivado |
| General | Aviso alpha | activado o desactivado |
| General | Reducir movimiento | activado o desactivado |
| General | Respetar otros mods | activado o desactivado |
| General | Servidor directo | local o en línea |
| Animaciones | Interruptor general | activado o desactivado |
| Animaciones | Cambio de mano suave | activado o desactivado |
| Animaciones | Resplandor de slots | activado o desactivado |
| Animaciones | Diálogos oscuros | activado o desactivado |
| Animaciones | Overlays inmersivos | activado o desactivado |
| Transiciones | Animación de pantallas | activado o desactivado |
| Transiciones | Hotbar fluida | activado o desactivado |
| Transiciones | Chat animado | activado o desactivado |
| Transiciones | Scroll suave | activado o desactivado |
| Velocidad | Desplazamiento de pantalla | 0, 5, 10, 15, 20 |
| Velocidad | Duración de pantalla (ms) | 120, 220, 320, 450 |
| Velocidad | Velocidad de hotbar | 12, 24, 36, 48 |
| Velocidad | Desvanecer chat (ms) | 90, 180, 300, 450 |
| Velocidad | Velocidad de scroll | 8, 16, 24, 32 |
| Velocidad | Velocidad de mano | 9, 18, 27, 36 |

Al pulsar una tarjeta de velocidad pasa al siguiente valor y vuelve al primero al llegar al final.

---

## Preguntas Frecuentes

### Lanzamiento y disponibilidad

**¿Cuándo abre HK4?**
No hay una fecha definitiva fijada. El servidor se abrirá cuando los sistemas estén completamente desarrollados, probados y verificados.

**¿Estará el servidor en línea 24/7?**
Sí, el plan de operación es 24/7 continuo, salvo ventanas breves de mantenimiento programado.

**¿Cuántos jugadores entrarán?**
El objetivo de capacidad es de 50+ jugadores simultáneos.

**¿Qué hardware necesito?**
El servidor y el mod están optimizados para funcionar en hardware básico, sin requerir equipos de gama alta.

### Plataformas y Juego Cruzado

**¿Pueden entrar jugadores de Bedrock al servidor?**
Sí. Mediante Geyser y Floodgate, los usuarios de Bedrock en móviles, consolas y Windows pueden jugar en el mismo mundo.

**¿Es obligatorio instalar el mod de Fabric para jugar en Java?**
No. El mod de cliente es 100% opcional. Los jugadores sin mod pueden jugar normalmente desde clientes estándar de Java con los diálogos y comandos del servidor.

**¿Pueden los jugadores de Bedrock ver el menú temático del mod?**
No. Los mods de cliente Fabric son exclusivos de Java Edition. Los usuarios de Bedrock navegan mediante menús nativos de Bedrock y formularios de Floodgate.

### Estilo de juego y mundos

**¿HK4 es un servidor de anarquía?**
No. HK4 es un mundo de supervivencia comunitario pacífico y ordenado, no un servidor de anarquía ni de festivales de destrucción.

**¿Habrá dos mundos distintos?**
Sí. Hay dos mundos planificados y gestionados mediante Zelly's Guard:
1. **Mundo PvP:** Semipacífico, con combate regulado y sistema de bromas (`/zn prank`).
2. **Mundo Pacífico:** Convivencia pura y construcción comunitaria sin combate entre jugadores.

**¿Se pueden transferir objetos entre los dos mundos?**
Se planea implementar un sistema de peaje con economía para cruzar objetos de un mundo a otro; si no se abona el peaje, se inicia el otro mundo con inventario limpio de cero.

**¿Estarán protegidas mis construcciones y cofres?**
Sí. La protección de terrenos y claims se gestiona con Zelly's Guard, y la protección de contenedores y bloques individuales se realiza mediante BlockProt Reloaded 1.4.2.

**¿Qué dificultad tendrá el servidor?**
La dificultad configurada es Difícil (*Hard*).

### Clanes, chat y economía

**¿Habrá clanes o equipos?**
Sí, implementados mediante Zelly's Nexus. Los jugadores pueden crear clanes, establecer una base comunitaria y mostrar su etiqueta de clan en el chat y en la lista de jugadores.

**¿El chat es global entre ambos mundos?**
Sí, el chat es unificado y global para permitir la comunicación entre los habitantes de ambos mundos.

**¿Los mensajes de muerte muestran coordenadas?**
La opción existe de forma configurable en el servidor, pero está desactivada por defecto para preservar la privacidad de las bases.

**¿Habrá economía y tiendas?**
La economía no estará activa en el lanzamiento inicial. Se implementará más adelante con la moneda "Geo" (inspirada en Hollow Knight), tienda de ítems y un sistema de progresión interactiva de habilidades.

**¿Habrá rangos de pago?**
No en el lanzamiento. Si se llegan a implementar rangos en el futuro, serán estrictamente cosméticos y nunca otorgarán ventajas de juego (*pay-to-win*).

### Mod de cliente y ediciones anteriores

**¿El mod requiere escribir comandos?**
No. El mod HollowKraft se controla al 100% mediante su interfaz gráfica dentro del juego (pulsando la tecla `K`) y desde el menú principal. Todo está en la interfaz.

**¿Qué ediciones anteriores existieron?**
La comunidad ha operado tres ediciones anteriores: HollowKraft 1 en Aternos, HollowKraft 2 en Shockbyte y HollowKraft 3 en HolyHosting. HollowKraft 4 representa la edición más avanzada y personalizada con plugins propios.

## Relacionado

HollowKraft se apoya en los proyectos documentados en este sitio: [Zelly's Guard](guard/index.md), [Zelly's Nexus](nexus/index.md) y [BlockProt Reloaded](blockprot/index.md).
