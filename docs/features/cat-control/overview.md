# Resumen del control CAT

El control CAT permite que el software externo de registro de QSO y de concursos controle la FLEX-8600 a través de interfaces compatibles con rigctld. AetherSDR ejecuta hasta cuatro servidores independientes —uno por segmento (A, B, C, D)— mediante TCP, puertos serie virtuales (PTY) o ambos simultáneamente.

En la versión 26.5.3, la ubicación del enlace simbólico PTY se trasladó de `/tmp` a directorios de ejecución por usuario para corregir una vulnerabilidad de enlace simbólico entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico del enlace simbólico mediante symlink(.tmp) + rename(.tmp, final) cierra la ventana TOCTOU.

## Antes de comenzar

- Debe haber una FLEX-8600 conectada. El applet de control CAT requiere una conexión activa con la radio.
- El applet CAT está oculto de forma predeterminada. Haga clic en el botón de la bandeja CAT en la barra lateral derecha para mostrarlo.

## Cómo funciona

Cada uno de los cuatro canales (A, B, C, D) se asigna a un segmento de radio. Cuando TCP está habilitado, cada canal escucha en su propio puerto a partir del puerto base: canal A en `Base`, B en `Base+1`, C en `Base+2`, D en `Base+3`. Cuando TTY está habilitado en Linux o macOS, cada canal crea un enlace simbólico PTY que el software de registro puede abrir como un dispositivo serie.

Los programas externos se conectan al canal que controla el segmento que desean operar. Varios clientes pueden conectarse al mismo canal simultáneamente; la fila de estado por canal muestra el número actual de clientes.

AetherSDR puede iniciar los servidores TCP y los enlaces PTY automáticamente al arrancar mediante `Settings > Autostart rigctld with AetherSDR` y `Settings > Autostart CAT with AetherSDR`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Enable TCP | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro servidores TCP de rigctld en los puertos Base hasta Base+3. También escribe el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D` (Linux) o `~/Library/Caches/AetherSDR/cat-A` a `cat-D` (macOS). Disponible solo en Linux y macOS. |
| Base | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera del rango válido vuelven a 4532. Si los servidores TCP están ejecutándose cuando se cambia este valor, se reinician en los nuevos puertos de inmediato. |
| Filas de canal A / B / C / D | Indicador | (detenido) | — | — | Cada fila muestra una insignia de segmento codificada por colores, el estado TCP (por ejemplo `:4532 (1 cliente)` o `(detenido)`) y la ruta del enlace simbólico PTY para ese canal. |

## Indicadores por canal

| Indicador | Estados | Significado |
|---|---|---|
| Estado TCP por canal | `(detenido)`, `:<puerto> (1 cliente)`, `:<puerto> (N clientes)` | Estado del servidor y número de clientes conectados por canal. |
| Ruta PTY por canal | `detenido`, `ruta PTY en ejecución` | Ruta del enlace simbólico que el software de registro puede abrir como dispositivo serie. Se encuentra en `$XDG_RUNTIME_DIR/aethersdr/cat-A` (Linux) o `~/Library/Caches/AetherSDR/cat-A` (macOS). |

## Consejos

- Si un puerto ya está siendo utilizado por otra aplicación, el servidor de ese canal no podrá iniciarse. Cambie `Base` a un rango de puertos libre y haga clic en Enable TCP nuevamente.
- Las rutas de los enlaces simbólicos PTY se calculan a partir de los directorios de ejecución por usuario. En Linux, las rutas están en `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`. En macOS, las rutas están en `~/Library/Caches/AetherSDR/cat-A` a `cat-D`. La ruta exacta aparece en la fila del canal cuando el PTY está en ejecución.
- Puede ejecutar TCP y TTY al mismo tiempo en el mismo canal.

## Relacionado

- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Enable CAT PTY so Linux/macOS apps can open a serial-style CAT port](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Change the base TCP port](change-the-base-tcp-port.md)
- [Autostart CAT servers with AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Check how many external clients are connected to each channel](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Setting up digital modes (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
