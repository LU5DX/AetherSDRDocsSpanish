# Seleccionar una antena para la Entrada A del ShackSwitch

Utilice el applet ShackSwitch para enrutar una antena específica a la Entrada A de su dispositivo ShackSwitch. Esto controla qué antena utiliza el Puerto A de su radio para recepción y transmisión.

## Antes de comenzar

- Un dispositivo ShackSwitch debe estar descubierto en la LAN o conectado a través de la pestaña Periféricos en Configuración de Radio. El applet aparece automáticamente cuando se encuentra un dispositivo.
- El applet ShackSwitch debe estar visible en el Panel de Applets. Si no está visible, haga clic en el botón de la bandeja SS en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el Panel de Applets. Si el applet ShackSwitch no está visible, haga clic en el botón de la bandeja SS en la barra lateral derecha.
2. Localice la lista de antenas en el applet. Cada antena aparece como una fila con un nombre de antena y uno o dos botones etiquetados como `[A]` y `[B]`.
3. Busque la fila de la antena que desea asignar a la Entrada A.
4. Haga clic en el botón `[A]` en esa fila.
5. Confirme la selección: la tarjeta ENTRADA A en la parte superior del applet se actualiza para mostrar el nombre de la antena que seleccionó.

Para anular la selección de la antena actual de la Entrada A sin elegir otra, haga clic nuevamente en el botón `[A]` activo. La tarjeta ENTRADA A volverá a mostrar —.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Tarjeta ENTRADA A | Muestra la banda y el nombre de la antena actualmente asignados al Puerto A. Muestra — cuando no hay ninguna antena seleccionada. | — |
| Botón `[A]` (por fila de antena) | Selecciona esa antena para la Entrada A. Haga clic nuevamente para anular la selección. Parpadea en ámbar cuando el Puerto A y el Puerto B están asignados a la misma antena. | — |
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión del firmware, o un mensaje de desconexión. | — |
| Selector de carga ficticia | Designa una antena como carga ficticia. Cuando está configurado, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |
| Configuración ⚙ | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Utiliza `SS_ManualIp` como alternativa si no hay una conexión activa disponible. El puerto se toma de `SS_WebPort` o utiliza el valor predeterminado 5000. | `SS_ManualIp`, `SS_WebPort` |

## Consejos

- El botón `[A]` se resalta en cian cuando está activo, coincidiendo con el color cian de la tarjeta ENTRADA A. Un botón `[A]` no seleccionado se muestra en un estilo atenuado.
- En dispositivos de un solo puerto (R4), la tarjeta ENTRADA B y los botones `[B]` están ocultos. Solo está disponible la selección de la Entrada A.

## Solución de problemas

- **El botón `[A]` parpadea en ámbar después de la selección** — Tanto la Entrada A como la Entrada B están ahora asignadas a la misma antena. Esto es un conflicto. Consulte [Resolver un conflicto de antena entre la Entrada A y la Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md) para resolverlo.
- **La lista de antenas está vacía** — El applet aún no ha recibido datos de antenas del dispositivo. Verifique que el ShackSwitch sea accesible en la LAN y que la etiqueta de estado muestre una dirección IP conectada en lugar de un mensaje de desconexión.
- **La tarjeta ENTRADA A aún muestra — después de hacer clic en `[A]`** — Es posible que el dispositivo no haya confirmado la selección aún. Verifique que la etiqueta de estado muestre un dispositivo conectado. Si el dispositivo está desconectado, no se puede enviar el comando.

## Relacionados

- [Descripción general de ShackSwitch](overview.md)
- [Seleccionar una antena para la Entrada B del ShackSwitch](select-an-antenna-for-shackswitch-input-b.md)
- [Resolver un conflicto de antena entre la Entrada A y la Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Abrir la interfaz de configuración web del ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
