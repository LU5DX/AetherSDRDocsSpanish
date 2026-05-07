# Descripción general de la configuración de spots

El cuadro de diálogo Configuración de spots controla cómo aparecen los spots de DX y los canales de memoria en el panadapter, incluyendo si se muestran o no, qué tan densamente se apilan, cuánto tiempo persisten y cómo se colorean su texto y fondo. Ábralo desde el menú contextual del panadapter o desde la superposición de spots.

## Antes de comenzar

- No se requiere una conexión de radio para ajustar la configuración de spots; los cambios surten efecto cuando los spots se muestren la próxima vez.
- Los spots deben ser alimentados desde un clúster de DX configurado u otra fuente (consulte `Settings > SpotHub...`) antes de que aparezcan spots en el panadapter.

## Cómo funciona

El cuadro de diálogo Configuración de spots es una ventana independiente. Agrupa los controles en tres áreas: visibilidad y diseño, tiempo de vida y anulación de colores. Todos los cambios se guardan inmediatamente al interactuar con un control.

El indicador **Total Spots:** en la parte inferior del cuadro de diálogo muestra la cantidad de spots activos que se están rastreando actualmente.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Comportamiento | Notas |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | Activar/desactivar principal para la visualización de spots de DX. | — |
| Memories: | Botón de alternancia | Deshabilitado | Alterna las superposiciones de canales de memoria en el panadapter. | La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7. |
| Levels: | Deslizador (1–10) | 3 | Filas de apilamiento vertical para spots. | La clave de configuración cambió de `SpotsStackLevels` en v0.9.7. |
| Position: | Deslizador (0–100) | 50 | Posición vertical en el panadapter como porcentaje. | La clave de configuración cambió de `SpotsPosition` en v0.9.7. |
| Font Size: | Deslizador (8–32) | 16 | Tamaño del texto del spot en puntos. | La clave de configuración cambió de `SpotsFontSize` en v0.9.7. |
| Spot Lifetime: | Deslizador (10 seg – 24 h, no lineal) | — | Cuánto tiempo permanecen los spots antes de desvanecerse. | Se almacena en segundos (`DxClusterSpotLifetimeSec`). La clave de configuración cambió de `SpotsLifetime` en v0.9.7. Migra la clave anterior basada en minutos `DxClusterSpotLifetime` en la primera lectura. |
| Override Colors: | Botón de alternancia | Deshabilitado | Fuerza un solo color de texto para todos los spots. | — |
| Selector de color de texto de spot | Botón pulsador | `#FFFF00` | Abre un cuadro de diálogo de color para elegir el color del texto del spot. | — |
| Override Background: Enabled | Botón de alternancia | Habilitado | Dibuja un fondo debajo del texto del spot. | — |
| Override Background: Auto | Botón de alternancia | Habilitado | Selecciona automáticamente el color de fondo para el contraste. | — |
| Selector de color de fondo de spot | Botón pulsador | `#000000` | Abre un cuadro de diálogo de color para elegir el color de fondo del spot. | — |
| Background Opacity: | Deslizador (0–100) | 48 | Alfa del fondo del spot (0 = transparente, 100 = opaco). | La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7. |
| Spot Lines: | Botón de alternancia | Habilitado | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante los concursos para reducir el desorden visual. | Nuevo en v0.9.7 (#2349). |
| Clear All Spots | Botón pulsador | — | Elimina todos los spots del panadapter. | — |

## Consejos

- El deslizador Spot Lifetime es no lineal. Los movimientos pequeños en el extremo inferior del deslizador ajustan el tiempo de vida en segundos; los movimientos más grandes avanzan a través de minutos y luego horas hasta 24 horas.
- Al habilitar Override Background: Auto mientras Override Background: Enabled está activado, AetherSDR elige automáticamente colores de fondo contrastantes. Desactive Auto para aplicar su color elegido manualmente desde el selector de color de fondo de spot.
- Al habilitar Memories: se muestran los canales de memoria almacenados de su radio como superposiciones tipo spot, lo cual es útil para identificar rápidamente la actividad en los canales que ha guardado.
- Desactive Spot Lines: durante los concursos o cuando el panadapter esté abarrotado para reducir el desorden visual. Las etiquetas de los spots permanecen visibles; solo se ocultan las líneas verticales.

## Relacionado

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un solo color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
