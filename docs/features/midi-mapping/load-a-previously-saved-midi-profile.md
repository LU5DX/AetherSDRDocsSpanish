# Cargar un perfil MIDI previamente guardado

Cargar un perfil guardado reemplaza las vinculaciones actuales con las almacenadas bajo ese nombre de perfil, lo que le permite alternar entre configuraciones de controlador sin tener que volver a aprender cada vinculación.

## Antes de empezar

- Debe existir un perfil MIDI. Si aún no ha guardado ninguno, consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Abra el cuadro de diálogo MIDI Controller Mapping mediante `Settings > MIDI Mapping...`.

## Pasos

1. En el cuadro combinado **Profile:**, seleccione el nombre del perfil que desea cargar. Si la lista está vacía, aún no se han guardado perfiles.
2. Haga clic en Load.

Las vinculaciones actuales se reemplazan con las vinculaciones almacenadas en el perfil seleccionado. La tabla Bindings se actualiza inmediatamente para mostrar las vinculaciones cargadas.

## Función de cada control

| Control        | Tipo         | Comportamiento                                                       |
|----------------|--------------|----------------------------------------------------------------------|
| Profile:       | Cuadro combinado | Selecciona un perfil de asignación MIDI guardado para cargar o guardar. Editable. |
| Load           | Botón        | Reemplaza las vinculaciones actuales con las del perfil seleccionado.   |
| Bindings table | Lista        | Muestra las vinculaciones activas después de la carga.                |

## Consejos

- El cuadro combinado Profile: es editable. Si escribe un nombre que no coincide con un perfil guardado y hace clic en Load, no se carga nada; no se muestra ningún error y las vinculaciones actuales permanecen sin cambios.
- Después de cargar, las vinculaciones cargadas se persisten inmediatamente como las vinculaciones activas. No es necesario volver a hacer clic en Save para mantenerlas activas durante la sesión actual.

## Solución de problemas

- **Se hace clic en Load pero la tabla Bindings no cambia** — El nombre del perfil en el cuadro combinado Profile: no coincide con ningún perfil guardado, o el campo de nombre está vacío. Seleccione un nombre de la lista desplegable en lugar de escribirlo manualmente.
- **La lista Profile: está vacía** — No se han guardado perfiles. Consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).

## Relacionados

- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Registrar una nueva vinculación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Descripción general de MIDI Controller Mapping](overview.md)
