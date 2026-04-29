# Restablecer un atajo a su tecla predeterminada

Use esta página para restaurar un solo atajo de teclado a la tecla con la que fue entregado, sin afectar ninguna otra asignación.

## Antes de comenzar

- Abra `View > Configure Shortcuts...` para acceder al diálogo Keyboard Shortcuts.
- Identifique la acción cuya asignación desea restaurar. Si no está seguro de cuál es la tecla predeterminada, consulte la columna **Default Key** en la tabla de acciones.

## Pasos

1. Abra `View > Configure Shortcuts...`.
2. En la tabla de acciones, localice la acción que desea restablecer. Use el campo **Filter:** o el cuadro combinado **Category:** para reducir la lista si es necesario.
3. Haga clic en la fila de la tabla de acciones para seleccionar la acción.
4. En el mapa de teclado, confirme que la tecla correcta está resaltada y se muestra en el indicador **Key:**.
5. Haga clic en **Reset to Default**.

La asignación se restaura de inmediato a la tecla predeterminada de la acción. La tabla de acciones se actualiza para mostrar el cambio en la columna **Current Key**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Keyboard map | Indicador visual | Distribución QWERTY; haga clic en una tecla para seleccionarla y rellenar el indicador **Key:**. |
| **Key:** | Indicador | Muestra la tecla seleccionada actualmente. Muestra `(none)` cuando no hay ninguna tecla seleccionada. |
| **Action:** | Cuadro combinado | Muestra la acción asignada a la tecla seleccionada. |
| **Category** | Indicador | Muestra la categoría de la acción asignada a la tecla seleccionada. |
| **Reset to Default** | Botón | Restaura la tecla predeterminada de la acción actualmente asignada a la tecla seleccionada. |
| **Filter:** | Campo de texto | Filtra la tabla de acciones por texto. |
| **Category:** | Cuadro combinado | Filtra la tabla de acciones por categoría. |
| Action table | Lista | Todas las acciones con columnas: Action, Category, Current Key, Default Key. |
| **Reset All to Defaults** | Botón | Restablece todas las asignaciones a su tecla predeterminada — úselo con precaución. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- La columna **Default Key** en la tabla de acciones siempre muestra el valor predeterminado de fábrica, incluso después de haber cambiado la asignación. Úsela para confirmar qué restaurará **Reset to Default** antes de hacer clic.
- Si la acción que desea está asignada a una tecla que entra en conflicto con otra asignación, restablecer una acción puede liberar esa tecla para otra. Revise la columna **Current Key** después de restablecer.

## Relacionados

- [Descripción general de Keyboard Shortcuts](overview.md)
- [Reasignar un atajo de teclado](rebind-a-keyboard-shortcut.md)
- [Restablecer todos los atajos a sus valores predeterminados](reset-every-shortcut-back-to-defaults.md)
- [Ver la tecla predeterminada de cualquier acción](see-the-default-key-for-any-action.md)
- [Encontrar todas las acciones de una categoría](find-all-actions-in-a-category.md)
