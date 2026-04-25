# Cambiar la densidad y la posición vertical de los spots

Use Spot Settings para controlar cuántas filas verticales de spots aparecen en el panadapter y en qué lugar del panadapter se ubican.

## Antes de comenzar

- Abra un panadapter. Spot Settings se accede desde el menú contextual del panadapter, no desde el menú principal.
- Los spots deben estar habilitados. Si el ajuste `IsSpotsEnabled` está desactivado, los spots no aparecerán independientemente de la densidad o la posición. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el cuadro de diálogo **Spot Settings**.
3. Para cambiar la densidad de spots, arrastre el control deslizante **Levels:**. Los valores más altos añaden más filas de apilamiento vertical, lo que permite que aparezcan más spots simultáneamente sin superponerse. El rango es de 1 a 10; el valor predeterminado es 3.
4. Para cambiar la posición vertical, arrastre el control deslizante **Position:**. El valor es un porcentaje de la altura del panadapter desde la parte superior, con un rango de 0 a 100; el valor predeterminado es 50.
5. Los cambios surten efecto de inmediato. Cierre el cuadro de diálogo cuando termine.

## Qué hace cada control

| Control | Función | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| **Levels:** | Número de filas de apilamiento vertical para los spots. Más filas permiten una visualización más densa de spots sin superposición. | 3 | 1–10 | `SpotsStackLevels` |
| **Position:** | Posición vertical de la banda de spots en el panadapter, expresada como porcentaje de la altura del panadapter. | 50 | 0–100 | `SpotsPosition` |

## Consejos

- Si los spots se agrupan y se superponen, aumente **Levels:** para darles más filas en las que apilarse.
- Si los spots ocultan señales de interés, muévalos hacia arriba o hacia abajo con **Position:** hasta que queden en un área despejada del panadapter.
- Los controles deslizantes **Levels:** y **Position:** muestran su valor numérico actual a la derecha del control mientras se arrastra.

## Temas relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Ampliar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
