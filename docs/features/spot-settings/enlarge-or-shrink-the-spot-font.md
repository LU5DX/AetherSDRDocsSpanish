# Ampliar o reducir el tamaño de fuente de las estaciones

Use esta página para hacer que el texto de los indicativos de las estaciones sea más grande o más pequeño en el panadapter. Ajustar el tamaño de fuente ayuda cuando las estaciones son difíciles de leer a distancia o cuando se superponen con otros elementos de la pantalla.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El cuadro de diálogo Spot Settings debe ser accesible desde el panadapter. Si las estaciones no son visibles, confirme que el conmutador `IsSpotsEnabled` esté en Enabled — consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de estaciones para abrir el cuadro de diálogo **Spot Settings**.
3. Localice la fila **Font Size:**.
4. Arrastre el control deslizante hacia la izquierda para disminuir el tamaño de fuente o hacia la derecha para aumentarlo. El valor actual en puntos se muestra a la derecha del control deslizante.
5. Suelte el control deslizante. El cambio se aplica de inmediato y se guarda automáticamente.

## Descripción de cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Spots:** | Conmutador maestro para la visualización de estaciones DX. Haga clic para alternar entre los estados habilitado y deshabilitado. El botón siempre muestra "Enabled" independientemente del estado. Se almacena en `IsSpotsEnabled`. | Enabled |
| **Memories:** | Alterna las superposiciones de canales de memoria en el panadapter. Haga clic para alternar entre los estados habilitado y deshabilitado. El botón siempre muestra "Enabled" independientemente del estado. Se almacena en `IsMemorySpotsEnabled`. | Disabled |
| **Levels:** | Filas de apilamiento vertical para las estaciones. Rango 1-10. Se almacena en `SpotsMaxLevel`. | 3 |
| **Position:** | Posición vertical en el panadapter como porcentaje. Rango 0-100. Se almacena en `SpotsStartingHeightPercentage`. | 50 |
| **Font Size:** | Establece el tamaño de texto de los indicativos y etiquetas de las estaciones renderizados en el panadapter. El rango es de 8 a 32 puntos. Se almacena en `SpotFontSize`. | 16 |
| **Spot Lifetime:** | Tiempo que las estaciones permanecen antes de desvanecerse. Escala no lineal de 10 segundos a 24 horas. Se almacena en segundos en `DxClusterSpotLifetimeSec`. | 60 minutes |
| **Override Colors:** | Fuerza un color de texto único para todas las estaciones. Haga clic para alternar entre los estados habilitado y deshabilitado. El botón siempre muestra "Enabled" independientemente del estado. Se almacena en `IsSpotsOverrideColorsEnabled`. | Disabled |
| **Selector de color de texto de estaciones** | Abre un cuadro de diálogo de color para elegir el color del texto. Se almacena en `SpotsOverrideColor`. | #FFFF00 |
| **Override Background: Enabled** | Dibuja un fondo debajo del texto de las estaciones. Se almacena en `IsSpotsOverrideBackgroundColorsEnabled`. | Enabled |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para lograr contraste. Se almacena en `IsSpotsOverrideToAutoBackgroundColorEnabled`. | Enabled |
| **Selector de color de fondo de estaciones** | Abre un cuadro de diálogo de color para el color de fondo. Se almacena en `SpotsOverrideBgColor`. | #000000 |
| **Background Opacity:** | Alfa del fondo de las estaciones (0 = transparente, 100 = opaco). Se almacena en `SpotsBackgroundOpacity`. | 48 |
| **Spot Lines:** | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de estación. Haga clic para alternar entre los estados habilitado y deshabilitado. El botón siempre muestra "Enabled" independientemente del estado. Deshabilite durante los concursos para reducir el desorden visual. Se almacena en `IsSpotsLinesEnabled`. | Enabled |
| **Clear All Spots** | Limpia todas las estaciones del panadapter. | N/A |

## Indicadores

| Indicador | Descripción |
|---|---|
| **Total Spots:** | Muestra el recuento de estaciones activas actualmente rastreadas. |

## Consejos

- Un tamaño de fuente de 16 es el valor predeterminado. Los valores cercanos a 8 reducen el desorden cuando hay muchas estaciones visibles; los valores cercanos a 32 ayudan cuando se ve el panadapter desde una distancia.
- El tamaño de fuente se aplica a todas las estaciones simultáneamente. No existe una anulación de tamaño por estación.
- Deshabilitar **Spot Lines:** puede reducir significativamente el desorden visual durante los concursos cuando hay una gran cantidad de estaciones activas.
- El cuadro de diálogo Spot Settings ahora respeta el tema actual. Si tiene un tema personalizado aplicado, el título del cuadro de diálogo y la etiqueta Total Spots usarán los colores de texto de su tema.
- Los botones de alternancia (Spots, Memories, Override Colors, Spot Lines) siempre muestran "Enabled" independientemente de su estado actual. Verifique el resaltado visual del botón para determinar el estado real: un botón resaltado indica que la función está habilitada.

## Relacionado

- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
