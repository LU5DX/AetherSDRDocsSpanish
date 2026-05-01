# Seleccione una antena para el Puerto A o Puerto B

Use el applet Antenna Genius para asignar una antena específica al Puerto A o Puerto B en su conmutador 4O3A Antenna Genius. Esto le permite controlar qué antena física usa cada puerto de radio sin salir de AetherSDR.

## Antes de empezar

- El applet Antenna Genius debe estar visible. Se oculta hasta que se conecte o descubra un dispositivo. Vea [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe mostrar **Connected — \<nombre\> v\<versión\>** antes de que aparezcan los botones de antena.
- Abra el applet haciendo clic en el botón de bandeja **AG** en la barra lateral derecha.

## Pasos

1. Haga clic en el botón de bandeja **AG** para abrir el applet Antenna Genius.
2. Confirme que la etiqueta de estado muestra **Connected —** seguida del nombre del dispositivo y la versión.
3. Bajo el encabezado **Port A**, localice los botones de antena rellenados desde la lista de antenas del dispositivo.
4. Haga clic en el botón de la antena que desea asignar al Puerto A. El botón se resalta para indicar que está seleccionado.
5. Para deseleccionar la antena actual en el Puerto A, haga clic en el mismo botón nuevamente. El puerto vuelve a ninguna antena seleccionada (antena 0).
6. Si su dispositivo tiene dos puertos de radio, la sección **Port B** es visible debajo del separador. Repita los pasos 3–5 bajo el encabezado **Port B** para asignar una antena al Puerto B.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de antena del Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic nuevamente para deseleccionar. | Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX. Atenuado = sin permiso en la banda actual. Deshabilitado si la antena ya está seleccionada en el Puerto B. |
| Banda del Puerto A | Muestra la banda activa en el Puerto A, derivada de la frecuencia de radio. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del Puerto A | Muestra el nombre de la antena actualmente seleccionada para el Puerto A. | Muestra **\<ant\> TX:\<alt\>** cuando TX se enruta a una antena alternativa, y **\<ant\> [INHIBIT]** cuando se inhibe la transmisión. Se vuelve roja durante TX, naranja en TX alterno o inhibición. |
| Puerto A AUTO | Alternar. Habilita el seguimiento de banda en el Puerto A para que el conmutador siga automáticamente los cambios de banda de radio. | Vea [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Botones de antena del Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic nuevamente para deseleccionar. | Misma lista de antenas que el Puerto A. Oculto si el dispositivo reporta solo un puerto de radio. |
| Banda del Puerto B | Muestra la banda activa en el Puerto B. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del Puerto B | Muestra el nombre de la antena actualmente seleccionada para el Puerto B. | Mismo indicador de estado que la antena del Puerto A. |
| Puerto B AUTO | Alternar. Habilita el seguimiento de banda en el Puerto B. | Oculto cuando la sección Puerto B está oculta. |

## Consejos

- Una antena ya seleccionada en un puerto se deshabilita y atenúa en la cuadrícula de botones del otro puerto. No puede asignar la misma antena a ambos puertos simultáneamente.
- Los botones de antena resaltados en ámbar están disponibles para recepción pero no llevarán TX en la banda actual. Cambie a un botón azul antes de transmitir.

## Solución de problemas

- **La sección Puerto B no es visible** — El dispositivo conectado reporta solo un puerto de radio. El Puerto B se oculta automáticamente en este caso y no está disponible.
- **Los botones de antena no se muestran** — El dispositivo no está aún conectado, o la lista de antenas no se ha cargado. Confirme que la etiqueta de estado muestra **Connected —** y espere un momento a que se rellene la lista.
- **Hacer clic en un botón de antena no tiene efecto** — El botón puede estar deshabilitado porque esa antena ya está seleccionada en el otro puerto. Elija una antena diferente o deselecciónela en el otro puerto primero.
- **Se descubre un dispositivo ShackSwitch pero no aparece en el applet Antenna Genius** — Los dispositivos ShackSwitch se excluyen de la autoconexión en el applet Antenna Genius y se manejan mediante el applet ShackSwitch en su lugar. Abra el applet ShackSwitch para conectarse a ese dispositivo.

## Relacionado

- [Antenna Genius overview](overview.md)
- [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Spot which antennas cannot TX on the current band (amber or dim)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
