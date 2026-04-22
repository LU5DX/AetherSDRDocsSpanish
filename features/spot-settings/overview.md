# Descripción general de Spot Settings

El diálogo Spot Settings controla cómo aparecen los spots DX y los canales de memoria en el panadapter — incluyendo si se muestran o no, cuántas filas ocupan, dónde se ubican verticalmente, cuánto tiempo persisten y qué colores usan. Ábralo desde el menú contextual del panadapter o desde la superposición de spots; no requiere una conexión de radio activa.

## Cómo funciona

AetherSDR dibuja los spots DX como marcadores etiquetados directamente sobre la pantalla del panadapter. Cada spot se coloca en su frecuencia detectada y se apila verticalmente cuando varios spots coinciden en frecuencias cercanas. El diálogo agrupa sus controles en cuatro áreas: activación de visibilidad, diseño, duración y color.

**Visibilidad** — El interruptor principal `IsSpotsEnabled` debe estar activado para que aparezca cualquier spot. El interruptor `IsMemoriesShownOnPanadapter` controla de forma independiente si los canales de memoria del radio se muestran en la misma superposición.

**Diseño** — `SpotsStackLevels` establece cuántas filas verticales están disponibles cuando varios spots se agrupan en la misma frecuencia. `SpotsPosition` fija la altura base como porcentaje desde la parte inferior del panadapter. `SpotsFontSize` controla el tamaño del texto de las etiquetas de los spots.

**Duración** — `SpotsLifetime` determina cuánto tiempo permanece visible un spot antes de desvanecerse. El control deslizante usa una escala no lineal: avanza en pasos por segundos (10–55 s), luego por minutos (5–55 min) y luego por horas (1–24 hr), mostrando una etiqueta con formato como "15 mins" o "2 hrs".

**Color** — De forma predeterminada, los spots se dibujan con los colores asignados por la fuente del spot. `IsSpotsOverrideColorsEnabled` reemplaza todo el texto de los spots con un único color elegido (`SpotsOverrideColor`, predeterminado `#FFFF00`). El fondo se controla mediante `IsSpotsOverrideBackgroundColorsEnabled` (predeterminado activado), con `IsSpotsOverrideToAutoBackgroundColorEnabled` (predeterminado activado) seleccionando automáticamente un color de contraste. Cuando el modo automático está desactivado, se usa `SpotsOverrideBgColor` (predeterminado `#000000`). `SpotsOverrideBgOpacity` establece la transparencia del fondo en una escala de 0 a 100 (predeterminado 48).

El indicador **Total Spots:** en la parte inferior del diálogo muestra cuántos spots se están rastreando actualmente.

## Qué hace cada control

| Etiqueta | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | `IsSpotsEnabled` | Activación/desactivación principal de la superposición de spots DX. |
| Memories: | Botón de alternancia | Deshabilitado | `IsMemoriesShownOnPanadapter` | Muestra los canales de memoria del radio como marcadores similares a spots en el panadapter. |
| Levels: | Control deslizante | 3 | `SpotsStackLevels` | Número de filas de apilamiento vertical; rango 1–10. |
| Position: | Control deslizante | 50 | `SpotsPosition` | Altura base de la fila de spots como porcentaje (0–100) desde la parte inferior. |
| Font Size: | Control deslizante | 16 | `SpotsFontSize` | Tamaño del texto de la etiqueta del spot en puntos; rango 8–32. |
| Spot Lifetime: | Control deslizante | 30 min | `SpotsLifetime` | Tiempo que se muestra un spot; escala no lineal de 10 s a 24 hr. |
| Override Colors: | Botón de alternancia | Deshabilitado | `IsSpotsOverrideColorsEnabled` | Fuerza todo el texto de los spots a un único color en lugar de los colores asignados por la fuente. |
| Selector de color de texto del spot | Botón | `#FFFF00` | `SpotsOverrideColor` | Abre un selector de color para elegir el color de texto alternativo. Activo solo cuando Override Colors está habilitado. |
| Override Background: Enabled | Botón de alternancia | Habilitado | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo relleno detrás de cada etiqueta de spot. |
| Override Background: Auto | Botón de alternancia | Habilitado | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Selecciona automáticamente un color de fondo que contraste con el texto. Cuando está desactivado, utiliza el color de fondo elegido manualmente. |
| Selector de color de fondo del spot | Botón | `#000000` | `SpotsOverrideBgColor` | Abre un selector de color para elegir el color de fondo. Se usa cuando Auto está desactivado. |
| Background Opacity: | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Transparencia del fondo del spot; rango 0–100. |
| Clear All Spots | Botón | — | — | Elimina inmediatamente todos los spots del panadapter. Esta acción no se puede deshacer. |

## Consejos

- Si los spots de distintas fuentes usan colores que contrastan con el tema de su panadapter, active Override Colors y elija un único color legible en lugar de ajustar cada fuente individualmente.
- Active Override Background: Auto cada vez que cambie el color alternativo del texto; AetherSDR seleccionará automáticamente un fondo con contraste adecuado.
- El control deslizante Spot Lifetime se desplaza en pasos definidos. No es posible ingresar segundos de forma arbitraria; elija el paso más cercano disponible.
- Reducir Levels a 1 hace que la superposición sea más compacta, pero provoca que los spots en frecuencias cercanas se superpongan en lugar de apilarse.

## Relacionado

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
