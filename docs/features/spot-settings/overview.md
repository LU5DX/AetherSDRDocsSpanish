# Resumen de la configuración de spots

El cuadro de diálogo de Configuración de Spots controla cómo aparecen los spots de DX y los canales de memoria en el panadapter, incluyendo si se muestran, qué tan densamente se apilan, cuánto tiempo persisten y cómo se colorean su texto y fondo. Ábralo desde el menú contextual del panadapter o desde la superposición de spots.

## Antes de comenzar

- No se requiere una conexión de radio para ajustar la configuración de spots; los cambios surten efecto la próxima vez que se muestren spots.
- Los spots deben ser alimentados desde un clúster de DX configurado u otra fuente (consulte `Settings > SpotHub...`) antes de que aparezcan spots en el panadapter.

## Cómo funciona

El cuadro de diálogo de Configuración de Spots es una ventana independiente. Agrupa los controles en tres áreas: visibilidad y diseño, tiempo de vida y anulaciones de color. Todos los cambios se guardan inmediatamente al interactuar con un control. El diálogo sigue automáticamente el tema actual para colores y estilo.

El indicador **Total Spots:** en la parte inferior del diálogo muestra la cantidad de spots activos que se están rastreando actualmente.

Los botones de alternancia muestran "Enabled" permanentemente y usan un fondo de color (verde para habilitado, rojo/ámbar para deshabilitado) para indicar su estado. Ya no cambian su etiqueta de texto al alternarse.

## Función de cada control

| Etiqueta | Tipo | Valor predeterminado | Comportamiento | Notas |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | Activación general para la visualización de spots de DX. El texto del botón permanece "Enabled"; su color de fondo cambia para indicar el estado. | — |
| Memories: | Botón de alternancia | Deshabilitado | Alterna las superposiciones de canales de memoria en el panadapter. El texto del botón permanece "Enabled"; su color de fondo cambia para indicar el estado. | La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7. |
| Levels: | Deslizador (1–10) | 3 | Filas de apilamiento vertical para spots. | La clave de configuración cambió de `SpotsStackLevels` en v0.9.7. |
| Position: | Deslizador (0–100) | 50 | Posición vertical en el panadapter como porcentaje. | La clave de configuración cambió de `SpotsPosition` en v0.9.7. |
| Font Size: | Deslizador (8–32) | 16 | Tamaño del texto del spot en puntos. | La clave de configuración cambió de `SpotsFontSize` en v0.9.7. |
| Spot Lifetime: | Deslizador (10 seg – 24 h, no lineal) | — | Cuánto tiempo permanecen los spots antes de desvanecerse. | Se almacena en segundos (`DxClusterSpotLifetimeSec`). La clave de configuración cambió de `SpotsLifetime` en v0.9.7. Migra la clave antigua basada en minutos `DxClusterSpotLifetime` en la primera lectura. |
| Override Colors: | Botón de alternancia | Deshabilitado | Fuerza un solo color de texto para todos los spots. El texto del botón permanece "Enabled"; su color de fondo cambia para indicar el estado. | — |
| Selector de color de texto de spot | Botón pulsador | `#FFFF00` | Abre un cuadro de diálogo de color para elegir el color del texto del spot. | — |
| Override Background: Enabled | Botón de alternancia | Habilitado | Dibuja un fondo debajo del texto del spot. El texto del botón permanece "Enabled"; su color de fondo cambia para indicar el estado. | — |
| Override Background: Auto | Botón de alternancia | Habilitado | Selecciona automáticamente el color de fondo para lograr contraste. El texto del botón permanece "Enabled"; su color de fondo cambia para indicar el estado. | — |
| Selector de color de fondo de spot | Botón pulsador | `#000000` | Abre un cuadro de diálogo de color para elegir el color de fondo del spot. | — |
| Background Opacity: | Deslizador (0–100) | 48 | Alfa del fondo del spot (0 = transparente, 100 = opaco). | La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7. |
| Spot Lines: | Botón de alternancia | Habilitado | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. El texto del botón permanece "Enabled"; su color de fondo cambia para indicar el estado. | Nuevo en v0.9.7 (#2349). |
| Clear All Spots | Botón pulsador | — | Limpia todos los spots del panadapter. | — |

## Consejos

- Los botones de alternancia siempre muestran "Enabled" independientemente de su estado actual. El color de fondo del botón indica si la función está activada (verde) o desactivada (rojo/ámbar).
- El deslizador Spot Lifetime no es lineal. Los movimientos pequeños en el extremo inferior del deslizador ajustan la duración en segundos; los movimientos más grandes avanzan a través de minutos y luego horas hasta 24 horas.
- Habilitar Override Background: Auto mientras Override Background: Enabled está activado permite que AetherSDR elija colores de fondo contrastantes automáticamente. Desactive Auto para aplicar en su lugar el color elegido manualmente desde el selector de color de fondo de spot.
- Habilitar Memories: muestra los canales de memoria almacenados de su radio como superposiciones de tipo spot, lo cual es útil para identificar rápidamente actividad en los canales que ha guardado.
- Desactive Spot Lines: durante concursos o cuando el panadapter está abarrotado para reducir el desorden visual. Las etiquetas de los spots permanecen visibles; solo se ocultan las líneas verticales.
- El cuadro de diálogo Configuración de Spots sigue automáticamente el tema actual. Los colores de texto y fondo de los elementos del diálogo se actualizan al cambiar de tema.

## Relacionados

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un solo color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Limpiar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
