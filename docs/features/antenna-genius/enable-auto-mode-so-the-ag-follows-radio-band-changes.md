# Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio

El modo AUTO indica al Antenna Genius que rastree la banda activa de su radio y cambie las antenas automáticamente. Esto elimina la necesidad de seleccionar manualmente una antena cada vez que cambia de banda.

## Antes de comenzar

- El applet de Antenna Genius debe estar visible. Está oculto hasta que se descubre o conecta manualmente un dispositivo. Use el botón de bandeja AG en la barra lateral derecha para abrirlo.
- El applet debe mostrar un estado "Connected — \<nombre\> v\<versión\>". El modo AUTO no tiene efecto cuando está desconectado.

## Pasos

1. Haga clic en el botón de bandeja AG en la barra lateral derecha para abrir el applet Antenna Genius.
2. Confirme que la etiqueta de estado muestre "Connected — \<nombre\> v\<versión\>".
3. Para habilitar el seguimiento de banda en el Puerto A, haga clic en **AUTO** debajo de los botones de antena del Puerto A. El botón se ilumina en verde cuando está activo.
4. Para habilitar el seguimiento de banda en el Puerto B, haga clic en **AUTO** debajo de los botones de antena del Puerto B. El botón se ilumina en verde cuando está activo.
   - La sección del Puerto B está oculta si el dispositivo conectado informa solo un puerto de radio.
5. Para deshabilitar el modo AUTO en cualquier puerto, haga clic nuevamente en el botón **AUTO** iluminado. Vuelve a su estado apagado y el puerto revierte a la selección manual de antena.

## Función de cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Combo de dispositivo | Selecciona a qué dispositivo AG descubierto conectarse. Se autoselecciona y conecta cuando se descubre el primer dispositivo. | vacío |
| Connect / Disconnect | Se conecta al dispositivo seleccionado (o a la IP manual si no hay ninguno seleccionado); cambia a "Disconnect" cuando está conectado. | Connect |
| Manual IP | Ingrese una IP y presione Enter para conectarse al puerto 9007. Las direcciones inválidas muestran un estado rojo "Invalid IP address". | vacío |
| Botones de antena Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic nuevamente para deseleccionar (antena=0). Deshabilitados/atenuados si la antena ya está seleccionada en el Puerto B. Azul = TX+RX, ámbar = solo RX, atenuado = sin permiso en la banda actual. | ninguno |
| Puerto A AUTO | Activa/desactiva el seguimiento de banda en el Puerto A. Cuando está activo, el AG selecciona la antena para el Puerto A según la banda actual de la radio. | Desactivado |
| Botones de antena Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic nuevamente para deseleccionar. La sección del Puerto B está oculta si el dispositivo AG informa solo un puerto de radio. | ninguno |
| Puerto B AUTO | Activa/desactiva el seguimiento de banda en el Puerto B. Cuando está activo, el AG selecciona la antena para el Puerto B según la banda actual de la radio. Oculto en dispositivos de un solo puerto. | Desactivado |

## Significado de cada indicador

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de estado | "No device found", "Device found", "Connected — \<nombre\> v\<versión\>", "Disconnected", "Error: \<msg\>", "Invalid IP address" | Estado de descubrimiento/conexión del Antenna Genius. |
| Banda Puerto A | Nombre de banda o "—" | Banda activa en el Puerto A (reportada por el AG o derivada de la frecuencia). |
| Antena Puerto A | Nombre de antena, "\<ant\> TX:\<alt\>", "\<ant\> [INHIBIT]", "—" | Antena seleccionada; rojo al transmitir, naranja cuando TX se enruta a antena alternativa o hay inhibición activa. |
| Banda Puerto B | Nombre de banda o "—" | Banda activa en el Puerto B. |
| Antena Puerto B | Nombre de antena, "\<ant\> TX:\<alt\>", "\<ant\> [INHIBIT]", "—" | Antena seleccionada para el Puerto B. |

## Cambios al desconectar

Cuando se desconecta de un dispositivo Antenna Genius, todos los botones de antena se eliminan de la cuadrícula y las listas se vacían. Esto asegura que la pantalla y el modelo interno permanezcan coherentes mientras está desconectado. Cuando se reconecta, los botones de antena se reconstruyen automáticamente.

## Consejos

- Puede ejecutar AUTO en un puerto y seleccionar antenas manualmente en el otro. Los dos puertos son independientes.
- Cuando AUTO está activo, los indicadores de banda del Puerto A y Puerto B se actualizan mientras sintoniza a través de las bandas, confirmando que el AG está rastreando correctamente.

## Solución de problemas

- **El botón AUTO no responde a los clics** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected — \<nombre\> v\<versión\>" antes de habilitar AUTO. Si no está conectado, consulte las páginas a continuación.
- **El indicador de banda muestra "—" después de habilitar AUTO** — El AG aún no ha recibido un informe de banda de la radio. Sintonice una frecuencia dentro de una banda reconocida para activar una actualización.
- **Aparece un dispositivo ShackSwitch en el combo de dispositivo pero el applet no se conecta automáticamente a él** — Los dispositivos ShackSwitch son manejados por un applet separado y se omiten intencionalmente durante la autoconexión de Antenna Genius. Use el applet ShackSwitch para conectarse a ese dispositivo.
- **Faltan botones de antena después de reconectar** — Esto es normal y esperado. Los botones se borran al desconectar y se reconstruyen cuando el dispositivo se conecta nuevamente. Si no reaparecen, verifique que la conexión fue exitosa.

## Relacionado

- [Antenna Genius overview](overview.md)
- [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Select an antenna for Port A or Port B](select-an-antenna-for-port-a-or-port-b.md)
