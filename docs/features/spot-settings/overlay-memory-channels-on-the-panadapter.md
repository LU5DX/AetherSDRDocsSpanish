# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en el radio pueden mostrarse como marcadores similares a spots directamente en el panadapter. Esto facilita identificar cuáles de sus frecuencias guardadas están dentro de la vista actual sin necesidad de cambiar a una lista de memoria separada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots del panadapter para acceder al menú contextual.

## Pasos

1. Haga clic derecho en el panadapter para abrir el menú contextual y seleccione la opción Spot Settings para abrir el diálogo **Spot Settings**.
2. Ubique la fila **Memories:**.
3. Haga clic en el botón de alternancia junto a **Memories:**. El botón cambia de **Disabled** a **Enabled** y los canales de memoria aparecen inmediatamente como superposiciones en el panadapter.

Para ocultar las superposiciones de memoria, haga clic en el botón de alternancia nuevamente hasta que muestre **Disabled**.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Spots:** | Botón de alternancia | Enabled | `IsSpotsEnabled` | Control maestro para todas las superposiciones de spots y memoria. Los canales de memoria no aparecerán si está en Disabled, independientemente del ajuste de Memories:. |
| **Memories:** | Botón de alternancia | Disabled | `IsMemoriesShownOnPanadapter` | Muestra u oculta los canales de memoria del radio como superposiciones en el panadapter. |
| **Levels:** | Control deslizante | 3 | `SpotsStackLevels` | Número de filas de apilamiento vertical que se usan cuando las superposiciones se agrupan. Rango: 1–10. |
| **Position:** | Control deslizante | 50 | `SpotsPosition` | Posición vertical de la banda de superposición en el panadapter, expresada como porcentaje de la altura del panel. Rango: 0–100. |
| **Font Size:** | Control deslizante | 16 | `SpotsFontSize` | Tamaño del texto de las etiquetas de superposición. Rango: 8–32. |
| **Spot Lifetime:** | Control deslizante | 30 min | `SpotsLifetime` | Tiempo durante el cual un marcador de spot permanece visible antes de desvanecerse. Escala no lineal: 10–55 sec, luego 5–55 min, luego 1–24 hr. |
| **Override Colors:** | Botón de alternancia | Disabled | `IsSpotsOverrideColorsEnabled` | Fuerza que todo el texto de las superposiciones use un único color en lugar de los colores asignados por la fuente. |
| Selector de color del texto de spots | Botón de acción | `#FFFF00` | `SpotsOverrideColor` | Abre un selector de color para elegir el color del texto de reemplazo. Activo solo cuando **Override Colors:** está en Enabled. |
| **Override Background: Enabled** | Botón de alternancia | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo relleno detrás de cada etiqueta de superposición. |
| **Override Background: Auto** | Botón de alternancia | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Selecciona automáticamente un color de fondo para garantizar contraste. Cuando está en Disabled, se utiliza el color de fondo elegido manualmente. |
| Selector de color de fondo de spots | Botón de acción | `#000000` | `SpotsOverrideBgColor` | Abre un selector de color para elegir el color de fondo. Activo cuando **Override Background: Auto** está en Disabled. |
| **Background Opacity:** | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Nivel alfa del fondo de las superposiciones. Rango: 0–100. |
| **Clear All Spots** | Botón de acción | — | — | Elimina todos los marcadores de spots actuales del panadapter. No afecta las superposiciones de memoria. |

## Consejos

- El control maestro **Spots:** debe estar en Enabled para que aparezcan las superposiciones de memoria. Si activa **Memories:** pero no ve nada, verifique que **Spots:** también esté en Enabled.
- Las superposiciones de memoria comparten los mismos ajustes de posición, tamaño de fuente y color que los spots de DX. Ajuste **Levels:** y **Position:** para evitar que se superpongan con la traza de su señal.
- Si las etiquetas de memoria son difíciles de leer sobre el fondo del panadapter, active **Override Colors:** y use el selector de color de texto para elegir un color de alto contraste.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Aumentar o reducir el tamaño de fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
