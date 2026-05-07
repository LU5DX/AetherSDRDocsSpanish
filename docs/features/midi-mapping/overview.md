# Resumen de asignación de controlador MIDI

La función de asignación de controlador MIDI le permite vincular perillas físicas, deslizadores y botones de un controlador MIDI a parámetros de radio en AetherSDR. Una vez guardadas las asignaciones, puede recuperarlas como perfiles con nombre y, opcionalmente, reconectar el controlador automáticamente en cada inicio.

## Antes de empezar

- Su controlador MIDI debe estar conectado a la computadora antes de abrir el diálogo.
- El soporte MIDI debe estar presente en su compilación de AetherSDR. Si `Settings > MIDI Mapping...` no aparece en el menú, su compilación se compiló sin soporte MIDI.

## Cómo funciona

Abra el diálogo en `Settings > MIDI Mapping...`. El diálogo está dividido en dos secciones: **MIDI Device** y **Parameter Bindings**.

**MIDI Device** maneja la selección del puerto y la conexión. Seleccione su controlador en el cuadro combinado Port:, haga clic en Refresh si no aparece, luego haga clic en Connect para abrir el puerto. El indicador de estado del puerto muestra "Connected" (verde) o "Disconnected" (gris). El indicador de actividad muestra el mensaje MIDI más reciente recibido — por ejemplo, `Ch 1 CC #7 = 64` — que es útil para confirmar que su controlador está enviando datos.

**Parameter Bindings** es donde crea y administra las asignaciones entre mensajes MIDI y controles de radio. Use los cuadros combinados Category y Parameter para localizar el parámetro objetivo, luego haga clic en Learn y mueva una perilla o deslizador en su controlador. AetherSDR registra el mensaje MIDI entrante y agrega una fila a la tabla de asignaciones. Cada fila en la tabla se puede ajustar individualmente con las casillas de verificación Invert y Relative, o eliminarse con el botón × (eliminar fila). Haga clic en Clear All para eliminar todas las asignaciones a la vez.

Las asignaciones se pueden guardar en perfiles con nombre y cargar desde ellos usando los controles Profile:, Save y Load en la parte inferior del diálogo.

Las asignaciones y el último puerto utilizado se conservan automáticamente. La configuración `MidiPort` almacena el nombre del puerto seleccionado y `MidiAutoConnect` almacena si el puerto debe reabrirse al inicio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI. | `MidiPort` |
| Refresh | Botón | Vuelve a escanear los puertos MIDI disponibles. | — |
| Connect | Botón | Abre el puerto MIDI seleccionado. Cuando un puerto está abierto, la etiqueta cambia a Disconnect. | — |
| Port status | Indicador | Muestra si el puerto MIDI está actualmente abierto. Estados: Opened, Closed. | — |
| Activity indicator | Indicador | Muestra el mensaje MIDI más reciente recibido. | — |
| Auto-connect on startup | Casilla de verificación | Vuelve a abrir automáticamente el puerto MIDI guardado cuando se inicia AetherSDR. | `MidiAutoConnect` |
| Category | Cuadro combinado | Filtra el cuadro combinado Parameter a una categoría de control (All, RX, TX, Phone/CW, EQ, Global). | — |
| Parameter | Cuadro combinado | Selecciona el parámetro de radio objetivo para una nueva asignación. | — |
| Learn | Botón | Comienza a escuchar el siguiente mensaje MIDI entrante y lo vincula al parámetro seleccionado. Haga clic nuevamente (etiquetado Cancel Learn) para abortar. | — |
| Bindings table | Lista | Muestra todas las asignaciones existentes. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminar. | — |
| Invert | Casilla de verificación (por fila) | Invierte la dirección de control para esa asignación. | — |
| Relative | Casilla de verificación (por fila) | Trata el control como un codificador sin fin en lugar de un valor absoluto. | — |
| × (delete row) | Botón (por fila) | Elimina esa asignación. | — |
| Clear All | Botón | Elimina todas las asignaciones. | — |
| Profile: | Cuadro combinado | Selecciona o nombra un perfil de asignación MIDI guardado. El campo es editable. | — |
| Save | Botón | Guarda las asignaciones actuales con el nombre ingresado en Profile:. | — |
| Load | Botón | Carga las asignaciones del perfil seleccionado en Profile:. | — |
| Close | Botón | Cierra el diálogo. | — |

## Consejos

- Mueva un control en su hardware MIDI mientras el indicador de actividad esté visible para confirmar que AetherSDR está recibiendo mensajes antes de intentar agregar una asignación.
- Si usa múltiples controladores o diferentes configuraciones físicas, guarde un perfil separado para cada uno con un nombre distinto en Profile: para poder cambiar rápidamente con Load.

## Relacionado

- [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-connect MIDI controller on startup](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md)
- [Invert a knob or treat it as an endless encoder](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Delete a binding](delete-a-binding.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
