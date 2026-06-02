# Grabar un nuevo enlace con el modo Learn

Use el modo Learn para asignar una perilla, un fader o un botón físico de su controlador MIDI a un parámetro en AetherSDR. Después de hacer clic en Learn, mueva el control en su hardware y AetherSDR grabará el enlace automáticamente.

## Antes de comenzar

- Su controlador MIDI debe estar conectado a la computadora y visible como un dispositivo de entrada MIDI.
- El puerto MIDI debe estar abierto en AetherSDR. Si el estado del puerto muestra "Disconnected", conéctelo primero; consulte [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En la sección **Parameter Bindings**, use el cuadro combinado **Category** para reducir la lista; elija entre All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display o Frequency.
3. Use el cuadro combinado **Parameter** para seleccionar el parámetro de destino que desea controlar.
4. Haga clic en **Learn**. La etiqueta del botón cambia a **Cancel Learn**.
5. Mueva la perilla, el fader o presione el botón en su controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI entrante y graba el enlace.
6. El botón vuelve a **Learn** automáticamente cuando se captura el enlace. El nuevo enlace aparece como una fila en la **Bindings table**.
7. Haga clic en **Close** cuando haya terminado, o continúe agregando enlaces repitiendo los pasos 2 a 6.

## Descripción de cada control

| Control                 | Descripción                                                                                                                                                       | Notas |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| **Port:**               | Selecciona el dispositivo de entrada MIDI.                                                                                                                                | Se guarda como `MidiPort`. |
| **Refresh**             | Vuelve a escanear los puertos MIDI disponibles.                                                                                                                          |       |
| **Connect**             | Abre/cierra el puerto MIDI seleccionado. El estado del puerto se muestra junto al botón.                                                                               |       |
| **Auto-connect on startup** | Vuelve a abrir el puerto MIDI al iniciar.                                                                                                                        | Se guarda como `MidiAutoConnect`. |
| **Category**            | Filtra la lista de parámetros a una categoría de control específica (All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency).                    |       |
| **Parameter**           | Selecciona el parámetro de destino para enlazar.                                                                                                                          | En v0.9.7, se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW: "Trigger straight key", "Trigger CW Left Paddle", "Trigger CW Right Paddle". Los IDs heredados con puntos `cw.key`, `cw.dit`, `cw.dah` se migran automáticamente al leer. |
| **Learn**               | Comienza a escuchar el siguiente mensaje MIDI y lo enlaza al parámetro seleccionado. Haga clic de nuevo (se muestra como **Cancel Learn**) para abortar.              |       |
| **Bindings table**      | Muestra todos los enlaces actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminar.                                              |       |
| **Invert**              | Invierte la dirección del control para esa fila de enlace.                                                                                                             |       |
| **Relative**            | Trata el control asignado como un codificador sin fin en lugar de un control de valor absoluto.                                                                        |       |
| **× (eliminar fila)**   | Elimina ese enlace individual.                                                                                                                                         |       |
| **Clear All**           | Elimina todos los enlaces a la vez.                                                                                                                                 |       |
| **Profile:**            | Elige un perfil de mapeo MIDI guardado.                                                                                                                           |       |
| **Save**                | Guarda los enlaces actuales como un perfil.                                                                                                                        |       |
| **Load**                | Carga el perfil seleccionado.                                                                                                                                      |       |
| **Close**               | Cierra el diálogo.                                                                                                                                                |       |

## Consejos

- El **Activity indicator** en la sección MIDI Device muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Úselo para confirmar que su controlador está enviando datos antes de hacer clic en Learn.
- Si seleccionó el parámetro incorrecto antes de hacer clic en Learn, haga clic en **Cancel Learn** para abortar sin crear un enlace, luego seleccione el parámetro correcto e intente de nuevo.
- Los enlaces se guardan automáticamente cuando Learn se completa. Para conservar sus enlaces entre sesiones, guárdelos como un perfil con nombre; consulte [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md).
- Marque **Auto-connect on startup** (se guarda como `MidiAutoConnect`) para que el puerto se vuelva a abrir automáticamente la próxima vez. El puerto seleccionado se guarda como `MidiPort`.
- La geometría del diálogo se guarda y restaura automáticamente entre sesiones.
- El diálogo ahora usa el tema activo para todos los elementos visuales. Los colores de texto, fondos y acentos se ajustan automáticamente cuando cambia el tema de la aplicación.

## Solución de problemas

- **Learn no se completa después de mover un control** — Verifique que el estado del puerto muestre "Connected" en la sección MIDI Device. Si muestra "Disconnected", seleccione el puerto correcto en el cuadro combinado **Port:** y haga clic en **Connect**. Use el Activity indicator para confirmar que se están recibiendo mensajes MIDI entrantes.
- **El cuadro combinado Parameter está vacío** — La Category seleccionada puede no tener parámetros mapeados. Establezca **Category** en All y verifique si la lista de parámetros se llena.
- **Learn captura el control incorrecto** — Haga clic en **Cancel Learn**, espere hasta que no se esté moviendo ningún control en el hardware, luego haga clic en **Learn** de nuevo y mueva solo el control deseado.

## Relacionados

- [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-connect MIDI controller on startup](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Invert a knob or treat it as an endless encoder](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Delete a binding](delete-a-binding.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
