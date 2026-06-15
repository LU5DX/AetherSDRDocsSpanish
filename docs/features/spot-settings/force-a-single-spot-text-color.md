# Diálogo de Configuración de Spots

El diálogo **Spot Settings** proporciona un control rápido e independiente sobre cómo se renderizan los spots de DX y las superposiciones de canales de memoria en el panadapter. Puede ajustar la visibilidad, densidad, posición vertical, tamaño de texto, duración, líneas de spots y anulaciones de color.

## Abrir el diálogo de Configuración de Spots

- Haga clic derecho en cualquier lugar de la superposición de spots en el panadapter.
- Seleccione **Spot Settings** en el menú contextual.

## Antes de comenzar

- El interruptor **Spots:** activa/desactiva toda la visualización de spots. Si muestra "Disabled", haga clic en él para habilitar los spots primero.

## Qué hacen los controles

| Control | Predeterminado | Rango | Clave persistida |
|---|---|---|---|
| **Spots:** | Habilitado | On/Off | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | On/Off | `IsMemorySpotsEnabled` |
| **Levels:** | 3 | 1–10 | `SpotsMaxLevel` |
| **Position:** | 50 | 0–100 (% desde arriba) | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8–32 puntos | `SpotFontSize` |
| **Spot Lifetime:** | 10 min | 10 seg – 24 hrs (pasos no lineales) | `DxClusterSpotLifetimeSec` |
| **Override Colors:** | Deshabilitado | On/Off | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto de spots | `#FFFF00` | (color) | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | On/Off | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | On/Off | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de spots | `#000000` | (color) | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0–100 (0 = transparente) | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | On/Off | `IsSpotsLinesEnabled` |
| **Clear All Spots** | – | – | (acción, sin clave) |

## Indicador

| Indicador | Significado |
|---|---|
| **Total Spots:** | Conteo en vivo de spots de DX actualmente rastreados en el panadapter. |

## Líneas de Spots

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Está habilitada por defecto.

Para ocultar las líneas de spots, haga clic en el interruptor para que muestre **Disabled**. Esto establece `IsSpotsLinesEnabled` en `False`. Deshabilitar las líneas de spots es útil durante concursos donde muchos spots muy cercanos crean desorden visual en el panadapter.

Para restaurar las líneas de spots, haga clic en el interruptor nuevamente para que muestre **Enabled**.

## Forzar un solo color de texto de spots

Anule los colores por spot asignados por su fuente de cluster DX y renderice todas las etiquetas de spots en un solo color elegido. Útil cuando los colores predeterminados chocan con su tema del panadapter o son difíciles de leer.

1. En el diálogo Spot Settings, localice la fila **Override Colors:**.
2. Haga clic en el botón interruptor para que muestre **Enabled**. Esto se persiste como `IsSpotsOverrideColorsEnabled`.
3. Haga clic en el botón de muestra de color inmediatamente a la derecha de **Enabled**. Se abre un selector de color.
4. Seleccione el color que desea para todas las etiquetas de texto de spots, luego haga clic en **OK**.
5. La muestra se actualiza para mostrar su color elegido. Todos los spots en el panadapter se renderizan inmediatamente en ese color. El valor elegido se persiste como `SpotsOverrideColor`.

Para revertir a los colores por spot, haga clic en el interruptor **Override Colors:** nuevamente para que muestre **Disabled**.

## Consejos

- El selector de color solo tiene efecto mientras **Override Colors:** muestre **Enabled**. Puede pre-seleccionar un color mientras el interruptor está en Disabled; se aplicará la próxima vez que habilite la anulación.
- Si el texto de los spots sigue siendo difícil de leer después de establecer el color, ajuste el contraste del fondo usando los controles **Override Background:** — consulte [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md) y [Adjust spot background opacity](adjust-spot-background-opacity.md).
- Durante concursos, deshabilitar **Spot Lines:** mientras mantiene los spots habilitados reduce el desorden sin perder las etiquetas de frecuencia.

## Relacionado

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md)
- [Adjust spot background opacity](adjust-spot-background-opacity.md)
