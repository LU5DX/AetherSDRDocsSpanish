# Guardar la asiganación actual como un perfil nombrado

Guarde sus asignaciones MIDI actuales bajo un nombre para poder recuperarlas más tarde o cambiar entre configuraciones de controlador sin tener que volver a aprender cada asignación.

## Antes de comenzar

- Debe existir al menos una asignación en la tabla de Asignaciones. Se puede guardar una asignación vacía, pero no es útil.
- Abra `Settings > MIDI Mapping...` para acceder al diálogo de Asignación de Controlador MIDI.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Confirme que la tabla de Asignaciones muestra las asignaciones que desea guardar.
3. En el campo **Profile:**, escriba un nombre para el perfil. El campo acepta texto libre; también muestra los nombres de perfiles existentes en su lista desplegable si se han guardado algunos anteriormente.
4. Haga clic en **Save**.

El perfil se almacena inmediatamente. La lista desplegable **Profile:** se actualiza para incluir el nuevo nombre.

## Función de cada control

| Control      | Función                                                                                                              | Clave de configuración |
|--------------|----------------------------------------------------------------------------------------------------------------------|----------------------|
| **Profile:** | Cuadro combinado editable. Escriba un nombre nuevo para crear un perfil, o seleccione un nombre existente de la lista desplegable para sobrescribirlo. | —                    |
| **Save**     | Guarda las asignaciones actuales bajo el nombre mostrado en **Profile:**. No hace nada si el campo está vacío.          | —                    |
| **Load**     | Reemplaza las asignaciones actuales con las almacenadas bajo el nombre de perfil seleccionado.                         | —                    |

## Consejos

- Escribir un nombre que ya existe en **Profile:** y hacer clic en **Save** sobrescribe ese perfil sin una solicitud de confirmación.
- Para mantener las asignaciones de diferentes controladores separadas, use un nombre descriptivo como el modelo del controlador o el caso de uso.

## Solución de problemas

- **Al hacer clic en Save no ocurre nada** — El campo **Profile:** está vacío o contiene solo espacios. Escriba un nombre primero.
- **Un nombre de perfil no aparece en la lista desplegable después de guardar** — Haga clic en cualquier lugar para cerrar la lista desplegable y vuelva a abrirla; la lista se actualiza después de cada guardado.

## Relacionado

- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
- [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md)
- [Delete a binding](delete-a-binding.md)
- [MIDI Controller Mapping overview](overview.md)
