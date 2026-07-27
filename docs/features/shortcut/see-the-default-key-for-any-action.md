# Ver la tecla predeterminada de cualquier acción

La tabla de acciones en el diálogo de Atajos de Teclado muestra la tecla predeterminada de cada acción junto con su asignación actual, para que pueda consultar el atajo original sin cambiar nada.

## Antes de comenzar

- No se requiere conexión de radio.

## Pasos

1. Haga clic en `View > Configure Shortcuts...` para abrir el diálogo de Atajos de Teclado.
2. En la tabla de acciones, localice la acción que desea consultar. Cada fila muestra cuatro columnas: **Action**, **Category**, **Current Key** y **Default Key**.
3. Lea el valor en la columna **Default Key** de esa acción.

Para reducir la lista, escriba parte del nombre de la acción en el campo `Filter:` o seleccione una categoría en el cuadro combinado `Category:` sobre la tabla.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Keyboard map` | Indicador | Diseño QWERTY visual; haga clic en una tecla para seleccionarla. |
| `Key:` | Indicador | Muestra la tecla seleccionada. |
| `Action:` | Cuadro combinado | Asigna una acción a la tecla seleccionada. |
| `Category` | Indicador | Muestra la categoría de la acción seleccionada. |
| `Clear` | Botón | Elimina la asignación de la tecla seleccionada. |
| `Reset to Default` | Botón | Restaura la tecla predeterminada de la acción seleccionada. |
| `Filter:` | Campo de texto | Filtra la tabla de acciones para mostrar solo filas cuyo texto de Action o Category coincida con lo que escriba. |
| `Category:` | Cuadro combinado | Filtra la tabla de acciones a una sola categoría. Por defecto muestra **All**. |
| Tabla de acciones | Lista | Muestra todas las acciones con las columnas: Action, Category, Current Key, Default Key. Seleccione una fila para editarla. |
| `Import...` | Botón | Importa asignaciones de atajos de teclado desde un archivo CSV. |
| `Export...` | Botón | Exporta las asignaciones actuales de atajos de teclado a un archivo CSV. |
| `Reset All to Defaults` | Botón | Restablece todas las asignaciones a sus teclas predeterminadas. |
| `Close` | Botón | Cierra el diálogo. |

## Importar y exportar atajos de teclado

Puede respaldar sus atajos de teclado personalizados o transferirlos a otra instancia de AetherSDR mediante archivos CSV.

### Importar atajos desde un archivo CSV

1. Haga clic en `Import...` en la parte inferior del diálogo de Atajos de Teclado.
2. En el diálogo de archivos, navegue hasta el archivo CSV y selecciónelo.
3. Haga clic en **Open**. AetherSDR importa las asignaciones y actualiza la tabla de acciones.
   - Si alguna acción del archivo no está disponible en esta versión de AetherSDR, se omite y se lista en el texto de error detallado.
   - Si alguna asignación importada entra en conflicto con asignaciones locales existentes, esas asignaciones locales se eliminan y se listan en el diálogo de información.

### Exportar atajos a un archivo CSV

1. Haga clic en `Export...` en la parte inferior del diálogo de Atajos de Teclado.
2. En el diálogo de archivos, elija una ubicación y nombre para el archivo CSV.
3. Haga clic en **Save**. AetherSDR escribe todas las asignaciones actuales de atajos de teclado en el archivo.

El diálogo de importación/exportación recuerda el último directorio utilizado para operaciones posteriores.

## Consejos

- La columna **Default Key** siempre refleja el valor predeterminado de fábrica, incluso después de haber reasignado o limpiado la acción. Úsela como referencia antes de decidir si restaurar una asignación.
- Para restaurar una sola acción al valor mostrado en **Default Key**, seleccione su fila y luego haga clic en `Reset to Default`. Consulte [Restablecer un atajo a su tecla predeterminada](reset-one-shortcut-to-its-default-key.md).
- Exporte sus atajos periódicamente como respaldo antes de realizar cambios extensos.

## Relacionados

- [Resumen de Atajos de Teclado](overview.md)
- [Encontrar todas las acciones de una categoría](find-all-actions-in-a-category.md)
- [Restablecer un atajo a su tecla predeterminada](reset-one-shortcut-to-its-default-key.md)
- [Restablecer todos los atajos a los valores predeterminados](reset-every-shortcut-back-to-defaults.md)
