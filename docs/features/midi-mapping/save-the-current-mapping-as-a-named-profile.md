# Guardar el Mapeado Actual como un Perfil con Nombre

Guarde sus asignaciones MIDI actuales con un nombre para poder recuperarlas más tarde o cambiar entre configuraciones de controlador sin tener que reaprender cada asignación.

## Antes de comenzar

- Debe existir al menos una asignación en la tabla Bindings. Un mapeado vacío se puede guardar, pero no es útil.
- Abra `Settings > MIDI Mapping...` para acceder al diálogo MIDI Controller Mapping.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Confirme que la tabla Bindings muestra las asignaciones que desea guardar.
3. En el campo **Profile:**, escriba un nombre para el perfil. El campo acepta texto libre; también muestra los nombres de perfiles existentes en su lista desplegable si se ha guardado alguno anteriormente.
4. Haga clic en **Save**.

El perfil se almacena de inmediato. La lista desplegable **Profile:** se actualiza para incluir el nuevo nombre.

## Qué hace cada control

| Control | Función | Clave de configuración |
|---|---|---|
| **Profile:** | Cuadro combinado editable. Escriba un nombre nuevo para crear un perfil, o seleccione un nombre existente de la lista desplegable para sobreescribirlo. | — |
| **Save** | Guarda las asignaciones actuales con el nombre indicado en **Profile:**. No hace nada si el campo está vacío. | — |
| **Load** | Reemplaza las asignaciones actuales con las almacenadas bajo el nombre de perfil seleccionado. | — |

## Consejos

- Si escribe un nombre que ya existe en **Profile:** y hace clic en **Save**, ese perfil se sobreescribe sin ningún mensaje de confirmación.
- Para mantener asignaciones separadas para distintos controladores, utilice un nombre descriptivo, como el modelo del controlador o el caso de uso.

## Solución de problemas

- **Al hacer clic en Save no ocurre nada** — El campo **Profile:** está vacío o contiene solo espacios. Escriba un nombre primero.
- **El nombre de un perfil no aparece en la lista desplegable después de guardarlo** — Haga clic en cualquier lugar para cerrar la lista desplegable y vuelva a abrirla; la lista se actualiza después de cada guardado.

## Relacionado

- [Cargar un perfil MIDI guardado anteriormente](load-a-previously-saved-midi-profile.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Descripción general de MIDI Controller Mapping](overview.md)
