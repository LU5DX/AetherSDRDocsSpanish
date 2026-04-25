# Ajustar la opacidad del fondo de los spots

Use esta página para controlar qué tan transparente u opaco aparece el relleno de fondo detrás de las etiquetas de spots en el panadapter. Un valor más bajo hace que el fondo sea casi invisible; un valor más alto lo hace sólido y más fácil de leer sobre una visualización de espectro concurrida.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots del panadapter y seleccionándolo en el menú contextual.
- Confirme que "Override Background:" esté configurado en **Enabled**. El control deslizante de opacidad no tiene efecto visible si el fondo está desactivado.

## Pasos

1. En el diálogo Spot Settings, localice la fila **Override Background:** y confirme que el botón **Enabled** muestre "Enabled". Si muestra "Disabled", haga clic en él para activarlo.
2. Localice el control deslizante **Background Opacity:**.
3. Arrastre el control hacia la izquierda para disminuir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaco).
4. El valor numérico junto al control se actualiza de inmediato para mostrar el valor actual.
5. El panadapter se actualiza en tiempo real. No se requiere ningún paso de confirmación.

El valor se guarda automáticamente en `SpotsOverrideBgOpacity`.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Override Background: Enabled** | Enabled | Enabled / Disabled | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un relleno de fondo debajo del texto de los spots. La opacidad no tiene efecto cuando está en Disabled. |
| **Override Background: Auto** | Enabled | Enabled / Disabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Cuando está en Enabled, el color de fondo se elige automáticamente para garantizar contraste. Cuando está en Disabled, se usa el color definido por el selector de color de fondo. |
| **Background Opacity:** | 48 | 0 – 100 | `SpotsOverrideBgOpacity` | Establece el alfa del relleno de fondo de los spots. 0 es completamente transparente; 100 es completamente opaco. |

## Consejos

- La opacidad predeterminada de 48 proporciona un fondo semitransparente que permanece legible sin oscurecer el espectro subyacente.
- Si **Override Background: Auto** está en Enabled, el color de fondo se elige automáticamente para contrastar con el texto de los spots. Para usar un color específico con la opacidad que prefiera, configure **Override Background: Auto** en "Disabled" y use el selector de color de fondo.

## Solución de problemas

- **Cambiar el control deslizante no tiene efecto en el panadapter** — Confirme que **Override Background: Enabled** muestre "Enabled". Si la sobreposición de fondo está desactivada, no se dibuja ningún fondo y la opacidad no tiene nada sobre qué actuar.
- **El fondo es invisible incluso con una opacidad de 100** — Confirme que **Spots:** esté configurado en "Enabled". Si el interruptor principal de spots está desactivado, no se renderizan ni los spots ni sus fondos. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Relacionados

- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
