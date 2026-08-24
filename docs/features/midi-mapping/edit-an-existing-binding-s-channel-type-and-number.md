# Editar el canal, tipo y número de un enlace existente

Corrija el canal, tipo de mensaje o número de un enlace MIDI después de haberlo grabado con el modo Learn o agregado manualmente.

## Antes de comenzar

- Abra el diálogo de asignación del controlador MIDI: `Settings > MIDI Mapping...`
- El enlace que desea editar debe ser visible en la tabla de enlaces (Bindings).

## Pasos

1. En la tabla de enlaces (Bindings), localice la fila correspondiente al enlace que desea cambiar.
2. Haga clic en el botón **✎ (edit binding)** de esa fila.
3. En el diálogo del editor manual, cambie los campos **Channel**, **Message Type** y **Number** según sea necesario.
4. Haga clic en OK para guardar los cambios.
5. La tabla de enlaces (Bindings) se actualiza de inmediato con los valores corregidos.

## Qué hace cada control

El diálogo del editor manual le permite establecer tres valores para el enlace:

| Campo | Descripción |
|---|---|
| Channel | Canal MIDI (normalmente 1–16). |
| Message Type | El tipo de mensaje MIDI, como Note On, Control Change o Program Change. |
| Number | El número de mensaje MIDI (por ejemplo, el número de CC o el número de nota). |

El botón **✎ (edit binding)** aparece en cada fila de la tabla de enlaces (Bindings), entre la casilla Relative y el botón de eliminar. Abre el mismo editor manual que utiliza el botón **Manual…** en la fila "Add binding".

## Consejos

- Use el modo Learn para grabar un nuevo enlace si no está seguro de los valores exactos de canal, tipo y número; el editor manual es lo más adecuado para corregir un error conocido.
- Los cambios que realice aquí se aplican de inmediato; no hay una acción de guardado adicional para la edición.

## Relacionado

- [Add a MIDI binding manually by typing channel, type and number](add-a-midi-binding-manually-by-typing-channel-type-and-number.md)
- [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md)
- [Delete a binding](delete-a-binding.md)
- [MIDI Controller Mapping overview](overview.md)
