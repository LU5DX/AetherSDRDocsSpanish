# Reasignar un atajo de teclado

Use el diálogo de Atajos de Teclado para asignar una tecla diferente a cualquier acción, o para reasignar una tecla que ya está en uso.

## Antes de comenzar

- No se requiere conexión de radio para editar los atajos.
- Confirme que el procesamiento de atajos de teclado está habilitado mediante `View > Keyboard Shortcuts` (elemento seleccionable).

## Pasos

1. Abra `View > Configure Shortcuts...`.
2. Encuentre la acción que desea reasignar. Puede:
   - Hacer clic en la tecla objetivo en el mapa del teclado para seleccionarla, o
   - Localizar la acción en la tabla de acciones. Las columnas de la tabla son **Action**, **Category**, **Current Key** y **Default Key**. Use el campo **Filter:** o el cuadro combinado **Category:** para reducir la lista.
3. Haga clic en la tecla del mapa del teclado que desee usar como nuevo enlace. El indicador **Key:** se actualiza para mostrar la tecla seleccionada.
4. En el cuadro combinado **Action:**, seleccione la acción que desea asignar a esa tecla.
5. Si la tecla ya está vinculada a una acción diferente, aparece un diálogo de conflicto: "Key [X] is currently bound to 'Y'. Reassign it?" Haga clic en **Yes** para continuar o **No** para cancelar.
6. La tabla de acciones se actualiza automáticamente. Confirme que la columna **Current Key** muestra su nuevo enlace.
7. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Mapa del teclado | Visualización gráfica | Diseño QWERTY. Haga clic en una tecla para seleccionarla. |
| **Key:** | Indicador | Muestra la tecla actualmente seleccionada. Por defecto: `(none)`. |
| **Action:** | Cuadro combinado | Asigna una acción a la tecla seleccionada. |
| **Category** | Indicador | Muestra la categoría de la acción asignada a la tecla seleccionada. |
| **Clear** | Botón | Elimina la asignación de acción de la tecla seleccionada. |
| **Reset to Default** | Botón | Restaura la tecla por defecto para la acción en la tecla seleccionada. |
| **Filter:** | Campo de texto | Filtra la tabla de acciones por texto. |
| **Category:** | Cuadro combinado | Filtra la tabla de acciones por categoría. |
| Tabla de acciones | Lista | Todas las acciones con columnas: Action, Category, Current Key, Default Key. |
| **Reset All to Defaults** | Botón | Restablece todos los enlaces a sus teclas por defecto. Solicita confirmación. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- Las teclas están codificadas por colores en el mapa del teclado según la categoría. Una leyenda debajo del mapa identifica el color de cada categoría.
- Para eliminar un enlace sin asignar un reemplazo, seleccione la tecla en el mapa del teclado y haga clic en **Clear**.
- Para averiguar qué tecla usa una acción por defecto sin realizar cambios, revise la columna **Default Key** en la tabla de acciones.

## Solución de problemas

- **El cuadro combinado Action: no responde después de seleccionar una tecla** — No hay ninguna tecla seleccionada. El indicador **Key:** debe mostrar un nombre de tecla (no `(none)`) antes de que el cuadro combinado **Action:** surta efecto. Primero haga clic en una tecla del mapa del teclado.
- **No se puede reasignar una tecla y el diálogo de conflicto sigue apareciendo** — Haga clic en **Yes** en el diálogo de conflicto para confirmar la reasignación. Hacer clic en **No** cancela el cambio y deja el enlace original intacto.

## Relacionado

- [Keyboard Shortcuts overview](overview.md)
- [Reset one shortcut to its default key](reset-one-shortcut-to-its-default-key.md)
- [Reset every shortcut back to defaults](reset-every-shortcut-back-to-defaults.md)
- [Find all actions in a category](find-all-actions-in-a-category.md)
- [See the default key for any action](see-the-default-key-for-any-action.md)
