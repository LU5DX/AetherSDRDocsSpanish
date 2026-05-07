# Intercambio de Radios que Comparten el AG (Las Antenas en Uso por el Otro Puerto Están Bloqueadas)

Cuando dos radios comparten un Antenna Genius, cada radio se conecta a un puerto separado (Puerto A o Puerto B). Cualquier antena ya seleccionada en un puerto queda bloqueada — su botón aparece atenuado — en el otro puerto. Esta página explica cómo reasignar antenas entre puertos para que ninguna radio quede bloqueada.

## Antes de comenzar

- El applet de Antenna Genius debe estar visible. Si el botón de la bandeja del AG no aparece, conéctese primero a su dispositivo — consulte [Detección automática de un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Conexión manual a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe leer "Connected — \<name\> v\<version\>". No intente cambios de antena mientras esté desconectado.
- Su dispositivo AG debe informar dos puertos de radio. Si informa solo uno, la sección del Puerto B está oculta y este procedimiento no aplica.

## Pasos

1. Haga clic en el botón de la bandeja del AG en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Observe los botones de antena del Puerto A y del Puerto B. Los botones atenuados en un puerto ya están seleccionados en el otro puerto y no pueden elegirse hasta que se liberen.
3. Para liberar una antena bloqueada, haga clic en su botón actualmente iluminado en el puerto que la tiene. Hacer clic por segunda vez en un botón de antena seleccionado la deselecciona (establece ese puerto en "sin antena"). El botón vuelve a su estado apagado.
4. Una vez que la antena está deseleccionada en el puerto que la tenía, su botón se vuelve activo en el otro puerto.
5. Haga clic en el botón de antena ahora disponible en el puerto al que desea asignarla. El botón se ilumina y el nombre de la antena aparece en el indicador de antena del puerto en la parte superior de esa sección.
6. Confirme la asignación: el indicador de antena junto a "Port A" o "Port B" muestra el nombre de la antena. Si la antena soporta TX en la banda actual, el botón es azul; si es solo RX en la banda actual, es ámbar.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena del Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic nuevamente para deseleccionar. | Atenuados si la antena ya está seleccionada en el Puerto B. Azul = TX+RX permitido; ámbar = solo RX; atenuado = sin permiso en la banda actual. |
| Botones de antena del Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic nuevamente para deseleccionar. | Atenuados si la antena ya está seleccionada en el Puerto A. La sección del Puerto B está oculta si el dispositivo informa solo un puerto de radio. |
| Puerto A AUTO | Alternar. Habilita el seguimiento de banda en el Puerto A para que el AG rastree los cambios de banda automáticamente. | Desactive AUTO antes de reasignar antenas manualmente en el Puerto A si necesita control explícito. |
| Puerto B AUTO | Alternar. Habilita el seguimiento de banda en el Puerto B. | Misma advertencia que Puerto A AUTO. |
| Etiqueta de estado | Muestra el estado actual de la conexión: "Connected — \<name\> v\<version\>", "Disconnected", "Error: \<msg\>", etc. | Los botones de antena no funcionan cuando no hay conexión. |
| Indicador de antena del Puerto A | Muestra el nombre de la antena seleccionada; se vuelve rojo durante TX, naranja cuando TX se enruta a una antena alternativa o se activa la inhibición. | Muestra "—" cuando no hay antena seleccionada. |
| Indicador de antena del Puerto B | Igual que el indicador de antena del Puerto A, para el Puerto B. | Muestra "—" cuando no hay antena seleccionada. |

## Consejos

- **Deseleccione antes de reasignar**: debe liberar la antena de su puerto actual antes de que el botón esté disponible en el otro puerto. No hay intercambio por arrastrar y soltar — el paso de liberación es obligatorio.
- Si ambas radios están en modo AUTO, el AG seguirá la banda de cada radio de forma independiente. En ese caso, la resolución manual del bloqueo puede ser anulada inmediatamente por el próximo cambio de banda. Desactive AUTO en el puerto relevante antes de hacer cambios manuales.

## Solución de problemas

- **Un botón de antena permanece atenuado incluso después de hacer clic en el botón del otro puerto para deseleccionarlo** — confirme que la deselección surtió efecto verificando que el indicador de antena del otro puerto ahora muestre "—". Si el indicador aún muestra el nombre de la antena, es posible que el clic no se haya registrado; haga clic una vez más en el botón iluminado del otro puerto.
- **La sección del Puerto B no es visible** — el dispositivo AG conectado informa solo un puerto de radio. El uso compartido del Puerto B no está disponible en dispositivos de un solo puerto.
- **La etiqueta de estado muestra "Disconnected" o "Error: \<msg\>"** — los botones de antena no se pueden cambiar mientras esté desconectado. Reconéctese usando Connect o volviendo a ingresar la IP en Manual IP y presionando Enter. Las direcciones no válidas producen un estado rojo "Invalid IP address". La última IP manual utilizada se almacena en `AG_ManualIp` y se restaura en el próximo inicio.
- **Un dispositivo ShackSwitch aparece en el combo Device pero no se conecta automáticamente** — los dispositivos ShackSwitch descubiertos en la LAN se excluyen de la conexión automática en el applet de Antenna Genius. Son manejados por el applet de ShackSwitch. Seleccione el dispositivo Antenna Genius correcto en el combo Device y haga clic en Connect, o ingrese su IP en Manual IP y presione Enter.

## Relacionados

- [Seleccionar una antena para el Puerto A o Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Identificar qué antenas no pueden transmitir en la banda actual (ámbar o atenuado)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Detección automática de un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
