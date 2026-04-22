# Descripción general de Antenna Genius

El applet Antenna Genius le permite conectarse a un conmutador de antenas 4O3A Antenna Genius desde AetherSDR, seleccionar antenas para cada puerto de radio y, opcionalmente, hacer que el conmutador siga los cambios de banda de forma automática. Úselo cuando su estación disponga de un 4O3A Antenna Genius en la LAN o accesible a través de una red remota.

## Antes de comenzar

- Su 4O3A Antenna Genius debe estar encendido y ser accesible desde el equipo que ejecuta AetherSDR (misma LAN para el descubrimiento automático, o cualquier IP enrutable para la conexión manual).
- No se requiere ninguna conexión de radio para usar el applet Antenna Genius.

## Cómo funciona

El applet permanece oculto hasta que se detecta un Antenna Genius o se conecta manualmente. Una vez disponible, ábralo con el botón de bandeja **AG** en la barra lateral derecha.

Al iniciarse, AetherSDR envía una difusión UDP para descubrir dispositivos Antenna Genius en la red local. Cuando se encuentra el primer dispositivo, se agrega al **Device combo** y AetherSDR se conecta a él automáticamente. El **Status label** se actualiza continuamente para reflejar el estado actual.

Si no se encuentra ningún dispositivo automáticamente —por ejemplo, el conmutador está en una red remota— ingrese su dirección IP en **Manual IP** y presione Enter. AetherSDR se conecta a esa dirección en el puerto 9007 y guarda la dirección como `AG_ManualIp` para sesiones futuras.

Una vez conectado, el applet muestra botones de antena para **Port A** y, si el dispositivo reporta dos puertos de radio, **Port B**. Cada botón representa una antena. Al hacer clic en un botón se selecciona esa antena en el puerto; al hacer clic de nuevo se deselecciona (establece la antena en 0). El color del botón indica el permiso TX/RX en la banda actual:

- **Azul** — la antena tiene permiso de TX y RX en la banda actual.
- **Ámbar** — la antena tiene permiso de RX únicamente en la banda actual.
- **Tenue** — sin permiso en la banda actual.

Las antenas ya seleccionadas en el puerto opuesto se deshabilitan para que no sea posible asignar la misma antena a ambos puertos simultáneamente.

El botón **AUTO** en cada puerto activa el modo de seguimiento de banda: cuando la radio cambia de banda, el Antenna Genius cambia automáticamente a una antena adecuada para ese puerto sin intervención manual.

La sección **Port B** se oculta automáticamente si el dispositivo conectado reporta únicamente un puerto de radio.

## Qué hace cada control

| Control | Función | Configuración guardada |
|---|---|---|
| **Device combo** | Selecciona el dispositivo AG descubierto al que conectarse. Se llena mediante descubrimiento UDP. Selecciona automáticamente el primer dispositivo encontrado. | — |
| **Connect** / **Disconnect** | Se conecta al dispositivo seleccionado o a la dirección **Manual IP**. Cambia a **Disconnect** cuando está conectado. | — |
| **Manual IP** | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse al puerto 9007. Las direcciones no válidas muestran el estado rojo "Invalid IP address". | `AG_ManualIp` |
| **Botones de antena de Port A** | Haga clic para seleccionar una antena en Port A; haga clic de nuevo para deseleccionar. Se deshabilitan si la antena ya está en uso en Port B. | — |
| **AUTO de Port A** | Activa el seguimiento de banda en Port A. El conmutador sigue los cambios de banda de la radio automáticamente. | — |
| **Botones de antena de Port B** | Haga clic para seleccionar una antena en Port B; haga clic de nuevo para deseleccionar. Se ocultan si el dispositivo tiene solo un puerto de radio. | — |
| **AUTO de Port B** | Activa el seguimiento de banda en Port B. | — |

### Indicadores de estado

| Indicador | Qué muestra |
|---|---|
| **Status label** | Estado de descubrimiento y conexión: `No device found`, `Device found`, `Connected — <name> v<version>`, `Disconnected`, `Error: <msg>` o `Invalid IP address`. |
| **Banda de Port A** | Banda activa en Port A, o `—` si no está disponible. |
| **Antena de Port A** | Antena seleccionada en Port A. Muestra `<ant>  TX:<alt>` cuando el TX está enrutado a una antena alternativa, o `<ant> [INHIBIT]` cuando se activa la inhibición de TX. En rojo durante la transmisión, en naranja cuando el TX es redirigido o inhibido. |
| **Banda de Port B** | Banda activa en Port B, o `—`. |
| **Antena de Port B** | Antena seleccionada en Port B, con las mismas reglas de visualización de TX/inhibición que Port A. |

## Temas relacionados

- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para Port A o Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Identificar qué antenas no pueden transmitir en la banda actual (ámbar o tenue)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto quedan bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
