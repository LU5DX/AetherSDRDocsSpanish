# Descripción general del mapeo de controladores MIDI

La función de mapeo de controladores MIDI le permite asignar perillas físicas, deslizadores y botones de un controlador MIDI a parámetros de radio en AetherSDR. Una vez que los enlaces se guardan, puede recuperarlos como perfiles con nombre y, opcionalmente, reconectar el controlador automáticamente en cada inicio.

## Antes de comenzar

- Su controlador MIDI debe estar conectado a la computadora antes de abrir el diálogo.
- El soporte MIDI debe estar presente en su compilación de AetherSDR. Si `Settings > MIDI Mapping...` no aparece en el menú, su compilación se realizó sin soporte MIDI.

## Cómo funciona

Abra el diálogo en `Settings > MIDI Mapping...`. El diálogo está dividido en dos secciones: **MIDI Device** y **Parameter Bindings**.

**MIDI Device** gestiona la selección y conexión del puerto. Seleccione su controlador en el cuadro combinado Port:, haga clic en Refresh si no aparece y luego haga clic en Connect para abrir el puerto. El indicador de estado del puerto muestra "Connected" (verde) o "Disconnected" (gris). El indicador de actividad muestra el mensaje MIDI más reciente recibido — por ejemplo, `Ch 1 CC #7 = 64` — lo que resulta útil para confirmar que su controlador está enviando datos.

**Parameter Bindings** es donde crea y gestiona las asignaciones entre mensajes MIDI y controles de radio. Use los cuadros combinados Category y Parameter para localizar el parámetro deseado, luego haga clic en Learn y mueva una perilla o deslizador en su controlador. AetherSDR registra el mensaje MIDI entrante y agrega una fila a la tabla de enlaces. Cada fila de la tabla puede ajustarse individualmente con las casillas Invert y Relative, editarse con el botón ✎ (editar) o eliminarse con el botón × (eliminar fila). Haga clic en Clear All para eliminar todos los enlaces a la vez.

Como alternativa al modo Learn, puede hacer clic en Manual… para escribir directamente el canal, tipo de mensaje y número de un enlace en lugar de mover un control físico. El mismo editor manual también está disponible por fila mediante el botón ✎ (editar).

Los enlaces se pueden guardar, cargar, importar y exportar como perfiles con nombre mediante los controles Profile:, Save, Load, Import... y Export... en la parte inferior del diálogo.

Los enlaces y el último puerto utilizado se guardan automáticamente. La configuración `MidiPort` almacena el nombre del puerto seleccionado y `MidiAutoConnect` almacena si el puerto debe reabrirse al iniciar. El diálogo recuerda su tamaño y posición entre sesiones.

## Qué hace cada control

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI. | `MidiPort` |
| Refresh | Botón | Vuelve a escanear los puertos MIDI disponibles. | — |
| Connect | Botón | Abre el puerto MIDI seleccionado. Cuando un puerto está abierto, la etiqueta cambia a Disconnect. | — |
| Port status | Indicador | Muestra si el puerto MIDI está actualmente abierto. Estados: Opened, Closed. | — |
| Activity indicator | Indicador | Muestra el mensaje MIDI más reciente recibido. | — |
| Auto-connect on startup | Casilla | Reabre el puerto MIDI guardado automáticamente cuando se inicia AetherSDR. | `MidiAutoConnect` |
| Category | Cuadro combinado | Filtra el cuadro combinado Parameter por categoría de control. Las categorías incluyen: All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency. | — |
| Parameter | Cuadro combinado | Selecciona el parámetro de radio de destino para un nuevo enlace. En v0.9.7, se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW: "Trigger straight key" (id: `cwkey`), "Trigger CW Left Paddle" (id: `cwdit`), "Trigger CW Right Paddle" (id: `cwdah`). Los ID con puntos heredados (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leerlos. | — |
| Learn | Botón | Comienza a escuchar el siguiente mensaje MIDI entrante y lo enlaza al parámetro seleccionado. Haga clic nuevamente (etiquetado Cancel Learn) para abortar. | — |
| Manual… | Botón | Abre un diálogo para escribir el canal, tipo de mensaje y número de un enlace en lugar de usar el modo Learn. Nuevo en v26.8.4. Abre el mismo editor manual que usa el botón de edición por fila. | — |
| Bindings table | Lista | Muestra todos los enlaces existentes. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, botones de edición (✎) y eliminación (×). | — |
| ✎ (edit binding) | Botón (por fila) | Abre el editor manual para corregir el canal, tipo de mensaje y número de este enlace. Nuevo en v26.8.4. | — |
| Invert | Casilla (por fila) | Invierte la dirección de control para ese enlace. | — |
| Relative | Casilla (por fila) | Trata el control como un codificador sin fin en lugar de un valor absoluto. | — |
| × (delete row) | Botón (por fila) | Elimina ese enlace. | — |
| Clear All | Botón | Elimina todos los enlaces. | — |
| Profile: | Cuadro combinado | Selecciona o nombra un perfil de mapeo MIDI guardado. El campo es editable. | — |
| Save | Botón | Guarda los enlaces actuales bajo el nombre ingresado en Profile:. | — |
| Load | Botón | Carga los enlaces desde el perfil seleccionado en Profile:. | — |
| Import... | Botón | Importa un archivo de perfil al almacén — un archivo XML de perfil de AetherSDR o un archivo ".map" de SmartSDR. Nuevo en v26.8.4. Informa cuántos enlaces se importaron y le permite usar Load para aplicarlos. | — |
| Export... | Botón | Exporta los enlaces actuales como un archivo XML de perfil de AetherSDR. Nuevo en v26.8.4. Se recuerda el último directorio utilizado. | `MidiImportExportPath` |
| Close | Botón | Cierra el diálogo. | — |

## Consejos

- Mueva un control en su hardware MIDI mientras el indicador de actividad está visible para confirmar que AetherSDR está recibiendo mensajes antes de intentar agregar un enlace.
- Si usa varios controladores o configuraciones físicas diferentes, guarde un perfil separado para cada uno con un nombre distinto en Profile: para poder cambiar rápidamente con Load.
- Use las opciones ampliadas de Category (Mode, Band, Filter, Slice, Display, Frequency) para reducir rápidamente los parámetros para funciones específicas.
- El diálogo ahora se adapta al tema actual. El estado del puerto y las etiquetas de actividad, así como la tabla de enlaces, usan colores del tema en lugar de valores fijos.
- Al agregar un enlace, el modo Learn es la forma más rápida de capturar el mensaje exacto que envía su hardware. Use Manual… o el botón ✎ por fila solo cuando necesite especificar un mensaje difícil de generar con hardware, o para corregir un enlace existente.

## Relacionados

- [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-connect MIDI controller on startup](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md)
- [Enter a binding manually](enter-a-binding-manually.md)
- [Edit an existing binding](edit-an-existing-binding.md)
- [Invert a knob or treat it as an endless encoder](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Delete a binding](delete-a-binding.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
- [Import a MIDI mapping from a file](import-a-midi-mapping-from-a-file.md)
- [Export the current mapping to a file](export-the-current-mapping-to-a-file.md)
