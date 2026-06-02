# Aumentar o reducir el tamaño de fuente de los puntos

Use esta página para agrandar o achicar el texto de los indicativos de los puntos en el panadapter. Ajustar el tamaño de fuente ayuda cuando los puntos son difíciles de leer a distancia o cuando se superponen con otros elementos de la pantalla.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El cuadro de diálogo Spot Settings debe ser accesible desde el panadapter. Si los puntos no están visibles, confirme que el interruptor `IsSpotsEnabled` esté en Enabled; consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de puntos para abrir el cuadro de diálogo **Spot Settings**.
3. Localice la fila **Font Size:**.
4. Arrastre el control deslizante hacia la izquierda para disminuir el tamaño de fuente o hacia la derecha para aumentarlo. El valor actual en puntos se muestra a la derecha del control deslizante.
5. Suelte el control deslizante. El cambio se aplica de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Spots:** | Interruptor maestro para la visualización de puntos DX. Se almacena en `IsSpotsEnabled`. | Enabled |
| **Memories:** | Activa o desactiva las superposiciones de canales de memoria en el panadapter. Se almacena en `IsMemorySpotsEnabled`. | Disabled |
| **Levels:** | Filas de apilamiento vertical para puntos. Rango 1-10. Se almacena en `SpotsMaxLevel`. | 3 |
| **Position:** | Posición vertical en el panadapter como porcentaje. Rango 0-100. Se almacena en `SpotsStartingHeightPercentage`. | 50 |
| **Font Size:** | Establece el tamaño de texto de los indicativos y etiquetas de puntos renderizados en el panadapter. Rango de 8 a 32 puntos. Se almacena en `SpotFontSize`. | 16 |
| **Spot Lifetime:** | Cuánto tiempo permanecen los puntos antes de desvanecerse. Escala no lineal de 10 segundos a 24 horas. Se almacena en segundos en `DxClusterSpotLifetimeSec`. | 60 minutos |
| **Override Colors:** | Fuerza un solo color de texto para todos los puntos. Se almacena en `IsSpotsOverrideColorsEnabled`. | Disabled |
| **Spot text color picker** | Abre un cuadro de diálogo de color para elegir el color del texto. Se almacena en `SpotsOverrideColor`. | #FFFF00 |
| **Override Background: Enabled** | Dibuja un fondo debajo del texto del punto. Se almacena en `IsSpotsOverrideBackgroundColorsEnabled`. | Enabled |
| **Override Background: Auto** | Elige automáticamente el color de fondo para el contraste. Se almacena en `IsSpotsOverrideToAutoBackgroundColorEnabled`. | Enabled |
| **Spot background color picker** | Abre un cuadro de diálogo de color para el color de fondo. Se almacena en `SpotsOverrideBgColor`. | #000000 |
| **Background Opacity:** | Alfa del fondo del punto (0 = transparente, 100 = opaco). Se almacena en `SpotsBackgroundOpacity`. | 48 |
| **Spot Lines:** | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de punto. Desactive durante concursos para reducir el desorden visual. Se almacena en `IsSpotsLinesEnabled`. | Enabled |
| **Clear All Spots** | Borra todos los puntos del panadapter. | N/A |

## Indicadores

| Indicador | Descripción |
|---|---|
| **Total Spots:** | Muestra la cantidad de puntos activos que se están rastreando actualmente. |

## Consejos

- Un tamaño de fuente de 16 es el valor predeterminado. Los valores cercanos a 8 reducen el desorden cuando hay muchos puntos visibles; los valores cercanos a 32 ayudan cuando se ve el panadapter desde una distancia.
- El tamaño de fuente se aplica a todos los puntos simultáneamente. No existe una anulación de tamaño por punto.
- Deshabilitar **Spot Lines:** puede reducir significativamente el desorden visual durante concursos cuando hay una gran cantidad de puntos activos.
- El cuadro de diálogo Spot Settings ahora respeta el tema actual. Si tiene un tema personalizado aplicado, el título del cuadro de diálogo y la etiqueta Total Spots usarán los colores de texto de su tema.

## Relacionados

- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
