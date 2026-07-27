# Habilitar el modo AUTO para que el AG siga los cambios de banda del equipo

El modo AUTO le indica al Antenna Genius que rastree la banda activa de su equipo y cambie las antenas automáticamente. Esto elimina la necesidad de seleccionar manualmente una antena cada vez que cambie de banda.

## Antes de comenzar

- El applet del Antenna Genius debe ser visible. Está oculto hasta que se descubre o se conecta manualmente un dispositivo. Use el botón de la bandeja AG en la barra lateral derecha para abrirlo.
- El applet debe mostrar un estado "Connected — \<nombre\> v\<versión\>". El modo AUTO no tiene efecto cuando está desconectado.

## Pasos

1. Haga clic en el botón de la bandeja AG en la barra lateral derecha para abrir el applet del Antenna Genius.
2. Confirme que la etiqueta de estado diga "Connected — \<nombre\> v\<versión\>".
3. Para habilitar el seguimiento de banda en el Puerto A, haga clic en **AUTO** debajo de los botones de antena del Puerto A. El botón se ilumina en verde cuando está activo.
4. Para habilitar el seguimiento de banda en el Puerto B, haga clic en **AUTO** debajo de los botones de antena del Puerto B. El botón se ilumina en verde cuando está activo.
   - La sección del Puerto B está oculta si el dispositivo conectado reporta solo un puerto de equipo. Esto se determina a partir de la respuesta de información del dispositivo (al conectar mediante IP manual) o de la baliza UDP (en descubrimiento automático).
5. Para deshabilitar el modo AUTO en cualquier puerto, haga clic nuevamente en el botón **AUTO** iluminado. Este vuelve a su estado apagado y el puerto regresa a la selección manual de antena.

## Función de cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Desplegable de dispositivo | Selecciona a qué dispositivo AG descubierto conectarse. Se autoselecciona y conecta cuando se descubre el primer dispositivo. | vacío |
| Connect / Disconnect | Se conecta al dispositivo seleccionado (o a la IP manual si no hay ninguno seleccionado); se vuelve "Disconnect" cuando está conectado. | Connect |
| IP manual | Ingrese una IP y presione Enter para conectarse al puerto 9007. Las direcciones inválidas producen un estado rojo "Invalid IP address". | vacío |
| Botones de antena del Puerto A | Haga clic para seleccionar una antena en el Puerto A; haga clic nuevamente para anular la selección (antena=0). Deshabilitados/atenuados si la antena ya está seleccionada en el Puerto B. Azul = TX+RX, ámbar = solo RX, atenuado = sin permiso en la banda actual. | ninguno |
| Puerto A AUTO | Alterna el seguimiento de banda en el Puerto A. Cuando está activo, el AG selecciona la antena para el Puerto A según la banda actual del equipo. | Off |
| Botones de antena del Puerto B | Haga clic para seleccionar una antena en el Puerto B; haga clic nuevamente para anular la selección. La sección del Puerto B está oculta si el dispositivo AG reporta solo un puerto de equipo. | ninguno |
| Puerto B AUTO | Alterna el seguimiento de banda en el Puerto B. Cuando está activo, el AG selecciona la antena para el Puerto B según la banda actual del equipo. Oculto en dispositivos de un solo puerto. | Off |

## Significado de cada indicador

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de estado | "No device found", "Device found", "Connected — \<nombre\> v\<versión\>", "Disconnected", "Error: \<msg\>", "Invalid IP address" | Estado de descubrimiento/conexión del Antenna Genius. |
| Banda del Puerto A | Nombre de banda o "—" | Banda activa en el Puerto A (reportada por el AG o derivada de la frecuencia). |
| Antena del Puerto A | Nombre de antena, "\<ant\> TX:\<alt\>", "\<ant\> [INHIBIT]", "—" | Antena seleccionada; rojo al transmitir, naranja cuando TX se enruta a una antena alternativa o se afirma el inhibidor. |
| Banda del Puerto B | Nombre de banda o "—" | Banda activa en el Puerto B. |
| Antena del Puerto B | Nombre de antena, "\<ant\> TX:\<alt\>", "\<ant\> [INHIBIT]", "—" | Antena seleccionada para el Puerto B. |

## Qué cambia al desconectar

Cuando se desconecta de un dispositivo Antenna Genius, todos los botones de antena se borran de la cuadrícula y las listas se vacían. Esto asegura que la visualización y el modelo interno permanezcan coherentes mientras está desconectado. Al reconectar, los botones de antena se reconstruyen automáticamente.

## Consejos

- Puede ejecutar AUTO en un puerto y seleccionar antenas manualmente en el otro. Los dos puertos son independientes.
- Cuando AUTO está activo, los indicadores de banda del Puerto A y del Puerto B se actualizan mientras sintoniza entre bandas, confirmando que el AG está rastreando correctamente.
- La visibilidad del Puerto B se actualiza automáticamente cuando se recibe la información del dispositivo, ya sea desde una baliza UDP o una conexión IP manual.

## Solución de problemas

- **El botón AUTO no responde a los clics** — El applet no está conectado. Verifique que la etiqueta de estado diga "Connected — \<nombre\> v\<versión\>" antes de habilitar AUTO. Si no está conectado, consulte las páginas a continuación.
- **El indicador de banda muestra "—" después de habilitar AUTO** — El AG aún no ha recibido un informe de banda del equipo. Sintonice una frecuencia dentro de una banda reconocida para activar una actualización.
- **Aparece un dispositivo ShackSwitch en el desplegable de dispositivo pero el applet no se conecta automáticamente a él** — Los dispositivos ShackSwitch son manejados por un applet separado y se omiten intencionalmente durante la autoconexión del Antenna Genius. Use el applet ShackSwitch para conectarse a ese dispositivo.
- **Faltan botones de antena después de reconectar** — Esto es normal y esperado. Los botones se borran al desconectar y se reconstruyen cuando el dispositivo se vuelve a conectar. Si no reaparecen, verifique que la conexión fue exitosa.
- **La sección del Puerto B está oculta cuando espera dos puertos** — El dispositivo puede haber reportado solo un puerto de equipo. Esta información se obtiene de la respuesta de información del dispositivo (ruta IP manual) o de la baliza UDP (ruta de descubrimiento automático). Verifique que el dispositivo soporte dos puertos de equipo.

## Relacionados

- [Antenna Genius overview](overview.md)
- [Auto-discover an Antenna Genius on the LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Manually connect to an AG over a remote network](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Select an antenna for Port A or Port B](select-an-antenna-for-port-a-or-port-b.md)
