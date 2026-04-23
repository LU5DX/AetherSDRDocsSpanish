# Seleccionar una antena para el Puerto A o el Puerto B

Use el applet Antenna Genius para asignar una antena específica al Puerto A o al Puerto B de su conmutador 4O3A Antenna Genius. Esto le permite controlar qué antena física usa cada puerto de radio sin salir de AetherSDR.

## Antes de comenzar

- El applet Antenna Genius debe estar visible. Permanece oculto hasta que se conecta o detecta un dispositivo. Consulte [Detección automática de un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe mostrar **Connected — \<name\> v\<version\>** antes de que aparezcan los botones de antena.
- Abra el applet haciendo clic en el botón de bandeja **AG** en la barra lateral derecha.

## Pasos

1. Haga clic en el botón de bandeja **AG** para abrir el applet Antenna Genius.
2. Confirme que la etiqueta de estado muestre **Connected —** seguido del nombre y la versión del dispositivo.
3. Bajo el encabezado **Port A**, localice los botones de antena que se han cargado desde la lista de antenas del dispositivo.
4. Haga clic en el botón de la antena que desea asignar al Puerto A. El botón se resalta para indicar que está seleccionado.
5. Para deseleccionar la antena actual del Puerto A, haga clic en el mismo botón de nuevo. El puerto vuelve al estado sin antena seleccionada (antena 0).
6. Si su dispositivo tiene dos puertos de radio, la sección **Port B** es visible debajo del separador. Repita los pasos 3–5 bajo el encabezado **Port B** para asignar una antena al Puerto B.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena del Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic de nuevo para deseleccionar. | Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX. Atenuado = sin permiso en la banda actual. Deshabilitado si la antena ya está seleccionada en el Puerto B. |
| Banda del Puerto A | Muestra la banda activa en el Puerto A, derivada de la frecuencia del radio. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del Puerto A | Muestra el nombre de la antena actualmente seleccionada para el Puerto A. | Muestra **\<ant\>  TX:\<alt\>** cuando el TX está enrutado hacia una antena alternativa, y **\<ant\> [INHIBIT]** cuando la transmisión está inhibida. Se vuelve rojo durante TX; naranja en TX alternativo o en inhibición. |
| **Port A AUTO** | Conmutador. Activa el seguimiento de banda en el Puerto A para que el conmutador siga automáticamente los cambios de banda del radio. | Consulte [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Botones de antena del Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic de nuevo para deseleccionar. | La misma lista de antenas que el Puerto A. Oculto si el dispositivo reporta solo un puerto de radio. |
| Banda del Puerto B | Muestra la banda activa en el Puerto B. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del Puerto B | Muestra el nombre de la antena actualmente seleccionada para el Puerto B. | El mismo indicador de estado que la antena del Puerto A. |
| **Port B AUTO** | Conmutador. Activa el seguimiento de banda en el Puerto B. | Oculto cuando la sección del Puerto B está oculta. |

## Consejos

- Una antena que ya está seleccionada en un puerto aparece deshabilitada y atenuada en la cuadrícula de botones del otro puerto. No es posible asignar la misma antena a ambos puertos de forma simultánea.
- Los botones de antena resaltados en ámbar están disponibles para recepción, pero no permitirán TX en la banda actual. Cambie a un botón azul antes de transmitir.

## Solución de problemas

- **La sección del Puerto B no es visible** — El dispositivo conectado reporta solo un puerto de radio. El Puerto B se oculta automáticamente en este caso y no está disponible.
- **Los botones de antena no se muestran** — El dispositivo aún no está conectado o la lista de antenas no se ha cargado. Confirme que la etiqueta de estado muestre **Connected —** y espere un momento para que se complete la lista.
- **Al hacer clic en un botón de antena no ocurre nada** — Es posible que el botón esté deshabilitado porque esa antena ya está seleccionada en el otro puerto. Elija una antena diferente o deselecciónela en el otro puerto primero.

## Relacionados

- [Descripción general de Antenna Genius](overview.md)
- [Detección automática de un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Identificar qué antenas no pueden transmitir en la banda actual (ámbar o atenuado)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto están bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
