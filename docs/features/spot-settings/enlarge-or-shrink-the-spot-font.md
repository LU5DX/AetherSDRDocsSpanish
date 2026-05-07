# Aumentar o reducir el tamaño de la fuente de las marcas

Use esta página para hacer que el texto de los indicativos de las marcas sea más grande o más pequeño en el panadapter. Ajustar el tamaño de la fuente ayuda cuando las marcas son difíciles de leer desde lejos o cuando se superponen con otros elementos de la pantalla.

## Antes de empezar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El cuadro de diálogo Spot Settings debe ser accesible desde el panadapter. Si las marcas no son visibles, confirme que el conmutador `IsSpotsEnabled` esté en Enabled — consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de marcas para abrir el cuadro de diálogo **Spot Settings**.
3. Localice la fila **Font Size:**.
4. Arrastre el control deslizante hacia la izquierda para disminuir el tamaño de la fuente o hacia la derecha para aumentarlo. El valor actual en puntos se muestra a la derecha del control deslizante.
5. Suelte el control deslizante. El cambio surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Font Size:** | Establece el tamaño del texto de los indicativos y etiquetas de las marcas que se muestran en el panadapter. El rango es de 8 a 32 puntos. Se almacena en `SpotFontSize`. | 16 |
| **Spot Lines:** | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Desactívelo durante los concursos para reducir el desorden visual. Se almacena en `IsSpotsLinesEnabled`. Nuevo en v0.9.7. | Enabled |

## Consejos

- Un tamaño de fuente de 16 es el valor predeterminado. Los valores cercanos a 8 reducen el desorden cuando hay muchas marcas visibles; los valores cercanos a 32 ayudan cuando se ve el panadapter desde lejos.
- El tamaño de la fuente se aplica a todas las marcas simultáneamente. No existe una anulación de tamaño por marca.
- Desactivar **Spot Lines:** puede reducir significativamente el desorden visual durante los concursos cuando hay una gran cantidad de marcas activas.

## Temas relacionados

- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
