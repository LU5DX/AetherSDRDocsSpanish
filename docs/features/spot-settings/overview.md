# Descripción general de Spot Settings

El diálogo Spot Settings controla cómo aparecen los spots de DX y los canales de memoria en el panadapter — incluyendo si se muestran, qué tan densos y grandes son, cuánto tiempo persisten y cómo se colorean su texto y fondo. Ábralo desde el menú contextual del panadapter o desde la superposición Spots.

## Antes de comenzar

- No se requiere conexión a un equipo para cambiar estos ajustes.
- Los spots deben recibirse desde un clúster DX configurado u otra fuente mediante `Settings > SpotHub...` antes de que aparezca algún spot en el panadapter.

## Cómo funciona

Cuando los spots están habilitados, AetherSDR recibe datos de spots desde las fuentes conectadas (clúster DX, RBN, WSJTX y otras) y representa cada spot como un marcador etiquetado en el panadapter a la frecuencia correspondiente. El diálogo Spot Settings le da control sobre cada aspecto visual de esa representación.

El indicador **Total Spots:** en la parte superior del diálogo muestra un conteo en tiempo real de los spots que se están rastreando actualmente, independientemente de si la visualización está habilitada.

Los ajustes se guardan inmediatamente al cambiar un control. No se necesita botón Apply ni OK.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Clave persistida | Qué hace |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | `IsSpotsEnabled` | Activación/desactivación principal de la visualización de spots de DX en el panadapter. |
| Memories: | Botón de alternancia | Deshabilitado | `IsMemoriesShownOnPanadapter` | Muestra los canales de memoria del equipo como marcadores similares a spots en el panadapter. |
| Levels: | Control deslizante | 3 | `SpotsStackLevels` | Número de filas de apilamiento vertical que se usan cuando los spots se concentran en la misma área de frecuencia. Rango: 1–10. |
| Position: | Control deslizante | 50 | `SpotsPosition` | Posición vertical de la fila de spots en el panadapter, como porcentaje de arriba hacia abajo. Rango: 0–100. |
| Font Size: | Control deslizante | 16 | `SpotsFontSize` | Tamaño del texto para las etiquetas de spots. Rango: 8–32. |
| Spot Lifetime: | Control deslizante | 30 min | `SpotsLifetime` | Tiempo que un spot permanece en el panadapter antes de expirar. El control deslizante usa una escala no lineal: 10–55 segundos en pasos de 5 segundos, 5–55 minutos en pasos de 5 minutos, luego 1–24 horas en pasos de 1 hora. |
| Override Colors: | Botón de alternancia | Deshabilitado | `IsSpotsOverrideColorsEnabled` | Cuando está habilitado, fuerza todo el texto de los spots a un único color en lugar de los colores por fuente. |
| Selector de color de texto de spot | Botón | #FFFF00 | `SpotsOverrideColor` | Abre un selector de color para elegir el color de texto de reemplazo. Activo solo cuando Override Colors: está habilitado. |
| Override Background: Enabled | Botón de alternancia | Habilitado | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo relleno detrás de cada etiqueta de spot para facilitar la lectura. |
| Override Background: Auto | Botón de alternancia | Habilitado | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Cuando está habilitado, selecciona automáticamente un color de fondo que contraste con el texto del spot. Cuando está deshabilitado, usa el color de fondo elegido manualmente. |
| Selector de color de fondo de spot | Botón | #000000 | `SpotsOverrideBgColor` | Abre un selector de color para elegir un color de fondo fijo. Se usa cuando Override Background: Auto está deshabilitado. |
| Background Opacity: | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Transparencia alfa del fondo del spot. Rango: 0 (completamente transparente) a 100 (completamente opaco). |
| Clear All Spots | Botón | — | — | Elimina inmediatamente todos los spots del panadapter. No afecta a las fuentes de spots entrantes. |

## Consejos

- Establezca Override Background: Auto en habilitado cuando tenga muchas fuentes de spots con diferentes colores — la selección automática de contraste mantiene las etiquetas legibles independientemente del color del espectro subyacente.
- Si los spots de diferentes fuentes se apilan unos sobre otros, aumente Levels: para distribuirlos en más filas.
- El control deslizante Spot Lifetime: se ajusta a intervalos definidos (por ejemplo, "10 sec", "5 mins", "1 hr"). La etiqueta de visualización se actualiza mientras arrastra.
- Cambiar Spots: a deshabilitado detiene la representación en el panadapter, pero no desconecta las fuentes del clúster DX; el conteo Total Spots: continúa incrementándose.

## Solución de problemas

- **No aparecen spots aunque Spots: muestra Enabled** — Verifique que al menos una fuente de spots esté configurada y conectada en `Settings > SpotHub...`. El conteo Total Spots: mostrará 0 si no llegan datos.
- **Las etiquetas de spots son ilegibles sobre el fondo del panadapter** — Habilite Override Background: Enabled y Override Background: Auto, o reduzca el control deslizante Background Opacity: para disminuir la densidad del fondo.
- **Todos los spots desaparecen poco después de aparecer** — Es posible que Spot Lifetime: esté configurado en un valor muy bajo. Abra Spot Settings y arrastre el control deslizante Spot Lifetime: a un valor mayor, como 30 mins.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Borrar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
