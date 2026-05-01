# Descripción General de Antenna Genius

El applet Antenna Genius le permite controlar un conmutador de antena 4O3A Antenna Genius desde AetherSDR. Úselo para seleccionar antenas por puerto de radio, seguir automáticamente los cambios de banda y ver de un vistazo qué antenas están permitidas para TX en la banda actual.

## Antes de comenzar

- El dispositivo Antenna Genius debe estar encendido y accesible — ya sea en la LAN local (para descubrimiento automático) o en una dirección IP conocida (para conexión manual).
- El applet está oculto hasta que se detecte un dispositivo o se realice una conexión manual. Una vez visible, ábralo con el botón de bandeja "AG" en la barra lateral derecha.

## Cómo funciona

AetherSDR escucha dispositivos Antenna Genius en la LAN mediante descubrimiento UDP. Cuando se encuentra un dispositivo, el applet aparece y se conecta automáticamente. Tenga en cuenta que los dispositivos ShackSwitch descubiertos en la LAN no se conectan automáticamente aquí; son manejados por el applet ShackSwitch en su lugar. Si su dispositivo está en una red remota, ingrese su dirección IP en el campo Manual IP y presione Enter; la dirección se guarda como `AG_ManualIp` y se utiliza para conectarse en el puerto 9007.

Una vez conectado, el applet muestra dos secciones de puerto — Puerto A y Puerto B — cada una con una fila de botones de antena poblados desde la lista de antenas del dispositivo. Haga clic en un botón de antena para seleccionar esa antena en el puerto; hágale clic de nuevo para deseleccionarla (establece la antena en 0). Si un dispositivo reporta solo un puerto de radio, la sección Puerto B se oculta.

Los botones de antena están codificados por color para mostrar el permiso de TX/RX en la banda actual:

- **Azul** — TX y RX permitidos.
- **Ámbar** — Solo RX en esta banda.
- **Atenuado** — Sin permiso en la banda actual.

Una antena ya seleccionada en el otro puerto está deshabilitada y no puede ser seleccionada en este puerto.

La etiqueta de estado en la parte superior del applet rastrea el ciclo de vida de la conexión, y los indicadores por puerto muestran la banda activa y el nombre de la antena seleccionada en tiempo real.

## Qué hace cada control

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| Combo de dispositivo | Selecciona qué dispositivo AG descubierto conectar. Se completa mediante descubrimiento UDP. Selecciona y conecta automáticamente el primer dispositivo descubierto, siempre que no sea un ShackSwitch. | — | — |
| Connect / Disconnect | Se conecta al dispositivo seleccionado, o a la IP Manual si ningún dispositivo descubierto está seleccionado. Se convierte en "Disconnect" cuando está conectado. | Connect | — |
| Manual IP | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse al puerto 9007. La dirección se guarda para sesiones futuras. Una entrada inválida muestra un estado rojo "Invalid IP address". | — | `AG_ManualIp` |
| Botones de antena Puerto A | Haga clic para seleccionar una antena en Puerto A. Haga clic de nuevo para deseleccionar. Deshabilitado si la antena está en uso en Puerto B. El color refleja el permiso TX/RX (azul = TX+RX, ámbar = solo RX, atenuado = sin permiso). | — | — |
| Puerto A AUTO | Alterne para habilitar seguimiento de banda en Puerto A. Cuando está activo, el AG cambia antenas automáticamente cuando la radio cambia de banda. | — | — |
| Botones de antena Puerto B | El mismo comportamiento que los botones de antena Puerto A, para Puerto B. Oculto si el dispositivo conectado tiene solo un puerto de radio. | — | — |
| Puerto B AUTO | Alterne para habilitar seguimiento de banda en Puerto B. | — | — |

### Indicadores de estado

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de estado | No device found / Device found / Connected — \<nombre\> v\<versión\> / Disconnected / Error: \<msg\> / Invalid IP address | Estado de descubrimiento y conexión del Antenna Genius. |
| Banda Puerto A | Nombre de banda o — | Banda activa en Puerto A, derivada del reporte AG o de la frecuencia de radio. |
| Antena Puerto A | Nombre de antena / \<ant\>  TX:\<alt\> / \<ant\> [INHIBIT] / — | Antena seleccionada en Puerto A. Roja cuando está transmitiendo; naranja cuando TX se enruta a una antena alternativa o inhibit está activo. |
| Banda Puerto B | Nombre de banda o — | Banda activa en Puerto B. |
| Antena Puerto B | Nombre de antena / \<ant\>  TX:\<alt\> / \<ant\> [INHIBIT] / — | Antena seleccionada en Puerto B. Las mismas reglas de color que Puerto A. |

## Relacionado

- [Descubra automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conéctese manualmente a un AG en una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccione una antena para Puerto A o Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Habilite el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Identifique qué antenas no pueden hacer TX en la banda actual (ámbar o atenuado)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Intercambie radios que comparten el AG (antenas en uso por el otro puerto están bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
