# Descripción general de CAT Control

CAT Control permite que software externo de logging y concursos controle el FLEX-8600 a través de interfaces compatibles con rigctld. AetherSDR ejecuta hasta cuatro servidores independientes — uno por slice (A, B, C, D) — sobre TCP, puertos seriales virtuales (PTY), o ambos simultáneamente.

## Antes de comenzar

- Un FLEX-8600 debe estar conectado. El applet CAT Control requiere una conexión activa a la radio.
- El applet CAT está oculto por defecto. Haga clic en el botón CAT de la bandeja en la barra lateral derecha para mostrarlo.

## Cómo funciona

Cada uno de los cuatro canales (A, B, C, D) se asigna a un slice de radio. Cuando TCP está activado, cada canal escucha en su propio puerto comenzando en el puerto base: canal A en `Base`, B en `Base+1`, C en `Base+2`, D en `Base+3`. Cuando TTY está activado en Linux o macOS, cada canal crea un enlace simbólico PTY que el software de logging puede abrir como dispositivo serial.

Los programas externos se conectan al canal que controla el slice que desean operar. Múltiples clientes pueden conectarse al mismo canal simultáneamente; la fila de estado por canal muestra el número actual de clientes.

AetherSDR puede iniciar los servidores TCP y enlaces PTY automáticamente al arranque mediante `Settings > Autostart rigctld with AetherSDR` y `Settings > Autostart CAT with AetherSDR`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Enable TCP | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld en los puertos Base a Base+3. También escribe el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D`. Disponible solo en Linux y macOS. |
| Base | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera del rango válido se ajustan a 4532. Si los servidores TCP se están ejecutando cuando cambia este valor, se reinician en los nuevos puertos inmediatamente. |
| Filas de canal A / B / C / D | Indicador | (detenido) | — | — | Cada fila muestra un distintivo de slice con código de color, el estado TCP (por ejemplo `:4532 (1 client)` o `(stopped)`), y la ruta de enlace simbólico PTY para ese canal. |

## Consejos

- Si un puerto ya está en uso por otra aplicación, el servidor de ese canal no se iniciará. Cambie `Base` a un rango de puerto libre y haga clic en Enable TCP nuevamente.
- Las rutas de enlace simbólico PTY (`/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D`) son fijas hasta que inicie el PTY; una vez en ejecución, la ruta real reportada por el sistema aparece en la fila del canal.
- Puede ejecutar TCP y TTY simultáneamente en el mismo canal.

## Relacionado

- [Activar CAT TCP para que N1MM, Log4OM, WSJT-X controlen la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Activar CAT PTY para que aplicaciones de Linux/macOS abran un puerto CAT de estilo serial](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar servidores CAT automáticamente con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
