# Seleccionar un color de fondo personalizado para los spots

Esta página explica cómo establecer un color de fondo específico para las etiquetas de spots de DX en el panadapter. Úsela cuando desee un color fijo en lugar del color automático basado en contraste que AetherSDR selecciona por defecto.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter.
- Confirme que `IsSpotsOverrideBackgroundColorsEnabled` está activo — el botón "Override Background: Enabled" debe estar activado; de lo contrario, el color de fondo no tendrá efecto.

## Pasos

1. En el diálogo Spot Settings, localice la fila **Override Background:**.
2. Haga clic en el botón **Enabled** para que muestre "Enabled". Esto activa el fondo de los spots y conserva `IsSpotsOverrideBackgroundColorsEnabled`.
3. Haga clic en el botón **Auto** para que muestre "Disabled". Mientras Auto está activado, AetherSDR ignora su color personalizado y elige uno automáticamente por contraste. Desactivarlo permite que el color elegido tenga efecto. Esto conserva `IsSpotsOverrideToAutoBackgroundColorEnabled`.
4. Haga clic en el pequeño botón de muestra de color a la derecha de **Auto**. Se abre el selector de color del sistema.
5. Elija el color deseado y confirme. AetherSDR aplica el color de inmediato y lo guarda como `SpotsOverrideBgColor`.
6. Ajuste el control deslizante **Background Opacity:** si desea que el fondo sea más o menos transparente. El valor predeterminado es 48. Esto conserva `SpotsOverrideBgOpacity`.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botón **Override Background: Enabled** | Dibuja un fondo de color detrás del texto de los spots. | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| Botón **Override Background: Auto** | Cuando está activado, AetherSDR elige automáticamente un color de fondo por contraste. Desactívelo para usar su color personalizado. | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de spots (botón de muestra) | Abre el diálogo del selector de color para establecer un color de fondo fijo. | `#000000` | `SpotsOverrideBgColor` |
| Control deslizante **Background Opacity:** | Establece la transparencia del fondo de los spots. Rango: 0–100. | 48 | `SpotsOverrideBgOpacity` |

## Consejos

- Si el color elegido no aparece después de seleccionarlo, verifique que **Override Background: Auto** esté en "Disabled". El modo Auto anula la selección manual de color.
- Un valor de opacidad bajo (más cercano a 0) hace que el fondo sea casi transparente. Si el texto de los spots se vuelve difícil de leer, aumente el valor del control deslizante **Background Opacity:**.

## Solución de problemas

- **El color personalizado se ignora y el color de fondo sigue cambiando** — El botón **Override Background: Auto** sigue en "Enabled". Haga clic en él para desactivar el modo Auto; entonces se usará el color de `SpotsOverrideBgColor`.
- **El fondo no aparece en absoluto** — El botón **Override Background: Enabled** está en "Disabled". Haga clic en él para activarlo.
- **El fondo aparece pero es invisible** — El control deslizante **Background Opacity:** puede estar en 0. Auméntelo.

## Relacionado

- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
