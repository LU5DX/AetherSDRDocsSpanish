# Descripción general del control CAT

El applet de control CAT ejecuta hasta cuatro servidores compatibles con rigctld — uno por cada slice de radio — para que el software externo de registro y concursos pueda controlar el FLEX-8600 mediante comandos CAT estándar. Cada canal (A, B, C, D) es accesible por TCP y, en Linux y macOS, también a través de un puerto serie virtual (PTY).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet CAT requiere una conexión de radio activa.
- El botón CAT en la bandeja debe ser visible en la barra lateral derecha. Si el panel del applet está oculto, actívelo mediante `View > Applet Panel`.

## Cómo funciona

Al hacer clic en el botón CAT de la bandeja en la barra lateral derecha se abre el applet de control CAT. El applet gestiona cuatro canales independientes, de A hasta D, cada uno asignado a un slice de radio. Es posible iniciar servidores TCP, enlaces PTY o ambos simultáneamente.

**Los servidores TCP** escuchan en puertos consecutivos a partir del puerto base. Con el valor predeterminado de `4532`, el canal A se enlaza al puerto 4532, B al 4533, C al 4534 y D al 4535. Cualquier software compatible con rigctld — N1MM+, Log4OM, WSJT-X, entre otros — puede conectarse al puerto correspondiente y controlar el slice asociado.

**Los enlaces PTY** (solo en Linux y macOS) crean puertos serie virtuales en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Las aplicaciones que esperan un dispositivo serie en lugar de un socket TCP pueden abrir estas rutas directamente.

Los dos tipos de transporte son independientes. Es posible habilitar uno, ambos o ninguno.

Las opciones de inicio automático en el menú `Settings` permiten que AetherSDR levante los servidores TCP o los enlaces PTY automáticamente cada vez que se inicia, sin intervención manual.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Enable TCP | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro servidores TCP de rigctld en Base, Base+1, Base+2, Base+3. También persiste el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro enlaces PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Solo en Linux y macOS. |
| Base | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera de rango vuelven automáticamente a `4532`. Si los servidores TCP ya están en ejecución, se reinician de inmediato en los nuevos puertos. |
| Filas de canales A / B / C / D | Indicador | `(stopped)` | — | — | Cada fila muestra una insignia de canal con código de color, el estado TCP de ese canal y la ruta PTY. El estado TCP muestra `(stopped)` cuando el servidor no está en ejecución, o `:<port> (N client(s))` cuando sí lo está. |

## Consejos

- Si cambia el valor en Base mientras los servidores TCP están en ejecución, AetherSDR reinicia los cuatro servidores en los nuevos puertos de forma automática. No es necesario desactivar y volver a activar Enable TCP.
- Para verificar cuántos programas externos están conectados actualmente a cada canal, consulte el estado TCP por canal en las filas A/B/C/D. El contador se actualiza en tiempo real a medida que los clientes se conectan y desconectan.
- Para evitar iniciar manualmente los servidores CAT en cada sesión, utilice `Settings > Autostart CAT with AetherSDR` o `Settings > Autostart rigctld with AetherSDR`.

## Solución de problemas

- **Enable TCP no tiene efecto / los servidores no se inician** — AetherSDR debe estar conectado a una radio antes de que el applet CAT pueda iniciar servidores. Verifique la conexión de radio y luego intente Enable TCP nuevamente.
- **El campo de puerto vuelve a 4532** — El valor ingresado está fuera del rango válido de 1024–65535. Ingrese un valor dentro de ese rango.
- **Enable TTY no aparece o no hace nada** — Los enlaces PTY solo están disponibles en Linux y macOS. En Windows, el botón Enable TTY no tiene efecto.
- **El software externo no puede conectarse** — Confirme que el puerto base coincide con el que espera su software de registro y que ningún firewall está bloqueando el puerto. Cada canal ocupa un puerto: de Base hasta Base+3.

## Relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
