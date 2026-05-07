# Seleccionar una antena para el Puerto A o el Puerto B

Utilice el applet Antenna Genius para asignar una antena específica al Puerto A o al Puerto B de su conmutador 4O3A Antenna Genius. Esto le permite controlar qué antena física utiliza cada puerto de radio sin salir de AetherSDR.

## Antes de empezar

- El applet Antenna Genius debe estar visible. Está oculto hasta que un dispositivo se conecta o se descubre. Consulte [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe mostrar **Conectado — \<nombre\> v\<versión\>** antes de que aparezcan los botones de antena.
- Abra el applet haciendo clic en el botón de la bandeja **AG** en la barra lateral derecha.

## Pasos

1. Haga clic en el botón de la bandeja **AG** para abrir el applet Antenna Genius.
2. Confirme que la etiqueta de estado muestra **Conectado —** seguido del nombre y la versión del dispositivo.
3. Debajo del encabezado **Port A**, localice los botones de antena que se cargan desde la lista de antenas del dispositivo.
4. Haga clic en el botón de la antena que desea asignar al Puerto A. El botón se resalta para indicar que está seleccionado.
5. Para anular la selección de la antena actual en el Puerto A, vuelva a hacer clic en el mismo botón. El puerto vuelve al estado sin antena seleccionada (antena 0).
6. Si su dispositivo tiene dos puertos de radio, la sección **Port B** aparece debajo del separador. Repita los pasos 3–5 bajo el encabezado **Port B** para asignar una antena al Puerto B.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena de Port A | Haga clic para seleccionar una antena en el Puerto A; vuelva a hacer clic para anular la selección. | Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX. Atenuado = sin permiso en la banda actual. Deshabilitado si la antena ya está seleccionada en el Puerto B. |
| Banda de Port A | Muestra la banda activa en el Puerto A, derivada de la frecuencia de radio. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena de Port A | Muestra el nombre de la antena seleccionada actualmente para el Puerto A. | Muestra **\<ant\> TX:\<alt\>** cuando TX se enruta a una antena alternativa, y **\<ant\> [INHIBIT]** cuando la transmisión está inhibida. Se vuelve rojo durante TX, naranja en TX alternativa o inhibición. |
| AUTO de Port A | Alternancia. Habilita el seguimiento de banda en el Puerto A para que el conmutador siga automáticamente los cambios de banda de la radio. | Consulte [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Botones de antena de Port B | Haga clic para seleccionar una antena en el Puerto B; vuelva a hacer clic para anular la selección. | Misma lista de antenas que el Puerto A. Oculto si el dispositivo informa solo un puerto de radio. |
| Banda de Port B | Muestra la banda activa en el Puerto B. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena de Port B | Muestra el nombre de la antena seleccionada actualmente para el Puerto B. | Misma visualización de estado que la antena del Puerto A. |
| AUTO de Port B | Alternancia. Habilita el seguimiento de banda en el Puerto B. | Oculto cuando la sección Port B está oculta. |

## Consejos

- Una antena ya seleccionada en un puerto aparece deshabilitada y atenuada en la cuadrícula de botones del otro puerto. No puede asignar la misma antena a ambos puertos simultáneamente.
- Los botones de antena resaltados en ámbar están disponibles para recepción, pero no realizarán TX en la banda actual. Cambie a un botón azul antes de transmitir.

## Solución de problemas

- **La sección Port B no es visible**: el dispositivo conectado informa solo un puerto de radio. Port B se oculta automáticamente en este caso y no está disponible.
- **Los botones de antena no se muestran**: el dispositivo aún no está conectado o la lista de antenas no se ha cargado. Confirme que la etiqueta de estado muestra **Conectado —** y espere un momento a que se cargue la lista.
- **Hacer clic en un botón de antena no tiene efecto**: el botón puede estar deshabilitado porque esa antena ya está seleccionada en el otro puerto. Elija una antena diferente o anule la selección en el otro puerto primero.
- **Se descubre un dispositivo ShackSwitch pero no aparece en el applet Antenna Genius**: los dispositivos ShackSwitch están excluidos de la conexión automática en el applet Antenna Genius y son manejados por el applet ShackSwitch. Abra el applet ShackSwitch para conectarse a ese dispositivo.

## Relacionado

- [Antenna Genius overview](overview.md)
- [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Spot which antennas cannot TX on the current band (amber or dim)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
