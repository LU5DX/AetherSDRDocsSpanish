# Seleccionar una antena para la Entrada A del ShackSwitch

Use el applet ShackSwitch para enrutar una antena específica a la Entrada A de su dispositivo ShackSwitch. Esto controla qué antena utiliza el Puerto A de su radio para recepción y transmisión.

## Antes de comenzar

- Un dispositivo ShackSwitch debe estar descubierto en la LAN o conectado a través de la pestaña Periféricos en Configuración de radio. El applet aparece automáticamente cuando se encuentra un dispositivo.
- El applet ShackSwitch debe estar visible en el Panel de Applets. Si no está visible, haga clic en el botón de bandeja SS en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el Panel de Applets. Si el applet ShackSwitch no está visible, haga clic en el botón de bandeja SS en la barra lateral derecha.
2. Localice la lista de antenas en el applet. Cada antena aparece como una fila con un nombre de antena y uno o dos botones etiquetados `[A]` y `[B]`.
3. Encuentre la fila de la antena que desea asignar a la Entrada A.
4. Haga clic en el botón `[A]` en esa fila.
5. Confirme la selección: la tarjeta INPUT A en la parte superior del applet se actualiza para mostrar el nombre de la antena que seleccionó.

Para anular la selección de la antena actual de Entrada A sin elegir otra, haga clic nuevamente en el botón `[A]` activo. La tarjeta INPUT A volverá a mostrar —.

## Qué hace cada control

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión del firmware, o un mensaje de desconexión. | — |
| Tarjeta INPUT A | Muestra la banda actual y el nombre de la antena asignada al Puerto A. Resaltada en cian. | — |
| Tarjeta INPUT B | Muestra la banda actual y el nombre de la antena asignada al Puerto B. Resaltada en naranja. Oculto en dispositivos de un solo puerto (R4). | — |
| Botón `[A]` (por fila de antena) | Selecciona esa antena para la Entrada A. Haga clic nuevamente para anular la selección. Parpadea en ámbar cuando el Puerto A y el Puerto B están asignados a la misma antena (conflicto). | — |
| Botón `[B]` (por fila de antena) | Selecciona esa antena para la Entrada B. Haga clic nuevamente para anular la selección. Parpadea en ámbar cuando hay conflicto. Cuando se configura una carga ficticia y B se enruta automáticamente allí, el botón B de la fila prevista parpadea en ámbar y la fila de carga ficticia parpadea en naranja. | — |
| Selector de carga ficticia | Designa una antena como carga ficticia. Cuando está configurado, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |
| Configuración ⚙ | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Utiliza la dirección activa del par cuando está conectado, recurre a `SS_ManualIp`. El puerto se toma de `SS_WebPort`, el puerto web del beacon, o por defecto usa 5000. | `SS_ManualIp`, `SS_WebPort` |

## Consejos

- El botón `[A]` se resalta en cian cuando está activo, coincidiendo con el color cian de la tarjeta INPUT A. Un botón `[A]` no seleccionado se muestra en un estilo atenuado.
- En dispositivos de un solo puerto (R4), la tarjeta INPUT B y los botones `[B]` están ocultos. Solo está disponible la selección de Entrada A.
- El fondo del applet utiliza el estilo del tema activo de AetherSDR para mantener la coherencia con otros applets.

## Solución de problemas

- **El botón `[A]` parpadea en ámbar después de la selección** — Tanto la Entrada A como la Entrada B están ahora asignadas a la misma antena. Esto es un conflicto. Consulte [Resolver un conflicto de antena entre Entrada A y Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md) para solucionarlo.
- **La lista de antenas está vacía** — El applet aún no ha recibido datos de antena del dispositivo. Verifique que el ShackSwitch sea accesible en la LAN y que la etiqueta de estado muestre una dirección IP conectada en lugar de un mensaje de desconexión.
- **La tarjeta INPUT A aún muestra — después de hacer clic en `[A]`** — Es posible que el dispositivo no haya confirmado la selección aún. Verifique que la etiqueta de estado muestre un dispositivo conectado. Si el dispositivo está desconectado, no se puede enviar el comando.

## Relacionados

- [Descripción general de ShackSwitch](overview.md)
- [Seleccionar una antena para la Entrada B del ShackSwitch](select-an-antenna-for-shackswitch-input-b.md)
- [Resolver un conflicto de antena entre Entrada A y Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Abrir la interfaz de configuración web del ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
