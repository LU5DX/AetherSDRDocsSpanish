# Forzar un único color de texto para todos los spots

Anule los colores asignados por su fuente de cluster DX a cada spot y muestre todas las etiquetas de spots en un único color de su elección. Resulta útil cuando los colores predeterminados contrastan mal con el tema del panadapter o son difíciles de leer.

## Antes de comenzar

- Los spots deben estar habilitados. Si el interruptor `IsSpotsEnabled` muestra "Disabled", habilítelo primero — consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).
- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter.

## Pasos

1. En el diálogo Spot Settings, localice la fila **Override Colors:**.
2. Haga clic en el botón de interruptor hasta que muestre **Enabled**. Este valor se guarda como `IsSpotsOverrideColorsEnabled`.
3. Haga clic en el botón de muestra de color (swatch) ubicado inmediatamente a la derecha de **Enabled**. Se abre un diálogo de selección de color.
4. Seleccione el color que desea aplicar a todas las etiquetas de texto de spots y haga clic en **OK**.
5. La muestra se actualiza para mostrar el color elegido. Todos los spots en el panadapter se renderizan inmediatamente con ese color. El valor elegido se guarda como `SpotsOverrideColor`.

Para volver a los colores individuales por spot, haga clic nuevamente en el interruptor **Override Colors:** hasta que muestre **Disabled**.

## Qué hace cada control

| Control | Valor predeterminado | Clave guardada | Comportamiento |
|---|---|---|---|
| Interruptor **Override Colors:** | Disabled | `IsSpotsOverrideColorsEnabled` | Cuando está en Enabled, fuerza que el texto de todos los spots se muestre en un único color en lugar de los colores asignados por la fuente. |
| Selector de color del texto de spots (botón swatch) | `#FFFF00` | `SpotsOverrideColor` | Abre el diálogo de selección de color. El color seleccionado se aplica a todas las etiquetas de spots cuando Override Colors está en Enabled. |

## Consejos

- El selector de color solo tiene efecto mientras **Override Colors:** muestre **Enabled**. Puede preseleccionar un color con el interruptor aún en Disabled; se aplicará la próxima vez que habilite la anulación.
- Si el texto de los spots sigue siendo difícil de leer después de establecer el color, ajuste el contraste del fondo mediante los controles **Override Background:** — consulte [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md) y [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md).

## Temas relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
