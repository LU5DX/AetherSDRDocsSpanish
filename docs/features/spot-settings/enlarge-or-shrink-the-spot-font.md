# Aumentar o reducir el tamaño de la fuente de los spots

Utilice esta página para hacer que el texto de los indicativos de los spots aparezca más grande o más pequeño en el panadapter. Ajustar el tamaño de fuente ayuda cuando los spots son difíciles de leer a distancia o cuando se superponen con otros elementos de la pantalla.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El cuadro de diálogo Spot Settings debe ser accesible desde el panadapter. Si los spots no son visibles, confirme que el interruptor `IsSpotsEnabled` esté en Enabled — consulte [Activar o desactivar spots](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el cuadro de diálogo **Spot Settings**.
3. Localice la fila **Font Size:**.
4. Arrastre el control deslizante hacia la izquierda para disminuir el tamaño de fuente o hacia la derecha para aumentarlo. El valor actual en puntos se muestra a la derecha del control deslizante.
5. Suelte el control deslizante. El cambio tiene efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Spots:** | Interruptor maestro para la visualización de spots DX. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando los spots están activos y a "Disabled" cuando están desactivados. Se almacena en `IsSpotsEnabled`. | Enabled |
| **Memories:** | Activa o desactiva las superposiciones de canales de memoria en el panadapter. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando las memorias están activas y a "Disabled" cuando están desactivadas. Se almacena en `IsMemorySpotsEnabled`. | Disabled |
| **Levels:** | Filas de apilamiento vertical para spots. Rango 1-10. Se almacena en `SpotsMaxLevel`. | 3 |
| **Position:** | Posición vertical en el panadapter como porcentaje. Rango 0-100. Se almacena en `SpotsStartingHeightPercentage`. | 50 |
| **Font Size:** | Establece el tamaño del texto de los indicativos y etiquetas de los spots representados en el panadapter. El rango es de 8 a 32 puntos. Se almacena en `SpotFontSize`. | 16 |
| **Spot Lifetime:** | Tiempo que los spots permanecen antes de desvanecerse. Escala no lineal desde 10 segundos hasta 24 horas. Se almacena en segundos en `DxClusterSpotLifetimeSec`. | 60 minutos |
| **Override Colors:** | Fuerza un único color de texto para todos los spots. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando la anulación está activa y a "Disabled" cuando está desactivada. Se almacena en `IsSpotsOverrideColorsEnabled`. | Disabled |
| **Selector de color de texto de spot** | Abre un cuadro de diálogo de color para elegir el color del texto. Se almacena en `SpotsOverrideColor`. | #FFFF00 |
| **Override Background: Enabled** | Dibuja un fondo debajo del texto del spot. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando el fondo está activo y a "Disabled" cuando está desactivado. Se almacena en `IsSpotsOverrideBackgroundColorsEnabled`. | Enabled |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para el contraste. Se almacena en `IsSpotsOverrideToAutoBackgroundColorEnabled`. | Enabled |
| **Selector de color de fondo de spot** | Abre un cuadro de diálogo de color para el color de fondo. Se almacena en `SpotsOverrideBgColor`. | #000000 |
| **Background Opacity:** | Alpha del fondo del spot (0 = transparente, 100 = opaco). Se almacena en `SpotsBackgroundOpacity`. | 48 |
| **Spot Lines:** | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando las líneas están activas y a "Disabled" cuando están desactivadas. Desactive durante concursos para reducir el desorden visual. Se almacena en `IsSpotsLinesEnabled`. | Enabled |
| **Clear All Spots** | Elimina todos los spots del panadapter. | N/A |

## Indicadores

| Indicador | Descripción |
|---|---|
| **Total Spots:** | Muestra el recuento de spots activos actualmente rastreados. |

## Consejos

- Un tamaño de fuente de 16 es el valor predeterminado. Los valores cercanos a 8 reducen el desorden cuando hay muchos spots visibles; los valores cercanos a 32 ayudan al ver el panadapter desde una distancia.
- El tamaño de fuente se aplica a todos los spots simultáneamente. No existe una anulación de tamaño por spot.
- Desactivar **Spot Lines:** puede reducir significativamente el desorden visual durante concursos cuando hay una gran cantidad de spots activos.
- El cuadro de diálogo Spot Settings ahora respeta el tema actual. Si tiene un tema personalizado aplicado, el título del cuadro de diálogo y la etiqueta Total Spots utilizarán los colores de texto de su tema.
- Los botones de alternancia (Spots, Memories, Override Colors, Override Background: Enabled, Spot Lines) ahora muestran "Enabled" cuando la función está activa y "Disabled" cuando la función está inactiva. Verifique el texto del botón para determinar el estado actual.

## Relacionado

- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
