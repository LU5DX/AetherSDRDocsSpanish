# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en su FLEX-8600 pueden mostrarse como marcadores similares a spots en el panadapter, lo que facilita ver las frecuencias guardadas en contexto con las señales en vivo. Esta página explica cómo activar esa superposición y ajustarla junto con otras configuraciones de spots.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar estas configuraciones.
- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en el panadapter y seleccionando la opción Spots overlay en el menú contextual.

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual y luego abra el cuadro de diálogo Spot Settings.
2. Localice la fila **Memories:**.
3. Haga clic en el botón de alternancia junto a **Memories:**. Por defecto muestra "Disabled". Haga clic una vez para cambiarlo a "Enabled".
4. Los canales de memoria aparecen ahora como superposiciones en el panadapter. Haga clic en el alternador nuevamente para volver a "Disabled" si desea ocultarlos.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Alternador **Spots:** | Activa o desactiva globalmente todas las superposiciones de spots y memoria. Las memorias no aparecerán si está desactivado. | Enabled | `IsSpotsEnabled` |
| Alternador **Memories:** | Muestra u oculta los marcadores de canales de memoria en el panadapter. | Disabled | `IsMemoriesShownOnPanadapter` |
| Control deslizante **Levels:** | Número de filas de apilamiento vertical que se usan cuando los spots o memorias se superponen. Rango: 1–10. | 3 | `SpotsStackLevels` |
| Control deslizante **Position:** | Posición vertical de la banda de superposición en el panadapter, como porcentaje desde la parte superior. Rango: 0–100. | 50 | `SpotsPosition` |
| Control deslizante **Font Size:** | Tamaño del texto para las etiquetas de spots y memorias. Rango: 8–32. | 16 | `SpotsFontSize` |
| Control deslizante **Spot Lifetime:** | Cuánto tiempo permanecen los spots antes de desvanecerse. Escala no lineal: 10–55 segundos, luego 5–55 minutos, luego 1–24 horas. | 30 min | `SpotsLifetime` |
| Alternador **Override Colors:** | Fuerza un único color de texto para todos los spots y memorias en lugar de los colores asignados por la fuente. | Disabled | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto del spot | Abre un selector de color para elegir el color de texto de sustitución. Predeterminado: `#FFFF00`. | `#FFFF00` | `SpotsOverrideColor` |
| Alternador **Override Background: Enabled** | Dibuja un fondo de color detrás del texto de spots y memorias. | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| Alternador **Override Background: Auto** | Selecciona automáticamente un color de fondo para mayor contraste en lugar de usar el color manual. | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | Abre un selector de color para el color de fondo manual. Predeterminado: `#000000`. | `#000000` | `SpotsOverrideBgColor` |
| Control deslizante **Background Opacity:** | Establece la transparencia del fondo del spot. Rango: 0–100. | 48 | `SpotsOverrideBgOpacity` |
| **Clear All Spots** | Elimina todos los spots del panadapter de inmediato. No afecta a las memorias. | — | — |

## Consejos

- Las superposiciones de memoria comparten las mismas configuraciones de posición, fuente, apilamiento y color que los spots de DX. Ajuste **Levels:** y **Position:** para evitar que los marcadores de memoria oculten los picos de señal.
- Si los marcadores de memoria no son visibles después de activar **Memories:**, confirme que el alternador **Spots:** también esté configurado en "Enabled". El alternador maestro de Spots controla el renderizado de todas las superposiciones.
- El alternador **Override Background: Auto** está activo de forma predeterminada y selecciona automáticamente colores de fondo con contraste adecuado. Desactívelo solo si desea establecer un color de fondo específico con el selector de color de fondo.

## Solución de problemas

- **Memories: muestra "Enabled" pero no aparecen marcadores en el panadapter** — Verifique que el alternador **Spots:** esté configurado en "Enabled". El alternador maestro de spots debe estar activado para que cualquier superposición, incluidas las memorias, se muestre.
- **Los marcadores de memoria se superponen y son difíciles de leer** — Aumente el valor del control deslizante **Levels:** para dar al renderizador más filas de apilamiento, o ajuste **Position:** para mover la superposición a un área menos congestionada del panadapter.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Cambiar la densidad de spots y la posición vertical](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
