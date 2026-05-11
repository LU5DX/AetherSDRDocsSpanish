# Grabar una nueva asignación con el modo Aprender

Use el modo Aprender para asignar un mando, deslizador o botón físico de su controlador MIDI a un parámetro en AetherSDR. Después de hacer clic en Aprender, mueva el control en su hardware y AetherSDR grabará la asignación automáticamente.

## Antes de comenzar

- Su controlador MIDI debe estar conectado a la computadora y visible como un dispositivo de entrada MIDI.
- El puerto MIDI debe estar abierto en AetherSDR. Si el estado del puerto muestra "Disconnected", conéctelo primero — consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En la sección **Parameter Bindings**, use el cuadro combinado **Category** para filtrar la lista — elija entre All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display o Frequency.
3. Use el cuadro combinado **Parameter** para seleccionar el parámetro de destino que desea controlar.
4. Haga clic en **Learn**. La etiqueta del botón cambia a **Cancel Learn**.
5. Mueva el mando, deslizador o presione el botón en su controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI entrante y graba la asignación.
6. El botón vuelve a **Learn** automáticamente cuando se captura la asignación. La nueva asignación aparece como una fila en la **Bindings table**.
7. Haga clic en **Close** cuando termine, o continúe agregando asignaciones repitiendo los pasos 2–6.

## Función de cada control

| Control                  | Descripción                                                                                                                                | Notas                                                 |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| **Port:**                | Selecciona el dispositivo de entrada MIDI.                                                                                                 | Persistido como `MidiPort`.                          |
| **Refresh**              | Vuelve a escanear los puertos MIDI disponibles.                                                                                            |                                                       |
| **Connect**              | Abre/cierra el puerto MIDI seleccionado. El estado del puerto se muestra junto al botón.                                                   |                                                       |
| **Auto-connect on startup** | Reabre el puerto MIDI al iniciar.                                                                                                          | Persistido como `MidiAutoConnect`.                   |
| **Category**             | Filtra la lista de Parámetros por una categoría de control específica (All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency). |                                                       |
| **Parameter**            | Selecciona el parámetro de destino a asignar.                                                                                              | En v0.9.7, se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW: "Trigger straight key", "Trigger CW Left Paddle", "Trigger CW Right Paddle". Los IDs con puntos heredados `cw.key`, `cw.dit`, `cw.dah` se migran automáticamente al leer. |
| **Learn**                | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado. Haga clic de nuevo (se muestra como **Cancel Learn**) para cancelar. |                                                       |
| **Bindings table**       | Muestra todas las asignaciones actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, y un botón de eliminar.              |                                                       |
| **Invert**               | Invierte la dirección del control para esa fila de asignación.                                                                             |                                                       |
| **Relative**             | Trata el control asignado como un codificador sin fin en lugar de un control de valor absoluto.                                            |                                                       |
| **× (delete row)**       | Elimina esa asignación individual.                                                                                                         |                                                       |
| **Clear All**            | Elimina todas las asignaciones a la vez.                                                                                                   |                                                       |
| **Profile:**             | Elige un perfil de mapeo MIDI guardado.                                                                                                    |                                                       |
| **Save**                 | Guarda las asignaciones actuales como un perfil.                                                                                            |                                                       |
| **Load**                 | Carga el perfil seleccionado.                                                                                                              |                                                       |
| **Close**                | Cierra el cuadro de diálogo.                                                                                                               |                                                       |

## Consejos

- El **Activity indicator** en la sección MIDI Device muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Úselo para confirmar que su controlador está enviando datos antes de hacer clic en Aprender.
- Si selecciona el parámetro incorrecto antes de hacer clic en Aprender, haga clic en **Cancel Learn** para cancelar sin crear una asignación, luego seleccione el parámetro correcto e intente de nuevo.
- Las asignaciones se guardan automáticamente cuando Aprender se completa. Para conservar sus asignaciones entre sesiones, guárdelas como un perfil con nombre — consulte [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Marque **Auto-connect on startup** (persistido como `MidiAutoConnect`) para que el puerto se reabra automáticamente la próxima vez. El puerto seleccionado se persiste como `MidiPort`.

## Solución de problemas

- **Aprender no se completa después de mover un control** — Verifique que el estado del puerto muestre "Connected" en la sección MIDI Device. Si muestra "Disconnected", seleccione el puerto correcto en el cuadro combinado **Port:** y haga clic en **Connect**. Use el Activity indicator para confirmar que se están recibiendo mensajes MIDI entrantes.
- **El cuadro combinado Parameter está vacío** — La Category seleccionada puede no tener parámetros asignados. Establezca **Category** en All y verifique si la lista de Parámetros se llena.
- **Aprender captura el control incorrecto** — Haga clic en **Cancel Learn**, espere hasta que ningún control en el hardware esté siendo movido, luego haga clic en **Learn** nuevamente y mueva solo el control deseado.

## Relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-conectar controlador MIDI al iniciar](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Invertir un mando o tratarlo como un codificador sin fin](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado anteriormente](load-a-previously-saved-midi-profile.md)
