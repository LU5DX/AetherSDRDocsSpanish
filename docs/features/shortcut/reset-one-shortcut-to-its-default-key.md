# Restablecer un acceso directo a su tecla predeterminada

Use esta página para restaurar un solo acceso directo del teclado a la tecla con la que se envió, sin afectar ninguna otra asignación.

## Antes de empezar

- Abra `View > Configure Shortcuts...` para acceder al cuadro de diálogo de Accesos directos del teclado.
- Identifique la acción cuya asignación desea restaurar. Si no está seguro de cuál es la tecla predeterminada, revise la columna **Default Key** en la tabla de acciones.

## Pasos

1. Abra `View > Configure Shortcuts...`.
2. En la tabla de acciones, ubique la acción que desea restablecer. Use el campo **Filter:** o el cuadro combinado **Category:** para reducir la lista si es necesario.
3. Haga clic en la fila de la tabla de acciones para seleccionar la acción.
4. En el mapa del teclado, confirme que la tecla correcta esté resaltada y se muestre en el indicador **Key:**.
5. Haga clic en **Reset to Default**.

La asignación se restaura inmediatamente a la tecla predeterminada de la acción. La tabla de acciones se actualiza para mostrar el cambio en la columna **Current Key**.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Mapa del teclado | Indicador visual | Diseño QWERTY; haga clic en una tecla para seleccionarla y llenar el indicador **Key:**. |
| **Key:** | Indicador | Muestra la tecla seleccionada actualmente. Muestra `(none)` cuando no hay ninguna tecla seleccionada. |
| **Action:** | Cuadro combinado | Muestra la acción asignada a la tecla seleccionada. |
| **Category** | Indicador | Muestra la categoría de la acción asignada a la tecla seleccionada. |
| **Clear** | Botón | Elimina la asignación de la tecla seleccionada. |
| **Reset to Default** | Botón | Restablece la tecla predeterminada para la acción actualmente asignada a la tecla seleccionada. |
| **Filter:** | Campo de texto | Filtra la tabla de acciones por texto. |
| **Category:** | Cuadro combinado | Filtra la tabla de acciones por categoría. |
| Tabla de acciones | Lista | Todas las acciones con columnas: Action, Category, Current Key, Default Key. Seleccione una fila para editarla. |
| **Import...** | Botón | Abre un cuadro de diálogo para importar accesos directos del teclado desde una copia de seguridad CSV portátil. |
| **Export...** | Botón | Abre un cuadro de diálogo para exportar accesos directos del teclado a una copia de seguridad CSV portátil. |
| **Reset All to Defaults** | Botón | Restablece todas las asignaciones a sus teclas predeterminadas — úselo con precaución. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

## Consejos

- La columna **Default Key** en la tabla de acciones siempre muestra el valor predeterminado de fábrica, incluso después de haber cambiado la asignación. Úsela para confirmar lo que **Reset to Default** restaurará antes de hacer clic.
- Si la acción que desea está asignada a una tecla que entra en conflicto con otra asignación, restablecer una acción puede liberar una tecla para otra. Revise la columna **Current Key** después de restablecer.
- Use **Export...** para crear una copia de seguridad de su configuración actual de accesos directos del teclado antes de hacer cambios extensos. El archivo exportado es un CSV que se puede compartir o importar en otra instancia de AetherSDR.
- El botón **Import...** permite restaurar una copia de seguridad CSV exportada anteriormente. Si alguna acción del archivo importado no está disponible en esta versión de AetherSDR, se omite y se reporta en un cuadro de diálogo de advertencia. Si los accesos directos importados desplazan asignaciones locales existentes, esos desplazamientos también se listan.

## Relacionados

- [Keyboard Shortcuts overview](overview.md)
- [Rebind a keyboard shortcut](rebind-a-keyboard-shortcut.md)
- [Reset every shortcut back to defaults](reset-every-shortcut-back-to-defaults.md)
- [See the default key for any action](see-the-default-key-for-any-action.md)
- [Find all actions in a category](find-all-actions-in-a-category.md)
- Export keyboard shortcuts
- Import keyboard shortcuts
