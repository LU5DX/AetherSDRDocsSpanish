# Seleccionar una antena para Port A o Port B

Use el applet Antenna Genius para elegir qué antena el conmutador 4O3A Antenna Genius enruta hacia Port A o Port B en su radio. Al seleccionar una antena aquí, el comando se envía inmediatamente al conmutador.

## Antes de comenzar

- El applet Antenna Genius debe estar visible en el panel de applets. Aparece automáticamente cuando se descubre o conecta un dispositivo. Si no está visible, haga clic en el botón AG tray en la barra lateral derecha.
- El Antenna Genius debe estar conectado. La etiqueta de estado debe mostrar "Connected — &lt;name&gt; v&lt;version&gt;". Si muestra "No device found" o "Disconnected", consulte [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La lista de antenas debe estar poblada. Los botones de antena aparecen automáticamente después de una conexión exitosa.

## Pasos

1. Haga clic en el botón AG tray en la barra lateral derecha para abrir el applet Antenna Genius.
2. Localice la sección Port A o Port B. Port B se oculta si el dispositivo conectado reporta solo un puerto de radio.
3. Haga clic en el botón de antena que desea seleccionar. El botón se resalta para indicar que está activo.
4. Para deseleccionar la antena actual en un puerto, haga clic nuevamente en su botón activo. El puerto regresa al estado sin antena seleccionada (antena 0).

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena de Port A | Haga clic para seleccionar una antena en Port A. Haga clic en el botón activo nuevamente para deseleccionar. | Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX en la banda actual. Tenue = sin permiso en la banda actual. Deshabilitado si la antena ya está seleccionada en Port B. |
| Port A AUTO | Active o desactive para habilitar el seguimiento de banda en Port A. El conmutador selecciona antenas automáticamente cuando el radio cambia de banda. | Consulte [Habilitar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Botones de antena de Port B | Haga clic para seleccionar una antena en Port B. Haga clic en el botón activo nuevamente para deseleccionar. | Mismo código de colores que Port A. Deshabilitado si la antena ya está seleccionada en Port A. Oculto si el dispositivo tiene solo un puerto de radio. |
| Port B AUTO | Active o desactive para habilitar el seguimiento de banda en Port B. | Consulte [Habilitar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Indicador de antena de Port A | Muestra el nombre de la antena actualmente seleccionada para Port A. Muestra `<ant>  TX:<alt>` cuando el TX se enruta a una antena alternativa, o `<ant> [INHIBIT]` cuando la transmisión está inhibida. | Se vuelve rojo durante la transmisión, naranja cuando el TX se redirige o el inhibidor está activo. |
| Indicador de antena de Port B | Igual que el indicador de antena de Port A, para Port B. | Mismo comportamiento de colores. |

## Consejos

- Un botón de antena que aparece tenue en la banda actual sigue siendo clicable, pero esa antena no tiene permiso de TX ni de RX configurado para esta banda en el Antenna Genius. Verifique la configuración de permisos de banda/antena en su AG si esto no es lo esperado.
- Si una antena que desea asignar a Port A aparece en gris y no es clicable, ya está seleccionada en Port B. Deselecciónela primero desde Port B.

## Solución de problemas

- **Los botones de antena no aparecen** — El applet está conectado pero no ha recibido una lista de antenas del dispositivo. Intente hacer clic en Disconnect y luego en Connect para restablecer la sesión.
- **Hacer clic en un botón no tiene efecto** — Es posible que el dispositivo haya perdido la conexión. Verifique la etiqueta de estado. Si no muestra "Connected — &lt;name&gt; v&lt;version&gt;", reconéctese usando el botón Connect.
- **La sección Port B no está visible** — El dispositivo Antenna Genius conectado reporta solo un puerto de radio. Los controles de Port B se ocultan automáticamente en este caso.

## Relacionado

- [Descripción general del Antenna Genius](overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Identificar qué antenas no pueden hacer TX en la banda actual (ámbar o tenue)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto quedan bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
