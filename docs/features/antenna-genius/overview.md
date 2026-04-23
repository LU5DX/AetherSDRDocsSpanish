# Descripción general de Antenna Genius

El applet Antenna Genius le permite controlar un conmutador de antenas 4O3A Antenna Genius desde AetherSDR. Úselo para seleccionar antenas por puerto de radio, seguir automáticamente los cambios de banda y ver de un vistazo qué antenas están permitidas para TX en la banda actual.

## Antes de comenzar

- El dispositivo Antenna Genius debe estar encendido y accesible — ya sea en la LAN local (para detección automática) o en una dirección IP conocida (para conexión manual).
- El applet permanece oculto hasta que se detecta un dispositivo o se realiza una conexión manual. Una vez visible, ábralo con el botón "AG" de la bandeja en la barra lateral derecha.

## Cómo funciona

AetherSDR escucha dispositivos Antenna Genius en la LAN mediante descubrimiento UDP. Cuando se encuentra un dispositivo, el applet aparece y se conecta automáticamente. Si su dispositivo está en una red remota, ingrese su dirección IP en el campo Manual IP y presione Enter; la dirección se guarda como `AG_ManualIp` y se usa para conectarse al puerto 9007.

Una vez conectado, el applet muestra dos secciones de puerto — Port A y Port B — cada una con una fila de botones de antena poblados desde la lista de antenas del dispositivo. Hacer clic en un botón de antena selecciona esa antena en el puerto; hacer clic nuevamente la deselecciona (establece la antena en 0). Si un dispositivo reporta solo un puerto de radio, la sección Port B se oculta.

Los botones de antena tienen código de colores para mostrar el permiso TX/RX en la banda actual:

- **Azul** — TX y RX permitidos.
- **Ámbar** — Solo RX en esta banda.
- **Atenuado** — Sin permiso en la banda actual.

Una antena ya seleccionada en el otro puerto queda deshabilitada y no puede seleccionarse en este puerto.

La etiqueta de estado en la parte superior del applet muestra el ciclo de vida de la conexión, y los indicadores por puerto muestran la banda activa y el nombre de la antena seleccionada en tiempo real.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Combo de dispositivo | Selecciona qué dispositivo AG descubierto conectar. Poblado por descubrimiento UDP. Selecciona automáticamente el primer dispositivo encontrado. | — | — |
| Connect / Disconnect | Conecta al dispositivo seleccionado, o a la Manual IP si no hay dispositivo descubierto seleccionado. Cambia a "Disconnect" cuando está conectado. | Connect | — |
| Manual IP | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse al puerto 9007. La dirección se guarda para sesiones futuras. Una entrada inválida muestra el estado rojo "Invalid IP address". | — | `AG_ManualIp` |
| Botones de antena Port A | Haga clic para seleccionar una antena en Port A. Haga clic nuevamente para deseleccionarla. Deshabilitado si la antena está en uso en Port B. El color refleja el permiso TX/RX (azul = TX+RX, ámbar = solo RX, atenuado = sin permiso). | — | — |
| Port A AUTO | Active o desactive el seguimiento de banda en Port A. Cuando está activo, el AG cambia las antenas automáticamente al cambiar de banda el radio. | — | — |
| Botones de antena Port B | Mismo comportamiento que los botones de antena de Port A, para Port B. Oculto si el dispositivo conectado tiene solo un puerto de radio. | — | — |
| Port B AUTO | Active o desactive el seguimiento de banda en Port B. | — | — |

### Indicadores de estado

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de estado | No device found / Device found / Connected — \<name\> v\<version\> / Disconnected / Error: \<msg\> / Invalid IP address | Estado de descubrimiento y conexión del Antenna Genius. |
| Banda Port A | Nombre de banda o — | Banda activa en Port A, derivada del reporte del AG o de la frecuencia del radio. |
| Antena Port A | Nombre de antena / \<ant\>  TX:\<alt\> / \<ant\> [INHIBIT] / — | Antena seleccionada en Port A. Rojo al transmitir; naranja cuando el TX se enruta a una antena alternativa o el inhibit está activo. |
| Banda Port B | Nombre de banda o — | Banda activa en Port B. |
| Antena Port B | Nombre de antena / \<ant\>  TX:\<alt\> / \<ant\> [INHIBIT] / — | Antena seleccionada en Port B. Mismas reglas de color que Port A. |

## Relacionado

- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para Port A o Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Identificar qué antenas no pueden hacer TX en la banda actual (ámbar o atenuado)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto quedan bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
