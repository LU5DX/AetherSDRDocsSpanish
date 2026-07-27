# Cambiar la densidad y la posición vertical de los spots

Utilice el cuadro de diálogo Spot Settings para controlar cuántas filas verticales de spots aparecen en el panadapter y dónde se sitúan esas filas en relación con la visualización del espectro.

## Antes de empezar

- Abra un panadapter. No es necesario que los spots estén recibiendo activamente, pero el panadapter debe estar visible.
- La alternancia **Spots:** debe estar configurada en **Enabled** para que los cambios sean visibles. Consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en el panadapter (o en la superposición de spots) para abrir el menú contextual, luego seleccione la opción que abre el cuadro de diálogo Spot Settings.
2. Se abre la ventana **Spot Settings**.
3. Para cambiar la densidad (la cantidad de filas de apilamiento vertical), arrastre el control deslizante **Levels:**. El valor actual se muestra a la derecha del control deslizante. Rango válido: 1–10.
4. Para cambiar la posición vertical (dónde se sitúa la pila de filas en el panadapter), arrastre el control deslizante **Position:**. El valor actual (0–100) se muestra a la derecha del control deslizante. Los valores más bajos mueven los spots hacia la parte superior; los valores más altos los mueven hacia la parte inferior.
5. Para mostrar u ocultar las líneas verticales trazadas desde la línea base del espectro hasta cada etiqueta de spot, haga clic en la alternancia **Spot Lines:**. Consulte [Qué hace cada control](#qué-hace-cada-control) a continuación.
6. Los cambios surten efecto de inmediato. Cierre el cuadro de diálogo cuando haya terminado.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Alternancia **Spots:** | Alternancia maestra para la visualización de spots DX. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsEnabled`. | Enabled |
| Alternancia **Memories:** | Alterna las superposiciones de canales de memoria en el panadapter. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsMemorySpotsEnabled`. | Disabled |
| Control deslizante **Levels:** | Establece el número de filas de apilamiento vertical disponibles para los spots. Más filas reducen la superposición cuando hay muchos spots en el mismo rango de frecuencia. Clave de configuración: `SpotsMaxLevel`. | 3 |
| Control deslizante **Position:** | Establece la posición vertical inicial de la pila de spots como un porcentaje de la altura del panadapter. Clave de configuración: `SpotsStartingHeightPercentage`. | 50 |
| Control deslizante **Font Size:** | Establece el tamaño del texto del spot en puntos. Clave de configuración: `SpotFontSize`. | 16 |
| Control deslizante **Spot Lifetime:** | Tiempo que los spots permanecen antes de desvanecerse. Escala no lineal de 10 segundos a 24 horas. Almacenado en segundos. Clave de configuración: `DxClusterSpotLifetimeSec`. | 10 seg |
| Alternancia **Override Colors:** | Fuerza un solo color de texto para todos los spots. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsOverrideColorsEnabled`. | Disabled |
| Botón **selector de color de texto de spot** | Abre un cuadro de diálogo de color para elegir el color del texto. Clave de configuración: `SpotsOverrideColor`. | #FFFF00 |
| Alternancia **Override Background: Enabled** | Dibuja un fondo debajo del texto del spot. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsOverrideBackgroundColorsEnabled`. | Enabled |
| Alternancia **Override Background: Auto** | Selecciona automáticamente el color de fondo para el contraste. Clave de configuración: `IsSpotsOverrideToAutoBackgroundColorEnabled`. | Enabled |
| Botón **selector de color de fondo de spot** | Abre un cuadro de diálogo de color para el color de fondo. Clave de configuración: `SpotsOverrideBgColor`. | #000000 |
| Control deslizante **Background Opacity:** | Alfa del fondo del spot (0 = transparente, 100 = opaco). Clave de configuración: `SpotsBackgroundOpacity`. | 48 |
| Alternancia **Spot Lines:** | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívela durante concursos para reducir el desorden visual. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsLinesEnabled`. | Enabled |
| Botón **Clear All Spots** | Elimina todos los spots del panadapter. | N/A |

## Consejos

- Si los spots se superponen mucho, aumente **Levels:** para darles más filas en las que apilarse.
- Si los spots cubren trazas de señal que necesita ver, reduzca el valor de **Position:** para empujar la pila hacia la parte superior del panadapter, o auméntelo para mover los spots hacia la parte inferior.
- Durante concursos, desactive **Spot Lines:** para reducir el desorden visual sin desactivar por completo las etiquetas de los spots.
- El indicador **Total Spots:** en el cuadro de diálogo muestra cuántos spots activos se están rastreando actualmente, lo que le ayuda a juzgar cuántos niveles se necesitan.
- Utilice el botón **Clear All Spots** para eliminar rápidamente todos los spots del panadapter sin cambiar ninguna configuración.

## Relacionado

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Clear every spot from the panadapter](clear-every-spot-from-the-panadapter.md)
