# Identificar qué antenas no pueden transmitir en la banda actual (color ámbar o atenuado)

Los botones de antena en el applet Antenna Genius tienen código de color para mostrar los permisos de TX y RX en la banda actual. Esto permite ver de un vistazo qué antenas están disponibles para transmitir antes de seleccionar una.

## Antes de comenzar

- El applet Antenna Genius debe estar abierto. Haga clic en el botón "AG" de la bandeja en la barra lateral derecha para mostrarlo.
- El applet debe estar conectado a un dispositivo. La etiqueta de estado debe mostrar "Connected — \<name\> v\<version\>".
- El radio debe estar en la banda que desea verificar. Los colores de los botones se actualizan automáticamente cuando cambia la banda.

## Pasos

1. Observe los botones de antena en la sección Port A o Port B.
2. Lea el color del botón:
   - **Azul (seleccionado)** — la antena seleccionada tiene permiso de TX y RX en la banda actual.
   - **Ámbar (seleccionado)** — la antena seleccionada tiene permiso solo de RX en la banda actual; la transmisión no está disponible en esta antena.
   - **Atenuado (no seleccionado, visualmente apagado)** — la antena no tiene permiso en la banda actual para TX ni para RX.
3. Si necesita una antena con capacidad de TX, haga clic en un botón que no esté atenuado. Después de seleccionarla, confirme que se ilumina en azul y no en ámbar.

## Qué hace cada control

| Control | Color / Estado | Significado |
|---|---|---|
| Botones de antena Port A | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port A | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port A | Atenuado | Sin permiso en la banda actual. |
| Botones de antena Port B | Azul | Antena seleccionada; TX y RX permitidos en la banda actual. |
| Botones de antena Port B | Ámbar | Antena seleccionada; solo RX en la banda actual — sin TX. |
| Botones de antena Port B | Atenuado | Sin permiso en la banda actual. |

Los botones también se deshabilitan y atenúan cuando la misma antena ya está seleccionada en el otro puerto. Consulte [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto quedan bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md) para obtener detalles sobre ese caso.

## Consejos

- Los colores de los botones se actualizan automáticamente cuando el radio cambia de banda, por lo que no es necesario volver a abrir el applet después de un cambio de banda.
- Si utiliza el modo AUTO, el applet selecciona antenas según las reglas de seguimiento de banda. El mismo código de color se aplica a la antena seleccionada automáticamente. Consulte [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md).

## Solución de problemas

- **Todos los botones están atenuados después de conectar** — Es posible que el applet no haya recibido aún la información de banda del radio. Confirme que el radio está sintonizado en una banda válida y que la etiqueta de estado muestra "Connected". Si el applet se abrió antes de que el radio estuviera en una banda, cambie de banda una vez para forzar una actualización.
- **Los colores no se actualizan al cambiar de banda** — La actualización de seguimiento de banda requiere una conexión activa al dispositivo Antenna Genius. Verifique que la etiqueta de estado siga mostrando "Connected — \<name\> v\<version\>" y que no se muestre ningún error.

## Relacionado

- [Descripción general de Antenna Genius](overview.md)
- [Seleccionar una antena para Port A o Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto quedan bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
