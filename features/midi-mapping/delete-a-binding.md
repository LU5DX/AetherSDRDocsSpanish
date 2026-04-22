# Eliminar un binding

Elimine un binding MIDI individual de la tabla de bindings, o borre todos a la vez. Use esto cuando una asignación de controlador sea incorrecta, redundante o ya no sea necesaria.

## Antes de comenzar

- El diálogo MIDI Mapping debe estar abierto. Vaya a `Settings > MIDI Mapping...`.
- Debe haber al menos un binding existente visible en la tabla de bindings.

## Pasos

### Eliminar un binding

1. Abra `Settings > MIDI Mapping...`.
2. Localice el binding que desea eliminar en la tabla de bindings.
3. Haga clic en `×` en la columna más a la derecha de esa fila.

La fila se elimina de inmediato. El cambio se guarda automáticamente.

### Eliminar todos los bindings a la vez

1. Abra `Settings > MIDI Mapping...`.
2. Haga clic en `Clear All`.

Todas las filas de la tabla de bindings se eliminan. El cambio se guarda automáticamente.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Tabla de bindings | Lista | Muestra todos los bindings actuales. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y una columna de eliminación. |
| `×` (eliminar fila) | Botón | Elimina el binding de esa fila. |
| `Clear All` | Botón | Elimina todos los bindings de la tabla. |

## Consejos

- No hay mensaje de confirmación para `×` ni para `Clear All`. Si elimina bindings por error, puede restaurarlos cargando un perfil guardado previamente.
- Antes de realizar cambios grandes, guarde el estado actual usando `Save` para poder recuperarlo con `Load`.

## Relacionado

- [Registrar un nuevo binding con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Guardar la asignación actual como perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado previamente](load-a-previously-saved-midi-profile.md)
- [Descripción general del mapeo de controlador MIDI](overview.md)
