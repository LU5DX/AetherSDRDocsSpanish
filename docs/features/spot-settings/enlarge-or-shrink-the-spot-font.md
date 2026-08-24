# Aumentar o reducir la fuente de las spots

Use esta página para hacer que el texto de los indicativos de las spots sea más grande o más pequeño en el panadapter. Ajustar el tamaño de la fuente ayuda cuando las spots son difíciles de leer a distancia o cuando se superponen con otros elementos de la visualización.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El cuadro de diálogo Spot Settings debe ser accesible desde el panadapter. Si las spots no son visibles, confirme que el conmutador `IsSpotsEnabled` esté configurado en Enabled — consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic con el botón derecho en cualquier parte del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el cuadro de diálogo **Spot Settings**.
3. Localice la fila **Font Size:**.
4. Arrastre el control deslizante hacia la izquierda para disminuir el tamaño de la fuente o hacia la derecha para aumentarlo. El valor actual en puntos se muestra a la derecha del control deslizante.
5. Suelte el control deslizante. El cambio se aplica de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control                          | Descripción                                                                                                                                                                                                                                                                                            | Predeterminado                 |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------|
| **Spots:**                       | Conmutador principal para la visualización de spots DX. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando las spots están activadas y a "Disabled" cuando están desactivadas. Se almacena en `IsSpotsEnabled`.                      | Enabled                        |
| **Memories:**                    | Alterna las superposiciones de canales de memoria en el panadapter. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando las memorias están activadas y a "Disabled" cuando están desactivadas. Se almacena en `IsMemorySpotsEnabled`. | Disabled                       |
| **Kiwi DX:**                     | Superpone las spots de la base de datos de la comunidad DX de KiwiSDR (balizas, utilidades, señales de tiempo) en la franja del plan de bandas. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando las spots de Kiwi DX están activadas y a "Disabled" cuando están desactivadas. Se almacena en `ShowKiwiDxSpots`. Nuevo en v26.8.4. | Disabled                       |
| **Levels:**                      | Filas de apilamiento vertical para las spots. Rango 1-10. Se almacena en `SpotsMaxLevel`.                                                                                                                                                                                                              | 3                              |
| **Position:**                    | Posición vertical en el panadapter como porcentaje. Rango 0-100. Se almacena en `SpotsStartingHeightPercentage`.                                                                                                                                                                                      | 50                             |
| **Font Size:**                   | Establece el tamaño del texto de los indicativos de las spots y las etiquetas renderizadas en el panadapter. El rango es de 8 a 32 puntos. Se almacena en `SpotFontSize`.                                                                                                                                 | 16                             |
| **Spot Lifetime:**               | Cuánto tiempo permanecen las spots antes de desvanecerse. Escala no lineal de 10 segundos a 24 horas. Se almacena en segundos en `DxClusterSpotLifetimeSec`.                                                                                                                                            | 60 minutos                     |
| **Override Colors:**             | Fuerza un único color de texto para todas las spots. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando la anulación está activada y a "Disabled" cuando está desactivada. Se almacena en `IsSpotsOverrideColorsEnabled`.          | Disabled                       |
| **Spot text color picker**       | Abre un cuadro de diálogo de color para elegir el color del texto. Se almacena en `SpotsOverrideColor`.                                                                                                                                                                                                | #FFFF00                        |
| **Override Background: Enabled** | Dibuja un fondo debajo del texto de las spots. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando el fondo está activado y a "Disabled" cuando está desactivado. Se almacena en `IsSpotsOverrideBackgroundColorsEnabled`.        | Enabled                        |
| **Override Background: Auto**    | Selecciona automáticamente el color de fondo para el contraste. Se almacena en `IsSpotsOverrideToAutoBackgroundColorEnabled`.                                                                                                                                                                           | Enabled                        |
| **Spot background color picker** | Abre un cuadro de diálogo de color para el color de fondo. Se almacena en `SpotsOverrideBgColor`.                                                                                                                                                                                                      | #000000                        |
| **Background Opacity:**          | Alfa del fondo de las spots (0 = transparente, 100 = opaco). Se almacena en `SpotsBackgroundOpacity`.                                                                                                                                                                                                  | 48                             |
| **Spot Lines:**                  | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Haga clic para alternar entre los estados habilitado y deshabilitado. El texto del botón se actualiza a "Enabled" cuando las líneas están activadas y a "Disabled" cuando están desactivadas. Deshabilítelo durante concursos para reducir el desorden visual. Se almacena en `IsSpotsLinesEnabled`. | Enabled                        |
| **Clear All Spots**              | Borra todas las spots del panadapter.                                                                                                                                                                                                                                                                  | N/A                            |

## Indicadores

| Indicador | Descripción |
|---|---|
| **Total Spots:** | Muestra el recuento de spots activas que se están rastreando actualmente. |

## Consejos

- Un tamaño de fuente de 16 es el predeterminado. Los valores cercanos a 8 reducen el desorden cuando hay muchas spots visibles; los valores cercanos a 32 ayudan cuando se visualiza el panadapter desde una distancia.
- El tamaño de fuente se aplica a todas las spots simultáneamente. No existe una anulación de tamaño por spot.
- Habilitar **Kiwi DX:** añade spots para balizas, utilidades y señales de tiempo de la base de datos de la comunidad DX de KiwiSDR a la franja del plan de bandas. Esto puede ser útil para monitorear balizas de propagación, pero puede añadir desorden en bandas concurridas.
- Deshabilitar **Spot Lines:** puede reducir significativamente el desorden visual durante concursos cuando hay una gran cantidad de spots activas.
- El cuadro de diálogo Spot Settings ahora respeta el tema actual. Si tiene un tema personalizado aplicado, el título del cuadro de diálogo y la etiqueta Total Spots usarán los colores de texto de su tema.
- Los botones de alternancia (Spots, Memories, Kiwi DX, Override Colors, Override Background: Enabled, Spot Lines) ahora muestran "Enabled" cuando la función está activa y "Disabled" cuando la función está inactiva. Verifique el texto del botón para determinar el estado actual.

## Relacionado

- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
