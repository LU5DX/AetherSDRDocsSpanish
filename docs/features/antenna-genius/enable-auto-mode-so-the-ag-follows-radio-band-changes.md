# Activar el modo AUTO para que el AG siga los cambios de banda del radio

El modo AUTO indica al Antenna Genius que rastree la banda activa de su radio y cambie las antenas automáticamente. Esto elimina la necesidad de seleccionar una antena manualmente cada vez que cambia de banda.

## Antes de comenzar

- El applet de Antenna Genius debe estar visible. Permanece oculto hasta que se descubre un dispositivo o se conecta manualmente. Use el botón del AG en la barra lateral derecha para abrirlo.
- El applet debe mostrar el estado "Connected — \<name\> v\<version\>". El modo AUTO no tiene efecto cuando está desconectado.

## Pasos

1. Haga clic en el botón del AG en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Confirme que la etiqueta de estado muestre "Connected — \<name\> v\<version\>".
3. Para activar el seguimiento de banda en Port A, haga clic en **AUTO** bajo los botones de antena de Port A. El botón se resalta en verde cuando está activo.
4. Para activar el seguimiento de banda en Port B, haga clic en **AUTO** bajo los botones de antena de Port B. El botón se resalta en verde cuando está activo.
   - La sección de Port B se oculta si el dispositivo conectado reporta únicamente un puerto de radio.
5. Para desactivar el modo AUTO en cualquiera de los puertos, haga clic nuevamente en el botón **AUTO** iluminado. Vuelve a su estado apagado y el puerto regresa a la selección manual de antena.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Port A AUTO | Activa o desactiva el seguimiento de banda en Port A. Cuando está activo, el AG selecciona la antena para Port A según la banda actual del radio. | Off |
| Port B AUTO | Activa o desactiva el seguimiento de banda en Port B. Cuando está activo, el AG selecciona la antena para Port B según la banda actual del radio. Se oculta en dispositivos de un solo puerto. | Off |

## Consejos

- Es posible ejecutar AUTO en un puerto y seleccionar antenas manualmente en el otro. Los dos puertos son independientes.
- Cuando AUTO está activo, los indicadores de banda de Port A y Port B se actualizan a medida que sintoniza distintas bandas, confirmando que el AG está rastreando correctamente.

## Resolución de problemas

- **El botón AUTO no responde a los clics** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected — \<name\> v\<version\>" antes de activar AUTO. Si no está conectado, consulte las páginas a continuación.
- **El indicador de banda muestra "—" después de activar AUTO** — El AG aún no ha recibido un reporte de banda del radio. Sintonice una frecuencia dentro de una banda reconocida para activar una actualización.

## Relacionados

- [Descripción general de Antenna Genius](overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar manualmente un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para Port A o Port B](select-an-antenna-for-port-a-or-port-b.md)
