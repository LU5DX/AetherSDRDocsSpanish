# Cargar un perfil MIDI guardado previamente

Cargar un perfil guardado reemplaza las asignaciones actuales con aquellas almacenadas bajo ese nombre de perfil, lo que le permite cambiar entre configuraciones de controlador sin tener que volver a aprender cada asignación.

## Antes de comenzar

- Debe existir un perfil MIDI. Si aún no ha guardado uno, consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Abra el cuadro de diálogo MIDI Controller Mapping mediante `Settings > MIDI Mapping...`.

## Pasos

1. En el cuadro combinado **Profile:**, seleccione el nombre del perfil que desea cargar. Si la lista está vacía, aún no se ha guardado ningún perfil.
2. Haga clic en **Load**.

Las asignaciones actuales se reemplazan con las asignaciones almacenadas en el perfil seleccionado. La tabla de Bindings se actualiza inmediatamente para mostrar las asignaciones cargadas.

## Función de cada control

| Control         | Tipo        | Comportamiento                                                     |
|-----------------|-------------|---------------------------------------------------------------------|
| Profile:        | Cuadro combinado | Selecciona un perfil de asignación MIDI guardado para cargar o guardar. Editable. |
| Load            | Botón       | Reemplaza las asignaciones actuales con las del perfil seleccionado. |
| Bindings table  | Lista       | Muestra las asignaciones ahora activas después de la carga.         |

## Opciones del filtro de categorías

El cuadro combinado **Category** filtra la lista de **Parameter** para mostrar solo los controles de un grupo específico. Categorías disponibles:

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

## Opciones de parámetros

El cuadro combinado **Parameter** contiene todos los parámetros disponibles para asignación. En v26.6.1, hay tres acciones momentáneas (Gate) disponibles en la categoría Phone/CW:

- **Trigger straight key** (id: `cwkey`)
- **Trigger CW Left Paddle** (id: `cwdit`)
- **Trigger CW Right Paddle** (id: `cwdah`)

Los ID heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al nuevo formato al cargar perfiles antiguos.

## Consejos

- El cuadro combinado **Profile:** es editable. Si escribe un nombre que no coincide con un perfil guardado y hace clic en Load, no se carga nada; no se muestra ningún error y las asignaciones actuales permanecen sin cambios.
- Después de cargar, las asignaciones cargadas se conservan inmediatamente como las asignaciones activas. No es necesario hacer clic en Save nuevamente para mantenerlas activas durante la sesión actual.

## Solución de problemas

- **Se hace clic en Load pero la tabla Bindings no cambia** — El nombre del perfil en el cuadro combinado **Profile:** no coincide con ningún perfil guardado, o el campo de nombre está vacío. Seleccione un nombre de la lista desplegable en lugar de escribirlo manualmente.
- **La lista de Profile: está vacía** — No se ha guardado ningún perfil. Consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).

## Relacionados

- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Descripción general de MIDI Controller Mapping](overview.md)
