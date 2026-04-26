# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en su FLEX-8600 pueden mostrarse como superposiciones similares a spots directamente en el panadapter. Esto le permite ver las frecuencias guardadas en contexto mientras explora la banda.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para configurar este ajuste.
- Abra el diálogo **Spot Settings** haciendo clic derecho en el área de superposición de spots del panadapter para acceder al menú contextual.

## Pasos

1. Haga clic derecho en la superposición de spots del panadapter para abrir el menú contextual y, a continuación, seleccione la opción que abre **Spot Settings**.
2. Localice la fila **Memories:** en el diálogo.
3. Haga clic en el botón de alternancia junto a **Memories:**. Cambiará de **Disabled** a **Enabled**.
4. Cierre el diálogo. Los canales de memoria aparecerán ahora como superposiciones en el panadapter.

Para ocultar las superposiciones de memoria, haga clic nuevamente en el botón **Memories:** para que muestre **Disabled**.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Alternancia **Memories:** | Disabled | Activa o desactiva las superposiciones de canales de memoria en el panadapter. | `IsMemoriesShownOnPanadapter` |
| Alternancia **Spots:** | Enabled | Control maestro para la visualización de todos los spots y superposiciones de memoria. Si está en **Disabled**, las superposiciones de memoria no aparecerán independientemente del ajuste de **Memories:**. | `IsSpotsEnabled` |
| Control deslizante **Levels:** | 3 | Número de filas de apilamiento vertical utilizadas para las superposiciones. Rango: 1–10. | `SpotsStackLevels` |
| Control deslizante **Position:** | 50 | Posición vertical de las superposiciones en el panadapter. Rango: 0–100. | `SpotsPosition` |
| Control deslizante **Font Size:** | 16 | Tamaño del texto para las etiquetas de superposición. Rango: 8–32. | `SpotsFontSize` |
| Control deslizante **Spot Lifetime:** | 30 min | Tiempo que permanecen los spots antes de desvanecerse. Escala no lineal: 10–55 seg, luego 5–55 min, luego 1–24 hr. | `SpotsLifetime` |
| Alternancia **Override Colors:** | Disabled | Fuerza un único color de texto para todas las superposiciones. | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto del spot | #FFFF00 | Abre un selector de color para elegir el color de texto de sustitución. Activo solo cuando **Override Colors:** está en **Enabled**. | `SpotsOverrideColor` |
| Alternancia **Override Background: Enabled** | Enabled | Dibuja un fondo detrás del texto de las superposiciones. | `IsSpotsOverrideBackgroundColorsEnabled` |
| Alternancia **Override Background: Auto** | Enabled | Selecciona automáticamente un color de fondo para garantizar el contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | #000000 | Abre un selector de color para elegir el color de fondo de forma manual. | `SpotsOverrideBgColor` |
| Control deslizante **Background Opacity:** | 48 | Alfa (transparencia) del fondo de la superposición. Rango: 0–100. | `SpotsOverrideBgOpacity` |
| **Clear All Spots** | — | Elimina todos los spots actuales del panadapter de inmediato. No afecta los canales de memoria almacenados en la radio. | — |

## Consejos

- Las superposiciones de memoria comparten los mismos ajustes de posición, tamaño de fuente, apilamiento y color que los spots de DX. Ajuste **Levels:** y **Position:** para evitar superposiciones si tiene muchos canales de memoria en una banda.
- Si no aparecen superposiciones después de activar **Memories:**, confirme que **Spots:** también esté en **Enabled**. El botón **Spots:** es el interruptor maestro para toda la visualización de superposiciones.

## Resolución de problemas

- **Memories: está en Enabled pero no aparece nada en el panadapter** — Verifique que **Spots:** también esté en **Enabled**. Las superposiciones no se mostrarán si el control maestro **Spots:** está en **Disabled**.
- **Las superposiciones de memoria aparecen pero son ilegibles** — Aumente **Font Size:** o active **Override Background: Enabled** para que el texto tenga un fondo de contraste.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Acortar o alargar la vida útil de los spots](shorten-or-lengthen-spot-lifetime.md)
