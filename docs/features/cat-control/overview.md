# Resumen de Control CAT

Control CAT permite que software externo de registro y concurso controle la FLEX-8600 a través de interfaces compatibles con rigctld. AetherSDR ejecuta hasta cuatro servidores independientes — uno por slice (A, B, C, D) — mediante TCP, puertos serie virtuales (PTY), o ambos simultáneamente.

En la v26.5.3, la ubicación del enlace simbólico PTY se movió de `/tmp` a directorios de ejecución por usuario para corregir una vulnerabilidad de enlace simbólico entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico de enlaces simbólicos mediante symlink(.tmp) + rename(.tmp, final) cierra la ventana TOCTOU.

En la v26.7.4, el botón principal Enable ahora muestra "Enabled" o "Disabled" en lugar de "Enable CAT", proporcionando una retroalimentación visual más clara de un vistazo. Las casillas de verificación de habilitación por puerto tienen un estilo de alto contraste para que el estado marcado sea visible incluso en fondos de applet oscuros.

## Antes de comenzar

- Debe haber una FLEX-8600 conectada. El applet Control CAT requiere una conexión de radio activa.
- El applet CAT está oculto por defecto. Haga clic en el botón de la bandeja CAT en la barra lateral derecha para mostrarlo.

## Cómo funciona

Cada uno de los cuatro canales (A, B, C, D) se asigna a un slice de radio. Cuando TCP está habilitado, cada canal escucha en su propio puerto comenzando en el puerto base: canal A en `Base`, B en `Base+1`, C en `Base+2`, D en `Base+3`. Cuando TTY está habilitado en Linux o macOS, cada canal crea un enlace simbólico PTY que el software de registro puede abrir como un dispositivo serie.

Los programas externos se conectan al canal que controla el slice que desean operar. Varios clientes pueden conectarse al mismo canal simultáneamente; la fila de estado por canal muestra el número actual de clientes.

AetherSDR puede iniciar los servidores TCP y los enlaces PTY automáticamente al inicio mediante `Settings > Autostart rigctld with AetherSDR` y `Settings > Autostart CAT with AetherSDR`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Enable CAT | Botón de alternancia | Apagado | — | `CatEnabled` | Inicia o detiene los cuatro servidores TCP rigctld (en los puertos Base hasta Base+3) y habilita o deshabilita los combos VFO por canal. El texto del botón cambia a "Enabled" o "Disabled" para reflejar el estado actual. |
| Enable TCP | Botón de alternancia | Apagado | — | — | Inicia o detiene los cuatro servidores TCP rigctld en los puertos Base hasta Base+3. También escribe el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de alternancia | Apagado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY bajo `$XDG_RUNTIME_DIR/aethersdr/cat-A` hasta `cat-D` (Linux) o `~/Library/Caches/AetherSDR/cat-A` hasta `cat-D` (macOS). Disponible solo en Linux y macOS. |
| Base | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera del rango válido vuelven a 4532. Si los servidores TCP están ejecutándose al cambiar este valor, se reinician en los nuevos puertos inmediatamente. |
| Filas de canal A / B / C / D | Indicador | (detenido) | — | — | Cada fila muestra una insignia de slice con código de color, una casilla de verificación de habilitación individual, un combo de selección VFO, el estado TCP (por ejemplo `:4532 (1 client)` o `(stopped)`), y la ruta del enlace simbólico PTY para ese canal. Las casillas de verificación de habilitación tienen un estilo de alto contraste con un color de acento relleno cuando están marcadas. |

## Indicadores por canal

| Indicador | Estados | Significado |
|---|---|---|
| Estado TCP por canal | `(stopped)`, `:<port> (1 client)`, `:<port> (N clients)` | Estado del servidor y número de clientes conectados por canal. |
| Ruta PTY por canal | `stopped`, `running PTY path` | Ruta del enlace simbólico que el software de registro puede abrir como dispositivo serie. Ubicada bajo `$XDG_RUNTIME_DIR/aethersdr/cat-A` (Linux) o `~/Library/Caches/AetherSDR/cat-A` (macOS). |

## Consejos

- Si un puerto ya está en uso por otra aplicación, el servidor de ese canal no podrá iniciarse. Cambie `Base` a un rango de puertos libre y haga clic en Enable TCP nuevamente.
- Las rutas de los enlaces simbólicos PTY se calculan a partir de los directorios de ejecución por usuario. En Linux, las rutas están bajo `$XDG_RUNTIME_DIR/aethersdr/cat-A` hasta `cat-D`. En macOS, las rutas están bajo `~/Library/Caches/AetherSDR/cat-A` hasta `cat-D`. La ruta exacta aparece en la fila del canal cuando el PTY está ejecutándose.
- Puede ejecutar TCP y TTY al mismo tiempo en el mismo canal.
- Cada fila de canal tiene su propia casilla de verificación de habilitación. Habilite el interruptor principal Enable CAT antes de configurar puertos individuales.

## Relacionados

- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Enable CAT PTY so Linux/macOS apps can open a serial-style CAT port](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Change the base TCP port](change-the-base-tcp-port.md)
- [Autostart CAT servers with AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Check how many external clients are connected to each channel](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Setting up digital modes (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
