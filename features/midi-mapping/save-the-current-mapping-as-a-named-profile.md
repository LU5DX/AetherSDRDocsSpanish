# Guardar la asignación actual como un perfil con nombre

Guarde sus asignaciones MIDI actuales con un nombre para poder recargarlas más adelante. Esto es útil cuando cambia entre controladores o desea mantener asignaciones separadas para diferentes modos de operación.

## Antes de comenzar

- Abra el diálogo MIDI Controller Mapping desde `Settings > MIDI Mapping...`.
- Tenga al menos una asignación en la tabla Bindings. Guardar una asignación vacía está permitido, pero rara vez es útil.

## Pasos

1. En el cuadro combinado **Profile:**, escriba un nombre para el perfil. El cuadro combinado es editable — haga clic en él y escriba directamente.
2. Haga clic en Save.

El perfil se almacena de inmediato. El cuadro combinado **Profile:** se actualiza y el nuevo nombre aparece en la lista.

## Qué hace cada control

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| Profile: | Cuadro combinado (editable) | Escriba un nombre nuevo o seleccione uno existente. Acepta texto libre. | — |
| Save | Botón | Guarda las asignaciones actuales con el nombre mostrado en **Profile:**. Si ya existe un perfil con ese nombre, se sobreescribe. | — |
| Load | Botón | Carga las asignaciones del perfil seleccionado en **Profile:**. Reemplaza todas las asignaciones actuales. | — |

## Sugerencias

- Los nombres de perfil se recortan de espacios iniciales y finales antes de guardarse. Un nombre vacío o compuesto solo de espacios no se guardará.
- Para sobreescribir un perfil existente, seleccione su nombre en el cuadro combinado **Profile:** y haga clic en Save nuevamente.

## Solución de problemas

- **Hacer clic en Save no tiene efecto** — El campo **Profile:** está en blanco o contiene solo espacios. Escriba un nombre antes de hacer clic en Save.
- **Un nombre de perfil que escribió no aparece en la lista después de guardar** — Es posible que el nombre contenga solo espacios. Confirme que el campo muestre caracteres visibles y haga clic en Save nuevamente.

## Temas relacionados

- [Cargar un perfil MIDI guardado anteriormente](load-a-previously-saved-midi-profile.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Descripción general de MIDI Controller Mapping](overview.md)
