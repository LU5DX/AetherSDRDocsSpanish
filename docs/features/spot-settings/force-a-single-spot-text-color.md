# Diálogo de Configuración de Spots

El diálogo **Configuración de Spots** proporciona control rápido e independiente sobre cómo se renderizan los spots de DX y las superposiciones de canales de memoria en el panadapter. Puede ajustar la visibilidad, densidad, posición vertical, tamaño de texto, vida útil, líneas de spots y anulación de colores.

## Abrir el diálogo de Configuración de Spots

- Haga clic derecho en cualquier lugar de la superposición de spots en el panadapter.
- Seleccione **Configuración de Spots** en el menú contextual.

## Antes de comenzar

- El conmutador **Spots:** activa o desactiva toda la visualización de spots. Si muestra "Deshabilitado", haga clic en él para habilitar los spots primero.

## Qué hacen los controles

| Control | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|
| **Spots:** | Habilitado | On/Off | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | On/Off | `IsMemorySpotsEnabled` |
| **Levels:** | 3 | 1–10 | `SpotsMaxLevel` |
| **Position:** | 50 | 0–100 (% desde arriba) | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8–32 puntos | `SpotFontSize` |
| **Spot Lifetime:** | 10 min | 10 s – 24 h (pasos no lineales) | `DxClusterSpotLifetimeSec` |
| **Override Colors:** | Deshabilitado | On/Off | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto de spot | `#FFFF00` | (color) | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | On/Off | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | On/Off | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de spot | `#000000` | (color) | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0–100 (0 = transparente) | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | On/Off | `IsSpotsLinesEnabled` |
| **Clear All Spots** | – | – | (acción, sin clave) |

## Indicador

| Indicador | Significado |
|---|---|
| **Total Spots:** | Conteo en vivo de los spots de DX actualmente rastreados en el panadapter. |

## Estado de visualización de los botones de alternancia

Cada botón de alternancia en el diálogo de Configuración de Spots actualiza su etiqueta para reflejar el estado habilitado o deshabilitado actual. Cuando una alternancia está habilitada, el botón muestra **Enabled**; cuando está deshabilitada, muestra **Disabled**. Esto se aplica a los siguientes controles:

- **Spots:**
- **Memories:**
- **Override Colors:**
- **Override Background: Enabled**
- **Spot Lines:**

## Líneas de Spots

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Está habilitado por defecto.

Para ocultar las líneas de spots, haga clic en la alternancia para que muestre **Disabled**. Esto establece `IsSpotsLinesEnabled` en `False`. Deshabilitar las líneas de spots es útil durante concursos donde muchos spots muy espaciados crean desorden visual en el panadapter.

Para restaurar las líneas de spots, haga clic nuevamente en la alternancia para que muestre **Enabled**.

## Forzar un único color de texto para spots

Anule los colores por spot asignados por su fuente de cluster de DX y renderice todas las etiquetas de spots en un solo color elegido. Útil cuando los colores predeterminados chocan con su tema del panadapter o son difíciles de leer.

1. En el diálogo de Configuración de Spots, localice la fila **Override Colors:**.
2. Haga clic en el botón de alternancia para que muestre **Enabled**. Esto se persiste como `IsSpotsOverrideColorsEnabled`.
3. Haga clic en el botón de muestra de color inmediatamente a la derecha de **Enabled**. Se abre un diálogo selector de color.
4. Seleccione el color deseado para todas las etiquetas de texto de spots, luego haga clic en **OK**.
5. La muestra se actualiza para mostrar su color elegido. Todos los spots en el panadapter se renderizan inmediatamente en ese color. El valor elegido se persiste como `SpotsOverrideColor`.

Para revertir a colores por spot, haga clic nuevamente en la alternancia **Override Colors:** para que muestre **Disabled**.

## Consejos

- El selector de color solo tiene efecto mientras **Override Colors:** muestre **Enabled**. Puede preseleccionar un color mientras la alternancia está aún en Disabled; se aplicará la próxima vez que habilite la anulación.
- Si el texto de los spots sigue siendo difícil de leer después de configurar el color, ajuste el contraste del fondo usando los controles **Override Background:** — consulte [Elegir un color de fondo personalizado para spots](pick-a-custom-background-color-for-spots.md) y [Ajustar la opacidad del fondo de spots](adjust-spot-background-opacity.md).
- Durante concursos, deshabilitar **Spot Lines:** mientras mantiene los spots habilitados reduce el desorden sin perder las etiquetas de frecuencia.

## Relacionado

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Elegir un color de fondo personalizado para spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de spots](adjust-spot-background-opacity.md)
