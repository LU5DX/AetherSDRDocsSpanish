# Cambiar la densidad y la posición vertical de los marcadores

Utilice el cuadro de diálogo Spot Settings para controlar cuántas filas verticales de marcadores aparecen en el panadapter y dónde se ubican esas filas en relación con la visualización del espectro.

## Antes de comenzar

- Abra un panadapter. Los marcadores no necesitan estar recibiendo activamente, pero el panadapter debe estar visible.
- El conmutador **Spots:** debe estar configurado en **Enabled** para que los cambios sean visibles. Consulte [Turn spots on or off](turn-spots-on-or-off.md).

## Pasos

1. Haga clic derecho en el panadapter (o en la superposición de marcadores) para abrir el menú contextual y, a continuación, seleccione la opción que abre el cuadro de diálogo Spot Settings.
2. Se abre la ventana **Spot Settings**.
3. Para cambiar la densidad (la cantidad de filas de apilamiento vertical), arrastre el control deslizante **Levels:**. El valor actual se muestra a la derecha del control deslizante. Rango válido: 1–10.
4. Para cambiar la posición vertical (dónde se ubica la pila de filas en el panadapter), arrastre el control deslizante **Position:**. El valor actual (0–100) se muestra a la derecha del control deslizante. Los valores más bajos mueven los marcadores hacia la parte superior; los valores más altos los mueven hacia la parte inferior.
5. Para mostrar u ocultar las líneas verticales trazadas desde la línea base del espectro hasta cada etiqueta de marcador, haga clic en el conmutador **Spot Lines:**. Consulte [What each control does](#what-each-control-does) a continuación.
6. Los cambios surten efecto de inmediato. Cierre el cuadro de diálogo cuando haya terminado.

## What each control does

| Control                                 | Comportamiento                                                                                                                                                                                                         | Predeterminado               |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| Conmutador **Spots:**                   | Conmutador maestro para la visualización de marcadores DX. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsEnabled`.                                            | Enabled                      |
| Conmutador **Memories:**                | Activa o desactiva las superposiciones de canales de memoria en el panadapter. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsMemorySpotsEnabled`.                   | Disabled                     |
| Conmutador **Kiwi DX:**                 | Superpone marcadores de la base de datos comunitaria de DX de KiwiSDR (balizas, servicios, señales horarias) en la franja del plan de bandas. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `ShowKiwiDxSpots`. | Disabled                     |
| Control deslizante **Levels:**          | Establece la cantidad de filas de apilamiento vertical disponibles para los marcadores. Más filas reducen la superposición cuando hay muchos marcadores en el mismo rango de frecuencia. Clave de configuración: `SpotsMaxLevel`. | 3                            |
| Control deslizante **Position:**        | Establece la posición inicial vertical de la pila de marcadores como porcentaje de la altura del panadapter. Clave de configuración: `SpotsStartingHeightPercentage`.                                                  | 50                           |
| Control deslizante **Font Size:**       | Establece el tamaño del texto de los marcadores en puntos. Clave de configuración: `SpotFontSize`.                                                                                                                     | 16                           |
| Control deslizante **Spot Lifetime:**   | Cuánto tiempo permanecen los marcadores antes de desvanecerse. Escala no lineal de 10 segundos a 24 horas. Almacenado en segundos. Clave de configuración: `DxClusterSpotLifetimeSec`.                                 | 10 seg                       |
| Conmutador **Override Colors:**         | Fuerza un único color de texto para todos los marcadores. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsOverrideColorsEnabled`.                                 | Disabled                     |
| Botón **Spot text color picker**        | Abre un cuadro de diálogo de color para elegir el color del texto. Clave de configuración: `SpotsOverrideColor`.                                                                                                       | #FFFF00                      |
| Conmutador **Override Background: Enabled** | Dibuja un fondo debajo del texto de los marcadores. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsOverrideBackgroundColorsEnabled`.                             | Enabled                      |
| Conmutador **Override Background: Auto**    | Selecciona automáticamente el color de fondo para el contraste. Clave de configuración: `IsSpotsOverrideToAutoBackgroundColorEnabled`.                                                                                 | Enabled                      |
| Botón **Spot background color picker**  | Abre un cuadro de diálogo de color para el color de fondo. Clave de configuración: `SpotsOverrideBgColor`.                                                                                                             | #000000                      |
| Control deslizante **Background Opacity:** | Alfa del fondo de los marcadores (0 = transparente, 100 = opaco). Clave de configuración: `SpotsBackgroundOpacity`.                                                                                                    | 48                           |
| Conmutador **Spot Lines:**              | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de marcador. Desactívelo durante concursos para reducir el desorden visual. El texto del botón se actualiza para mostrar "Enabled" o "Disabled". Clave de configuración: `IsSpotsLinesEnabled`. | Enabled                      |
| Botón **Clear All Spots**               | Borra todos los marcadores del panadapter.                                                                                                                                                                              | N/A                          |

## Consejos

- Si los marcadores se superponen considerablemente, aumente **Levels:** para darles más filas donde apilarse.
- Si los marcadores cubren trazas de señal que necesita ver, reduzca el valor de **Position:** para empujar la pila hacia la parte superior del panadapter, o auméntelo para mover los marcadores hacia la parte inferior.
- Durante concursos, desactive **Spot Lines:** para reducir el desorden visual sin desactivar por completo las etiquetas de los marcadores.
- Use el conmutador **Kiwi DX:** para mostrar marcadores de balizas, servicios y señales horarias de la base de datos comunitaria de DX de KiwiSDR en la franja del plan de bandas.
- El indicador **Total Spots:** en el cuadro de diálogo muestra cuántos marcadores activos se están rastreando actualmente, lo que le ayuda a determinar cuántos niveles se necesitan.
- Use el botón **Clear All Spots** para eliminar rápidamente todos los marcadores del panadapter sin cambiar ninguna configuración.

## Relacionado

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Clear every spot from the panadapter](clear-every-spot-from-the-panadapter.md)
