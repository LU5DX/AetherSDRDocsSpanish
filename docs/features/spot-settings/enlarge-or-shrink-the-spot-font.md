# Ampliar o reducir la fuente de los spots

Use esta página para hacer el texto de los indicativos de los spots más grande o más pequeño en el panadapter. Ajustar el tamaño de fuente es útil cuando los spots son difíciles de leer a distancia o cuando se superponen a otros elementos de la pantalla.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar esta configuración.
- El cuadro de diálogo **Spot Settings** debe ser accesible desde el panadapter. Si los spots no son visibles, confirme que el interruptor `IsSpotsEnabled` esté establecido en Enabled — consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el cuadro de diálogo **Spot Settings**.
3. Localice la fila **Font Size:**.
4. Arrastre el control deslizante hacia la izquierda para reducir el tamaño de fuente o hacia la derecha para aumentarlo. El valor actual en puntos se muestra a la derecha del control deslizante.
5. Suelte el control deslizante. El cambio surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Font Size:** | Establece el tamaño del texto de los indicativos y etiquetas de los spots representados en el panadapter. | 16 | 8 – 32 (puntos) | `SpotsFontSize` |

## Consejos

- El tamaño de fuente predeterminado es 16. Los valores cercanos a 8 reducen el desorden visual cuando hay muchos spots visibles; los valores cercanos a 32 son útiles al visualizar el panadapter desde lejos.
- El tamaño de fuente se aplica a todos los spots simultáneamente. No existe un ajuste de tamaño individual por spot.

## Relacionado

- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
