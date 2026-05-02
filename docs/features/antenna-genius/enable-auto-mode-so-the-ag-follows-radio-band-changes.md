# Habilitar el modo AUTO para que el AG siga los cambios de banda del radio

El modo AUTO le indica al Antenna Genius que rastree la banda activa de su radio y cambie las antenas automáticamente. Esto elimina la necesidad de seleccionar manualmente una antena cada vez que cambia de banda.

## Antes de comenzar

- El applet de Antenna Genius debe estar visible. Permanece oculto hasta que se descubre un dispositivo o se conecta manualmente. Use el botón de bandeja AG en la barra lateral derecha para abrirlo.
- El applet debe mostrar el estado "Connected — \<name\> v\<version\>". El modo AUTO no tiene efecto cuando está desconectado.

## Pasos

1. Haga clic en el botón de bandeja AG en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Confirme que la etiqueta de estado muestre "Connected — \<name\> v\<version\>".
3. Para habilitar el seguimiento de banda en el Puerto A, haga clic en **AUTO** bajo los botones de antena del Puerto A. El botón se resalta en verde cuando está activo.
4. Para habilitar el seguimiento de banda en el Puerto B, haga clic en **AUTO** bajo los botones de antena del Puerto B. El botón se resalta en verde cuando está activo.
   - La sección del Puerto B se oculta si el dispositivo conectado reporta solo un puerto de radio.
5. Para deshabilitar el modo AUTO en cualquier puerto, haga clic nuevamente en el botón **AUTO** encendido. Vuelve a su estado apagado y el puerto regresa a la selección manual de antena.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Puerto A AUTO | Activa o desactiva el seguimiento de banda en el Puerto A. Cuando está activo, el AG selecciona la antena para el Puerto A según la banda actual del radio. | Apagado |
| Puerto B AUTO | Activa o desactiva el seguimiento de banda en el Puerto B. Cuando está activo, el AG selecciona la antena para el Puerto B según la banda actual del radio. Oculto en dispositivos de un solo puerto. | Apagado |

## Consejos

- Puede ejecutar AUTO en un puerto y seleccionar antenas manualmente en el otro. Los dos puertos son independientes.
- Cuando AUTO está activo, los indicadores de banda del Puerto A y del Puerto B se actualizan a medida que sintoniza distintas bandas, confirmando que el AG está rastreando correctamente.

## Solución de problemas

- **El botón AUTO no responde a los clics** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected — \<name\> v\<version\>" antes de habilitar AUTO. Si no está conectado, consulte las páginas a continuación.
- **El indicador de banda muestra "—" después de habilitar AUTO** — El AG aún no ha recibido un reporte de banda del radio. Sintonice una frecuencia dentro de una banda reconocida para activar una actualización.
- **Un dispositivo ShackSwitch aparece en el combo de dispositivos pero el applet no se conecta automáticamente a él** — Los dispositivos ShackSwitch son manejados por un applet separado y se omiten intencionalmente durante la conexión automática del Antenna Genius. Use el applet de ShackSwitch para conectarse a ese dispositivo.

## Relacionados

- [Descripción general del Antenna Genius](overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o el Puerto B](select-an-antenna-for-port-a-or-port-b.md)
