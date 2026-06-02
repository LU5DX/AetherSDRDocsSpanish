# Identificar qué antenas no pueden transmitir en la banda actual (ámbar o atenuadas)

Los botones de antena en el applet de Antenna Genius tienen códigos de color que indican los permisos de TX y RX en la banda actual. Esto permite ver de un vistazo qué antenas están disponibles para transmitir antes de hacer clic en una.

## Antes de comenzar

- El applet de Antenna Genius debe estar abierto. Haga clic en el botón de bandeja "AG" en la barra lateral derecha para mostrarlo.
- El applet debe estar conectado a un dispositivo. La etiqueta de estado debe mostrar "Connected — \<nombre\> v\<versión\>".
- El radio debe estar en la banda que desea verificar. Los colores de los botones se actualizan automáticamente cuando cambia la banda.

## Pasos

1. Observe los botones de antena en la sección Port A o Port B.
2. Interprete el color del botón:
   - **Azul (marcado)** — la antena seleccionada tiene permiso de TX y RX en la banda actual.
   - **Ámbar (marcado)** — la antena seleccionada tiene permiso solo de RX en la banda actual; no se puede transmitir en esta antena.
   - **Atenuado (sin marcar, visualmente apagado)** — la antena no tiene permiso en la banda actual ni para TX ni para RX.
3. Si necesita una antena con capacidad de TX, haga clic en un botón que no esté atenuado. Después de la selección, confirme que se ilumine en azul en lugar de ámbar.

## Qué hace cada control

| Control | Color / Estado | Significado |
|---|---|---|
| Botones de antena Port A | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port A | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port A | Atenuado | Sin permiso en la banda actual. |
| Botones de antena Port B | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port B | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port B | Atenuado | Sin permiso en la banda actual. |

Los botones también se deshabilitan y atenúan cuando la misma antena ya está seleccionada en el otro puerto. Consulte [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md) para obtener detalles sobre ese caso.

## Consejos

- Los colores de los botones se actualizan automáticamente cuando el radio cambia de banda, por lo que no es necesario volver a abrir el applet después de un cambio de banda.
- Si usa el modo AUTO, el applet selecciona antenas según las reglas de seguimiento de banda. Se aplica el mismo código de color a la antena seleccionada automáticamente. Consulte [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md).

## Solución de problemas

- **Todos los botones están atenuados después de conectarse** — Es posible que el applet aún no haya recibido información de banda del radio. Confirme que el radio esté sintonizado en una banda válida y que la etiqueta de estado muestre "Connected". Si el applet se abrió antes de que el radio estuviera en una banda, cambie de banda una vez para activar una actualización.
- **Los colores no se actualizan al cambiar de banda** — La actualización de seguimiento de banda requiere una conexión activa al dispositivo Antenna Genius. Verifique que la etiqueta de estado siga mostrando "Connected — \<nombre\> v\<versión\>" y que no se muestre ningún error.
- **Un dispositivo ShackSwitch no se conecta automáticamente aquí** — Los dispositivos ShackSwitch descubiertos por UDP son gestionados por el applet ShackSwitch, no por el applet Antenna Genius. Si ve un ShackSwitch aparecer en el combo Device pero no se conecta automáticamente, abra el applet ShackSwitch para gestionarlo.

## Relacionados

- [Antenna Genius overview](overview.md)
- [Select an antenna for Port A or Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
