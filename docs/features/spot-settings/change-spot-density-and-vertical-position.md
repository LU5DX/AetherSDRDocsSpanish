# Cambiar la densidad y posición vertical de las marcas

Utilice el cuadro de diálogo Spot Settings para controlar cuántas filas verticales de marcas aparecen en el panadapter y dónde se ubican esas filas con respecto a la pantalla del espectro.

## Antes de comenzar

- Abra un panadapter. Las marcas no necesitan estar recibiendo activamente, pero el panadapter debe estar visible.
- La alternancia **Spots:** debe estar configurada en **Enabled** para que los cambios sean visibles. Consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en el panadapter (o en la superposición de marcas) para abrir el menú contextual, luego seleccione la opción que abre el cuadro de diálogo Spot Settings.
2. Se abre la ventana **Spot Settings**.
3. Para cambiar la densidad (la cantidad de filas de apilamiento vertical), arrastre el control deslizante **Levels:**. El valor actual se muestra a la derecha del control deslizante. Rango válido: 1–10.
4. Para cambiar la posición vertical (dónde se ubica la pila de filas en el panadapter), arrastre el control deslizante **Position:**. El valor actual (0–100) se muestra a la derecha del control deslizante. Los valores más bajos mueven las marcas hacia la parte superior; los valores más altos las mueven hacia la parte inferior.
5. Para mostrar u ocultar las líneas verticales trazadas desde la línea base del espectro hasta cada etiqueta de marca, haga clic en la alternancia **Spot Lines:**. La alternancia muestra **Enabled** o **Disabled**. Consulte [What each control does](#what-each-control-does) a continuación.
6. Los cambios surten efecto de inmediato. Cierre el cuadro de diálogo cuando haya terminado.

## What each control does

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Control deslizante **Levels:** | Establece la cantidad de filas de apilamiento vertical disponibles para las marcas. Más filas reducen la superposición cuando hay muchas marcas presentes en el mismo rango de frecuencia. Clave de configuración: `SpotsMaxLevel`. | 3 |
| Control deslizante **Position:** | Establece la posición vertical inicial de la pila de marcas como un porcentaje de la altura del panadapter. Clave de configuración: `SpotsStartingHeightPercentage`. | 50 |
| Alternancia **Spot Lines:** | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Desactívela durante los concursos para reducir el desorden visual. Clave de configuración: `IsSpotsLinesEnabled`. Nuevo en v0.9.7. | Enabled |

## Consejos

- Si las marcas se superponen mucho, aumente **Levels:** para darles más filas en las que apilarse.
- Si las marcas cubren trazas de señal que necesita ver, reduzca el valor de **Position:** para empujar la pila hacia la parte superior del panadapter, o auméntelo para mover las marcas hacia la parte inferior.
- Durante los concursos, desactive **Spot Lines:** para reducir el desorden visual sin desactivar las etiquetas de marca por completo.
- El indicador **Total Spots:** en el cuadro de diálogo muestra cuántas marcas activas se están rastreando actualmente, lo que le ayuda a juzgar cuántos niveles se necesitan.

## Relacionados

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Clear every spot from the panadapter](clear-every-spot-from-the-panadapter.md)
