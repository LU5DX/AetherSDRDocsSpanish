# Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto quedan bloqueadas)

Cuando dos radios comparten un único Antenna Genius, cada antena solo puede asignarse a un puerto a la vez. Esta página explica cómo reasignar antenas entre el Puerto A y el Puerto B sin conflictos, y cómo interpretar los indicadores de bloqueo antes de transmitir.

## Antes de comenzar

- El applet de Antenna Genius debe estar abierto y mostrar "Connected — \<name\> v\<version\>" en la etiqueta de estado.
- El dispositivo AG debe reportar dos puertos de radio. La sección del Puerto B queda oculta cuando el dispositivo reporta un solo puerto.
- Identifique qué antenas está usando actualmente cada radio leyendo los indicadores de antena del Puerto A y del Puerto B en la parte superior de cada sección de puerto.

## Pasos

1. Haga clic en el botón "AG" de la bandeja en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Observe las etiquetas indicadoras de antena del Puerto A y del Puerto B. Un botón de antena que aparece atenuado o deshabilitado en un puerto ya está seleccionado en el otro puerto y no puede seleccionarse.
3. Para liberar una antena que está bloqueada, vaya al puerto que actualmente la tiene asignada y haga clic en su botón de antena activo (marcado) para deseleccionarla. El botón se desactiva y la selección de antena vuelve a ninguna (antena 0).
4. El botón bloqueado en el otro puerto queda disponible de inmediato. Haga clic en él para asignar esa antena al nuevo puerto.
5. Si está habilitado Port A AUTO o Port B AUTO, el AG sigue los cambios de banda automáticamente y puede volver a seleccionar antenas por sí solo. Si necesita una asignación manual estable, haga clic en "AUTO" en el puerto correspondiente para deshabilitar el modo AUTO antes de realizar el intercambio.
6. Confirme el intercambio leyendo ambas etiquetas indicadoras de antena. El nombre de la antena debe aparecer ahora en el puerto deseado.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena del Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic de nuevo para deseleccionarla (vuelve a antena 0). | Aparecen atenuados cuando la antena ya está seleccionada en el Puerto B. Azul = TX+RX permitidos; ámbar = solo RX; atenuado = sin permiso en la banda actual. |
| Botones de antena del Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic de nuevo para deseleccionarla. | Aparecen atenuados cuando la antena ya está seleccionada en el Puerto A. La sección del Puerto B queda oculta si el dispositivo reporta un solo puerto de radio. |
| Port A AUTO | Conmutador. Habilita el seguimiento de banda en el Puerto A. | Deshabilítelo antes de intercambiar manualmente si necesita que la asignación permanezca fija. |
| Port B AUTO | Conmutador. Habilita el seguimiento de banda en el Puerto B. | Deshabilítelo antes de intercambiar manualmente si necesita que la asignación permanezca fija. |
| Indicador de antena del Puerto A | Muestra el nombre de la antena seleccionada. Se vuelve rojo durante la transmisión; naranja cuando el TX es enrutado a una antena alternativa o se activa una inhibición. | Muestra "—" cuando no hay ninguna antena seleccionada. |
| Indicador de antena del Puerto B | Igual que el indicador de antena del Puerto A, para el Puerto B. | Muestra "—" cuando no hay ninguna antena seleccionada. |

## Consejos

- Deseleccione la antena en su puerto actual primero. El botón en el otro puerto no quedará disponible para hacer clic hasta que la antena sea liberada.
- Los botones de color ámbar indican permiso de solo RX en la banda actual. Seleccionar una antena ámbar para un puerto que pretende transmitir enrutará el TX a una antena alternativa separada; confirme su configuración antes de activar la transmisión.
- El modo AUTO en cualquier puerto puede anular una selección manual de antena cuando la radio cambia de banda. Si ambos puertos comparten un conjunto limitado de antenas, dejar AUTO activado en ambos puertos simultáneamente puede causar conflictos en los cambios de banda.

## Resolución de problemas

- **Un botón de antena permanece atenuado después de deseleccionarlo en el otro puerto** — Verifique que la deselección haya surtido efecto: el indicador de antena del puerto que limpió debe mostrar "—". Si todavía muestra un nombre de antena, haga clic en el botón una vez más para desactivarlo.
- **La sección del Puerto B no es visible** — El dispositivo AG conectado reporta un solo puerto de radio. Los controles del Puerto B quedan ocultos en este caso y el compartimiento de antenas para dos radios no está disponible en este dispositivo.

## Relacionados

- [Seleccionar una antena para el Puerto A o el Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Identificar qué antenas no pueden hacer TX en la banda actual (ámbar o atenuadas)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Descripción general del Antenna Genius](overview.md)
