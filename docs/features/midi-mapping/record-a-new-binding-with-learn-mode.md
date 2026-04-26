# Registrar una nueva asignación con el modo Learn

Use el modo Learn para mapear un mando, fader o botón físico de su controlador MIDI a un parámetro en AetherSDR. Tras hacer clic en Learn, mueva el control en su hardware y AetherSDR registra la asignación automáticamente.

## Antes de comenzar

- Su controlador MIDI debe estar conectado al equipo y visible como dispositivo de entrada MIDI.
- El puerto MIDI debe estar abierto en AetherSDR. Si el estado del puerto muestra "Disconnected", conéctelo primero — consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En la sección **Parameter Bindings**, use el cuadro combinado **Category** para filtrar la lista — elija entre All, RX, TX, Phone/CW, EQ o Global.
3. Use el cuadro combinado **Parameter** para seleccionar el parámetro de destino que desea controlar.
4. Haga clic en **Learn**. La etiqueta del botón cambia a **Cancel Learn**.
5. Mueva el mando o fader, o presione el botón del controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI entrante y registra la asignación.
6. El botón vuelve a **Learn** automáticamente cuando se captura la asignación. La nueva asignación aparece como una fila en la **Bindings table**.
7. Haga clic en **Close** al terminar, o continúe agregando asignaciones repitiendo los pasos 2–6.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Category** | Filtra la lista de parámetros por una categoría de control específica (All, RX, TX, Phone/CW, EQ, Global). |
| **Parameter** | Selecciona el parámetro de destino que se desea asignar. |
| **Learn** | Comienza a escuchar el siguiente mensaje MIDI y lo vincula al parámetro seleccionado. Haga clic de nuevo (mostrado como **Cancel Learn**) para cancelar. |
| **Bindings table** | Muestra todas las asignaciones actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminar. |
| **Invert** | Invierte la dirección del control para esa fila de asignación. |
| **Relative** | Trata el control asignado como un encoder continuo en lugar de un control de valor absoluto. |
| **× (delete row)** | Elimina esa asignación individual. |
| **Clear All** | Elimina todas las asignaciones a la vez. |

## Consejos

- El **Activity indicator** en la sección MIDI Device muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Úselo para confirmar que su controlador está enviando datos antes de hacer clic en Learn.
- Si selecciona el parámetro incorrecto antes de hacer clic en Learn, haga clic en **Cancel Learn** para cancelar sin crear una asignación; luego seleccione el parámetro correcto e inténtelo de nuevo.
- Las asignaciones se guardan automáticamente cuando Learn finaliza. Para conservar sus asignaciones entre sesiones, guárdelas como un perfil con nombre — consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Active **Auto-connect on startup** (guardado como `MidiAutoConnect`) para que el puerto se reabra automáticamente la próxima vez. El puerto seleccionado se guarda como `MidiPort`.

## Solución de problemas

- **Learn no se completa al mover un control** — Verifique que el estado del puerto muestre "Connected" en la sección MIDI Device. Si muestra "Disconnected", seleccione el puerto correcto en el cuadro combinado **Port:** y haga clic en **Connect**. Use el Activity indicator para confirmar que se están recibiendo mensajes MIDI entrantes.
- **El cuadro combinado Parameter está vacío** — Es posible que la categoría seleccionada no tenga parámetros mapeados. Establezca **Category** en All y compruebe si la lista de parámetros se llena.
- **Learn captura el control incorrecto** — Haga clic en **Cancel Learn**, espere hasta que no se esté moviendo ningún control en el hardware, luego haga clic en **Learn** de nuevo y mueva únicamente el control deseado.

## Relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Conectar automáticamente el controlador MIDI al inicio](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Invertir un mando o tratarlo como encoder continuo](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado anteriormente](load-a-previously-saved-midi-profile.md)
