# Intercambiar radios que comparten la AG (las antenas en uso por el otro puerto están bloqueadas)

Cuando dos radios comparten una Antenna Genius, cada radio se conecta a un puerto diferente (Puerto A o Puerto B). Cualquier antena ya seleccionada en un puerto queda bloqueada —su botón aparece atenuado— en el otro puerto. Esta página explica cómo reasignar antenas entre puertos para que ninguna radio quede bloqueada.

## Antes de comenzar

- El applet Antenna Genius debe estar visible. Si el botón de bandeja AG no está presente, conéctese a su dispositivo primero — consulte [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe mostrar "Connected — \<name\> v\<version\>". No intente cambios de antena mientras está desconectado.
- Su dispositivo AG debe reportar dos puertos de radio. Si reporta solo uno, la sección del Puerto B está oculta y este procedimiento no aplica.

## Pasos

1. Haga clic en el botón de bandeja AG en la barra lateral derecha para abrir el applet Antenna Genius.
2. Observe los botones de antena del Puerto A y los botones de antena del Puerto B. Los botones atenuados en un puerto ya están seleccionados en el otro puerto y no pueden elegirse hasta que se liberen.
3. Para liberar una antena bloqueada, haga clic en su botón iluminado actualmente en el puerto que la tiene. Hacer clic en un botón de antena seleccionado una segunda vez lo deselecciona (asigna ese puerto a ninguna antena). El botón vuelve a su estado apagado.
4. Una vez que la antena está deseleccionada en el puerto que la tenía, su botón se activa en el otro puerto.
5. Haga clic en el botón de antena ahora disponible en el puerto al que desea asignarlo. El botón se ilumina y el nombre de la antena aparece en el indicador de antena del puerto en la parte superior de la sección de ese puerto.
6. Confirme la asignación: el indicador de antena junto a "Port A" o "Port B" muestra el nombre de la antena. Si la antena soporta TX en la banda actual, el botón es azul; si es solo RX en la banda actual, es ámbar.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena del Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic nuevamente para deseleccionar. | Atenuado si la antena ya está seleccionada en el Puerto B. Azul = TX+RX permitido; ámbar = solo RX; atenuado = sin permiso en la banda actual. |
| Botones de antena del Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic nuevamente para deseleccionar. | Atenuado si la antena ya está seleccionada en el Puerto A. La sección del Puerto B está oculta si el dispositivo reporta solo un puerto de radio. |
| AUTO del Puerto A | Alternar. Habilita el seguimiento de banda en el Puerto A para que la AG siga los cambios de banda automáticamente. | Deshabilite AUTO antes de reasignar manualmente antenas en el Puerto A si necesita control explícito. |
| AUTO del Puerto B | Alternar. Habilita el seguimiento de banda en el Puerto B. | La misma advertencia que AUTO del Puerto A. |
| Etiqueta de estado | Muestra el estado actual de la conexión: "Connected — \<name\> v\<version\>", "Disconnected", "Error: \<msg\>", etc. | Los botones de antena no funcionan cuando no está conectado. |
| Indicador de antena del Puerto A | Muestra el nombre de la antena seleccionada; se vuelve rojo durante TX, naranja cuando TX se enruta a una antena alternativa o se activa inhibit. | Muestra "—" cuando no hay antena seleccionada. |
| Indicador de antena del Puerto B | Lo mismo que el indicador de antena del Puerto A, para el Puerto B. | Muestra "—" cuando no hay antena seleccionada. |

## Consejos

- Deseleccione antes de reasignar: debe liberar la antena de su puerto actual antes de que el botón esté disponible en el otro puerto. No hay intercambio de arrastrar y soltar — el paso de liberación es obligatorio.
- Si ambas radios están en modo AUTO, la AG seguirá la banda de cada radio independientemente. En ese caso, la resolución manual de bloqueo puede ser anulada inmediatamente por el siguiente cambio de banda. Deshabilite AUTO en el puerto relevante antes de hacer cambios manuales.

## Solución de problemas

- **Un botón de antena permanece atenuado incluso después de hacer clic en el botón del otro puerto para deseleccionarlo** — confirme que la deselección se efectuó verificando que el indicador de antena para el otro puerto ahora muestra "—". Si el indicador todavía muestra el nombre de la antena, es posible que el clic no se haya registrado; haga clic en el botón iluminado del otro puerto una vez más.
- **La sección del Puerto B no es visible** — el dispositivo AG conectado reporta solo un puerto de radio. El intercambio del Puerto B no está disponible en dispositivos de un solo puerto.
- **La etiqueta de estado muestra "Disconnected" o "Error: \<msg\>"** — los botones de antena no pueden cambiarse mientras está desconectado. Reconéctese usando Connect o ingresando nuevamente la IP en Manual IP y presionando Enter. Las direcciones inválidas producen un estado rojo "Invalid IP address". La IP manual utilizada por última vez se almacena en `AG_ManualIp` y se restaura en el siguiente lanzamiento.
- **Un dispositivo ShackSwitch aparece en el combo Device pero no se conecta automáticamente** — los dispositivos ShackSwitch detectados en la LAN se excluyen de la conexión automática en el applet Antenna Genius. El applet ShackSwitch se encarga de ellos. Seleccione el dispositivo Antenna Genius correcto del combo Device y haga clic en Connect, o ingrese su IP en Manual IP y presione Enter.

## Relacionado

- [Select an antenna for Port A or Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Spot which antennas cannot TX on the current band (amber or dim)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md)
