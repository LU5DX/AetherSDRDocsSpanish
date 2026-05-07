# Resumen de accesos rápidos de teclado

AetherSDR permite asignar accesos rápidos de teclado a acciones de la aplicación y editar esas asignaciones en cualquier momento. Utilice el diálogo de Accesos rápidos de teclado para ver, reasignar, borrar o restablecer asignaciones sin necesidad de reiniciar la aplicación.

## Antes de empezar

- No se requiere conexión a la radio para abrir o usar el editor de accesos rápidos.
- El procesamiento de accesos rápidos de teclado debe estar habilitado. Verifique que `View > Keyboard Shortcuts` esté marcado.

## Cómo funciona

Abra el editor en `View > Configure Shortcuts...`. El diálogo tiene dos áreas principales: un mapa de teclado visual en la parte superior y una tabla de acciones filtrable debajo.

**Keyboard map** — Una distribución QWERTY que muestra todas las teclas. Las teclas con acciones asignadas están codificadas por colores según su categoría. Una leyenda debajo del mapa muestra qué color corresponde a cada categoría. Haga clic en cualquier tecla para seleccionarla; el panel debajo del mapa se actualiza para mostrar lo que está asignado a esa tecla.

**Selected key panel** — Aparece entre el mapa de teclado y la tabla de acciones. Cuando una tecla está seleccionada:

- `Key:` muestra el nombre de la tecla seleccionada. Valor predeterminado: `(none)` cuando no hay nada seleccionado.
- `Action:` es un cuadro combinado. Elija una acción de la lista para asignarla a la tecla seleccionada.
- `Category` muestra la categoría de la acción actualmente asignada.
- Haga clic en `Clear` para eliminar la asignación de la tecla seleccionada.
- Haga clic en `Reset to Default` para restaurar la tecla predeterminada para la acción asignada a la tecla seleccionada.

Si asigna una tecla que ya está vinculada a una acción diferente, AetherSDR le solicitará que confirme la reasignación antes de realizar el cambio.

**Action table** — Enumera todas las acciones disponibles. Las columnas son Action, Category, Current Key y Default Key. Haga clic en una fila para seleccionarla y reflejar esa acción en el panel de tecla seleccionada.

- `Filter:` reduce la tabla escribiendo cualquier parte del nombre de una acción o categoría.
- `Category:` filtra la tabla a una sola categoría. La selección predeterminada es `All`.

**Controles inferiores**

- `Reset All to Defaults` — Restablece todas las asignaciones a su tecla predeterminada. AetherSDR solicita confirmación antes de proceder.
- `Close` — Cierra el diálogo.

## Consejos

- La tabla de acciones siempre muestra tanto la tecla actual como la predeterminada para cada acción, para que pueda ver de un vistazo lo que se ha cambiado.
- Seleccionar una fila en la tabla de acciones y seleccionar una tecla en el mapa de teclado son operaciones independientes. Asigne un acceso rápido seleccionando primero una tecla en el mapa y luego eligiendo la acción del cuadro combinado `Action:`.

## Relacionado

- [Rebind a keyboard shortcut](rebind-a-keyboard-shortcut.md)
- [Reset one shortcut to its default key](reset-one-shortcut-to-its-default-key.md)
- [Reset every shortcut back to defaults](reset-every-shortcut-back-to-defaults.md)
- [Find all actions in a category](find-all-actions-in-a-category.md)
- [See the default key for any action](see-the-default-key-for-any-action.md)
