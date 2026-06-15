# Seleccionar una antena para el Puerto A o el Puerto B

Use el applet Antenna Genius para asignar una antena específica al Puerto A o al Puerto B de su conmutador 4O3A Antenna Genius. Esto le permite controlar qué antena física utiliza cada puerto de radio sin salir de AetherSDR.

## Antes de comenzar

- El applet Antenna Genius debe estar visible. Está oculto hasta que se conecta o descubre un dispositivo. Consulte [Auto-descubrir un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe indicar **Conectado — \<nombre\> v\<versión\>** antes de que aparezcan los botones de antena.
- Abra el applet haciendo clic en el botón de bandeja **AG** en la barra lateral derecha.

## Pasos

1. Haga clic en el botón de bandeja **AG** para abrir el applet Antenna Genius.
2. Confirme que la etiqueta de estado indique **Conectado —** seguido del nombre y la versión del dispositivo.
3. Bajo el encabezado **Port A**, localice los botones de antena que se poblaron desde la lista de antenas del dispositivo.
4. Haga clic en el botón de la antena que desea asignar al Puerto A. El botón se resalta para mostrar que está seleccionado.
5. Para anular la selección de la antena actual en el Puerto A, haga clic en el mismo botón nuevamente. El puerto vuelve al estado sin antena seleccionada (antena 0).
6. Si su dispositivo tiene dos puertos de radio, la sección **Port B** es visible debajo del separador. Repita los pasos 3–5 bajo el encabezado **Port B** para asignar una antena al Puerto B.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Lista desplegable de dispositivos | Selecciona a qué dispositivo AG descubierto conectarse. | Selecciona y conecta automáticamente cuando se descubre el primer dispositivo. |
| Conectar / Desconectar | Conecta al dispositivo seleccionado (o a la IP manual si no hay ninguno seleccionado); cambia a "Desconectar" cuando está conectado. | La etiqueta predeterminada es "Conectar". Cuando está desconectado, las cuadrículas de botones de antena se borran. |
| IP manual | Ingrese una dirección IPv4/IPv6 y presione Enter para conectarse al puerto 9007. | Las direcciones no válidas producen un estado rojo "Dirección IP no válida". La configuración se guarda como `AG_ManualIp`. |
| Botones de antena del Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic nuevamente para anular la selección. | Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX. Atenuado = sin permiso en la banda actual. Deshabilitado si la antena ya está seleccionada en el Puerto B. |
| Banda del Puerto A | Muestra la banda activa en el Puerto A, derivada de la frecuencia de la radio. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del Puerto A | Muestra el nombre de la antena actualmente seleccionada para el Puerto A. | Muestra **\<ant\> TX:\<alt\>** cuando la TX se enruta a una antena alternativa, y **\<ant\> [INHIBIR]** cuando la transmisión está inhibida. Se vuelve rojo durante TX, naranja en TX alternativa o inhibición. |
| AUTO del Puerto A | Alternancia. Habilita el seguimiento de banda en el Puerto A para que el conmutador siga automáticamente los cambios de banda de la radio. | Consulte [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md). |
| Botones de antena del Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic nuevamente para anular la selección. | Misma lista de antenas que el Puerto A. Oculto si el dispositivo informa solo un puerto de radio. |
| Banda del Puerto B | Muestra la banda activa en el Puerto B. | Muestra **—** cuando no se identifica ninguna banda. |
| Antena del Puerto B | Muestra el nombre de la antena actualmente seleccionada para el Puerto B. | Misma visualización de estado que la antena del Puerto A. |
| AUTO del Puerto B | Alternancia. Habilita el seguimiento de banda en el Puerto B. | Oculto cuando la sección del Puerto B está oculta. |

## Consejos

- Una antena ya seleccionada en un puerto aparece deshabilitada y atenuada en la cuadrícula de botones del otro puerto. No puede asignar la misma antena a ambos puertos simultáneamente.
- Los botones de antena resaltados en ámbar están disponibles para recepción pero no transportarán TX en la banda actual. Cambie a un botón azul antes de transmitir.
- Al desconectarse de un dispositivo, las cuadrículas de botones de antena se borran y la pantalla se reinicia. Los botones de antena se vuelven a poblar automáticamente cuando se reconecta.

## Solución de problemas

- **La sección del Puerto B no es visible** — El dispositivo conectado informa solo un puerto de radio. El Puerto B se oculta automáticamente en este caso y no está disponible.
- **Los botones de antena no se muestran** — El dispositivo aún no está conectado o la lista de antenas no se ha cargado. Confirme que la etiqueta de estado indique **Conectado —** y espere un momento a que la lista se complete. AetherSDR ahora evita borrar la cuadrícula de botones si la lista de antenas aún no se ha cargado, por lo que los botones permanecen visibles si se mostraban anteriormente.
- **Hacer clic en un botón de antena no tiene efecto** — El botón puede estar deshabilitado porque esa antena ya está seleccionada en el otro puerto. Elija una antena diferente o anule la selección en el otro puerto primero.
- **Se descubre un dispositivo ShackSwitch pero no aparece en el applet Antenna Genius** — Los dispositivos ShackSwitch se excluyen de la conexión automática en el applet Antenna Genius y son manejados por el applet ShackSwitch. Abra el applet ShackSwitch para conectarse a ese dispositivo.
- **La etiqueta de estado muestra "Dirección IP no válida"** — La dirección ingresada en el campo de IP manual no es una dirección IPv4 o IPv6 válida.

## Relacionados

- [Resumen de Antenna Genius](overview.md)
- [Auto-descubrir un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Identificar qué antenas no pueden transmitir en la banda actual (ámbar o atenuadas)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Intercambiar radios que comparten el AG (antenas en uso por el otro puerto están bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
