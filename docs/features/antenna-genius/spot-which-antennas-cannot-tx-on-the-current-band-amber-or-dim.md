# Identifique qué antenas no pueden transmitir en la banda actual (ámbar o atenuadas)

Los botones de antena en el applet de Antenna Genius están codificados por color para mostrar los permisos de TX y RX en la banda actual. Esto le permite ver de un vistazo qué antenas están disponibles para transmitir antes de hacer clic en una.

## Antes de comenzar

- El applet de Antenna Genius debe estar abierto. Haga clic en el botón de la bandeja "AG" en la barra lateral derecha para mostrarlo.
- El applet debe estar conectado a un dispositivo. La etiqueta de estado debe indicar "Connected — \<nombre\> v\<versión\>".
- El equipo debe estar en la banda que desea verificar. Los colores de los botones se actualizan automáticamente cuando cambia la banda.

## Pasos

1. Observe los botones de antena en la sección Port A o Port B.
2. Lea el color del botón:
   - **Azul (marcado)** — la antena seleccionada tiene permiso de TX y RX en la banda actual.
   - **Ámbar (marcado)** — la antena seleccionada tiene permiso solo de RX en la banda actual; no está disponible la transmisión en esta antena.
   - **Atenuado (sin marcar, visualmente opaco)** — la antena no tiene permiso en la banda actual ni para TX ni para RX.
3. Si necesita una antena con capacidad de TX, haga clic en un botón que no esté atenuado. Después de la selección, confirme que se ilumine en azul en lugar de ámbar.

## Función de cada control

| Control | Color / Estado | Significado |
|---|---|---|
| Botones de antena Port A | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port A | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port A | Atenuado | Sin permiso en la banda actual. |
| Botones de antena Port B | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port B | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port B | Atenuado | Sin permiso en la banda actual. |

Los botones también se deshabilitan y atenúan cuando la misma antena ya está seleccionada en el otro puerto. Consulte [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md) para obtener más detalles sobre ese caso.

## Consejos

- Los colores de los botones se actualizan automáticamente cuando el equipo cambia de banda, por lo que no es necesario volver a abrir el applet después de un cambio de banda.
- Si utiliza el modo AUTO, el applet selecciona antenas según las reglas de seguimiento de banda. La misma codificación de colores se aplica a la antena seleccionada automáticamente. Consulte [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md).

## Solución de problemas

- **Todos los botones están atenuados después de la conexión** — Es posible que el applet aún no haya recibido información de banda del equipo. Confirme que el equipo esté sintonizado en una banda válida y que la etiqueta de estado muestre "Connected". Si el applet se abrió antes de que el equipo estuviera en una banda, cambie de banda una vez para forzar una actualización.
- **Los colores no se actualizan al cambiar de banda** — La actualización de seguimiento de banda requiere una conexión activa con el dispositivo Antenna Genius. Verifique que la etiqueta de estado aún indique "Connected — \<nombre\> v\<versión\>" y que no se muestre ningún error.
- **Un dispositivo ShackSwitch no se conecta automáticamente aquí** — Los dispositivos ShackSwitch descubiertos por UDP son gestionados por el applet de ShackSwitch, no por el applet de Antenna Genius. Si ve que aparece un ShackSwitch en el combo Device pero no se conecta automáticamente, abra el applet de ShackSwitch para gestionarlo.

## Relacionado

- [Antenna Genius overview](overview.md)
- [Select an antenna for Port A or Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
