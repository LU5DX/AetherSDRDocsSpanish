# Activar el modo AUTO para que el AG siga los cambios de banda de la radio

El modo AUTO indica al Antenna Genius que rastree la banda activa de su radio y cambie las antenas automáticamente. Esto elimina la necesidad de seleccionar manualmente una antena cada vez que cambia de banda.

## Antes de comenzar

- El applet de Antenna Genius debe estar visible. Está oculto hasta que se descubre un dispositivo o se conecta manualmente. Use el botón de la bandeja AG en la barra lateral derecha para abrirlo.
- El applet debe mostrar un estado "Connected — \<nombre\> v\<versión\>". El modo AUTO no tiene efecto cuando está desconectado.

## Pasos

1. Haga clic en el botón de la bandeja AG en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Confirme que la etiqueta de estado muestre "Connected — \<nombre\> v\<versión\>".
3. Para habilitar el seguimiento de banda en el Puerto A, haga clic en **AUTO** debajo de los botones de antena del Puerto A. El botón se resalta en verde cuando está activo.
4. Para habilitar el seguimiento de banda en el Puerto B, haga clic en **AUTO** debajo de los botones de antena del Puerto B. El botón se resalta en verde cuando está activo.
   - La sección del Puerto B está oculta si el dispositivo conectado informa solo un puerto de radio.
5. Para deshabilitar el modo AUTO en cualquier puerto, haga clic nuevamente en el botón **AUTO** iluminado. Vuelve a su estado sin iluminación y el puerto regresa a la selección manual de antena.

## Función de cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Port A AUTO | Activa/desactiva el seguimiento de banda en el Puerto A. Cuando está activo, el AG selecciona la antena para el Puerto A según la banda actual de la radio. | Desactivado |
| Port B AUTO | Activa/desactiva el seguimiento de banda en el Puerto B. Cuando está activo, el AG selecciona la antena para el Puerto B según la banda actual de la radio. Oculto en dispositivos de un solo puerto. | Desactivado |

## Consejos

- Puede ejecutar AUTO en un puerto y seleccionar antenas manualmente en el otro. Los dos puertos son independientes.
- Cuando AUTO está activo, los indicadores de banda del Puerto A y del Puerto B se actualizan mientras sintoniza entre bandas, lo que confirma que el AG está rastreando correctamente.

## Solución de problemas

- **El botón AUTO no responde a los clics** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected — \<nombre\> v\<versión\>" antes de habilitar AUTO. Si no está conectado, consulte las páginas siguientes.
- **El indicador de banda muestra "—" después de habilitar AUTO** — El AG aún no ha recibido un informe de banda de la radio. Sintonice una frecuencia dentro de una banda reconocida para activar una actualización.
- **Aparece un dispositivo ShackSwitch en el combo de dispositivos, pero el applet no se conecta automáticamente a él** — Los dispositivos ShackSwitch son gestionados por un applet separado y se omiten intencionalmente durante la conexión automática de Antenna Genius. Use el applet de ShackSwitch para conectarse a ese dispositivo.

## Relacionado

- [Descripción general de Antenna Genius](overview.md)
- [Descubrimiento automático de un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o el Puerto B](select-an-antenna-for-port-a-or-port-b.md)
