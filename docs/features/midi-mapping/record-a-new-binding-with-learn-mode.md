# Grabar una nueva vinculación con el modo Learn

Use el modo Learn para asignar un potenciómetro, deslizador o botón físico de su controlador MIDI a un parámetro en AetherSDR. Después de hacer clic en Learn, mueva el control en su hardware y AetherSDR registrará la vinculación automáticamente.

## Antes de empezar

- Su controlador MIDI debe estar conectado al ordenador y visible como un dispositivo de entrada MIDI.
- El puerto MIDI debe estar abierto en AetherSDR. Si el estado del puerto muestra "Disconnected", conéctelo primero; consulte [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En la sección **Parameter Bindings**, use el cuadro combinado **Category** para reducir la lista; seleccione entre All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display o Frequency.
3. Use el cuadro combinado **Parameter** para seleccionar el parámetro de destino que desea controlar.
4. Haga clic en **Learn**. La etiqueta del botón cambia a **Cancel Learn**.
5. Mueva el potenciómetro, deslizador o presione el botón de su controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI entrante y registra la vinculación.
6. El botón vuelve a **Learn** automáticamente cuando se captura la vinculación. La nueva vinculación aparece como una fila en la **Bindings table**.
7. Haga clic en **Close** cuando termine, o continúe agregando vinculaciones repitiendo los pasos 2 a 6.

## Función de cada control

| Control            | Descripción                                                                                                                          | Notas |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------|-------|
| **Port:**          | Selecciona el dispositivo de entrada MIDI.                                                                                           | Se conserva como `MidiPort`. |
| **Refresh**        | Reescanea los puertos MIDI disponibles.                                                                                              |       |
| **Connect**        | Abre/cierra el puerto MIDI seleccionado. El estado del puerto se muestra junto al botón.                                             |       |
| **Auto-connect on startup** | Reabre el puerto MIDI al iniciar.                                                                                          | Se conserva como `MidiAutoConnect`. |
| **Category**       | Filtra la lista de parámetros a una categoría de control específica (All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency). |       |
| **Parameter**      | Selecciona el parámetro de destino a vincular.                                                                                      | En v0.9.7, se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW: "Trigger straight key", "Trigger CW Left Paddle", "Trigger CW Right Paddle". Los IDs heredados con puntos `cw.key`, `cw.dit`, `cw.dah` se migran automáticamente al leer. |
| **Learn**          | Comienza a escuchar el siguiente mensaje MIDI y lo vincula al parámetro seleccionado. Haga clic de nuevo (se muestra como **Cancel Learn**) para cancelar. |       |
| **Bindings table** | Muestra todas las vinculaciones actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminar.         |       |
| **Invert**         | Invierte la dirección del control para esa fila de vinculación.                                                                     |       |
| **Relative**       | Trata el control asignado como un codificador sin fin en lugar de un control de valor absoluto.                                     |       |
| **× (delete row)** | Elimina esa vinculación individual.                                                                                                  |       |
| **Clear All**      | Elimina todas las vinculaciones de una vez.                                                                                          |       |
| **Profile:**       | Selecciona un perfil de mapeo MIDI guardado.                                                                                        |       |
| **Save**           | Guarda las vinculaciones actuales como un perfil.                                                                                    |       |
| **Load**           | Carga el perfil seleccionado.                                                                                                        |       |
| **Close**          | Cierra el diálogo.                                                                                                                   |       |

## Consejos

- El **Activity indicator** en la sección MIDI Device muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Úselo para confirmar que su controlador está enviando datos antes de hacer clic en Learn.
- Si selecciona el parámetro incorrecto antes de hacer clic en Learn, haga clic en **Cancel Learn** para cancelar sin crear una vinculación, luego seleccione el parámetro correcto e intente de nuevo.
- Las vinculaciones se guardan automáticamente cuando Learn se completa. Para conservar sus vinculaciones entre sesiones, guárdelas como un perfil con nombre; consulte [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md).
- Marque **Auto-connect on startup** (se conserva como `MidiAutoConnect`) para que el puerto se reabra automáticamente la próxima vez. El puerto seleccionado se conserva como `MidiPort`.
- La geometría del diálogo se guarda y restaura automáticamente entre sesiones.

## Solución de problemas

- **Learn no se completa después de mover un control** — Verifique que el estado del puerto muestre "Connected" en la sección MIDI Device. Si muestra "Disconnected", seleccione el puerto correcto en el cuadro combinado **Port:** y haga clic en **Connect**. Use el Activity indicator para confirmar que se están recibiendo mensajes MIDI entrantes.
- **El cuadro combinado Parameter está vacío** — La categoría seleccionada puede no tener parámetros mapeados. Establezca **Category** en All y verifique si la lista de parámetros se llena.
- **Learn captura el control incorrecto** — Haga clic en **Cancel Learn**, espere hasta que ningún control del hardware se esté moviendo, luego haga clic en **Learn** de nuevo y mueva solo el control deseado.

## Relacionados

- [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-connect MIDI controller on startup](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Invert a knob or treat it as an endless encoder](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Delete a binding](delete-a-binding.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
