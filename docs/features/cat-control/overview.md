# Resumen del control CAT

El control CAT permite que el software externo de registro y concurso controle la FLEX-8600 a través de interfaces compatibles con rigctld. AetherSDR ejecuta hasta cuatro servidores independientes, uno por slice (A, B, C, D), mediante TCP, puertos serie virtuales (PTY) o ambos simultáneamente.

En la v26.5.3, la ubicación del enlace simbólico PTY se trasladó de `/tmp` a directorios de ejecución por usuario para solucionar una vulnerabilidad de enlace simbólico entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico del enlace simbólico mediante symlink(.tmp) + rename(.tmp, final) cierra la ventana TOCTOU.

## Antes de comenzar

- Debe haber una FLEX-8600 conectada. El applet de control CAT requiere una conexión de radio activa.
- El applet CAT está oculto de forma predeterminada. Haga clic en el botón de la bandeja CAT en la barra lateral derecha para mostrarlo.

## Cómo funciona

Cada uno de los cuatro canales (A, B, C, D) se asigna a un slice de radio. Cuando TCP está habilitado, cada canal escucha en su propio puerto comenzando por el puerto base: canal A en `Base`, B en `Base+1`, C en `Base+2`, D en `Base+3`. Cuando TTY está habilitado en Linux o macOS, cada canal crea un enlace simbólico PTY que el software de registro puede abrir como un dispositivo serie.

Los programas externos se conectan al canal que controla el slice que desean operar. Varios clientes pueden conectarse al mismo canal simultáneamente; la fila de estado por canal muestra el número actual de clientes.

AetherSDR puede iniciar los servidores TCP y los enlaces PTY automáticamente al iniciarse mediante `Settings > Autostart rigctld with AetherSDR` y `Settings > Autostart CAT with AetherSDR`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Enable TCP | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro servidores TCP de rigctld en los puertos Base a Base+3. También escribe el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D` (Linux) o `~/Library/Caches/AetherSDR/cat-A` a `cat-D` (macOS). Disponible solo en Linux y macOS. |
| Base | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera del rango válido se restablecen a 4532. Si los servidores TCP están en ejecución al cambiar este valor, se reinician inmediatamente en los nuevos puertos. |
| Filas de canal A / B / C / D | Indicador | (detenido) | — | — | Cada fila muestra una insignia de slice con código de colores, el estado TCP (por ejemplo, `:4532 (1 client)` o `(stopped)`) y la ruta del enlace simbólico PTY para ese canal. |

## Indicadores por canal

| Indicador | Estados | Significado |
|---|---|---|
| Estado TCP por canal | `(stopped)`, `:<port> (1 client)`, `:<port> (N clients)` | Estado del servidor y número de clientes conectados por canal. |
| Ruta PTY por canal | `stopped`, `running PTY path` | Ruta del enlace simbólico que el software de registro puede abrir como dispositivo serie. Ubicado en `$XDG_RUNTIME_DIR/aethersdr/cat-A` (Linux) o `~/Library/Caches/AetherSDR/cat-A` (macOS). |

## Consejos

- Si un puerto ya está en uso por otra aplicación, el servidor de ese canal no se iniciará. Cambie `Base` a un rango de puertos libre y haga clic en Enable TCP nuevamente.
- Las rutas de los enlaces simbólicos PTY se calculan a partir de los directorios de ejecución por usuario. En Linux, las rutas están en `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`. En macOS, las rutas están en `~/Library/Caches/AetherSDR/cat-A` a `cat-D`. La ruta exacta aparece en la fila del canal cuando el PTY está en ejecución.
- Puede ejecutar TCP y TTY al mismo tiempo en el mismo canal.

## Relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que las aplicaciones Linux/macOS puedan abrir un puerto CAT tipo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Inicio automático de servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
