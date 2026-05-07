# Resumen del control CAT

El control CAT permite que software externo de registro y concurso comande la FLEX-8600 a través de interfaces compatibles con rigctld. AetherSDR ejecuta hasta cuatro servidores independientes — uno por slice (A, B, C, D) — mediante TCP, puertos serie virtuales (PTY), o ambos simultáneamente.

## Antes de comenzar

- Debe haber una FLEX-8600 conectada. El applet de control CAT requiere una conexión activa con la radio.
- El applet CAT está oculto de forma predeterminada. Haga clic en el botón de la bandeja CAT en la barra lateral derecha para mostrarlo.

## Cómo funciona

Cada uno de los cuatro canales (A, B, C, D) se asigna a un slice de radio. Cuando TCP está habilitado, cada canal escucha en su propio puerto a partir del puerto base: canal A en `Base`, B en `Base+1`, C en `Base+2`, D en `Base+3`. Cuando TTY está habilitado en Linux o macOS, cada canal crea un enlace simbólico PTY que el software de registro puede abrir como un dispositivo serie.

Los programas externos se conectan al canal que controla el slice que desean operar. Múltiples clientes pueden conectarse al mismo canal simultáneamente; la fila de estado de cada canal muestra el número actual de clientes.

AetherSDR puede iniciar los servidores TCP y los enlaces PTY automáticamente al inicio mediante `Settings > Autostart rigctld with AetherSDR` y `Settings > Autostart CAT with AetherSDR`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Enable TCP | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld en los puertos Base hasta Base+3. También escribe el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Disponible solo en Linux y macOS. |
| Base | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera del rango válido se revierten a 4532. Si los servidores TCP están en ejecución al cambiar este valor, se reinician en los nuevos puertos inmediatamente. |
| Filas de canal A / B / C / D | Indicador | (detenido) | — | — | Cada fila muestra una insignia de slice con código de color, el estado TCP (por ejemplo `:4532 (1 cliente)` o `(detenido)`), y la ruta del enlace simbólico PTY para ese canal. |

## Consejos

- Si un puerto ya está siendo utilizado por otra aplicación, el servidor para ese canal no podrá iniciarse. Cambie `Base` a un rango de puertos libre y haga clic en Enable TCP nuevamente.
- Las rutas de los enlaces simbólicos PTY (`/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`) son fijas hasta que se inicia el PTY; una vez en ejecución, la ruta real informada por el sistema aparece en la fila del canal.
- Puede ejecutar TCP y TTY al mismo tiempo en el mismo canal.

## Relacionado

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que las aplicaciones Linux/macOS puedan abrir un puerto CAT estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar servidores CAT automáticamente con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
