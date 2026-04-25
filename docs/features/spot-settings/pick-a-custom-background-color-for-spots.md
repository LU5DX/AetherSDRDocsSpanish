# Elegir un color de fondo personalizado para los spots

Esta página explica cómo establecer un color de fondo específico que aparece detrás de las etiquetas de spots en el panadapter, en lugar de dejar que AetherSDR elija el color automáticamente.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho en el panadapter y seleccionándolo desde el menú contextual de la superposición de spots.
- Confirme que el interruptor `IsSpotsOverrideBackgroundColorsEnabled` está activo — el selector de color de fondo no tiene efecto si la anulación de fondo está desactivada.

## Pasos

1. En el diálogo Spot Settings, localice la fila **Override Background:**.
2. Confirme que el botón de interruptor **Enabled** muestra **Enabled**. Si muestra **Disabled**, haga clic en él para habilitar las anulaciones de fondo. Esto controla `IsSpotsOverrideBackgroundColorsEnabled`.
3. Haga clic en el botón de interruptor **Auto** para que muestre **Disabled**. Mientras **Auto** está habilitado, AetherSDR elige el color de fondo automáticamente e ignora su color personalizado. Deshabilitarlo establece `IsSpotsOverrideToAutoBackgroundColorEnabled` = False.
4. Haga clic en el pequeño botón de muestra de color a la derecha de **Auto**. Este es el selector de color de fondo de spots y abre un diálogo de selección de color.
5. Seleccione el color deseado en el diálogo de color y confirme la selección.
6. La muestra se actualiza para mostrar el color elegido. El valor se guarda inmediatamente en `SpotsOverrideBgColor`.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Interruptor **Override Background: Enabled** | Dibuja un fondo detrás del texto de los spots. Cuando está en **Disabled**, no se dibuja ningún fondo y todos los controles de fondo quedan inactivos. | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| Interruptor **Override Background: Auto** | Cuando está en **Enabled**, AetherSDR selecciona automáticamente un color de fondo contrastante e ignora el selector de color personalizado. Establézcalo en **Disabled** para usar el color elegido. | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de spots | Abre un diálogo de color para elegir el color de fondo personalizado. Activo solo cuando **Auto** está en **Disabled**. | `#000000` | `SpotsOverrideBgColor` |
| Control deslizante **Background Opacity:** | Controla la transparencia del fondo de los spots. Rango 0–100; predeterminado 48. | 48 | `SpotsOverrideBgOpacity` |

## Consejos

- El color personalizado establecido aquí solo tiene efecto cuando **Enabled** está activo y **Auto** está en **Disabled**. Si los spots siguen mostrando colores de fondo automáticos después de elegir un color, verifique que **Auto** indique **Disabled**.
- Para ajustar la visibilidad del fondo sin cambiar el color, ajuste el control deslizante **Background Opacity:** después de establecer su color. Consulte [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md).

## Solución de problemas

- **El color de fondo no cambia después de seleccionar un nuevo color** — Verifique que **Override Background:** muestre **Enabled** y que el interruptor **Auto** muestre **Disabled**. Si **Auto** está en **Enabled**, el color personalizado se ignora.
- **No aparece ningún fondo** — El interruptor **Enabled** bajo **Override Background:** está en **Disabled**. Haga clic en él para que indique **Enabled**.

## Relacionados

- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
