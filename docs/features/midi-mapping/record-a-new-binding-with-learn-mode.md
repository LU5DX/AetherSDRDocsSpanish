# Grabar una nueva asignación con el modo Learn

Use el modo Learn para asignar un potenciómetro, un fader o un botón físico de su controlador MIDI a un parámetro en AetherSDR. Después de hacer clic en Learn, mueva el control en su hardware y AetherSDR registrará la asignación automáticamente.

## Antes de comenzar

- Su controlador MIDI debe estar conectado a la computadora y visible como un dispositivo de entrada MIDI.
- El puerto MIDI debe estar abierto en AetherSDR. Si el estado del puerto muestra "Disconnected", conéctelo primero — consulte [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En la sección **Parameter Bindings**, use el cuadro combinado **Category** para filtrar la lista — elija entre All, RX, TX, Phone/CW, EQ o Global.
3. Use el cuadro combinado **Parameter** para seleccionar el parámetro de destino que desea controlar.
4. Haga clic en **Learn**. La etiqueta del botón cambia a **Cancel Learn**.
5. Gire el potenciómetro, mueva el fader o presione el botón en su controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI entrante y registra la asignación.
6. El botón vuelve automáticamente a **Learn** cuando la asignación es capturada. La nueva asignación aparece como una fila en la tabla **Bindings table**.
7. Haga clic en **Close** cuando termine, o continúe agregando asignaciones repitiendo los pasos 2–6.

## Qué hace cada control

| Control              | Descripción                                                                                                                           | Notas |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------|-------|
| **Category**         | Filtra la lista de parámetros a una categoría de control específica (All, RX, TX, Phone/CW, EQ, Global).                              |       |
| **Parameter**        | Selecciona el parámetro de destino a asignar.                                                                                         |       |
| **Learn**            | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado. Haga clic de nuevo (se muestra como **Cancel Learn**) para cancelar. |       |
| **Bindings table**   | Muestra todas las asignaciones actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminación.       |       |
| **Invert**           | Invierte la dirección del control para esa fila de asignación.                                                                        |       |
| **Relative**         | Trata el control asignado como un codificador sin fin en lugar de un control de valor absoluto.                                       |       |
| **× (eliminar fila)**| Elimina esa asignación individual.                                                                                                    |       |
| **Clear All**        | Elimina todas las asignaciones de una vez.                                                                                            |       |

## Consejos

- El **Activity indicator** en la sección MIDI Device muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Úselo para confirmar que su controlador está enviando datos antes de hacer clic en Learn.
- Si selecciona el parámetro incorrecto antes de hacer clic en Learn, haga clic en **Cancel Learn** para cancelar sin crear una asignación, luego seleccione el parámetro correcto e intente de nuevo.
- Las asignaciones se guardan automáticamente cuando Learn se completa. Para conservar sus asignaciones entre sesiones, guárdelas como un perfil con nombre — consulte [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md).
- Marque **Auto-connect on startup** (persistido como `MidiAutoConnect`) para que el puerto se vuelva a abrir automáticamente la próxima vez. El puerto seleccionado se persiste como `MidiPort`.

## Solución de problemas

- **Learn no se completa después de mover un control** — Verifique que el estado del puerto muestre "Connected" en la sección MIDI Device. Si muestra "Disconnected", seleccione el puerto correcto en el cuadro combinado **Port:** y haga clic en **Connect**. Use el Activity indicator para confirmar que se están recibiendo mensajes MIDI entrantes.
- **El cuadro combinado Parameter está vacío** — Es posible que la Category seleccionada no tenga parámetros asignados. Establezca **Category** en All y verifique si la lista de parámetros se completa.
- **Learn captura el control incorrecto** — Haga clic en **Cancel Learn**, espere hasta que ningún control del hardware se esté moviendo, luego haga clic en **Learn** de nuevo y mueva solo el control deseado.

## Relacionado

- [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-connect MIDI controller on startup](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Invert a knob or treat it as an endless encoder](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Delete a binding](delete-a-binding.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
