# Identifique qué antenas no pueden transmitir en la banda actual (ámbar o atenuadas)

Los botones de antena en el applet de Antenna Genius tienen códigos de color que muestran los permisos de TX y RX en la banda actual. Esto le permite ver de un vistazo qué antenas están disponibles para transmitir antes de hacer clic en una.

## Antes de comenzar

- El applet de Antenna Genius debe estar abierto. Haga clic en el botón de la bandeja "AG" en la barra lateral derecha para mostrarlo.
- El applet debe estar conectado a un dispositivo. La etiqueta de estado debe mostrar "Connected — \<nombre\> v\<versión\>".
- El radio debe estar en la banda que desea verificar. Los colores de los botones se actualizan automáticamente cuando cambia la banda.

## Pasos

1. Observe los botones de antena en la sección Puerto A o Puerto B.
2. Lea el color del botón:
   - **Azul (marcado)** — la antena seleccionada tiene permiso de TX y RX en la banda actual.
   - **Ámbar (marcado)** — la antena seleccionada tiene solo permiso de RX en la banda actual; la transmisión no está disponible en esta antena.
   - **Atenuado (sin marcar, visualmente opaco)** — la antena no tiene permiso en la banda actual ni para TX ni para RX.
3. Si necesita una antena con capacidad de TX, haga clic en un botón que no esté atenuado. Después de la selección, confirme que se ilumine en azul en lugar de ámbar.

## Qué hace cada control

| Control | Color / Estado | Significado |
|---|---|---|
| Botones de antena del Puerto A | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena del Puerto A | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena del Puerto A | Atenuado | Sin permiso en la banda actual. |
| Botones de antena del Puerto B | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena del Puerto B | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena del Puerto B | Atenuado | Sin permiso en la banda actual. |

Los botones también están deshabilitados y atenuados cuando la misma antena ya está seleccionada en el otro puerto. Consulte [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md) para más detalles sobre ese caso.

## Consejos

- Los colores de los botones se actualizan automáticamente cuando el radio cambia de banda, por lo que no necesita volver a abrir el applet después de un cambio de banda.
- Si usa el modo AUTO, el applet selecciona antenas según las reglas de seguimiento de banda. El mismo código de color se aplica a la antena seleccionada automáticamente. Consulte [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md).
- Cuando está desconectado, la cuadrícula de botones de antena se limpia automáticamente para mantener la visualización coherente con el estado del modelo.

## Solución de problemas

- **Todos los botones están atenuados después de conectar** — Es posible que el applet aún no haya recibido información de banda del radio. Confirme que el radio esté sintonizado en una banda válida y que la etiqueta de estado muestre "Connected". Si el applet se abrió antes de que el radio estuviera en una banda, cambie de banda una vez para activar una actualización.
- **Todos los botones están en blanco (no se muestran botones de antena) después de conectar** — Es posible que la lista de antenas aún no se haya cargado. El applet espera a que el dispositivo envíe su lista de antenas antes de construir la cuadrícula de botones. Si los botones permanecen en blanco, desconecte y vuelva a conectar al dispositivo.
- **Falta la sección del Puerto B** — El dispositivo Antenna Genius conectado informa solo un puerto de radio. El Puerto B se oculta automáticamente cuando el dispositivo tiene menos de dos puertos de radio. Este estado se determina a partir de la respuesta de información del dispositivo (para conexiones IP manuales) o la baliza UDP (para dispositivos descubiertos). Si espera el Puerto B, verifique que el dispositivo esté configurado con dos puertos de radio.
- **Los colores no se actualizan al cambiar de banda** — La actualización por seguimiento de banda requiere una conexión activa con el dispositivo Antenna Genius. Verifique que la etiqueta de estado aún muestre "Connected — \<nombre\> v\<versión\>" y que no se muestre ningún error.
- **Un dispositivo ShackSwitch no se conecta automáticamente aquí** — Los dispositivos ShackSwitch descubiertos mediante UDP son manejados por el applet de ShackSwitch, no por el applet de Antenna Genius. Si ve que aparece un ShackSwitch en el combo Dispositivo pero no se conecta automáticamente, abra el applet de ShackSwitch para administrarlo.

## Relacionado

- [Antenna Genius overview](overview.md)
- [Select an antenna for Port A or Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Enable AUTO mode so the AG follows radio band changes](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Swap radios that share the AG (antennas in use by the other port are locked out)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
