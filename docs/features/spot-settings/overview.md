# Resumen de los ajustes de spots

El diálogo de Ajustes de Spots controla cómo aparecen los spots de DX y los canales de memoria en el panadapter, incluyendo si se muestran, qué tan densamente se apilan, cuánto tiempo persisten y cómo se colorean su texto y fondo. Ábralo desde el menú contextual del panadapter o desde la superposición de spots.

## Antes de comenzar

- No se requiere una conexión de radio para ajustar los ajustes de spots; los cambios surten efecto cuando los spots se muestren la próxima vez.
- Los spots deben alimentarse desde un clúster de DX configurado u otra fuente (consulte `Settings > SpotHub...`) antes de que aparezcan en el panadapter.

## Cómo funciona

El diálogo de Ajustes de Spots es una ventana independiente. Agrupa los controles en tres áreas: visibilidad y diseño, tiempo de vida y anulaciones de color. Todos los cambios se guardan inmediatamente al interactuar con un control. El diálogo sigue automáticamente el tema actual para colores y estilo.

El indicador **Total Spots:** en la parte inferior del diálogo muestra la cantidad de spots activos que se están rastreando.

Los botones de alternancia muestran el texto "Enabled" o "Disabled" que se actualiza para reflejar el estado actual, con un fondo de color (verde para habilitado, rojo/ámbar para deshabilitado).

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Comportamiento | Notas |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Enabled | Alternancia maestra para la visualización de spots de DX. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | — |
| Memories: | Botón de alternancia | Disabled | Alterna las superposiciones de canales de memoria en el panadapter. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | Clave de ajuste cambiada de `IsMemoriesShownOnPanadapter` en v0.9.7. |
| Levels: | Deslizador (1–10) | 3 | Filas de apilamiento vertical para spots. | Clave de ajuste cambiada de `SpotsStackLevels` en v0.9.7. |
| Position: | Deslizador (0–100) | 50 | Posición vertical en el panadapter como porcentaje. | Clave de ajuste cambiada de `SpotsPosition` en v0.9.7. |
| Font Size: | Deslizador (8–32) | 16 | Tamaño del texto del spot en puntos. | Clave de ajuste cambiada de `SpotsFontSize` en v0.9.7. |
| Spot Lifetime: | Deslizador (10 seg – 24 hrs, no lineal) | — | Cuánto tiempo permanecen los spots antes de desvanecerse. | Se almacena en segundos (`DxClusterSpotLifetimeSec`). Clave de ajuste cambiada de `SpotsLifetime` en v0.9.7. Migra la clave anterior basada en minutos `DxClusterSpotLifetime` en la primera lectura. |
| Override Colors: | Botón de alternancia | Disabled | Fuerza un solo color de texto para todos los spots. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | — |
| Selector de color de texto del spot | Botón pulsador | `#FFFF00` | Abre un diálogo de color para elegir el color del texto del spot. | — |
| Override Background: Enabled | Botón de alternancia | Enabled | Dibuja un fondo debajo del texto del spot. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | — |
| Override Background: Auto | Botón de alternancia | Enabled | Selecciona automáticamente el color de fondo para contraste. El texto del botón permanece "Auto"; su color de fondo cambia para indicar el estado. | — |
| Selector de color de fondo del spot | Botón pulsador | `#000000` | Abre un diálogo de color para elegir el color de fondo del spot. | — |
| Background Opacity: | Deslizador (0–100) | 48 | Canal alfa del fondo del spot (0 = transparente, 100 = opaco). | Clave de ajuste cambiada de `SpotsOverrideBgOpacity` en v0.9.7. |
| Spot Lines: | Botón de alternancia | Enabled | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelas durante concursos para reducir el desorden visual. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | Nuevo en v0.9.7 (#2349). |
| Clear All Spots | Botón pulsador | — | Limpia todos los spots del panadapter. | — |

## Consejos

- Los botones de alternancia muestran el texto "Enabled" o "Disabled" que se actualiza para reflejar el estado actual, con un fondo verde cuando están habilitados y rojo/ámbar cuando están deshabilitados.
- El deslizador Spot Lifetime es no lineal. Los movimientos pequeños en el extremo inferior del deslizador ajustan la vida útil en segundos; los movimientos más grandes avanzan a través de minutos y luego horas hasta 24 horas.
- Habilitar Override Background: Auto mientras Override Background: Enabled está activado permite que AetherSDR elija automáticamente colores de fondo contrastantes. Desactive Auto para aplicar su color seleccionado manualmente desde el selector de color de fondo del spot en su lugar.
- Habilitar Memories: muestra los canales de memoria almacenados de su radio como superposiciones de estilo spot, lo cual es útil para identificar rápidamente actividad en los canales que ha guardado.
- Desactive Spot Lines: durante concursos o cuando el panadapter esté abarrotado para reducir el desorden visual. Las etiquetas de spot permanecen visibles; solo se ocultan las líneas verticales.
- El diálogo de Ajustes de Spots sigue automáticamente el tema actual. Los colores de texto y fondo de los elementos del diálogo se actualizan al cambiar de tema.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la vida útil de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un solo color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Limpiar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
