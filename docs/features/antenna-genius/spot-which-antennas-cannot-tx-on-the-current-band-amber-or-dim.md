# Identifique qué antenas no pueden transmitir en la banda actual (ámbar u opaco)

Los botones de antena en el applet Antenna Genius están codificados por color para mostrar el permiso de TX y RX en la banda actual. Esto le permite ver de un vistazo qué antenas están disponibles para transmitir antes de hacer clic en una.

## Antes de empezar

- El applet Antenna Genius debe estar abierto. Haga clic en el botón de bandeja "AG" en la barra lateral derecha para mostrarlo.
- El applet debe estar conectado a un dispositivo. La etiqueta de estado debe mostrar "Connected — \<name\> v\<version\>".
- La radio debe estar en la banda que desea verificar. Los colores de los botones se actualizan automáticamente cuando cambia la banda.

## Pasos

1. Observe los botones de antena en la sección Port A o Port B.
2. Lea el color del botón:
   - **Azul (marcado)** — la antena seleccionada tiene permiso de TX y RX en la banda actual.
   - **Ámbar (marcado)** — la antena seleccionada tiene permiso de solo RX en la banda actual; la transmisión no está disponible en esta antena.
   - **Opaco (sin marcar, visualmente atenuado)** — la antena no tiene permiso en la banda actual para TX ni RX.
3. Si necesita una antena capaz de TX, haga clic en un botón que no esté opaco. Después de la selección, confirme que se ilumina en azul en lugar de ámbar.

## Qué hace cada control

| Control | Color / Estado | Significado |
|---|---|---|
| Botones de antena Port A | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port A | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port A | Opaco | Sin permiso en la banda actual. |
| Botones de antena Port B | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port B | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port B | Opaco | Sin permiso en la banda actual. |

Los botones también se desactivan y se atenúan cuando la misma antena ya está seleccionada en el otro puerto. Consulte [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md) para obtener detalles sobre ese caso.

## Consejos

- Los colores de los botones se actualizan automáticamente cuando la radio cambia de banda, por lo que no es necesario reabrir el applet después de un cambio de banda.
- Si utiliza el modo AUTO, el applet selecciona antenas según reglas de seguimiento de banda. La misma codificación de color se aplica a la antena seleccionada automáticamente. Consulte [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md).

## Solución de problemas

- **Todos los botones están opacos después de conectarse** — El applet puede que aún no haya recibido información de banda de la radio. Confirme que la radio está sintonizada a una banda válida y que la etiqueta de estado muestra "Connected". Si el applet se abrió antes de que la radio estuviera en una banda, cambie de banda una vez para activar una actualización.
- **Los colores no se actualizan al cambiar de banda** — La actualización de seguimiento de banda requiere una conexión activa al dispositivo Antenna Genius. Verifique que la etiqueta de estado aún muestre "Connected — \<name\> v\<version\>" y que no se muestre ningún error.
- **Un dispositivo ShackSwitch no se conecta automáticamente aquí** — Los dispositivos ShackSwitch descubiertos por UDP se manejan en el applet ShackSwitch, no en el applet Antenna Genius. Si ve un ShackSwitch en el combo Device pero no se conecta automáticamente, abra el applet ShackSwitch para administrarlo.

## Relacionado

- [Antenna Genius overview](overview.md)
- [Select an antenna for Port A or Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
