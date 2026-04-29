# Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto están bloqueadas)

Cuando dos radios comparten un Antenna Genius, cada radio se conecta a un puerto separado (Port A o Port B). Cualquier antena ya seleccionada en un puerto queda bloqueada — su botón aparece atenuado — en el otro puerto. Esta página explica cómo reasignar antenas entre puertos para que ninguna radio quede bloqueada.

## Antes de comenzar

- El applet de Antenna Genius debe estar visible. Si el botón del AG en la bandeja no aparece, conéctese primero a su dispositivo — consulte [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe indicar "Connected — \<name\> v\<version\>". No intente cambiar antenas mientras esté desconectado.
- Su dispositivo AG debe reportar dos puertos de radio. Si reporta solo uno, la sección Port B estará oculta y este procedimiento no aplica.

## Pasos

1. Haga clic en el botón del AG en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Observe los botones de antena de Port A y los botones de antena de Port B. Los botones que aparecen atenuados en un puerto ya están seleccionados en el otro puerto y no pueden elegirse hasta que sean liberados.
3. Para liberar una antena bloqueada, haga clic en su botón encendido en el puerto que la retiene. Hacer clic por segunda vez en un botón de antena seleccionado lo deselecciona (deja ese puerto sin antena). El botón vuelve a su estado apagado.
4. Una vez que la antena es deseleccionada en el puerto que la retenía, su botón queda activo en el otro puerto.
5. Haga clic en el botón de antena ahora disponible en el puerto al que desea asignarla. El botón se enciende y el nombre de la antena aparece en el indicador de antena del puerto, en la parte superior de la sección de ese puerto.
6. Confirme la asignación: el indicador de antena junto a "Port A" o "Port B" muestra el nombre de la antena. Si la antena admite TX en la banda actual, el botón es azul; si es solo RX en la banda actual, es ámbar.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena de Port A | Haga clic para seleccionar una antena en Port A; haga clic de nuevo para deseleccionar. | Atenuado si la antena ya está seleccionada en Port B. Azul = TX+RX permitido; ámbar = solo RX; atenuado = sin permiso en la banda actual. |
| Botones de antena de Port B | Haga clic para seleccionar una antena en Port B; haga clic de nuevo para deseleccionar. | Atenuado si la antena ya está seleccionada en Port A. La sección Port B está oculta si el dispositivo reporta solo un puerto de radio. |
| Port A AUTO | Conmutador. Habilita el seguimiento de banda en Port A para que el AG siga los cambios de banda automáticamente. | Deshabilite AUTO antes de reasignar antenas manualmente en Port A si necesita control explícito. |
| Port B AUTO | Conmutador. Habilita el seguimiento de banda en Port B. | Misma advertencia que Port A AUTO. |
| Etiqueta de estado | Muestra el estado actual de la conexión: "Connected — \<name\> v\<version\>", "Disconnected", "Error: \<msg\>", etc. | Los botones de antena no funcionan cuando no hay conexión. |
| Indicador de antena de Port A | Muestra el nombre de la antena seleccionada; se torna rojo durante TX, naranja cuando TX es enrutado hacia una antena alternativa o se activa una inhibición. | Muestra "—" cuando no hay antena seleccionada. |
| Indicador de antena de Port B | Igual que el indicador de antena de Port A, para Port B. | Muestra "—" cuando no hay antena seleccionada. |

## Consejos

- Deseleccione antes de reasignar: debe liberar la antena de su puerto actual antes de que el botón quede disponible en el otro puerto. No existe un intercambio por arrastrar y soltar — el paso de liberación es obligatorio.
- Si ambas radios están en modo AUTO, el AG seguirá la banda de cada radio de forma independiente. En ese caso, la resolución manual del bloqueo puede ser anulada de inmediato por el siguiente cambio de banda. Deshabilite AUTO en el puerto correspondiente antes de realizar cambios manuales.

## Solución de problemas

- **Un botón de antena permanece atenuado incluso después de haber hecho clic en el botón del otro puerto para deseleccionarla** — confirme que la deselección tuvo efecto verificando que el indicador de antena del otro puerto ahora muestre "—". Si el indicador aún muestra el nombre de la antena, es posible que el clic no haya sido registrado; haga clic una vez más en el botón encendido del otro puerto.
- **La sección Port B no es visible** — el dispositivo AG conectado reporta solo un puerto de radio. El uso compartido de Port B no está disponible en dispositivos de un solo puerto.
- **La etiqueta de estado muestra "Disconnected" o "Error: \<msg\>"** — los botones de antena no pueden cambiarse mientras esté desconectado. Reconéctese usando Connect o volviendo a ingresar la IP en Manual IP y presionando Enter. Las direcciones no válidas producen un estado rojo con el mensaje "Invalid IP address". La última IP manual utilizada se almacena en `AG_ManualIp` y se restaura al siguiente inicio.

## Relacionados

- [Seleccionar una antena para Port A o Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Identificar qué antenas no pueden hacer TX en la banda actual (ámbar o atenuado)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
