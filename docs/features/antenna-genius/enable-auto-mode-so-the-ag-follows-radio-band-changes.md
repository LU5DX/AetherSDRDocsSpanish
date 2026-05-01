# Activar el modo AUTO para que el Antenna Genius siga los cambios de banda de radio

El modo AUTO le indica al Antenna Genius que rastree la banda activa de su radio y cambie las antenas automáticamente. Esto elimina la necesidad de seleccionar manualmente una antena cada vez que cambia de banda.

## Antes de comenzar

- El applet Antenna Genius debe estar visible. Permanece oculto hasta que se detecta un dispositivo o se conecta manualmente. Utilice el botón AG tray en la barra lateral derecha para abrirlo.
- El applet debe mostrar un estado "Connected — \<name\> v\<version\>". El modo AUTO no tiene efecto cuando está desconectado.

## Pasos

1. Haga clic en el botón AG tray en la barra lateral derecha para abrir el applet Antenna Genius.
2. Confirme que la etiqueta de estado muestre "Connected — \<name\> v\<version\>".
3. Para activar el seguimiento de banda en el Puerto A, haga clic en **AUTO** debajo de los botones de antena del Puerto A. El botón se resalta en verde cuando está activo.
4. Para activar el seguimiento de banda en el Puerto B, haga clic en **AUTO** debajo de los botones de antena del Puerto B. El botón se resalta en verde cuando está activo.
   - La sección Puerto B está oculta si el dispositivo conectado reporta solo un puerto de radio.
5. Para desactivar el modo AUTO en cualquier puerto, haga clic nuevamente en el botón **AUTO** encendido. Vuelve a su estado apagado y el puerto revierte a la selección manual de antenas.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Puerto A AUTO | Activa/desactiva el seguimiento de banda en el Puerto A. Cuando está activo, el AG selecciona la antena para el Puerto A según la banda actual de la radio. | Desactivado |
| Puerto B AUTO | Activa/desactiva el seguimiento de banda en el Puerto B. Cuando está activo, el AG selecciona la antena para el Puerto B según la banda actual de la radio. Oculto en dispositivos de un solo puerto. | Desactivado |

## Consejos

- Puede ejecutar AUTO en un puerto y seleccionar antenas manualmente en el otro. Los dos puertos son independientes.
- Cuando AUTO está activo, los indicadores de banda del Puerto A y Puerto B se actualizan mientras sintoniza entre bandas, confirmando que el AG está rastreando correctamente.

## Resolución de problemas

- **El botón AUTO no responde a los clics** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected — \<name\> v\<version\>" antes de activar AUTO. Si no está conectado, consulte las páginas a continuación.
- **El indicador de banda muestra "—" después de activar AUTO** — El AG aún no ha recibido un reporte de banda de la radio. Sintonice una frecuencia dentro de una banda reconocida para activar una actualización.
- **Un dispositivo ShackSwitch aparece en el combo Device pero el applet no se conecta automáticamente a él** — Los dispositivos ShackSwitch se manejan mediante un applet separado y se omiten intencionalmente durante la conexión automática de Antenna Genius. Utilice el applet ShackSwitch para conectarse a ese dispositivo.

## Relacionado

- [Descripción general del Antenna Genius](overview.md)
- [Detectar automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o Puerto B](select-an-antenna-for-port-a-or-port-b.md)
