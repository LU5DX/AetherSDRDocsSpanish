# Cambiar la densidad y la posición vertical de los spots

Use el cuadro de diálogo Spot Settings para controlar cuántas filas verticales de spots aparecen en el panadapter y dónde se ubican esas filas en relación con la altura de la pantalla.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para ajustar estos parámetros.
- Abra el cuadro de diálogo Spot Settings haciendo clic derecho sobre la capa de spots o el panadapter para acceder al menú contextual.

## Pasos

1. Haga clic derecho en el panadapter para abrir el menú contextual y seleccione la opción para abrir **Spot Settings**.
2. Localice el control deslizante **Levels:**. Arrástrelo hacia la izquierda o la derecha para definir el número de filas de apilamiento vertical utilizadas para mostrar los spots. El valor actual aparece a la derecha del control.
3. Localice el control deslizante **Position:**. Arrástrelo hacia la izquierda o la derecha para establecer la posición vertical de las filas de spots en el panadapter. El valor actual aparece a la derecha del control.
4. Los cambios surten efecto de inmediato. Cierre el cuadro de diálogo cuando haya terminado.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Levels:** | Define el número de filas de apilamiento vertical para los spots. Más filas permiten mostrar spots con mayor densidad sin superposición. | 3 | 1–10 | `SpotsStackLevels` |
| **Position:** | Establece la posición vertical de la banda de spots en el panadapter, expresada como porcentaje de la altura de la pantalla. Los valores más bajos mueven los spots hacia la parte superior; los valores más altos los mueven hacia la parte inferior. | 50 | 0–100 | `SpotsPosition` |

## Consejos

- Si los spots se agolpan entre sí, aumente **Levels:** para darles más filas en las que distribuirse.
- Si los spots están ocultando señales de interés, ajuste **Position:** para desplazar toda la banda de spots fuera de la zona más concurrida de la pantalla.
- El interruptor principal **Spots:** debe estar en **Enabled** para que los spots aparezcan, independientemente de estos ajustes.

## Solución de problemas

- **Los spots no aparecen después de ajustar Levels: o Position:** — Confirme que el interruptor **Spots:** muestre **Enabled**. Si muestra **Disabled**, haga clic en él para habilitar la visualización de spots.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Descripción general de Spot Settings](overview.md)
