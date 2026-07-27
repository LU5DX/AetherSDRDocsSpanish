# Seleccionar una antena para el Puerto A o el Puerto B

Use la applet Antenna Genius para asignar una antena específica al Puerto A o al Puerto B de su conmutador 4O3A Antenna Genius. Esto le permite controlar qué antena física utiliza cada puerto de radio sin salir de AetherSDR.

## Antes de comenzar

- La applet Antenna Genius debe estar visible. Está oculta hasta que se conecte o descubra un dispositivo. Consulte [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe mostrar **Connected — \<nombre\> v\<versión\>** antes de que aparezcan los botones de antena.
- Abra la applet haciendo clic en el botón de la bandeja **AG** en la barra lateral derecha.

## Pasos

1. Haga clic en el botón de la bandeja **AG** para abrir la applet Antenna Genius.
2. Confirme que la etiqueta de estado muestra **Connected —** seguido del nombre del dispositivo y la versión.
3. Bajo el encabezado **Port A**, localice los botones de antena que se completan desde la lista de antenas del dispositivo.
4. Haga clic en el botón de la antena que desea asignar al Puerto A. El botón se resalta para indicar que está seleccionado.
5. Para deseleccionar la antena actual en el Puerto A, vuelva a hacer clic en el mismo botón. El puerto vuelve al estado sin antena seleccionada (antena 0).
6. Si su dispositivo tiene dos puertos de radio, la sección **Port B** es visible debajo del separador. Repita los pasos 3 a 5 bajo el encabezado **Port B** para asignar una antena al Puerto B.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Device combo | Selecciona a qué dispositivo AG descubierto conectarse. | Selecciona y conecta automáticamente cuando se descubre el primer dispositivo. |
| Connect / Disconnect | Conecta al dispositivo seleccionado (o a la IP manual si no hay ninguno seleccionado); cambia a "Disconnect" cuando está conectado. | La etiqueta predeterminada es "Connect". Cuando está desconectado, las cuadrículas de botones de antena se limpian. |
| Manual IP | Ingrese una dirección IPv4/IPv6 y presione Enter para conectarse al puerto 9007. | Las direcciones no válidas producen un estado rojo "Invalid IP address". La configuración se guarda como `AG_ManualIp`. |
| Port A antenna buttons | Haga clic para seleccionar una antena en el Puerto A; haga clic de nuevo para deseleccionar. | Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX. Atenuado = sin permiso en la banda actual. Deshabilitado si la antena ya está seleccionada en el Puerto B. |
| Port A band | Muestra la banda activa en el Puerto A, derivada de la frecuencia de radio. | Muestra **—** cuando no se identifica ninguna banda. |
| Port A antenna | Muestra el nombre de la antena actualmente seleccionada para el Puerto A. | Muestra **\<ant\>  TX:\<alt\>** cuando la TX está enrutada a una antena alternativa, y **\<ant\> [INHIBIT]** cuando la transmisión está inhibida. Se vuelve rojo durante TX, naranja en TX alternativa o inhibición. |
| Port A AUTO | Alternancia. Habilita el seguimiento de banda en el Puerto A para que el conmutador rastree automáticamente los cambios de banda de radio. | Consulte [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Port B antenna buttons | Haga clic para seleccionar una antena en el Puerto B; haga clic de nuevo para deseleccionar. | Misma lista de antenas que el Puerto A. Oculto si el dispositivo informa solo un puerto de radio. |
| Port B band | Muestra la banda activa en el Puerto B. | Muestra **—** cuando no se identifica ninguna banda. |
| Port B antenna | Muestra el nombre de la antena actualmente seleccionada para el Puerto B. | Misma visualización de estado que la antena del Puerto A. |
| Port B AUTO | Alternancia. Habilita el seguimiento de banda en el Puerto B. | Oculto cuando la sección del Puerto B está oculta. |

## Consejos

- Una antena ya seleccionada en un puerto aparece deshabilitada y atenuada en la cuadrícula de botones del otro puerto. No puede asignar la misma antena a ambos puertos simultáneamente.
- Los botones de antena resaltados en ámbar están disponibles para recepción pero no transmitirán en la banda actual. Cambie a un botón azul antes de transmitir.
- Al desconectarse de un dispositivo, las cuadrículas de botones de antena se limpian y la pantalla se restablece. Los botones de antena se vuelven a completar automáticamente cuando se reconecta.

## Solución de problemas

- **La sección Port B no es visible** — El dispositivo conectado informa solo un puerto de radio. El Puerto B se oculta automáticamente en este caso y no está disponible. La visibilidad del Puerto B se actualiza dinámicamente cuando se determina el número de puertos de radio del dispositivo, ya sea desde la respuesta de información del dispositivo (para conexiones IP manuales) o desde un beacon UDP (para dispositivos descubiertos).
- **Los botones de antena no se muestran** — El dispositivo aún no está conectado, o la lista de antenas no se ha cargado. Confirme que la etiqueta de estado muestra **Connected —** y espere un momento a que la lista se complete. AetherSDR ahora evita limpiar la cuadrícula de botones si la lista de antenas aún no se ha cargado, por lo que los botones permanecen visibles si se mostraban previamente.
- **Hacer clic en un botón de antena no tiene efecto** — El botón puede estar deshabilitado porque esa antena ya está seleccionada en el otro puerto. Elija una antena diferente o deselecciónela primero en el otro puerto.
- **Se descubre un dispositivo ShackSwitch pero no aparece en la applet Antenna Genius** — Los dispositivos ShackSwitch están excluidos de la conexión automática en la applet Antenna Genius y son gestionados por la applet ShackSwitch en su lugar. Abra la applet ShackSwitch para conectarse a ese dispositivo.
- **La etiqueta de estado muestra "Invalid IP address"** — La dirección ingresada en el campo Manual IP no es una dirección IPv4 o IPv6 válida.

## Relacionados

- [Antenna Genius overview](overview.md)
- [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Spot which antennas cannot TX on the current band (amber or dim)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
