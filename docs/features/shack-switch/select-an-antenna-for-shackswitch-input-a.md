# Seleccionar una antena para la entrada A del ShackSwitch

Use el applet ShackSwitch para enrutar una antena específica a la entrada A de su dispositivo ShackSwitch. Esto controla qué antena usa el puerto A de su radio para recibir y transmitir.

## Antes de comenzar

- El dispositivo ShackSwitch debe estar descubierto en la LAN o conectado mediante la pestaña Peripherals en Radio Setup. El applet aparece automáticamente cuando se detecta un dispositivo.
- El applet ShackSwitch debe estar visible en el panel de applets (Applet Panel). Si no está visible, haga clic en el botón SS del panel lateral derecho para mostrarlo.

## Pasos

1. Abra el Applet Panel. Si el applet ShackSwitch no está visible, haga clic en el botón SS del panel lateral derecho.
2. Localice la lista de antenas en el applet. Cada antena aparece como una fila con el nombre de la antena y uno o dos botones etiquetados `[A]` y `[B]`.
3. Encuentre la fila correspondiente a la antena que desea asignar a la entrada A.
4. Haga clic en el botón `[A]` de esa fila.
5. Confirme la selección: la tarjeta INPUT A en la parte superior del applet se actualiza para mostrar el nombre de la antena seleccionada.

Para deseleccionar la antena de la entrada A sin elegir otra, haga clic nuevamente en el botón `[A]` activo. La tarjeta INPUT A volverá a mostrar —.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Tarjeta INPUT A | Muestra la banda y el nombre de la antena asignados actualmente al puerto A. Muestra — cuando no hay ninguna antena seleccionada. | — |
| Botón `[A]` (por fila de antena) | Selecciona esa antena para la entrada A. Haga clic de nuevo para deseleccionar. Parpadea en ámbar cuando el puerto A y el puerto B están asignados a la misma antena. | — |
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión de firmware, o un mensaje de desconexión. | — |
| Selector de carga ficticia (dummy load) | Designa una antena como carga ficticia. Cuando está configurado, el puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |
| Settings ⚙ | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Recurre a `SS_ManualIp` si no hay conexión activa disponible. El puerto se toma de `SS_WebPort` o usa 5000 por defecto. | `SS_ManualIp`, `SS_WebPort` |

## Consejos

- El botón `[A]` se resalta en cian cuando está activo, combinando con el color cian de la tarjeta INPUT A. Un botón `[A]` no seleccionado se muestra en un estilo atenuado.
- En dispositivos de un solo puerto (R4), la tarjeta INPUT B y los botones `[B]` están ocultos. Solo está disponible la selección de la entrada A.

## Solución de problemas

- **El botón `[A]` parpadea en ámbar tras la selección** — La entrada A y la entrada B están asignadas ahora a la misma antena. Esto constituye un conflicto. Consulte [Resolver un conflicto de antena entre la entrada A y la entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md) para resolverlo.
- **La lista de antenas está vacía** — El applet aún no ha recibido datos de antenas del dispositivo. Verifique que el ShackSwitch sea accesible en la LAN y que la etiqueta de estado muestre una dirección IP conectada en lugar de un mensaje de desconexión.
- **La tarjeta INPUT A sigue mostrando — después de hacer clic en `[A]`** — Es posible que el dispositivo aún no haya confirmado la selección. Verifique que la etiqueta de estado muestre un dispositivo conectado. Si el dispositivo está desconectado, el comando no puede enviarse.

## Relacionados

- [Descripción general del ShackSwitch](overview.md)
- [Seleccionar una antena para la entrada B del ShackSwitch](select-an-antenna-for-shackswitch-input-b.md)
- [Resolver un conflicto de antena entre la entrada A y la entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Abrir la interfaz de configuración web del ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
