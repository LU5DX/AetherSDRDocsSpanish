# Cargar un perfil MIDI previamente guardado

Cargar un perfil guardado reemplaza las asignaciones actuales con las almacenadas bajo ese nombre de perfil, permitiéndole cambiar entre configuraciones de controlador sin tener que volver a aprender cada asignación.

## Antes de comenzar

- Debe existir un perfil MIDI. Si aún no ha guardado ninguno, consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Abra el diálogo de Asignación de Controlador MIDI mediante `Settings > MIDI Mapping...`.

## Pasos

1. En el cuadro combinado **Profile:**, seleccione el nombre del perfil que desea cargar. Si la lista está vacía, aún no se han guardado perfiles.
2. Haga clic en **Load**.

Las asignaciones actuales se reemplazan con las asignaciones almacenadas en el perfil seleccionado. La tabla de asignaciones se actualiza inmediatamente para mostrar las asignaciones cargadas.

## Qué hace cada control

| Control         | Tipo           | Comportamiento                                                     |
|-----------------|----------------|--------------------------------------------------------------------|
| Profile:        | Cuadro combinado | Selecciona un perfil de asignación MIDI guardado para cargar o guardar. Editable. |
| Load            | Botón          | Reemplaza las asignaciones actuales con las del perfil seleccionado. |
| Tabla de asignaciones | Lista        | Muestra las asignaciones activas después de la carga.              |

## Opciones del filtro de categoría

El cuadro combinado **Category** filtra la lista de **Parameter** para mostrar solo controles de un grupo específico. Categorías disponibles:

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

## Consejos

- El cuadro combinado **Profile:** es editable. Si escribe un nombre que no coincide con un perfil guardado y hace clic en **Load**, no se carga nada — no se muestra ningún error y las asignaciones actuales permanecen sin cambios.
- Después de cargar, las asignaciones cargadas se persisten inmediatamente como las asignaciones activas. No necesita hacer clic en **Save** nuevamente para mantenerlas activas durante la sesión actual.

## Solución de problemas

- **Se hace clic en Load pero la tabla de asignaciones no cambia** — El nombre del perfil en el cuadro combinado **Profile:** no coincide con ningún perfil guardado, o el campo de nombre está vacío. Seleccione un nombre de la lista desplegable en lugar de escribirlo manualmente.
- **La lista Profile: está vacía** — No se han guardado perfiles. Consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).

## Relacionados

- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Grabar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Visión general de la asignación de controlador MIDI](overview.md)
