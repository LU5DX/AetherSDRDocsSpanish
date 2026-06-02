# Resumen de Atajos de Teclado

AetherSDR le permite asignar atajos de teclado a las acciones de la aplicación y editar esas asignaciones en cualquier momento. Utilice el cuadro de diálogo de Atajos de Teclado para ver, reasignar, limpiar o restablecer las asignaciones sin necesidad de reiniciar la aplicación.

## Antes de comenzar

- No se requiere conexión de radio para abrir o usar el editor de atajos.
- El procesamiento de atajos de teclado debe estar habilitado. Confirme que `View > Keyboard Shortcuts` esté marcado.

## Cómo funciona

Abra el editor en `View > Configure Shortcuts...`. El cuadro de diálogo tiene dos áreas principales: un mapa de teclado visual en la parte superior y una tabla de acciones filtrable debajo.

**Mapa de teclado** — Una distribución QWERTY que muestra todas las teclas. Las teclas con acciones asignadas están codificadas por colores según la categoría. Una leyenda debajo del mapa muestra qué color corresponde a cada categoría. Haga clic en cualquier tecla para seleccionarla; el panel debajo del mapa se actualiza para mostrar qué está asignado a esa tecla.

**Panel de tecla seleccionada** — Aparece entre el mapa de teclado y la tabla de acciones. Cuando se selecciona una tecla:

- `Key:` muestra el nombre de la tecla seleccionada. Valor predeterminado: `(none)` cuando no hay nada seleccionado.
- `Action:` es un cuadro combinado. Elija una acción de la lista para asignarla a la tecla seleccionada.
- `Category` muestra la categoría de la acción actualmente asignada.
- Haga clic en `Clear` para eliminar la asignación de la tecla seleccionada.
- Haga clic en `Reset to Default` para restaurar la tecla predeterminada para la acción asignada a la tecla seleccionada.

Si asigna una tecla que ya está vinculada a una acción diferente, AetherSDR le solicita que confirme la reasignación antes de realizar el cambio.

**Tabla de acciones** — Enumera todas las acciones disponibles. Las columnas son: Action, Category, Current Key y Default Key. Haga clic en una fila para seleccionarla y reflejar esa acción en el panel de tecla seleccionada.

- `Filter:` reduce la tabla escribiendo cualquier parte del nombre de una acción o nombre de categoría.
- `Category:` filtra la tabla a una sola categoría. La selección predeterminada es `All`.

**Controles inferiores**

- `Reset All to Defaults` — Restablece todas las asignaciones a sus teclas predeterminadas. AetherSDR solicita confirmación antes de proceder.
- `Close` — Cierra el cuadro de diálogo.

## Consejos

- La tabla de acciones siempre muestra tanto la tecla actual como la predeterminada para cada acción, para que pueda ver de un vistazo lo que se ha cambiado.
- Seleccionar una fila en la tabla de acciones y seleccionar una tecla en el mapa de teclado son operaciones independientes. Asigne una vinculación seleccionando primero una tecla en el mapa y luego eligiendo la acción del cuadro combinado `Action:`.

## Relacionados

- [Rebind a keyboard shortcut](rebind-a-keyboard-shortcut.md)
- [Reset one shortcut to its default key](reset-one-shortcut-to-its-default-key.md)
- [Reset every shortcut back to defaults](reset-every-shortcut-back-to-defaults.md)
- [Find all actions in a category](find-all-actions-in-a-category.md)
- [See the default key for any action](see-the-default-key-for-any-action.md)
