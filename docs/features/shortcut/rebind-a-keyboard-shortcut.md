# Reasignar un atajo de teclado

Utilice el cuadro de diálogo Atajos de teclado para asignar una tecla diferente a cualquier acción, o para reasignar una tecla que ya está en uso.

## Antes de comenzar

- No se requiere conexión de radio para editar atajos.
- Confirme que el procesamiento de atajos de teclado está habilitado mediante `View > Keyboard Shortcuts` (elemento seleccionable).

## Pasos

1. Abra `View > Configure Shortcuts...`.
2. Busque la acción que desea reasignar. Puede:
   - Hacer clic en la tecla de destino en el mapa del teclado para seleccionarla, o
   - Localizar la acción en la tabla de acciones. Las columnas de la tabla son **Action**, **Category**, **Current Key** y **Default Key**. Utilice el campo **Filter:** o el cuadro combinado **Category:** para reducir la lista.
3. Haga clic en la tecla del mapa del teclado que desea usar como nuevo enlace. El indicador **Key:** se actualiza para mostrar la tecla seleccionada.
4. En el cuadro combinado **Action:**, seleccione la acción que desea asignar a esa tecla.
5. Si la tecla ya está vinculada a una acción diferente, aparece un cuadro de diálogo de conflicto: "La tecla [X] está actualmente vinculada a 'Y'. ¿Reasignarla?". Haga clic en **Yes** para continuar o en **No** para cancelar.
6. La tabla de acciones se actualiza automáticamente. Confirme que la columna **Current Key** muestra su nuevo enlace.
7. Haga clic en **Close**.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Keyboard map | Visualización gráfica | Diseño QWERTY. Haga clic en una tecla para seleccionarla. Las teclas están codificadas por colores según la categoría. |
| **Key:** | Indicador | Muestra la tecla actualmente seleccionada. Valor predeterminado: `(none)`. |
| **Action:** | Cuadro combinado | Asigna una acción a la tecla seleccionada. |
| **Category** | Indicador | Muestra la categoría de la acción asignada a la tecla seleccionada. |
| **Clear** | Botón | Elimina la asignación de acción de la tecla seleccionada. |
| **Reset to Default** | Botón | Restaura la tecla predeterminada para la acción en la tecla seleccionada. |
| **Filter:** | Campo de texto | Filtra la tabla de acciones por texto. |
| **Category:** | Cuadro combinado | Filtra la tabla de acciones por categoría. |
| Action table | Lista | Todas las acciones con columnas: Action, Category, Current Key, Default Key. Seleccione una fila para editarla. |
| **Import...** | Botón | Abre un cuadro de diálogo de archivo para importar atajos de teclado desde un archivo de respaldo CSV. |
| **Export...** | Botón | Abre un cuadro de diálogo de archivo para exportar atajos de teclado a un archivo de respaldo CSV. |
| **Reset All to Defaults** | Botón | Restablece cada enlace a su tecla predeterminada. Solicita confirmación. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

## Importación y exportación de atajos de teclado

Puede transferir sus asignaciones personalizadas de atajos de teclado entre instalaciones de AetherSDR mediante archivos CSV.

### Importar atajos

1. Abra `View > Configure Shortcuts...`.
2. Haga clic en **Import...**.
3. En el cuadro de diálogo de archivo, navegue hasta el archivo CSV que contiene los atajos a importar y haga clic en **Open**.
4. Un cuadro de mensaje informa la cantidad de acciones importadas.
   - Si algunas acciones en el archivo no están disponibles en esta versión de AetherSDR, se omiten y se enumeran en los detalles del mensaje.
   - Si los atajos importados desplazan enlaces locales existentes, las acciones afectadas se enumeran en los detalles del mensaje.
5. El cuadro de diálogo se actualiza para mostrar los atajos importados.

### Exportar atajos

1. Abra `View > Configure Shortcuts...`.
2. Haga clic en **Export...**.
3. En el cuadro de diálogo de archivo, elija una ubicación y un nombre de archivo para el archivo de respaldo CSV y haga clic en **Save**.
4. El archivo exportado contiene todas las asignaciones de atajos de teclado actuales.

El cuadro de diálogo recuerda el último directorio utilizado para importación o exportación y lo reutiliza la próxima vez.

## Consejos

- Las teclas están codificadas por colores en el mapa del teclado según la categoría. Una leyenda debajo del mapa identifica el color de cada categoría.
- Para eliminar un enlace sin asignar un reemplazo, seleccione la tecla en el mapa del teclado y haga clic en **Clear**.
- Para averiguar qué tecla usa una acción por defecto sin realizar cambios, revise la columna **Default Key** en la tabla de acciones.
- El cuadro de diálogo utiliza el tema actual de AetherSDR para los colores. La leyenda del mapa del teclado, la etiqueta de la tecla seleccionada y las etiquetas de acciones se adaptan al tema activo.

## Solución de problemas

- **El cuadro combinado Action: no responde después de seleccionar una tecla** — No hay ninguna tecla seleccionada. El indicador **Key:** debe mostrar un nombre de tecla (no `(none)`) antes de que el cuadro combinado **Action:** surta efecto. Primero haga clic en una tecla del mapa del teclado.
- **Una tecla no se puede reasignar y el cuadro de diálogo de conflicto sigue apareciendo** — Haga clic en **Yes** en el cuadro de diálogo de conflicto para confirmar la reasignación. Haga clic en **No** para cancelar el cambio y mantener el enlace original intacto.

## Relacionado

- [Keyboard Shortcuts overview](overview.md)
- [Reset one shortcut to its default key](reset-one-shortcut-to-its-default-key.md)
- [Reset every shortcut back to defaults](reset-every-shortcut-back-to-defaults.md)
- [Find all actions in a category](find-all-actions-in-a-category.md)
- [See the default key for any action](see-the-default-key-for-any-action.md)
