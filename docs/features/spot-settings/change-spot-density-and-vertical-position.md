# Cambiar la densidad y posición vertical de los spots

Use el diálogo Spot Settings para controlar cuántas filas de apilamiento de spots (manchas de frecuencia) aparecen en el panadapter y dónde se ubican esas filas en el eje vertical.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar estas configuraciones.
- Los spots deben ser visibles en el panadapter. Si no lo son, consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho sobre la capa de spots en el panadapter para abrir el menú contextual del panadapter, luego seleccione la opción que abre **Spot Settings**.
2. Localice el control deslizante **Levels:**. Arrástrelo hacia la izquierda para reducir el número de filas de apilamiento vertical; arrástrelo hacia la derecha para aumentarlas. El valor actual aparece a la derecha del control deslizante. Rango válido: 1–10.
3. Localice el control deslizante **Position:**. Arrástrelo hacia la izquierda para mover las filas de spots hacia la parte superior del panadapter; arrástrelo hacia la derecha para moverlas hacia la parte inferior. El valor actual es un porcentaje (0–100) que se muestra a la derecha del control deslizante.
4. Cierre el diálogo. Los cambios surten efecto de inmediato y se guardan automáticamente.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Levels:** | Establece el número de filas de apilamiento vertical que se usan cuando los spots se superponen en frecuencias similares. | 3 | 1–10 | `SpotsStackLevels` |
| **Position:** | Establece la posición vertical de las filas de spots como porcentaje de la altura del panadapter. | 50 | 0–100 | `SpotsPosition` |

## Consejos

- Si los spots se superponen y los indicativos son ilegibles, aumente **Levels:** para darles más filas donde apilarse.
- Si los spots ocultan actividad de señal que desea observar, mueva **Position:** hacia 0 para desplazar las filas hacia la parte superior del panadapter.
- El indicador **Total Spots:** en el diálogo muestra cuántos spots se están rastreando actualmente, lo que puede ayudarle a determinar cuántos niveles necesita.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
