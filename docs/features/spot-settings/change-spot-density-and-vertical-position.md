# Cambiar la densidad y la posición vertical de los spots

Use el cuadro de diálogo Spot Settings para controlar cuántas filas verticales de spots aparecen en el panadapter y dónde se ubican esas filas en relación con la visualización del espectro.

## Antes de comenzar

- Abra un panadapter. Los spots no necesitan estar recibiendo activamente, pero el panadapter debe estar visible.
- El selector "Spots:" debe estar en "Enabled" para que los cambios sean visibles. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en el panadapter (o sobre la capa de spots) para abrir el menú contextual y seleccione la opción que abre el cuadro de diálogo Spot Settings.
2. Se abre la ventana **Spot Settings**.
3. Para cambiar la densidad —el número de filas de apilamiento vertical— arrastre el control deslizante **Levels:**. El valor actual se muestra a la derecha del control. Rango válido: 1–10.
4. Para cambiar la posición vertical —el lugar donde se ubica la pila de filas en el panadapter— arrastre el control deslizante **Position:**. El valor actual (0–100) se muestra a la derecha del control. Los valores más bajos mueven los spots hacia la parte superior; los valores más altos los mueven hacia la parte inferior.
5. Los cambios surten efecto de inmediato. Cierre el cuadro de diálogo cuando haya terminado.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Control deslizante **Levels:** | Establece el número de filas de apilamiento vertical disponibles para los spots. Más filas reducen la superposición cuando hay muchos spots en el mismo rango de frecuencia. | 3 | 1–10 | `SpotsStackLevels` |
| Control deslizante **Position:** | Establece la posición de inicio vertical de la pila de spots como porcentaje de la altura del panadapter. | 50 | 0–100 | `SpotsPosition` |

## Consejos

- Si los spots se superponen con frecuencia, aumente **Levels:** para darles más filas en las que apilarse.
- Si los spots cubren trazas de señal que necesita ver, reduzca el valor de **Position:** para desplazar la pila hacia la parte superior del panadapter, o auméntelo para mover los spots hacia la parte inferior.
- El indicador **Total Spots:** del cuadro de diálogo muestra cuántos spots activos se están rastreando en ese momento, lo que le ayuda a determinar cuántos niveles son necesarios.

## Temas relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o prolongar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
