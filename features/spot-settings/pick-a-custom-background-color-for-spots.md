# Elegir un color de fondo personalizado para los spots

Esta página explica cómo establecer un color de fondo específico para las etiquetas de spots en el panadapter. Utilice esta opción cuando desee colores de fondo consistentes y seleccionados manualmente, en lugar de la selección automática basada en contraste.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter.
- Confirme que `IsSpotsOverrideBackgroundColorsEnabled` esté activo: el botón "Override Background: Enabled" debe estar marcado. Si no lo está, el selector de color de fondo no tendrá efecto.
- Desactive la selección automática de color de fondo: el botón "Override Background: Auto" debe estar desmarcado. Mientras Auto esté activo, AetherSDR ignorará el color elegido manualmente.

## Pasos

1. Haga clic derecho sobre la capa de spots en el panadapter y abra Spot Settings.
2. Localice la fila **Override Background:**.
3. Si el botón "Enabled" aparece desmarcado, haga clic en él para que muestre "Enabled".
4. Si el botón "Auto" aparece marcado, haga clic en él para desmarcarlo. Esto desactiva la selección automática de color y habilita el selector de color manual.
5. Haga clic en el pequeño botón de muestra de color (el cuadrado a la derecha de "Auto") para abrir el selector de color.
6. Seleccione el color de fondo deseado en el diálogo de color y confirme. La muestra se actualiza de inmediato y el color se guarda en `SpotsOverrideBgColor`.

## Qué hace cada control

| Control | Valor predeterminado | Configuración persistida | Comportamiento |
|---|---|---|---|
| Override Background: Enabled | Habilitado | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo detrás del texto de las etiquetas de spots. Debe estar habilitado para que se aplique cualquier configuración de color de fondo. |
| Override Background: Auto | Habilitado | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Cuando está habilitado, AetherSDR elige un color de fondo automáticamente para garantizar contraste. Desactívelo para usar un color elegido manualmente. |
| Selector de color de fondo de spots | `#000000` | `SpotsOverrideBgColor` | Abre el diálogo del selector de color. El color seleccionado se usa como fondo del spot cuando Auto está desactivado. |
| Background Opacity: | 48 | `SpotsOverrideBgOpacity` | Controla la transparencia del fondo del spot, de 0 (completamente transparente) a 100 (completamente opaco). |

## Consejos

- Si cambia el color de fondo pero los spots siguen mostrando el color automático, verifique que "Override Background: Auto" esté desmarcado. Auto tiene prioridad sobre el color manual.
- El color de fondo y la opacidad son independientes. Después de elegir un color, ajuste el control deslizante **Background Opacity:** para controlar con qué intensidad se renderiza sobre el panadapter.

## Solución de problemas

- **El selector de color se abre pero los cambios no tienen efecto visible** — "Override Background: Auto" todavía está marcado. Desmárquelo para que se use el color manual en `SpotsOverrideBgColor`.
- **No aparece ningún fondo detrás del texto del spot** — "Override Background: Enabled" está desmarcado. Haga clic en él para que muestre "Enabled".
- **El fondo es invisible a pesar de tener el color correcto y el estado Enabled activo** — El control deslizante **Background Opacity:** puede estar en 0. Auméntelo por encima de 0.

## Relacionados

- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
