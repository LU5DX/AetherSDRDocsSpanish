# Activar o desactivar los spots

Los spots de DX provenientes de fuentes de cluster aparecen como superposiciones en el panadapter. Esta página explica cómo habilitar o deshabilitar esa visualización mediante el interruptor principal de spots en el diálogo **Spot Settings**.

## Antes de comenzar

- El panadapter debe estar visible en la ventana principal.
- Las fuentes de spots (cluster de DX, RBN, etc.) deben configurarse en `Settings > SpotHub...` si desea que los spots en vivo aparezcan una vez que habilite la superposición.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el diálogo **Spot Settings**.
3. Localice el botón de alternancia **Spots:** en la parte superior del diálogo.
4. Haga clic en el botón para alternar entre **Enabled** y **Disabled**.
   - Cuando está en **Enabled**, los spots de DX se dibujan sobre el panadapter.
   - Cuando está en **Disabled**, no se dibuja ningún spot. La configuración se guarda de inmediato; no se requiere confirmación adicional.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Spots:** | Botón de alternancia | Enabled | `IsSpotsEnabled` | Interruptor principal de activación/desactivación de la visualización de spots de DX en el panadapter. |
| **Memories:** | Botón de alternancia | Disabled | `IsMemoriesShownOnPanadapter` | Muestra los canales de memoria de la radio como marcadores similares a spots en el panadapter. |
| **Levels:** | Control deslizante | 3 | `SpotsStackLevels` | Número de filas de apilamiento vertical cuando los spots se superponen. Rango: 1–10. |
| **Position:** | Control deslizante | 50 | `SpotsPosition` | Posición vertical de la banda de spots en el panadapter. Rango: 0–100. |
| **Font Size:** | Control deslizante | 16 | `SpotsFontSize` | Tamaño del texto para las etiquetas de spots. Rango: 8–32. |
| **Spot Lifetime:** | Control deslizante | 30 min | `SpotsLifetime` | Tiempo que un spot permanece visible antes de expirar. Los pasos van desde 10 segundos hasta 24 horas. |
| **Override Colors:** | Botón de alternancia | Disabled | `IsSpotsOverrideColorsEnabled` | Fuerza que todo el texto de los spots use un único color seleccionado, en lugar de los colores asignados por la fuente. |
| Selector de color del texto de spots | Botón | `#FFFF00` | `SpotsOverrideColor` | Abre un selector de color para elegir el color de texto de sustitución. Activo solo cuando **Override Colors:** está en **Enabled**. |
| **Override Background: Enabled** | Botón de alternancia | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo relleno detrás de cada etiqueta de spot. |
| **Override Background: Auto** | Botón de alternancia | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Selecciona automáticamente un color de fondo para lograr contraste, en lugar de usar el color elegido manualmente. |
| Selector de color de fondo de spots | Botón | `#000000` | `SpotsOverrideBgColor` | Abre un selector de color para el fondo manual. Se usa cuando **Override Background: Auto** está en **Disabled**. |
| **Background Opacity:** | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Nivel alfa del fondo de los spots. Rango: 0–100. |
| **Clear All Spots** | Botón | — | — | Elimina inmediatamente todos los spots del panadapter. No afecta el estado de activación/desactivación. |

El indicador **Total Spots:** en la parte inferior del diálogo muestra cuántos spots en vivo se están rastreando actualmente.

## Consejos

- Cambiar **Spots:** a **Disabled** no elimina los spots almacenados en el búfer. Al volver a habilitarlo, los spots que aún no hayan expirado reaparecerán.
- El control deslizante **Spot Lifetime:** utiliza una escala no lineal: pasos finos en segundos en el extremo inferior, luego minutos y finalmente horas hasta 24 horas.

## Temas relacionados

- [Descripción general de Spot Settings](overview.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad de spots y la posición vertical](change-spot-density-and-vertical-position.md)
- [Ampliar o reducir el tamaño de la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
