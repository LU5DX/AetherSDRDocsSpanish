# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en su radio pueden mostrarse como etiquetas similares a spots directamente en el panadapter. Esto le permite ver de un vistazo qué frecuencias de memoria se encuentran dentro de su vista actual.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un radio para cambiar estos ajustes.
- Abra el diálogo Spot Settings haciendo clic derecho en el panadapter y seleccionando la opción de superposición Spots en el menú contextual.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual y luego abra el diálogo Spot Settings.
2. Localice la fila **Memories:**.
3. Haga clic en el botón de alternancia junto a **Memories:** hasta que muestre **Enabled**. El estado predeterminado es **Disabled**.
4. Las etiquetas de canales de memoria aparecerán en el panadapter de inmediato. Cierre el diálogo cuando termine.

Para ocultar las superposiciones de memoria nuevamente, haga clic en el botón **Memories:** hasta que muestre **Disabled**.

## Qué hace cada control

| Etiqueta | Tipo | Predeterminado | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| Spots: | Botón de alternancia | Enabled | `IsSpotsEnabled` | Control maestro para todas las superposiciones de spots y memoria. Las memorias no aparecerán si este está en Disabled. |
| Memories: | Botón de alternancia | Disabled | `IsMemoriesShownOnPanadapter` | Muestra los canales de memoria del radio como etiquetas en el panadapter. |
| Levels: | Control deslizante | 3 | `SpotsStackLevels` | Número de filas de apilamiento vertical que se usan cuando las etiquetas se superponen. Rango: 1–10. |
| Position: | Control deslizante | 50 | `SpotsPosition` | Posición vertical de las etiquetas en el panadapter. Rango: 0–100. |
| Font Size: | Control deslizante | 16 | `SpotsFontSize` | Tamaño de texto de las etiquetas. Rango: 8–32. |
| Spot Lifetime: | Control deslizante | 30 min | `SpotsLifetime` | Tiempo que los spots permanecen visibles antes de desvanecerse. Escala no lineal de 10 segundos a 24 horas. |
| Override Colors: | Botón de alternancia | Disabled | `IsSpotsOverrideColorsEnabled` | Obliga a que todas las etiquetas de spots y memoria usen un único color de texto. |
| Selector de color de texto de spot | Botón | `#FFFF00` | `SpotsOverrideColor` | Abre un selector de color para elegir el color de texto de la superposición. |
| Override Background: Enabled | Botón de alternancia | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un relleno de fondo detrás del texto de las etiquetas. |
| Override Background: Auto | Botón de alternancia | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Selecciona automáticamente un color de fondo para mejorar el contraste de legibilidad. |
| Selector de color de fondo de spot | Botón | `#000000` | `SpotsOverrideBgColor` | Abre un selector de color para elegir el color de fondo cuando Auto está en Disabled. |
| Background Opacity: | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Nivel de transparencia del fondo de las etiquetas. Rango: 0–100. |
| Clear All Spots | Botón | — | — | Elimina todos los spots actuales del panadapter. No afecta las memorias. |

## Consejos

- Las etiquetas de memoria comparten los mismos ajustes de posición, tamaño de fuente, apilamiento y color que los spots de DX. Ajuste esos controles para cambiar la apariencia de ambos.
- Si no aparecen etiquetas de memoria después de habilitar **Memories:**, confirme que el botón **Spots:** también esté en **Enabled**. El control maestro **Spots:** controla ambos.
- El modo **Override Background: Auto** está habilitado de forma predeterminada y selecciona automáticamente un fondo con contraste adecuado. Desactívelo para usar el selector de color de fondo manual en su lugar.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Cambiar la densidad de spots y la posición vertical](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
