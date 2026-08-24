# Cargar un perfil MIDI guardado previamente

Cargar un perfil guardado reemplaza las asignaciones actuales por las almacenadas bajo ese nombre de perfil, lo que le permite cambiar entre configuraciones de controlador sin tener que volver a aprender cada asignación.

## Antes de comenzar

- Debe existir un perfil MIDI. Si aún no ha guardado uno, consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Abra el diálogo MIDI Controller Mapping mediante `Settings > MIDI Mapping...`.

## Pasos

1. En el cuadro combinado **Profile:**, seleccione el nombre del perfil que desea cargar. Si la lista está vacía, no se ha guardado ningún perfil todavía.
2. Haga clic en **Load**.

Las asignaciones actuales se reemplazan por las asignaciones almacenadas en el perfil seleccionado. La tabla Bindings se actualiza inmediatamente para mostrar las asignaciones cargadas.

## Qué hace cada control

| Control          | Tipo                                                                                             | Comportamiento                                                                                                                                                                                                                                                          |
|------------------|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Port:            | Cuadro combinado                                                                                 | Selecciona el dispositivo de entrada MIDI.                                                                                                                                                                                                                              |
| Refresh          | Botón                                                                                            | Vuelve a escanear los puertos MIDI disponibles.                                                                                                                                                                                                                         |
| Connect          | Botón                                                                                            | Abre o cierra el puerto MIDI seleccionado.                                                                                                                                                                                                                              |
| Auto-connect on startup | Casilla de verificación                                                                   | Reabre el puerto MIDI al iniciar la aplicación.                                                                                                                                                                                                                         |
| Category         | Cuadro combinado                                                                                 | Filtra la lista Parameter a una categoría de control.                                                                                                                                                                                                                   |
| Parameter        | Cuadro combinado                                                                                 | Elige el parámetro de destino para una nueva asignación. En v26.8.4, hay tres acciones momentáneas (Gate) disponibles en la categoría Phone/CW: **Trigger straight key** (`cwkey`), **Trigger CW Left Paddle** (`cwdit`), **Trigger CW Right Paddle** (`cwdah`). Los IDs heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leerlos. |
| Learn            | Botón                                                                                            | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado.                                                                                                                                                                                    |
| Manual…          | Botón                                                                                            | Abre un diálogo para escribir el canal, tipo de mensaje y número de una asignación en lugar de usar el modo Learn. Nuevo en v26.8.4 (#4760). Abre el mismo editor manual que usa el botón de edición por fila.                                                          |
| Bindings table   | Muestra las asignaciones existentes con controles por fila de Invert, Relative, edición (✎) y eliminación. | Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (editar), (eliminar).                                                                                                                                                                                       |
| ✎ (editar asignación) | Botón                                                                                     | Abre el editor manual para corregir el canal, tipo y número de esta asignación. Nuevo en v26.8.4 (#4760).                                                                                                                                                               |
| Invert           | Casilla de verificación                                                                          | Invierte la dirección del control para la fila.                                                                                                                                                                                                                         |
| Relative         | Casilla de verificación                                                                          | Trata el control como un codificador rotatorio infinito.                                                                                                                                                                                                                |
| × (eliminar fila) | Botón                                                                                            | Elimina esa asignación.                                                                                                                                                                                                                                                 |
| Clear All        | Botón                                                                                            | Elimina todas las asignaciones.                                                                                                                                                                                                                                         |
| Profile:         | Cuadro combinado                                                                                 | Selecciona un perfil de mapeo MIDI guardado para cargar o guardar. Editable.                                                                                                                                                                                            |
| Save             | Botón                                                                                            | Guarda las asignaciones actuales como un perfil.                                                                                                                                                                                                                        |
| Load             | Botón                                                                                            | Reemplaza las asignaciones actuales con las del perfil seleccionado.                                                                                                                                                                                                    |
| Import...        | Botón                                                                                            | Importa un archivo de perfil al almacén — XML de perfil de AetherSDR o un archivo ".map" de SmartSDR. Nuevo en v26.8.4. Informa cuántas asignaciones se importaron y permite al usuario hacer clic en Load para aplicarlas.                                               |
| Export...        | Botón                                                                                            | Exporta las asignaciones actuales como un archivo XML de perfil de AetherSDR. Nuevo en v26.8.4. El directorio recordado se conserva bajo `MidiImportExportPath`.                                                                                                        |
| Close            | Botón                                                                                            | Cierra el diálogo.                                                                                                                                                                                                                                                      |

## Indicador de estado del puerto

El indicador **Port status** muestra si el puerto MIDI está actualmente abierto:
- **Opened** — El puerto MIDI está activo y recibiendo mensajes.
- **Closed** — El puerto MIDI no está abierto.

## Indicador de actividad

El **Activity indicator** muestra el mensaje MIDI más reciente recibido, lo que le ayuda a confirmar que el controlador está enviando datos.

## Opciones de filtro por categoría

El cuadro combinado **Category** filtra la lista **Parameter** para mostrar solo los controles de un grupo específico. Categorías disponibles:

- All
- RX
- TX
- Phone/CW
- EQ
- Global
- Mode
- Band
- Filter
- Slice
- Display
- Frequency

Seleccionar una categoría limita el cuadro combinado **Parameter** a las entradas de ese grupo, lo que facilita encontrar el control que desea asignar.

## Opciones de parámetro

El cuadro combinado **Parameter** contiene todos los parámetros disponibles para asignación. En v26.8.4, hay tres acciones momentáneas (Gate) disponibles en la categoría Phone/CW:

- **Trigger straight key** (id: `cwkey`)
- **Trigger CW Left Paddle** (id: `cwdit`)
- **Trigger CW Right Paddle** (id: `cwdah`)

Los IDs heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al nuevo formato al cargar perfiles antiguos.

## Consejos

- El cuadro combinado **Profile:** es editable. Si escribe un nombre que no coincide con un perfil guardado y hace clic en Load, no se carga nada — no se muestra ningún error y las asignaciones actuales permanecen sin cambios.
- Después de cargar, las asignaciones cargadas se conservan inmediatamente como asignaciones activas. No necesita hacer clic en Save nuevamente para mantenerlas activas durante la sesión actual.
- Use **Import...** para traer un archivo `.map` de SmartSDR. Después de la importación, haga clic en Load para aplicar las asignaciones importadas.
- El diálogo **Export...** recuerda el último directorio que usó, por lo que las exportaciones posteriores comienzan en la misma carpeta.

## Solución de problemas

- **Se hace clic en Load pero la tabla Bindings no cambia** — El nombre del perfil en el cuadro combinado **Profile:** no coincide con ningún perfil guardado, o el campo de nombre está vacío. Seleccione un nombre de la lista desplegable en lugar de escribirlo manualmente.
- **La lista Profile: está vacía** — No se ha guardado ningún perfil. Consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- **El puerto MIDI no se abre** — Haga clic en Refresh para volver a escanear los puertos disponibles, luego seleccione el dispositivo correcto en el cuadro combinado **Port:** y haga clic en Connect.

## Relacionado

- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Descripción general de MIDI Controller Mapping](overview.md)
