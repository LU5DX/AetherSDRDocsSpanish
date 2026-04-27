# Descripción general de Spot Settings

El diálogo Spot Settings controla cómo aparecen los spots de DX y los canales de memoria en el panadapter — incluyendo si se muestran, qué tan densamente se apilan, cuánto tiempo persisten y cómo se colorean su texto y fondos. Ábralo desde el menú contextual del panadapter o desde la superposición de spots.

## Antes de comenzar

- No se requiere una conexión de radio para ajustar la configuración de spots; los cambios tienen efecto la próxima vez que se muestren los spots.
- Los spots deben provenir de un clúster de DX configurado u otra fuente (consulte `Settings > SpotHub...`) antes de que aparezca algún spot en el panadapter.

## Cómo funciona

El diálogo Spot Settings es una ventana independiente. Agrupa los controles en tres áreas: visibilidad y diseño, duración y anulaciones de color. Todos los cambios se guardan inmediatamente al interactuar con un control.

El indicador **Total Spots:** en la parte inferior del diálogo muestra la cantidad de spots activos que se están rastreando en ese momento.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | `IsSpotsEnabled` | Control maestro para mostrar spots de DX en el panadapter. |
| Memories: | Botón de alternancia | Deshabilitado | `IsMemoriesShownOnPanadapter` | Superpone los canales de memoria de la radio en el panadapter como marcadores similares a spots. |
| Levels: | Control deslizante | 3 | `SpotsStackLevels` | Establece el número de filas de apilamiento vertical cuando los spots están próximos en frecuencia. Rango: 1–10. |
| Position: | Control deslizante | 50 | `SpotsPosition` | Establece la posición vertical de la fila de spots en el panadapter como porcentaje desde la parte superior. Rango: 0–100. |
| Font Size: | Control deslizante | 16 | `SpotsFontSize` | Controla el tamaño del texto de la etiqueta del spot. Rango: 8–32. |
| Spot Lifetime: | Control deslizante | 30 min | `SpotsLifetime` | Tiempo durante el cual un spot permanece visible antes de expirar. Utiliza una escala no lineal: 10–55 segundos en pasos de 5 segundos, luego 5–55 minutos en pasos de 5 minutos, luego 1–24 horas en pasos de 1 hora. |
| Override Colors: | Botón de alternancia | Deshabilitado | `IsSpotsOverrideColorsEnabled` | Cuando está habilitado, fuerza a que todo el texto de los spots use el color único elegido por el selector de color de texto, en lugar de los colores por fuente. |
| Selector de color de texto de spot | Botón de acción | `#FFFF00` | `SpotsOverrideColor` | Abre un diálogo de color para elegir el color de texto de anulación. Solo se aplica cuando Override Colors: está habilitado. |
| Override Background: Enabled | Botón de alternancia | Habilitado | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo relleno detrás de cada etiqueta de spot para mejorar la legibilidad. |
| Override Background: Auto | Botón de alternancia | Habilitado | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Cuando está habilitado, selecciona automáticamente un color de fondo para lograr contraste, en lugar de usar el color elegido manualmente. |
| Selector de color de fondo de spot | Botón de acción | `#000000` | `SpotsOverrideBgColor` | Abre un diálogo de color para elegir el color de fondo. Se utiliza solo cuando Override Background: Auto está deshabilitado. |
| Background Opacity: | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Establece la transparencia del fondo del spot. Rango: 0–100. |
| Clear All Spots | Botón de acción | — | — | Elimina todos los spots actuales del panadapter de inmediato. Esta acción no se puede deshacer. |

## Consejos

- El control deslizante Spot Lifetime es no lineal. Los movimientos pequeños en el extremo inferior del control ajustan la duración en segundos; los movimientos más amplios avanzan por minutos y luego por horas hasta 24 horas.
- Al habilitar Override Background: Auto mientras Override Background: Enabled está activado, AetherSDR elige automáticamente colores de fondo con contraste. Deshabilite Auto para aplicar el color elegido manualmente desde el selector de color de fondo de spot.
- Habilitar Memories: muestra los canales de memoria almacenados en su radio como superposiciones estilo spot, lo cual es útil para identificar rápidamente actividad en canales que ha guardado.

## Relacionado

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Aumentar o reducir el tamaño de la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
