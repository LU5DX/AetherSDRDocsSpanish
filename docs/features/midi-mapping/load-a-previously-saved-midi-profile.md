# Cargar un perfil MIDI guardado previamente

Cargue un perfil de mapeo MIDI con nombre para restaurar un conjunto completo de asignaciones guardadas anteriormente. Esto es útil al cambiar entre controladores o posiciones de operación.

## Antes de comenzar

- Debe existir al menos un perfil. Si aún no ha guardado un perfil, consulte [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Abra el diálogo MIDI Controller Mapping mediante `Settings > MIDI Mapping...`.

## Pasos

1. En el cuadro combinado **Profile:**, seleccione el nombre del perfil que desea cargar. Si la lista está vacía, todavía no se ha guardado ningún perfil.
2. Haga clic en **Load**.

Las asignaciones existentes se borran y se reemplazan con las almacenadas en el perfil seleccionado. La tabla de asignaciones se actualiza inmediatamente para reflejar el perfil cargado.

## Consejos

- Cargar un perfil sobrescribe todas las asignaciones actuales sin un mensaje de confirmación. Si desea conservar las asignaciones actuales, guárdelas como perfil antes de cargar otro.
- El cuadro combinado **Profile:** es editable. Escriba un nombre o seleccione uno de la lista desplegable.

## Solución de problemas

- **Al hacer clic en Load no ocurre nada** — El campo **Profile:** puede estar vacío o contener solo espacios en blanco. Seleccione un nombre de perfil de la lista desplegable antes de hacer clic en Load.
- **La lista Profile: está vacía** — Todavía no se ha guardado ningún perfil. Consulte [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- **La tabla de asignaciones está vacía después de cargar** — El perfil seleccionado se guardó sin asignaciones, o los datos del perfil no pudieron leerse. Guarde un nuevo perfil con las asignaciones correctas e inténtelo de nuevo.

## Relacionados

- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
