# Descripción general del mapeo de controladores MIDI

La función de mapeo de controladores MIDI permite asignar perillas físicas, faders y botones de un controlador MIDI a parámetros de radio en AetherSDR. Una vez guardadas las asignaciones, puede recuperarlas como perfiles con nombre y, opcionalmente, reconectar el controlador de forma automática en cada inicio.

## Antes de comenzar

- El controlador MIDI debe estar conectado a la computadora antes de abrir el diálogo.
- La compatibilidad con MIDI debe estar presente en su versión de AetherSDR. Si `Settings > MIDI Mapping...` no aparece en el menú, su versión fue compilada sin soporte MIDI.

## Cómo funciona

Abra el diálogo en `Settings > MIDI Mapping...`. El diálogo está dividido en dos secciones: **MIDI Device** y **Parameter Bindings**.

**MIDI Device** gestiona la selección del puerto y la conexión. Seleccione su controlador en el cuadro combinado Port:, haga clic en Refresh si no aparece y, luego, haga clic en Connect para abrir el puerto. El indicador de estado del puerto muestra "Connected" (verde) o "Disconnected" (gris). El indicador de actividad muestra el mensaje MIDI recibido más recientemente — por ejemplo, `Ch 1 CC #7 = 64` — lo cual es útil para confirmar que su controlador está enviando datos.

**Parameter Bindings** es donde se crean y gestionan las asignaciones entre mensajes MIDI y controles de radio. Use los cuadros combinados Category y Parameter para localizar el parámetro objetivo; luego, haga clic en Learn y mueva una perilla o un fader en su controlador. AetherSDR registra el mensaje MIDI entrante y agrega una fila a la tabla de asignaciones. Cada fila de la tabla puede ajustarse individualmente con las casillas Invert y Relative, o eliminarse con el botón × (eliminar fila). Haga clic en Clear All para eliminar todas las asignaciones a la vez.

Las asignaciones pueden guardarse y cargarse desde perfiles con nombre mediante los controles Profile:, Save y Load ubicados en la parte inferior del diálogo.

Las asignaciones y el último puerto utilizado se guardan automáticamente. El parámetro `MidiPort` almacena el nombre del puerto seleccionado y `MidiAutoConnect` almacena si el puerto debe reabrirse al iniciar.

## Qué hace cada control

| Control | Tipo | Comportamiento | Parámetro guardado |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI. | `MidiPort` |
| Refresh | Botón | Vuelve a analizar los puertos MIDI disponibles. | — |
| Connect | Botón | Abre el puerto MIDI seleccionado. Cuando el puerto está abierto, la etiqueta cambia a Disconnect. | — |
| Port status | Indicador | Muestra si el puerto MIDI está actualmente abierto. Estados: Opened, Closed. | — |
| Activity indicator | Indicador | Muestra el mensaje MIDI recibido más recientemente. | — |
| Auto-connect on startup | Casilla | Reabre el puerto MIDI guardado automáticamente cuando AetherSDR se inicia. | `MidiAutoConnect` |
| Category | Cuadro combinado | Filtra el cuadro combinado Parameter según una categoría de control (All, RX, TX, Phone/CW, EQ, Global). | — |
| Parameter | Cuadro combinado | Selecciona el parámetro de radio objetivo para una nueva asignación. | — |
| Learn | Botón | Comienza a escuchar el siguiente mensaje MIDI entrante y lo asigna al parámetro seleccionado. Haga clic de nuevo (etiquetado como Cancel Learn) para cancelar. | — |
| Bindings table | Lista | Muestra todas las asignaciones existentes. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminación. | — |
| Invert | Casilla (por fila) | Invierte la dirección del control para esa asignación. | — |
| Relative | Casilla (por fila) | Trata el control como un encoder continuo en lugar de un valor absoluto. | — |
| × (eliminar fila) | Botón (por fila) | Elimina esa asignación. | — |
| Clear All | Botón | Elimina todas las asignaciones. | — |
| Profile: | Cuadro combinado | Selecciona o nombra un perfil de mapeo MIDI guardado. El campo es editable. | — |
| Save | Botón | Guarda las asignaciones actuales con el nombre ingresado en Profile:. | — |
| Load | Botón | Carga las asignaciones desde el perfil seleccionado en Profile:. | — |
| Close | Botón | Cierra el diálogo. | — |

## Consejos

- Mueva un control en su hardware MIDI mientras el indicador de actividad esté visible para confirmar que AetherSDR está recibiendo mensajes antes de intentar agregar una asignación.
- Si usa varios controladores o diferentes configuraciones físicas, guarde un perfil separado para cada uno con un nombre distinto en Profile:, de modo que pueda cambiar rápidamente con Load.

## Relacionado

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Conectar automáticamente el controlador MIDI al iniciar](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Invertir una perilla o tratarla como un encoder continuo](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado anteriormente](load-a-previously-saved-midi-profile.md)
