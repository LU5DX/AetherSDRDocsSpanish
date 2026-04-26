# Cargar un perfil MIDI guardado previamente

Cargar un perfil guardado reemplaza las asignaciones actuales con las almacenadas bajo ese nombre de perfil, lo que permite cambiar entre configuraciones de controlador sin tener que reasignar cada enlace manualmente.

## Antes de comenzar

- Debe existir un perfil MIDI previamente guardado. Si aún no ha guardado ninguno, consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).
- Abra el diálogo MIDI Controller Mapping mediante `Settings > MIDI Mapping...`.

## Pasos

1. En el combo box **Profile:**, seleccione el nombre del perfil que desea cargar. Si la lista está vacía, no se ha guardado ningún perfil todavía.
2. Haga clic en Load.

Las asignaciones actuales se reemplazan con las almacenadas en el perfil seleccionado. La tabla Bindings se actualiza de inmediato para mostrar las asignaciones cargadas.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Profile: | Combo box | Selecciona un perfil de asignación MIDI guardado para cargar o guardar. Editable. | — |
| Load | Botón | Reemplaza las asignaciones actuales con las del perfil seleccionado. | — |
| Bindings table | Lista | Muestra las asignaciones activas tras la carga. | — |

## Consejos

- El combo box Profile: es editable. Si escribe un nombre que no coincide con ningún perfil guardado y hace clic en Load, no se cargará nada — no se mostrará ningún error y las asignaciones actuales permanecerán sin cambios.
- Después de cargar, las asignaciones cargadas quedan persistidas de inmediato como las asignaciones activas. No es necesario hacer clic en Save nuevamente para mantenerlas activas durante la sesión actual.

## Solución de problemas

- **Se hace clic en Load pero la tabla Bindings no cambia** — El nombre de perfil en el combo box Profile: no coincide con ningún perfil guardado, o el campo de nombre está vacío. Seleccione un nombre de la lista desplegable en lugar de escribirlo manualmente.
- **La lista Profile: está vacía** — No se ha guardado ningún perfil. Consulte [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).

## Relacionado

- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Descripción general de MIDI Controller Mapping](overview.md)
