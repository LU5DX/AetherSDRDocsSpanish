# Seleccionar una antena para el puerto A o el puerto B

Use el applet Antenna Genius para asignar una antena específica al puerto A o al puerto B de su conmutador 4O3A Antenna Genius. Esto le permite controlar qué antena física utiliza cada puerto de radio sin salir de AetherSDR.

## Antes de comenzar

- El applet Antenna Genius debe estar visible. Está oculto hasta que se conecte o descubra un dispositivo. Consulte [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe indicar **Connected — \<nombre\> v\<versión\>** antes de que aparezcan los botones de antena.
- Abra el applet haciendo clic en el botón de bandeja **AG** en la barra lateral derecha.

## Pasos

1. Haga clic en el botón de bandeja **AG** para abrir el applet Antenna Genius.
2. Confirme que la etiqueta de estado indique **Connected —** seguido del nombre y la versión del dispositivo.
3. Bajo el encabezado **Port A**, localice los botones de antena generados a partir de la lista de antenas del dispositivo.
4. Haga clic en el botón de la antena que desea asignar al puerto A. El botón se resalta para indicar que está seleccionado.
5. Para anular la selección de la antena actual en el puerto A, haga clic en el mismo botón nuevamente. El puerto vuelve al estado sin antena seleccionada (antena 0).
6. Si su dispositivo tiene dos puertos de radio, la sección **Port B** es visible debajo del separador. Repita los pasos 3–5 bajo el encabezado **Port B** para asignar una antena al puerto B.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Lista desplegable de dispositivos | Selecciona a qué dispositivo AG descubierto conectarse. | Se autoselecciona y conecta cuando se descubre el primer dispositivo. |
| Conectar / Desconectar | Conecta al dispositivo seleccionado (o a la IP manual si no hay ninguno seleccionado); cambia a "Desconectar" cuando está conectado. | La etiqueta predeterminada es "Conectar". |
| IP manual | Ingrese una dirección IPv4/IPv6 y presione Enter para conectarse al puerto 9007. | Las direcciones inválidas producen un estado rojo "Invalid IP address". La configuración se guarda como `AG_ManualIp`. |
| Botones de antena del puerto A | Haga clic para seleccionar una antena en el puerto A; haga clic nuevamente para anular la selección. | Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX. Atenuado = sin permiso en la banda actual. Deshabilitado si la antena ya está seleccionada en el puerto B. |
| Banda del puerto A | Muestra la banda activa en el puerto A, derivada de la frecuencia de radio. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del puerto A | Muestra el nombre de la antena actualmente seleccionada para el puerto A. | Muestra **\<ant\>  TX:\<alt\>** cuando la TX se enruta a una antena alternativa, y **\<ant\> [INHIBIT]** cuando la transmisión está inhibida. Se vuelve rojo durante TX, naranja en TX alternativa o inhibición. |
| AUTO del puerto A | Alternancia. Activa el seguimiento de banda en el puerto A para que el conmutador rastree automáticamente los cambios de banda de la radio. | Consulte [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Botones de antena del puerto B | Haga clic para seleccionar una antena en el puerto B; haga clic nuevamente para anular la selección. | Misma lista de antenas que el puerto A. Oculto si el dispositivo reporta solo un puerto de radio. |
| Banda del puerto B | Muestra la banda activa en el puerto B. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del puerto B | Muestra el nombre de la antena actualmente seleccionada para el puerto B. | Misma visualización de estado que la antena del puerto A. |
| AUTO del puerto B | Alternancia. Activa el seguimiento de banda en el puerto B. | Oculto cuando la sección del puerto B está oculta. |

## Consejos

- Una antena ya seleccionada en un puerto aparece deshabilitada y atenuada en la cuadrícula de botones del otro puerto. No puede asignar la misma antena a ambos puertos simultáneamente.
- Los botones de antena resaltados en ámbar están disponibles para recepción pero no transmitirán en la banda actual. Cambie a un botón azul antes de transmitir.

## Solución de problemas

- **La sección del puerto B no es visible** — El dispositivo conectado reporta solo un puerto de radio. El puerto B se oculta automáticamente en este caso y no está disponible.
- **Los botones de antena no se muestran** — El dispositivo aún no está conectado, o la lista de antenas no se ha cargado. Confirme que la etiqueta de estado indique **Connected —** y espere un momento para que la lista se cargue.
- **Hacer clic en un botón de antena no tiene efecto** — El botón puede estar deshabilitado porque esa antena ya está seleccionada en el otro puerto. Elija una antena diferente o anule la selección en el otro puerto primero.
- **Se descubre un dispositivo ShackSwitch pero no aparece en el applet Antenna Genius** — Los dispositivos ShackSwitch están excluidos de la conexión automática en el applet Antenna Genius y son manejados por el applet ShackSwitch. Abra el applet ShackSwitch para conectarse a ese dispositivo.
- **La etiqueta de estado muestra "Invalid IP address"** — La dirección ingresada en el campo de IP manual no es una dirección IPv4 o IPv6 válida.

## Relacionados

- [Antenna Genius overview](overview.md)
- [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Spot which antennas cannot TX on the current band (amber or dim)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
