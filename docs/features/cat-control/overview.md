# Descripción general del control CAT

El control CAT permite que programas externos de registro y de concurso controlen el FLEX-8600 mediante interfaces compatibles con rigctld. AetherSDR ejecuta hasta cuatro servidores independientes — uno por slice (A, B, C, D) — a través de TCP, puertos serie virtuales (PTY), o ambos simultáneamente.

## Antes de comenzar

- El FLEX-8600 debe estar conectado. El applet de CAT requiere una conexión activa con la radio.
- El applet de CAT está oculto de forma predeterminada. Haga clic en el botón CAT de la bandeja en la barra lateral derecha para mostrarlo.

## Cómo funciona

Cada uno de los cuatro canales (A, B, C, D) corresponde a un slice de la radio. Cuando TCP está habilitado, cada canal escucha en su propio puerto a partir del puerto base: el canal A en `Base`, B en `Base+1`, C en `Base+2`, D en `Base+3`. Cuando TTY está habilitado en Linux o macOS, cada canal crea un enlace simbólico PTY que el software de registro puede abrir como dispositivo serie.

Los programas externos se conectan al canal que controla el slice con el que desean operar. Varios clientes pueden conectarse al mismo canal simultáneamente; la fila de estado de cada canal muestra el número actual de clientes conectados.

AetherSDR puede iniciar los servidores TCP y los enlaces PTY automáticamente al arrancar, mediante `Settings > Autostart rigctld with AetherSDR` y `Settings > Autostart CAT with AetherSDR`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|---|
| Enable TCP | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP de rigctld en los puertos Base a Base+3. También escribe el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Disponible solo en Linux y macOS. |
| Base | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera del rango válido vuelven automáticamente a 4532. Si los servidores TCP están en ejecución cuando se cambia este valor, se reinician en los nuevos puertos de inmediato. |
| Filas de canales A / B / C / D | Indicador | (detenido) | — | — | Cada fila muestra una insignia de slice con código de color, el estado TCP (por ejemplo `:4532 (1 client)` o `(stopped)`), y la ruta del enlace simbólico PTY para ese canal. |

## Sugerencias

- Si otro programa ya está usando un puerto, el servidor de ese canal no podrá iniciarse. Cambie `Base` a un rango de puertos disponible y haga clic nuevamente en Enable TCP.
- Las rutas de los enlaces simbólicos PTY (`/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`) son fijas hasta que el PTY se inicia; una vez en ejecución, la ruta real reportada por el sistema aparece en la fila del canal.
- Es posible ejecutar TCP y TTY al mismo tiempo en el mismo canal.

## Temas relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT tipo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
