# Registrar un nuevo enlace con el modo Learn

Use el modo Learn para asignar un mando, fader o botón físico de su controlador MIDI a un parámetro en AetherSDR. Después de hacer clic en Learn, mueva el control en su hardware y AetherSDR registrará el enlace automáticamente.

## Antes de comenzar

- Su controlador MIDI debe estar conectado al equipo y visible como dispositivo de entrada MIDI.
- El puerto MIDI debe estar abierto en AetherSDR. Si el estado del puerto muestra "Disconnected", conéctelo primero — consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En la sección **Parameter Bindings**, use el cuadro combinado **Category** para reducir la lista — elija entre All, RX, TX, Phone/CW, EQ o Global.
3. Use el cuadro combinado **Parameter** para seleccionar el parámetro de destino que desea controlar.
4. Haga clic en **Learn**. La etiqueta del botón cambia a **Cancel Learn**.
5. Mueva el mando, el fader o pulse el botón de su controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI entrante y registra el enlace.
6. El botón regresa a **Learn** automáticamente cuando el enlace es capturado. El nuevo enlace aparece como una fila en la tabla **Bindings table**.
7. Haga clic en **Close** cuando termine, o continúe agregando enlaces repitiendo los pasos 2–6.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Category** | Filtra la lista de parámetros a una categoría de control específica (All, RX, TX, Phone/CW, EQ, Global). |
| **Parameter** | Selecciona el parámetro de destino que se va a enlazar. |
| **Learn** | Comienza a escuchar el siguiente mensaje MIDI y lo enlaza al parámetro seleccionado. Haga clic de nuevo (se muestra como **Cancel Learn**) para cancelar. |
| **Bindings table** | Muestra todos los enlaces actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminación. |
| **Invert** | Invierte la dirección del control para esa fila de enlace. |
| **Relative** | Trata el control asignado como un encoder sin fin en lugar de un control de valor absoluto. |
| **× (delete row)** | Elimina ese enlace individual. |
| **Clear All** | Elimina todos los enlaces a la vez. |

## Consejos

- El **Activity indicator** en la sección MIDI Device muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Úselo para confirmar que su controlador está enviando datos antes de hacer clic en Learn.
- Si selecciona el parámetro incorrecto antes de hacer clic en Learn, haga clic en **Cancel Learn** para cancelar sin crear un enlace; luego seleccione el parámetro correcto e inténtelo de nuevo.
- Los enlaces se guardan automáticamente cuando Learn finaliza. Para conservar sus enlaces entre sesiones, guárdelos como un perfil con nombre — consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Active **Auto-connect on startup** (almacenado como `MidiAutoConnect`) para que el puerto se vuelva a abrir automáticamente la próxima vez. El puerto seleccionado se almacena como `MidiPort`.

## Solución de problemas

- **Learn no se completa después de mover un control** — Verifique que el estado del puerto muestre "Connected" en la sección MIDI Device. Si muestra "Disconnected", seleccione el puerto correcto en el cuadro combinado **Port:** y haga clic en **Connect**. Use el Activity indicator para confirmar que se están recibiendo mensajes MIDI entrantes.
- **El cuadro combinado Parameter está vacío** — Es posible que la categoría seleccionada no tenga parámetros asignados. Establezca **Category** en All y compruebe si la lista de parámetros se llena.
- **Learn captura el control incorrecto** — Haga clic en **Cancel Learn**, espere hasta que no se estén moviendo controles en el hardware y luego haga clic en **Learn** de nuevo y mueva únicamente el control deseado.

## Relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Conectar automáticamente el controlador MIDI al inicio](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Invertir un mando o tratarlo como un encoder sin fin](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Eliminar un enlace](delete-a-binding.md)
- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado anteriormente](load-a-previously-saved-midi-profile.md)
