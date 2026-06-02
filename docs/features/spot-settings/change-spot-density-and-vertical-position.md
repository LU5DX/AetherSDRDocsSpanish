# Cambiar la densidad y la posición vertical de las marcas

Utilice el cuadro de diálogo Spot Settings para controlar cuántas filas verticales de marcas aparecen en el panadapter y dónde se ubican esas filas en relación con la visualización del espectro.

## Antes de comenzar

- Abra un panadapter. No es necesario que las marcas estén recibiendo activamente, pero el panadapter debe estar visible.
- La opción **Spots:** debe estar en **Enabled** para que los cambios sean visibles. Consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en el panadapter (o en la superposición de marcas) para abrir el menú contextual y, a continuación, seleccione la opción que abre el cuadro de diálogo Spot Settings.
2. Se abre la ventana **Spot Settings**.
3. Para cambiar la densidad (la cantidad de filas de apilamiento vertical), arrastre el control deslizante **Levels:**. El valor actual se muestra a la derecha del control deslizante. Rango válido: 1–10.
4. Para cambiar la posición vertical (dónde se ubica la pila de filas en el panadapter), arrastre el control deslizante **Position:**. El valor actual (0–100) se muestra a la derecha del control deslizante. Los valores más bajos mueven las marcas hacia la parte superior; los valores más altos las mueven hacia la parte inferior.
5. Para mostrar u ocultar las líneas verticales trazadas desde la línea base del espectro hasta cada etiqueta de marca, haga clic en la opción **Spot Lines:**. La opción muestra **Enabled** o **Disabled**. Consulte [What each control does](#what-each-control-does) a continuación.
6. Los cambios surten efecto de inmediato. Cierre el cuadro de diálogo cuando haya terminado.

## What each control does

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Opción **Spots:** | Opción principal para la visualización de marcas de DX. Clave de configuración: `IsSpotsEnabled`. | Enabled |
| Opción **Memories:** | Activa o desactiva las superposiciones de canales de memoria en el panadapter. Clave de configuración: `IsMemorySpotsEnabled`. | Disabled |
| Control deslizante **Levels:** | Establece el número de filas de apilamiento vertical disponibles para las marcas. Más filas reducen la superposición cuando hay muchas marcas en el mismo rango de frecuencia. Clave de configuración: `SpotsMaxLevel`. | 3 |
| Control deslizante **Position:** | Establece la posición vertical inicial de la pila de marcas como un porcentaje de la altura del panadapter. Clave de configuración: `SpotsStartingHeightPercentage`. | 50 |
| Control deslizante **Font Size:** | Establece el tamaño del texto de las marcas en puntos. Clave de configuración: `SpotFontSize`. | 16 |
| Control deslizante **Spot Lifetime:** | Cuánto tiempo permanecen las marcas antes de desaparecer. Escala no lineal de 10 segundos a 24 horas. Se almacena en segundos. Clave de configuración: `DxClusterSpotLifetimeSec`. | 10 seg |
| Opción **Override Colors:** | Fuerza un solo color de texto para todas las marcas. Clave de configuración: `IsSpotsOverrideColorsEnabled`. | Disabled |
| Botón **Spot text color picker** | Abre un cuadro de diálogo de color para elegir el color del texto. Clave de configuración: `SpotsOverrideColor`. | #FFFF00 |
| Opción **Override Background: Enabled** | Dibuja un fondo debajo del texto de las marcas. Clave de configuración: `IsSpotsOverrideBackgroundColorsEnabled`. | Enabled |
| Opción **Override Background: Auto** | Selecciona automáticamente el color de fondo para el contraste. Clave de configuración: `IsSpotsOverrideToAutoBackgroundColorEnabled`. | Enabled |
| Botón **Spot background color picker** | Abre un cuadro de diálogo de color para el color de fondo. Clave de configuración: `SpotsOverrideBgColor`. | #000000 |
| Control deslizante **Background Opacity:** | Alfa del fondo de las marcas (0 = transparente, 100 = opaco). Clave de configuración: `SpotsBackgroundOpacity`. | 48 |
| Opción **Spot Lines:** | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Desactívelo durante concursos para reducir el desorden visual. Clave de configuración: `IsSpotsLinesEnabled`. | Enabled |
| Botón **Clear All Spots** | Borra todas las marcas del panadapter. | N/D |

## Consejos

- Si las marcas se superponen en gran medida, aumente **Levels:** para darles más filas en las que apilarse.
- Si las marcas cubren trazas de señal que necesita ver, reduzca el valor de **Position:** para empujar la pila hacia la parte superior del panadapter, o auméntelo para mover las marcas hacia la parte inferior.
- Durante concursos, desactive **Spot Lines:** para reducir el desorden visual sin desactivar las etiquetas de las marcas por completo.
- El indicador **Total Spots:** en el cuadro de diálogo muestra cuántas marcas activas se están rastreando actualmente, lo que le ayuda a juzgar cuántos niveles se necesitan.
- Use el botón **Clear All Spots** para eliminar rápidamente todas las marcas del panadapter sin cambiar ninguna configuración.

## Relacionados

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Clear every spot from the panadapter](clear-every-spot-from-the-panadapter.md)
