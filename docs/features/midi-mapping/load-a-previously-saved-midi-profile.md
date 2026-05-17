# Cargar un perfil MIDI guardado previamente

Cargar un perfil guardado reemplaza las asignaciones actuales por las almacenadas en ese perfil, permitiéndole cambiar entre configuraciones de controlador sin tener que volver a aprender cada asignación.

## Antes de comenzar

- Debe existir un perfil MIDI. Si aún no ha guardado ninguno, consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Abra el diálogo de mapeo del controlador MIDI mediante `Settings > MIDI Mapping...`.

## Pasos

1. En el cuadro combinado **Profile:**, seleccione el nombre del perfil que desea cargar. Si la lista está vacía, significa que aún no se han guardado perfiles.
2. Haga clic en **Load**.

Las asignaciones actuales se reemplazan por las almacenadas en el perfil seleccionado. La tabla de asignaciones se actualiza inmediatamente para mostrar las asignaciones cargadas.

## Función de cada control

| Control        | Tipo          | Comportamiento                                                     |
|----------------|---------------|--------------------------------------------------------------------|
| Profile:       | Cuadro combinado | Selecciona un perfil de mapeo MIDI guardado para cargar o guardar. Editable. |
| Load           | Botón         | Reemplaza las asignaciones actuales por las del perfil seleccionado. |
| Tabla de asignaciones | Lista | Muestra las asignaciones activas después de la carga.             |

## Opciones del filtro por categoría

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

Seleccionar una categoría limita el cuadro combinado **Parameter** a las entradas de ese grupo, facilitando la búsqueda del control que desea asignar.

## Opciones de parámetros

El cuadro combinado **Parameter** contiene todos los parámetros disponibles para asignación. En la versión v26.5.2.1, se agregaron tres acciones momentáneas (Gate) en la categoría Phone/CW:

- **Trigger straight key** (id: `cwkey`)
- **Trigger CW Left Paddle** (id: `cwdit`)
- **Trigger CW Right Paddle** (id: `cwdah`)

Los IDs heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al nuevo formato al cargar perfiles antiguos.

## Consejos

- El cuadro combinado **Profile:** es editable. Si escribe un nombre que no coincide con un perfil guardado y hace clic en Load, no se carga nada; no se muestra ningún error y las asignaciones actuales permanecen sin cambios.
- Después de cargar, las asignaciones cargadas se guardan inmediatamente como asignaciones activas. No es necesario hacer clic en Save nuevamente para mantenerlas activas en la sesión actual.

## Solución de problemas

- **Se hace clic en Load pero la tabla de asignaciones no cambia** — El nombre del perfil en el cuadro combinado **Profile:** no coincide con ningún perfil guardado, o el campo de nombre está vacío. Seleccione un nombre de la lista desplegable en lugar de escribirlo manualmente.
- **La lista de Profile: está vacía** — No se han guardado perfiles. Consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).

## Relacionados

- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Grabar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Descripción general del mapeo del controlador MIDI](overview.md)
