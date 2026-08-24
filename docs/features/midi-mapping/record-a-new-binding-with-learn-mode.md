# Grabar un nuevo mapeo con el modo Learn

Use el modo Learn para asignar una perilla, un deslizador o un botón físico de su controlador MIDI a un parámetro en AetherSDR. Después de hacer clic en Learn, mueva el control en su hardware y AetherSDR grabará el mapeo automáticamente.

## Antes de comenzar

- Su controlador MIDI debe estar conectado a la computadora y visible como un dispositivo de entrada MIDI.
- El puerto MIDI debe estar abierto en AetherSDR. Si el estado del puerto muestra "Disconnected", conéctelo primero; consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En la sección **Parameter Bindings**, use el cuadro combinado **Category** para reducir la lista; elija entre All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display o Frequency.
3. Use el cuadro combinado **Parameter** para seleccionar el parámetro de destino que desea controlar.
4. Haga clic en **Learn**. La etiqueta del botón cambia a **Cancel Learn**.
5. Mueva la perilla, el deslizador o presione el botón en su controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI entrante y graba el mapeo.
6. El botón vuelve a **Learn** automáticamente cuando se captura el mapeo. El nuevo mapeo aparece como una fila en la **Bindings table**.
7. Haga clic en **Close** al terminar, o continúe agregando mapeos repitiendo los pasos 2–6.

## Agregar un mapeo manualmente sin el modo Learn

Si conoce el canal MIDI, el tipo de mensaje y el número exactos del control que desea asignar, puede ingresarlos directamente en lugar de usar el modo Learn.

1. Abra `Settings > MIDI Mapping...`.
2. Seleccione la **Category** y el **Parameter** de destino para el mapeo.
3. Haga clic en **Manual…**.
4. En el diálogo, escriba el canal, el tipo de mensaje y el número del mapeo.
5. Haga clic en **OK** para agregar el mapeo a la tabla.

También puede editar el canal, el tipo de mensaje o el número de un mapeo existente haciendo clic en el botón **✎ (edit binding)** de esa fila y corrigiendo los valores en el mismo editor manual.

## Qué hace cada control

| Control                     | Descripción                                                                                                                                    | Notas                                                                                                                                                                                                                                     |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Port:**                   | Selecciona el dispositivo de entrada MIDI.                                                                                                     | Se conserva como `MidiPort`.                                                                                                                                                                                                              |
| **Refresh**                 | Vuelve a escanear los puertos MIDI disponibles.                                                                                                |                                                                                                                                                                                                                                           |
| **Connect**                 | Abre/cierra el puerto MIDI seleccionado. El estado del puerto se muestra junto al botón.                                                       |                                                                                                                                                                                                                                           |
| **Auto-connect on startup** | Reabre el puerto MIDI al iniciar.                                                                                                              | Se conserva como `MidiAutoConnect`.                                                                                                                                                                                                       |
| **Category**                | Filtra la lista de Parameter a una categoría de control específica (All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency). |                                                                                                                                                                                                                                           |
| **Parameter**               | Selecciona el parámetro de destino a mapear.                                                                                                   | En v0.9.7, se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW: "Trigger straight key", "Trigger CW Left Paddle", "Trigger CW Right Paddle". Los IDs heredados con puntos `cw.key`, `cw.dit`, `cw.dah` se migran automáticamente al leerlos. |
| **Learn**                   | Comienza a escuchar el siguiente mensaje MIDI y lo vincula al parámetro seleccionado. Haga clic de nuevo (se muestra como **Cancel Learn**) para cancelar. |                                                                                                                                                                                                                                           |
| **Manual…**                 | Abre un diálogo para escribir el canal, tipo de mensaje y número de un mapeo en lugar de usar el modo Learn.                                    | Nuevo en v26.8.4. Abre el mismo editor manual que usa el botón de edición por fila.                                                                                                                                                       |
| **Bindings table**          | Muestra todos los mapeos actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, botones de editar (✎) y eliminar.                 |                                                                                                                                                                                                                                           |
| **✎ (edit binding)**        | Abre el editor manual para corregir el canal, tipo y número de este mapeo.                                                                     | Nuevo en v26.8.4.                                                                                                                                                                                                                         |
| **Invert**                  | Invierte la dirección del control para esa fila de mapeo.                                                                                        |                                                                                                                                                                                                                                           |
| **Relative**                | Trata el control asignado como un codificador sin fin en lugar de un control de valor absoluto.                                                 |                                                                                                                                                                                                                                           |
| **× (delete row)**          | Elimina ese mapeo individual.                                                                                                                   |                                                                                                                                                                                                                                           |
| **Clear All**               | Elimina todos los mapeos a la vez.                                                                                                              |                                                                                                                                                                                                                                           |
| **Profile:**                | Selecciona un perfil de mapeo MIDI guardado.                                                                                                     |                                                                                                                                                                                                                                           |
| **Save**                    | Guarda los mapeos actuales como un perfil.                                                                                                      |                                                                                                                                                                                                                                           |
| **Load**                    | Carga el perfil seleccionado.                                                                                                                   |                                                                                                                                                                                                                                           |
| **Import...**               | Importa un archivo de perfil al almacén: XML de perfil de AetherSDR o un archivo ".map" de SmartSDR.                                            | Nuevo en v26.8.4. Informa cuántos mapeos se importaron y permite al usuario hacer clic en Load para aplicarlos.                                                                                                                             |
| **Export...**               | Exporta los mapeos actuales como un archivo XML de perfil de AetherSDR.                                                                         | Nuevo en v26.8.4. El directorio recordado se conserva bajo `MidiImportExportPath`.                                                                                                                                                       |
| **Close**                   | Cierra el diálogo.                                                                                                                               |                                                                                                                                                                                                                                           |

## Consejos

- El **indicador de actividad** en la sección MIDI Device muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Úselo para confirmar que su controlador envía datos antes de hacer clic en Learn.
- Si selecciona el parámetro incorrecto antes de hacer clic en Learn, haga clic en **Cancel Learn** para cancelar sin crear un mapeo, luego seleccione el parámetro correcto e intente de nuevo.
- Use el botón **Manual…** o el botón **✎** de la fila para corregir un mapeo cuando conozca los detalles exactos del mensaje MIDI; esto es más rápido que eliminar y volver a aprender el mapeo.
- Los mapeos se guardan automáticamente cuando Learn se completa. Para conservar sus mapeos entre sesiones, guárdelos como un perfil con nombre; consulte [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Marque **Auto-connect on startup** (conservado como `MidiAutoConnect`) para que el puerto se reabra automáticamente la próxima vez. El puerto seleccionado se conserva como `MidiPort`.
- La geometría del diálogo se guarda y restaura automáticamente entre sesiones.
- El diálogo ahora usa el tema activo para todos los elementos visuales. Los colores de texto, fondos y acentos se ajustan automáticamente al cambiar el tema de la aplicación.

## Solución de problemas

- **Learn no se completa después de mover un control** — Verifique que el estado del puerto muestre "Connected" en la sección MIDI Device. Si muestra "Disconnected", seleccione el puerto correcto en el cuadro combinado **Port:** y haga clic en **Connect**. Use el indicador de actividad para confirmar que se están recibiendo mensajes MIDI entrantes.
- **El cuadro combinado Parameter está vacío** — La Category seleccionada puede no tener parámetros mapeados. Establezca **Category** en All y verifique si la lista de Parameter se llena.
- **Learn captura el control incorrecto** — Haga clic en **Cancel Learn**, espere hasta que ningún control del hardware se esté moviendo, luego haga clic en **Learn** de nuevo y mueva únicamente el control deseado.
- **Import no se aplica de inmediato** — Después de importar un archivo de perfil, haga clic en **Load** en la sección Profile para aplicar los mapeos importados.

## Relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-conectar el controlador MIDI al inicio](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Invertir una perilla o tratarla como un codificador sin fin](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Eliminar un mapeo](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado previamente](load-a-previously-saved-midi-profile.md)
