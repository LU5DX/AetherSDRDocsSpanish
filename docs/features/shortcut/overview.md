# Descripción general de los atajos de teclado

AetherSDR permite asignar atajos de teclado a las acciones de la aplicación y editar esas asignaciones en cualquier momento. Use el diálogo Keyboard Shortcuts para ver, reasignar, borrar o restablecer asignaciones sin necesidad de reiniciar la aplicación.

## Antes de comenzar

- No se requiere conexión a una radio para abrir o usar el editor de atajos.
- El procesamiento de atajos de teclado debe estar habilitado. Confirme que `View > Keyboard Shortcuts` esté marcado.

## Cómo funciona

Abra el editor desde `View > Configure Shortcuts...`. El diálogo tiene dos áreas principales: un mapa visual del teclado en la parte superior y una tabla de acciones con filtro en la parte inferior.

**Mapa del teclado** — Un diseño QWERTY que muestra todas las teclas. Las teclas con acciones asignadas están codificadas por color según la categoría. Una leyenda debajo del mapa indica qué color corresponde a qué categoría. Haga clic en cualquier tecla para seleccionarla; el panel debajo del mapa se actualiza para mostrar lo que está asignado a esa tecla.

**Panel de tecla seleccionada** — Aparece entre el mapa del teclado y la tabla de acciones. Cuando se selecciona una tecla:

- `Key:` muestra el nombre de la tecla seleccionada. Valor predeterminado: `(none)` cuando no hay nada seleccionado.
- `Action:` es un cuadro combinado. Elija una acción de la lista para asignarla a la tecla seleccionada.
- `Category` muestra la categoría de la acción asignada actualmente.
- Haga clic en `Clear` para eliminar la asignación de la tecla seleccionada.
- Haga clic en `Reset to Default` para restaurar la tecla predeterminada de la acción asignada a la tecla seleccionada.

Si asigna una tecla que ya está vinculada a una acción diferente, AetherSDR le pedirá que confirme la reasignación antes de realizar el cambio.

**Tabla de acciones** — Lista todas las acciones disponibles. Las columnas son Action, Category, Current Key y Default Key. Haga clic en una fila para seleccionarla y reflejar esa acción en el panel de tecla seleccionada.

- `Filter:` reduce la tabla al escribir cualquier parte del nombre de una acción o de una categoría.
- `Category:` filtra la tabla a una sola categoría. La selección predeterminada es `All`.

**Controles inferiores**

- `Reset All to Defaults` — Restablece todas las asignaciones a sus teclas predeterminadas. AetherSDR solicita confirmación antes de continuar.
- `Close` — Cierra el diálogo.

## Consejos

- La tabla de acciones siempre muestra tanto la tecla actual como la tecla predeterminada de cada acción, de modo que se puede ver de un vistazo qué ha cambiado.
- Seleccionar una fila en la tabla de acciones y seleccionar una tecla en el mapa del teclado son operaciones independientes. Para asignar un atajo, seleccione primero una tecla en el mapa y luego elija la acción en el cuadro combinado `Action:`.

## Temas relacionados

- [Reasignar un atajo de teclado](rebind-a-keyboard-shortcut.md)
- [Restablecer un atajo a su tecla predeterminada](reset-one-shortcut-to-its-default-key.md)
- [Restablecer todos los atajos a sus valores predeterminados](reset-every-shortcut-back-to-defaults.md)
- [Buscar todas las acciones de una categoría](find-all-actions-in-a-category.md)
- [Ver la tecla predeterminada de cualquier acción](see-the-default-key-for-any-action.md)
