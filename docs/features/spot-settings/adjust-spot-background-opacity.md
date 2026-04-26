# Ajustar la opacidad del fondo de los spots

Use el control deslizante **Background Opacity:** para controlar qué tan transparente u opaco aparece el relleno de fondo detrás de las etiquetas de spots en el panadapter.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter.
- Confirme que "Override Background: Enabled" está activo (el botón muestra "Enabled"). Si no lo está, el control deslizante de opacidad no tendrá ningún efecto visible.

## Pasos

1. En el diálogo Spot Settings, localice la fila "Override Background:".
2. Confirme que el botón de alternancia "Enabled" está activado (mostrando "Enabled"). Si no lo está, haga clic en "Enabled" para activarlo.
3. Localice el control deslizante "Background Opacity:" cerca de la parte inferior del diálogo.
4. Arrastre el control deslizante hacia la izquierda para reducir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaco).
5. La etiqueta numérica junto al control deslizante se actualiza de inmediato. El panadapter refleja el cambio en tiempo real.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Alternancia "Override Background: Enabled" | Enabled | Enabled / Disabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| Alternancia "Override Background: Auto" | Enabled | Enabled / Disabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Control deslizante "Background Opacity:" | 48 | 0 – 100 | `SpotsOverrideBgOpacity` |

## Consejos

- Un valor de 0 hace que el fondo sea completamente transparente; el texto del spot sigue apareciendo pero sin relleno detrás.
- Un valor de 100 hace que el fondo sea completamente opaco. Esto puede ocultar la traza del espectro bajo grupos densos de spots, por lo que un valor intermedio como el predeterminado (48) suele ser un punto de partida práctico.
- El botón "Override Background: Auto", cuando está en "Enabled", permite que AetherSDR elija automáticamente el color de fondo para garantizar contraste. Para usar un color fijo en su lugar, haga clic en "Auto" de modo que muestre "Disabled" y, a continuación, use el selector de color de fondo de spots. Consulte [Seleccionar un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md).

## Solución de problemas

- **El control deslizante se mueve pero el fondo en el panadapter no cambia** — Verifique que "Override Background: Enabled" muestre "Enabled". Si `IsSpotsEnabled` también está desactivado (la alternancia "Spots:" muestra "Disabled"), no se renderizará ningún elemento de spot. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Relacionados

- [Seleccionar un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Forzar un color de texto único para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
