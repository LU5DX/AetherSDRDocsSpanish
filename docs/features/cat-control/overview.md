# Descripción general del control CAT

El applet de control CAT permite que software externo de registro y de concursos controle el FLEX-8600, exponiendo hasta cuatro interfaces independientes compatibles con rigctld — una por slice. Cada canal puede alcanzarse mediante TCP o, en Linux y macOS, a través de un enlace simbólico PTY que el software percibe como un puerto serie.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El applet CAT requiere una conexión de radio activa.
- Conozca qué puerto espera su software de registro. El puerto base predeterminado es 4532.

## Cómo funciona

El applet de control CAT ejecuta hasta cuatro servidores compatibles con rigctld, uno por cada canal de slice (A, B, C, D). Cuando TCP está habilitado, cada canal escucha en un puerto consecutivo a partir del valor de `CatTcpPort`: el canal A en el puerto base, B en base+1, C en base+2 y D en base+3. Cuando TTY está habilitado en Linux o macOS, cada canal también crea un enlace simbólico PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D` que el software puede abrir como dispositivo serie virtual.

El applet está oculto de forma predeterminada. Haga clic en el botón **CAT** de la barra lateral derecha para mostrarlo. Cada fila de canal muestra una insignia con código de color (A/B/C/D que coincide con el color del slice), el estado actual del servidor TCP y la ruta PTY. El estado TCP se actualiza en tiempo real a medida que los clientes se conectan y desconectan.

El comportamiento de inicio automático se controla por separado mediante `Settings > Autostart rigctld with AetherSDR` (TCP) y `Settings > Autostart CAT with AetherSDR` (TTY).

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| **Enable TCP** | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld en los puertos Base a Base+3. También guarda el puerto base actual en `CatTcpPort`. |
| **Enable TTY** | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Solo en Linux y macOS. |
| **Base** | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales se enlazan a Base, Base+1, Base+2 y Base+3. Los valores fuera del rango válido vuelven automáticamente a 4532. Si los servidores están en ejecución cuando cambia este valor, se reinician de inmediato en los nuevos puertos. |
| **Filas de canales A/B/C/D** | Indicador | (detenido) | — | — | Cada fila muestra la insignia del canal, el estado TCP (p. ej., `:4532 (1 client)`) y la ruta PTY. La insignia y el texto de estado activo tienen código de color para coincidir con el slice. |

## Consejos

- Si el software de registro no puede conectarse, verifique que **Enable TCP** esté activado y que ningún cortafuegos esté bloqueando el puerto. La fila del canal mostrará `(stopped)` si el servidor no está en ejecución, o un puerto y un recuento de clientes cuando sí lo esté.
- Cada canal se asigna a un slice (A=slice 0, B=slice 1, etc.). Ejecute varios canales si desea que programas independientes controlen slices separados simultáneamente.
- Cambiar el puerto **Base** mientras los servidores están en ejecución los reinicia automáticamente — los clientes conectados serán desconectados y deberán reconectarse.

## Solución de problemas

- **La fila del canal siempre muestra `(stopped)` después de hacer clic en Enable TCP** — es posible que el puerto ya esté en uso por otra aplicación. Cambie el valor de **Base** a un rango de puertos libre e inténtelo de nuevo.
- **Los enlaces simbólicos PTY no aparecen** — Enable TTY solo funciona en Linux y macOS. El control no tiene efecto en Windows.
- **El software de registro pierde la conexión después de un cambio de puerto** — cambiar **Base** reinicia todos los servidores. Reconecte el software de registro al nuevo puerto.

## Relacionado

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
