# Atajos de Teclado (v26.6.1)

El diálogo de Atajos de Teclado le permite ver, asignar y restablecer las combinaciones de teclas para todas las acciones en AetherSDR. Los cambios surten efecto de inmediato.

## Abrir el diálogo

- Abra `View > Configure Shortcuts...`.

## Mapa de teclado

La parte superior del diálogo muestra un diseño de teclado QWERTY visual. Haga clic en cualquier tecla para seleccionarla. La tecla seleccionada se resalta y su etiqueta aparece en el indicador **Key:**.

## Asignar un atajo

1. Haga clic en una tecla en el mapa de teclado.
2. El indicador **Key:** muestra la tecla seleccionada.
3. En el cuadro combinado **Action:**, seleccione la acción que desea asignar.
4. El indicador **Category:** muestra la categoría de la acción seleccionada.

## Limpiar un atajo

1. Haga clic en la tecla del mapa de teclado que tenga la asignación que desea eliminar.
2. Haga clic en **Clear**. La tecla queda sin asignar.

## Restablecer un solo atajo a su valor predeterminado

1. Seleccione la tecla en el mapa de teclado.
2. Haga clic en **Reset to Default**. La tecla vuelve a su asignación de fábrica.

## Filtrar la tabla de acciones

La tabla de acciones en la parte inferior del diálogo enumera todas las acciones con columnas para **Action**, **Category**, **Current Key** y **Default Key**.

- Use el campo de texto **Filter:** para filtrar acciones por nombre.
- Use el cuadro combinado **Category:** para filtrar por categoría de acción.

Seleccione una fila en la tabla para editar su asignación directamente.

## Restablecer todos los atajos a los valores predeterminados

1. Haga clic en **Reset All to Defaults** en la esquina inferior izquierda del diálogo.
2. Cuando aparezca el mensaje de confirmación, haga clic en **Yes**.
3. Haga clic en **Close**.

## Cerrar el diálogo

- Haga clic en **Close**. Los cambios surten efecto de inmediato; no hay un paso de guardado separado.

## Estado del indicador

Cuando el diálogo está en modo de captura de teclas (después de hacer clic en una tecla del mapa de teclado), la siguiente pulsación de tecla se captura como la nueva asignación. El indicador **Key:** se actualiza para mostrar la tecla capturada.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Mapa de teclado (diseño QWERTY visual) | Haga clic en una tecla para seleccionarla y editarla. |
| Indicador **Key:** | Muestra la tecla seleccionada. |
| Cuadro combinado **Action:** | Asigna una acción a la tecla seleccionada. |
| Indicador **Category:** | Muestra la categoría de la acción seleccionada. |
| Botón **Clear** | Elimina la asignación de la tecla seleccionada. |
| Botón **Reset to Default** | Restaura la tecla predeterminada para la acción seleccionada. |
| Campo de texto **Filter:** | Filtra la tabla de acciones por texto. |
| Cuadro combinado **Category:** | Filtra la tabla de acciones por categoría. |
| Tabla de acciones (lista) | Todas las acciones con columnas: Action, Category, Current Key, Default Key. Seleccione una fila para editar. |
| Botón **Reset All to Defaults** | Restablece cada asignación a su tecla predeterminada. Aparece un mensaje de confirmación antes de aplicar cualquier cambio. |
| Botón **Close** | Cierra el diálogo. |

## Consejos

- Para verificar cuál es la tecla predeterminada para una acción específica antes de restablecerla, consulte la columna **Default Key** en la tabla de acciones.
- Si solo desea restablecer un solo atajo en lugar de todos ellos, use **Reset to Default** después de seleccionar la tecla correspondiente en el mapa de teclado.

## Relacionado

- [Restablecer un atajo a su tecla predeterminada](reset-one-shortcut-to-its-default-key.md)
- [Reasignar un atajo de teclado](rebind-a-keyboard-shortcut.md)
- [Ver la tecla predeterminada de cualquier acción](see-the-default-key-for-any-action.md)
- [Resumen de Atajos de Teclado](overview.md)
