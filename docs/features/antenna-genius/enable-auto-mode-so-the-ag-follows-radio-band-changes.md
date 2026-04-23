# Activar el modo AUTO para que el AG siga los cambios de banda del radio

El modo AUTO indica al Antenna Genius que rastree la banda activa de su radio y cambie las antenas automáticamente. Esto elimina la necesidad de seleccionar manualmente una antena cada vez que cambia de banda.

## Antes de comenzar

- El applet del Antenna Genius debe estar visible. Permanece oculto hasta que se descubre un dispositivo o se conecta manualmente. Use el botón de bandeja AG en la barra lateral derecha para abrirlo.
- El applet debe mostrar el estado "Connected — \<name\> v\<version\>". El modo AUTO no tiene efecto cuando está desconectado.

## Pasos

1. Haga clic en el botón de bandeja AG en la barra lateral derecha para abrir el applet del Antenna Genius.
2. Confirme que la etiqueta de estado muestra "Connected — \<name\> v\<version\>".
3. Para activar el seguimiento de banda en Port A, haga clic en **AUTO** debajo de los botones de antena de Port A. El botón se resalta en verde cuando está activo.
4. Para activar el seguimiento de banda en Port B, haga clic en **AUTO** debajo de los botones de antena de Port B. El botón se resalta en verde cuando está activo.
   - La sección de Port B está oculta si el dispositivo conectado reporta un solo puerto de radio.
5. Para desactivar el modo AUTO en cualquier puerto, haga clic de nuevo en el botón **AUTO** encendido. Regresa a su estado apagado y el puerto vuelve a la selección manual de antena.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Port A AUTO | Activa o desactiva el seguimiento de banda en Port A. Cuando está activo, el AG selecciona la antena para Port A según la banda actual del radio. | Off |
| Port B AUTO | Activa o desactiva el seguimiento de banda en Port B. Cuando está activo, el AG selecciona la antena para Port B según la banda actual del radio. Oculto en dispositivos de un solo puerto. | Off |

## Consejos

- Puede ejecutar AUTO en un puerto y seleccionar antenas manualmente en el otro. Los dos puertos son independientes.
- Cuando AUTO está activo, los indicadores de banda de Port A y Port B se actualizan a medida que sintoniza distintas bandas, lo que confirma que el AG está rastreando correctamente.

## Solución de problemas

- **El botón AUTO no responde a los clics** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected — \<name\> v\<version\>" antes de activar AUTO. Si no está conectado, consulte las páginas a continuación.
- **El indicador de banda muestra "—" después de activar AUTO** — El AG aún no ha recibido un reporte de banda del radio. Sintonice una frecuencia dentro de una banda reconocida para activar una actualización.

## Relacionados

- [Descripción general del Antenna Genius](overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para Port A o Port B](select-an-antenna-for-port-a-or-port-b.md)
