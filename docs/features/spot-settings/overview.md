# Descripción general de la configuración de spots

El diálogo de Configuración de Spots controla cómo aparecen los spots de DX y los canales de memoria en el panadapter, incluyendo si se muestran, cuán densamente se apilan, cuánto tiempo persisten y cómo se colorean el texto y los fondos. Ábralo desde el menú contextual del panadapter o desde la superposición de spots.

## Antes de comenzar

- No se requiere una conexión de radio para ajustar la configuración de spots; los cambios surten efecto cuando los spots se muestren la próxima vez.
- Los spots deben provenir de un cluster de DX configurado u otra fuente (consulte `Settings > SpotHub...`) antes de que aparezcan en el panadapter.

## Cómo funciona

El diálogo de Configuración de Spots es una ventana independiente. Agrupa los controles en tres áreas: visibilidad y diseño, duración y anulaciones de color. Todos los cambios se guardan inmediatamente al interactuar con un control. El diálogo sigue automáticamente el tema actual para colores y estilo.

El indicador **Total Spots:** en la parte inferior del diálogo muestra la cantidad de spots activos que se están rastreando actualmente.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Comportamiento | Notas |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | Activación general de la visualización de spots de DX. | — |
| Memories: | Botón de alternancia | Deshabilitado | Activa/desactiva las superposiciones de canales de memoria en el panadapter. | La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7. |
| Levels: | Deslizador (1–10) | 3 | Filas de apilamiento vertical para spots. | La clave de configuración cambió de `SpotsStackLevels` en v0.9.7. |
| Position: | Deslizador (0–100) | 50 | Posición vertical en el panadapter como porcentaje. | La clave de configuración cambió de `SpotsPosition` en v0.9.7. |
| Font Size: | Deslizador (8–32) | 16 | Tamaño del texto de los spots en puntos. | La clave de configuración cambió de `SpotsFontSize` en v0.9.7. |
| Spot Lifetime: | Deslizador (10 seg – 24 hrs, no lineal) | — | Cuánto tiempo permanecen los spots antes de desvanecerse. | Se almacena en segundos (`DxClusterSpotLifetimeSec`). La clave de configuración cambió de `SpotsLifetime` en v0.9.7. Migra la clave anterior basada en minutos `DxClusterSpotLifetime` en la primera lectura. |
| Override Colors: | Botón de alternancia | Deshabilitado | Fuerza un solo color de texto para todos los spots. | — |
| Selector de color de texto de spots | Botón pulsador | `#FFFF00` | Abre un diálogo de color para elegir el color del texto de los spots. | — |
| Override Background: Enabled | Botón de alternancia | Habilitado | Dibuja un fondo debajo del texto de los spots. | — |
| Override Background: Auto | Botón de alternancia | Habilitado | Selecciona automáticamente el color de fondo para contraste. | — |
| Selector de color de fondo de spots | Botón pulsador | `#000000` | Abre un diálogo de color para elegir el color de fondo de los spots. | — |
| Background Opacity: | Deslizador (0–100) | 48 | Alfa del fondo de los spots (0 = transparente, 100 = opaco). | La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7. |
| Spot Lines: | Botón de alternancia | Habilitado | Dibuja líneas verticales desde la línea de base del espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. | Nuevo en v0.9.7 (#2349). |
| Clear All Spots | Botón pulsador | — | Borra todos los spots del panadapter. | — |

## Consejos

- El deslizador Spot Lifetime no es lineal. Los movimientos pequeños en el extremo inferior del deslizador ajustan la duración en segundos; los movimientos más grandes avanzan por minutos y luego hasta 24 horas.
- Activar Override Background: Auto mientras Override Background: Enabled está habilitado permite que AetherSDR elija automáticamente colores de fondo contrastantes. Deshabilite Auto para aplicar su color seleccionado manualmente desde el selector de color de fondo de spots.
- Activar Memories: muestra los canales de memoria almacenados de su radio como superposiciones tipo spot, lo cual es útil para identificar rápidamente actividad en canales que ha guardado.
- Deshabilite Spot Lines: durante concursos o cuando el panadapter esté abarrotado para reducir el desorden visual. Las etiquetas de los spots permanecen visibles; solo se ocultan las líneas verticales.
- El diálogo de Configuración de Spots sigue automáticamente el tema actual. Los colores de texto y fondo de los elementos del diálogo se actualizan al cambiar de tema.

## Relacionado

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un solo color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Borrar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
