# Descripción general de Spot Settings

El diálogo Spot Settings controla cómo aparecen los spots de DX y los canales de memoria en el panadapter — incluyendo si se muestran, cuántas filas ocupan, dónde se ubican verticalmente, cuánto tiempo persisten y cómo se colorean su texto y fondos.

## Antes de comenzar

- Debe haber un panadapter abierto. No se puede acceder al diálogo Spot Settings desde el menú principal.
- Para recibir spots de DX en tiempo real, configure al menos una fuente de spots mediante `Settings > SpotHub...`.

## Cómo funciona

Abra el diálogo haciendo clic derecho sobre la capa de spots en el panadapter y seleccionando la opción de configuración de spots en el menú contextual. El diálogo se titula "Spot Settings" y no requiere conexión con la radio para operar — todos los cambios se guardan inmediatamente en la configuración persistente.

Un indicador **Total Spots:** en la parte superior del diálogo muestra la cantidad de spots activos que se están rastreando en ese momento.

Los controles se dividen en cuatro áreas:

**Visibilidad y densidad** — si los spots y las memorias se dibujan, cuántas filas de apilamiento se usan y dónde se ubican en el panadapter.

**Apariencia** — tamaño de fuente y tiempo que permanece visible cada spot antes de desvanecerse.

**Color de texto** — una anulación opcional que fuerza a todos los spots a usar un único color en lugar del color asignado por la fuente.

**Fondo** — un fondo configurable que se dibuja detrás del texto de los spots, con modo de contraste automático, selección manual de color y control de opacidad.

Al hacer clic en `Clear All Spots` se eliminan todos los spots del panadapter de inmediato. Esta acción no es persistente; los spots reaparecerán a medida que lleguen nuevos desde las fuentes configuradas.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | `IsSpotsEnabled` | Interruptor principal para la visualización de spots de DX. |
| Memories: | Botón de alternancia | Deshabilitado | `IsMemoriesShownOnPanadapter` | Muestra los canales de memoria de la radio como marcadores similares a spots en el panadapter. |
| Levels: | Control deslizante | 3 | `SpotsStackLevels` | Establece el número de filas de apilamiento vertical para los spots (rango: 1–10). |
| Position: | Control deslizante | 50 | `SpotsPosition` | Establece la posición vertical de la banda de spots en el panadapter como porcentaje desde la parte superior (rango: 0–100). |
| Font Size: | Control deslizante | 16 | `SpotsFontSize` | Establece el tamaño del texto de la etiqueta del spot en puntos (rango: 8–32). |
| Spot Lifetime: | Control deslizante | 30 min | `SpotsLifetime` | Establece cuánto tiempo permanece visible un spot antes de desvanecerse. El control deslizante usa una escala no lineal: 10–55 segundos en pasos de 5 segundos, luego 5–55 minutos en pasos de 5 minutos, luego 1–24 horas en pasos de 1 hora. |
| Override Colors: | Botón de alternancia | Deshabilitado | `IsSpotsOverrideColorsEnabled` | Cuando está habilitado, todo el texto de los spots se dibuja con el color seleccionado en el selector de color de texto de spots, en lugar del color asignado por la fuente de cada spot. |
| Selector de color de texto de spots | Botón de color | `#FFFF00` | `SpotsOverrideColor` | Abre un selector de color para el color de texto de anulación. Activo solo cuando Override Colors: está habilitado. |
| Override Background: Enabled | Botón de alternancia | Habilitado | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo relleno detrás de cada etiqueta de spot. |
| Override Background: Auto | Botón de alternancia | Habilitado | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Cuando está habilitado, AetherSDR selecciona el color de fondo automáticamente para mejorar el contraste. Cuando está deshabilitado, se usa el color de fondo elegido manualmente. |
| Selector de color de fondo de spots | Botón de color | `#000000` | `SpotsOverrideBgColor` | Abre un selector de color para el color de fondo manual. Se usa cuando Override Background: Auto está deshabilitado. |
| Background Opacity: | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Establece la transparencia del fondo de los spots (rango: 0–100, donde 0 es completamente transparente y 100 es completamente opaco). |
| Clear All Spots | Botón | — | — | Elimina todos los spots del panadapter de inmediato. No es persistente. |

## Consejos

- Si los spots son difíciles de leer sobre un panadapter con mucha actividad, habilite Override Background: Enabled y aumente Background Opacity: para mejorar el contraste sin cambiar los colores de los spots.
- El control deslizante Spot Lifetime: se ajusta a pasos predefinidos. El valor actual se muestra como una etiqueta con formato (por ejemplo, "30 mins" o "2 hrs") junto al control deslizante.
- Levels: y Position: interactúan entre sí: aumentar Levels: expande la banda de spots hacia abajo desde el punto de anclaje de Position:. Ajuste primero Position: y luego regule Levels:.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Ampliar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
