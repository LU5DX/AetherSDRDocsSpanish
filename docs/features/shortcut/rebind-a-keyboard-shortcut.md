# Reasignar un atajo de teclado

Use el diálogo Keyboard Shortcuts para asignar una tecla diferente a cualquier acción, o para reasignar una tecla que ya está en uso.

## Antes de comenzar

- No se requiere conexión a la radio para editar los atajos.
- Confirme que el procesamiento de atajos de teclado esté habilitado mediante `View > Keyboard Shortcuts` (elemento con marca de verificación).

## Pasos

1. Abra `View > Configure Shortcuts...`.
2. Encuentre la acción que desea reasignar. Puede:
   - Hacer clic en la tecla de destino en el mapa de teclado para seleccionarla, o
   - Ubicar la acción en la tabla de acciones. Las columnas de la tabla son **Action**, **Category**, **Current Key** y **Default Key**. Use el campo **Filter:** o el cuadro combinado **Category:** para reducir la lista.
3. Haga clic en la tecla del mapa de teclado que desea usar como nueva asignación. El indicador **Key:** se actualiza para mostrar la tecla seleccionada.
4. En el cuadro combinado **Action:**, seleccione la acción que desea asignar a esa tecla.
5. Si la tecla ya está asignada a una acción diferente, aparece un diálogo de conflicto: "Key [X] is currently bound to 'Y'. Reassign it?" Haga clic en **Yes** para continuar o en **No** para cancelar.
6. La tabla de acciones se actualiza automáticamente. Confirme que la columna **Current Key** muestre su nueva asignación.
7. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Keyboard map | Pantalla visual | Distribución QWERTY. Haga clic en una tecla para seleccionarla. |
| **Key:** | Indicador | Muestra la tecla seleccionada actualmente. Valor predeterminado: `(none)`. |
| **Action:** | Cuadro combinado | Asigna una acción a la tecla seleccionada. |
| **Category** | Indicador | Muestra la categoría de la acción asignada a la tecla seleccionada. |
| **Clear** | Botón | Elimina la asignación de acción de la tecla seleccionada. |
| **Reset to Default** | Botón | Restaura la tecla predeterminada para la acción en la tecla seleccionada. |
| **Filter:** | Campo de texto | Filtra la tabla de acciones por texto. |
| **Category:** | Cuadro combinado | Filtra la tabla de acciones por categoría. |
| Action table | Lista | Todas las acciones con columnas: Action, Category, Current Key, Default Key. |
| **Reset All to Defaults** | Botón | Restablece todas las asignaciones a su tecla predeterminada. Solicita confirmación. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- Las teclas están codificadas por color en el mapa de teclado según su categoría. Una leyenda debajo del mapa identifica el color de cada categoría.
- Para eliminar una asignación sin asignar un reemplazo, seleccione la tecla en el mapa de teclado y haga clic en **Clear**.
- Para saber qué tecla usa una acción de forma predeterminada sin cambiar nada, consulte la columna **Default Key** en la tabla de acciones.

## Solución de problemas

- **El cuadro combinado Action: no responde después de seleccionar una tecla** — No hay ninguna tecla seleccionada. El indicador **Key:** debe mostrar el nombre de una tecla (no `(none)`) antes de que el cuadro combinado **Action:** surta efecto. Haga clic primero en una tecla del mapa de teclado.
- **No se puede reasignar una tecla y el diálogo de conflicto sigue apareciendo** — Haga clic en **Yes** en el diálogo de conflicto para confirmar la reasignación. Hacer clic en **No** cancela el cambio y deja intacta la asignación original.

## Temas relacionados

- [Descripción general de Keyboard Shortcuts](overview.md)
- [Restablecer un atajo a su tecla predeterminada](reset-one-shortcut-to-its-default-key.md)
- [Restablecer todos los atajos a sus valores predeterminados](reset-every-shortcut-back-to-defaults.md)
- [Buscar todas las acciones de una categoría](find-all-actions-in-a-category.md)
- [Ver la tecla predeterminada de cualquier acción](see-the-default-key-for-any-action.md)
