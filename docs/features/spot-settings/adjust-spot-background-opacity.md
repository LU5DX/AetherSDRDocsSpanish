# Ajustar la opacidad del fondo de los spots

Use esta página para controlar qué tan transparente u opaco aparece el fondo detrás de las etiquetas de spots en el panadapter. Reducir la opacidad permite ver el espectro a través del fondo; aumentarla facilita la lectura del texto de los spots sobre señales concurridas.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter.
- Confirme que "Override Background: Enabled" esté activo (el botón muestra "Enabled"). El control deslizante de opacidad no tiene efecto visible si el fondo está desactivado.

## Pasos

1. En el diálogo Spot Settings, localice la fila **Background Opacity:**.
2. Arrastre el control deslizante hacia la izquierda para disminuir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaco).
3. El valor numérico junto al control se actualiza inmediatamente para reflejar el valor actual.
4. Cierre el diálogo. El cambio se guarda automáticamente en `SpotsOverrideBgOpacity`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Control deslizante **Background Opacity:** | 48 | 0 – 100 | `SpotsOverrideBgOpacity` |
| Interruptor **Override Background: Enabled** | Enabled | Enabled / Disabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| Interruptor **Override Background: Auto** | Enabled | Enabled / Disabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de spots | `#000000` | Cualquier color | `SpotsOverrideBgColor` |

## Consejos

- Un valor de 0 hace el fondo completamente transparente; el texto de los spots seguirá apareciendo pero sin relleno de fondo.
- Un valor de 100 hace el fondo completamente opaco. Esto puede ocultar señales débiles que queden debajo de una etiqueta de spot.
- Cuando "Override Background: Auto" está en Enabled, AetherSDR selecciona automáticamente el color de fondo para garantizar contraste. El control deslizante de opacidad se aplica igualmente sobre ese color seleccionado automáticamente.
- Si desea un color de fondo específico, desactive "Override Background: Auto" primero y luego use el selector de color de fondo de spots para elegir un color antes de ajustar la opacidad.

## Solución de problemas

- **Mover el control deslizante no tiene efecto** — Confirme que "Override Background: Enabled" muestre "Enabled". Si muestra "Disabled", haga clic en él para activar el fondo y luego ajuste el control deslizante.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Seleccionar un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
