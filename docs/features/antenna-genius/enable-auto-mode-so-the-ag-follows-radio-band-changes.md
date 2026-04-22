# Activar el modo AUTO para que el AG siga los cambios de banda del radio

El modo AUTO indica al Antenna Genius que seleccione las antenas automáticamente a medida que el radio cambia de banda, en lugar de requerir que el usuario elija una antena de forma manual. Se activa de forma independiente para el Puerto A y el Puerto B.

## Antes de comenzar

- El applet del Antenna Genius debe estar visible. Aparece únicamente después de que se detecta un dispositivo o se conecta manualmente. Ábralo haciendo clic en el botón AG del panel lateral derecho.
- El applet debe mostrar un estado de **Connected — \<name\> v\<version\>**. El modo AUTO no puede activarse mientras el dispositivo está desconectado.

## Pasos

1. Haga clic en el botón AG del panel lateral derecho para abrir el applet del Antenna Genius.
2. Confirme que la etiqueta de estado muestra **Connected —** seguido del nombre del dispositivo y la versión.
3. Para activar el seguimiento de banda en el Puerto A, haga clic en **AUTO** debajo de los botones de antena del Puerto A. El botón se resalta en verde cuando está activo.
4. Para activar el seguimiento de banda en el Puerto B, haga clic en **AUTO** debajo de los botones de antena del Puerto B. El botón se resalta en verde cuando está activo.
5. Para desactivar el modo AUTO en un puerto, haga clic nuevamente en el botón **AUTO** resaltado. El botón vuelve a su apariencia inactiva y es posible seleccionar las antenas de forma manual.

## Qué hace cada control

| Control | Ubicación | Comportamiento | Valor predeterminado |
|---|---|---|---|
| Puerto A AUTO | Debajo de los botones de antena del Puerto A | Activa o desactiva el modo de seguimiento de banda para el Puerto A. Cuando está activo, el AG selecciona la antena del Puerto A a medida que el radio cambia de banda. | Off |
| Puerto B AUTO | Debajo de los botones de antena del Puerto B | Activa o desactiva el modo de seguimiento de banda para el Puerto B. Cuando está activo, el AG selecciona la antena del Puerto B a medida que el radio cambia de banda. | Off |

> **Nota:** La sección del Puerto B se oculta si el dispositivo AG conectado reporta únicamente un puerto de radio.

## Consejos

- El modo AUTO se aplica por puerto. Es posible tener el Puerto A en AUTO mientras el Puerto B permanece en modo manual, o viceversa.
- Cuando AUTO está activo, los botones de antena de ese puerto continúan actualizándose para reflejar la antena seleccionada en ese momento y el color de permiso TX/RX correspondiente. Observe los indicadores de antena del Puerto A y del Puerto B para confirmar que el AG está siguiendo correctamente los cambios de banda.

## Resolución de problemas

- **El botón AUTO no tiene efecto o no permanece resaltado** — El applet no está conectado. Verifique que la etiqueta de estado muestre **Connected —** y no **Disconnected**, **No device found** ni **Error: \<msg\>**. Conéctese primero y luego active AUTO.
- **El AUTO del Puerto B no está visible** — El dispositivo conectado tiene únicamente un puerto de radio. Los controles del Puerto B se ocultan automáticamente en este caso.

## Relacionados

- [Descripción general del Antenna Genius](overview.md)
- [Detectar automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o el Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Identificar qué antenas no pueden transmitir en la banda actual (ámbar o atenuadas)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
