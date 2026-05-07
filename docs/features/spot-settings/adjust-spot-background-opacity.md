# Ajustar la opacidad del fondo de las marcas

Use esta página para controlar el nivel de transparencia u opacidad del fondo detrás de las etiquetas de las marcas en el panadapter. Reducir la opacidad permite que el espectro se vea a través; aumentarla facilita la lectura del texto de las marcas sobre señales densas.

## Antes de comenzar

- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en la superposición de marcas en el panadapter.
- Confirme que "Override Background: Enabled" está activo (el botón muestra "Enabled"). El control deslizante de opacidad no tendrá efecto visible si el fondo está deshabilitado.

## Pasos

1. En el cuadro de diálogo Spot Settings, localice la fila **Background Opacity:**.
2. Arrastre el control deslizante hacia la izquierda para disminuir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaca).
3. El valor numérico junto al control deslizante se actualiza inmediatamente para reflejar el valor actual.
4. Cierre el cuadro de diálogo. El cambio se guarda automáticamente en `SpotsBackgroundOpacity`.

## Función de cada control

| Control | Valor predeterminado | Rango válido |
|---|---|---|
| Control deslizante **Background Opacity:** | 48 | 0 – 100 |
| Alternador **Override Background: Enabled** | Enabled | Enabled / Disabled |
| Alternador **Override Background: Auto** | Enabled | Enabled / Disabled |
| Selector de color de fondo de marcas | `#000000` | Cualquier color |
| Alternador **Spot Lines:** | Enabled | Enabled / Disabled |

## Consejos

- Un valor de 0 hace que el fondo sea completamente transparente; el texto de las marcas aún se mostrará pero sin relleno de fondo.
- Un valor de 100 hace que el fondo sea completamente opaco. Esto puede ocultar señales débiles debajo de una etiqueta de marca.
- Cuando "Override Background: Auto" está en Enabled, AetherSDR elige automáticamente el color de fondo para lograr contraste. El control deslizante de opacidad sigue aplicándose sobre ese color seleccionado automáticamente.
- Si desea un color de fondo específico, deshabilite primero "Override Background: Auto", luego use el selector de color de fondo de marcas para elegir un color antes de ajustar la opacidad.
- El alternador **Spot Lines:** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Esta configuración se almacena en `IsSpotsLinesEnabled`. Desactívelo durante concursos para reducir el desorden visual.

## Solución de problemas

- **Mover el control deslizante no tiene efecto** — Confirme que "Override Background: Enabled" muestra "Enabled". Si muestra "Disabled", haga clic para habilitar el fondo y luego ajuste el control deslizante.

## Relacionados

- [Visión general de Spot Settings](overview.md)
- [Elegir un color de fondo personalizado para las marcas](pick-a-custom-background-color-for-spots.md)
- [Forzar un único color de texto para las marcas](force-a-single-spot-text-color.md)
- [Activar o desactivar las marcas](turn-spots-on-or-off.md)
