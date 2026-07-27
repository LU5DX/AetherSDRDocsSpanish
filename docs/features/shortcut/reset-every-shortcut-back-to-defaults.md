# Atajos de Teclado (v26.7.4)

El cuadro de diálogo de Atajos de Teclado le permite ver, asignar, restablecer, importar y exportar combinaciones de teclas para todas las acciones en AetherSDR. Los cambios surten efecto de inmediato.

## Abrir el cuadro de diálogo

- Abra `View > Configure Shortcuts...`.

## Mapa de teclado

La parte superior del cuadro de diálogo muestra un diseño visual de teclado QWERTY. Haga clic en cualquier tecla para seleccionarla. La tecla seleccionada se resalta y su etiqueta aparece en el indicador **Key:**.

## Asignar un atajo

1. Haga clic en una tecla en el mapa de teclado.
2. El indicador **Key:** muestra la tecla seleccionada.
3. En el cuadro combinado **Action:**, seleccione la acción que desea asignar.
4. El indicador **Category:** muestra la categoría de la acción seleccionada.

## Limpiar un atajo

1. Haga clic en la tecla del mapa de teclado que tiene la asignación que desea eliminar.
2. Haga clic en **Clear**. La tecla queda sin asignar.

## Restablecer un solo atajo a su valor predeterminado

1. Seleccione la tecla en el mapa de teclado.
2. Haga clic en **Reset to Default**. La tecla vuelve a su combinación de fábrica.

## Filtrar la tabla de acciones

La tabla de acciones en la parte inferior del cuadro de diálogo enumera todas las acciones con las columnas **Action**, **Category**, **Current Key** y **Default Key**.

- Use el campo de texto **Filter:** para filtrar acciones por nombre.
- Use el cuadro combinado **Category:** para filtrar por categoría de acción.

Seleccione una fila en la tabla para editar su combinación directamente.

## Restablecer todos los atajos a los valores predeterminados

1. Haga clic en **Reset All to Defaults** en la esquina inferior izquierda del cuadro de diálogo.
2. Cuando aparezca el mensaje de confirmación, haga clic en **Yes**.

## Importar atajos desde un archivo

1. Haga clic en **Import...** en la fila inferior de botones.
2. En el cuadro de diálogo de archivos, navegue hasta un archivo CSV que contenga definiciones de atajos de teclado de AetherSDR y haga clic en **Open**.
3. Un cuadro de diálogo de resumen muestra la cantidad de atajos importados. Si alguna acción del archivo no está disponible en esta versión de AetherSDR, se omite y se enumera en los detalles del cuadro de diálogo. Si algún atajo importado desplaza combinaciones locales existentes, esas acciones desplazadas también se enumeran.
4. La tabla de acciones se actualiza para reflejar las combinaciones importadas.

## Exportar atajos a un archivo

1. Haga clic en **Export...** en la fila inferior de botones.
2. En el cuadro de diálogo de archivos, elija una ubicación y un nombre para el archivo CSV y haga clic en **Save**.
3. Un cuadro de diálogo de confirmación muestra la cantidad de atajos exportados y la ruta del archivo.

El archivo CSV exportado se puede compartir con otros usuarios de AetherSDR o usarse como copia de seguridad personal. El archivo usa la extensión `.csv`.

## Cerrar el cuadro de diálogo

- Haga clic en **Close**. Los cambios surten efecto de inmediato; no hay un paso separado de Guardar.

## Estado del indicador

Cuando el cuadro de diálogo está en modo de captura de teclas (después de hacer clic en una tecla en el mapa de teclado), la siguiente pulsación de tecla se captura como la nueva combinación. El indicador **Key:** se actualiza para mostrar la tecla capturada.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Mapa de teclado (diseño visual QWERTY) | Haga clic en una tecla para seleccionarla y editarla. |
| Indicador **Key:** | Muestra la tecla seleccionada. |
| Cuadro combinado **Action:** | Asigna una acción a la tecla seleccionada. |
| Indicador **Category:** | Muestra la categoría de la acción seleccionada. |
| Botón **Clear** | Elimina la asignación de la tecla seleccionada. |
| Botón **Reset to Default** | Restaura la tecla predeterminada para la acción seleccionada. |
| Campo de texto **Filter:** | Filtra la tabla de acciones por texto. |
| Cuadro combinado **Category:** | Filtra la tabla de acciones por categoría. |
| Tabla de acciones (lista) | Todas las acciones con columnas: Action, Category, Current Key, Default Key. Seleccione una fila para editarla. |
| Botón **Import...** | Abre un cuadro de diálogo de archivos para importar atajos de teclado desde un archivo CSV de respaldo. |
| Botón **Export...** | Abre un cuadro de diálogo de archivos para exportar atajos de teclado a un archivo CSV portátil de respaldo. |
| Botón **Reset All to Defaults** | Restablece cada combinación a su tecla predeterminada. Aparece un mensaje de confirmación antes de aplicar cualquier cambio. |
| Botón **Close** | Cierra el cuadro de diálogo. |

## Consejos

- Para verificar cuál es la tecla predeterminada para una acción específica antes de restablecerla, consulte la columna **Default Key** en la tabla de acciones.
- Si solo desea restablecer un solo atajo en lugar de todos, use **Reset to Default** después de seleccionar la tecla relevante en el mapa de teclado.
- Exporte sus atajos regularmente como copia de seguridad antes de hacer cambios importantes.
- La importación y exportación usan el formato CSV, lo que facilita compartir o controlar versiones de sus atajos.

## Relacionados

- [Restablecer un atajo a su tecla predeterminada](reset-one-shortcut-to-its-default-key.md)
- [Reasignar un atajo de teclado](rebind-a-keyboard-shortcut.md)
- [Ver la tecla predeterminada para cualquier acción](see-the-default-key-for-any-action.md)
- [Resumen de Atajos de Teclado](overview.md)
