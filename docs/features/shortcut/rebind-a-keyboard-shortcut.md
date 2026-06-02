# Reasignar un atajo de teclado

Use el diálogo de Atajos de Teclado para asignar una tecla diferente a cualquier acción, o para reasignar una tecla que ya está en uso.

## Antes de comenzar

- No se requiere conexión de radio para editar los atajos.
- Confirme que el procesamiento de atajos de teclado esté habilitado mediante `View > Keyboard Shortcuts` (elemento marcable).

## Pasos

1. Abra `View > Configure Shortcuts...`.
2. Encuentre la acción que desea reasignar. Ya sea:
   - Haga clic en la tecla destino en el mapa del teclado para seleccionarla, o
   - Localice la acción en la tabla de acciones. Las columnas de la tabla son **Action**, **Category**, **Current Key** y **Default Key**. Use el campo **Filter:** o el cuadro combinado **Category:** para reducir la lista.
3. Haga clic en la tecla del mapa del teclado que desea usar como nuevo enlace. El indicador **Key:** se actualiza para mostrar la tecla seleccionada.
4. En el cuadro combinado **Action:**, seleccione la acción que desea asignar a esa tecla.
5. Si la tecla ya está vinculada a una acción diferente, aparece un diálogo de conflicto: "Key [X] is currently bound to 'Y'. Reassign it?" Haga clic en **Yes** para continuar o **No** para cancelar.
6. La tabla de acciones se actualiza automáticamente. Confirme que la columna **Current Key** muestre su nuevo enlace.
7. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Keyboard map | Visualización gráfica | Disposición QWERTY. Haga clic en una tecla para seleccionarla. Las teclas están codificadas por colores según la categoría. |
| **Key:** | Indicador | Muestra la tecla seleccionada actualmente. Valor predeterminado: `(none)`. |
| **Action:** | Cuadro combinado | Asigna una acción a la tecla seleccionada. |
| **Category** | Indicador | Muestra la categoría de la acción asignada a la tecla seleccionada. |
| **Clear** | Botón | Elimina la asignación de acción de la tecla seleccionada. |
| **Reset to Default** | Botón | Restaura la tecla predeterminada para la acción en la tecla seleccionada. |
| **Filter:** | Campo de texto | Filtra la tabla de acciones por texto. |
| **Category:** | Cuadro combinado | Filtra la tabla de acciones por categoría. |
| Action table | Lista | Todas las acciones con columnas: Action, Category, Current Key, Default Key. Seleccione una fila para editarla. |
| **Reset All to Defaults** | Botón | Restablece cada enlace a su tecla predeterminada. Solicita confirmación. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- Las teclas están codificadas por colores en el mapa del teclado según la categoría. Una leyenda debajo del mapa identifica el color de cada categoría.
- Para eliminar un enlace sin asignar un reemplazo, seleccione la tecla en el mapa del teclado y haga clic en **Clear**.
- Para saber qué tecla usa una acción de forma predeterminada sin cambiar nada, revise la columna **Default Key** en la tabla de acciones.
- El diálogo usa el tema actual de AetherSDR para los colores. La leyenda del mapa del teclado, la etiqueta de la tecla seleccionada y las etiquetas de las acciones se ajustan al tema activo.

## Solución de problemas

- **El cuadro combinado Action: no responde después de seleccionar una tecla** — No hay ninguna tecla seleccionada. El indicador **Key:** debe mostrar un nombre de tecla (no `(none)`) antes de que el cuadro combinado **Action:** tenga efecto. Haga clic primero en una tecla del mapa del teclado.
- **Una tecla no se puede reasignar y el diálogo de conflicto sigue apareciendo** — Haga clic en **Yes** en el diálogo de conflicto para confirmar la reasignación. Hacer clic en **No** cancela el cambio y deja el enlace original intacto.

## Relacionado

- [Keyboard Shortcuts overview](overview.md)
- [Reset one shortcut to its default key](reset-one-shortcut-to-its-default-key.md)
- [Reset every shortcut back to defaults](reset-every-shortcut-back-to-defaults.md)
- [Find all actions in a category](find-all-actions-in-a-category.md)
- [See the default key for any action](see-the-default-key-for-any-action.md)
