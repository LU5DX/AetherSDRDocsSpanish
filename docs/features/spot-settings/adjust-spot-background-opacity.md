# Ajustar la opacidad del fondo de las marcas

Use esta página para controlar qué tan transparente u opaco aparece el fondo detrás de las etiquetas de las marcas en el panadapter. Reducir la opacidad permite que el espectro se vea a través; aumentarla hace que el texto de las marcas sea más legible sobre señales densas.

## Antes de comenzar

- Abra el diálogo de Configuración de Marcas haciendo clic derecho en la superposición de marcas en el panadapter.
- Confirme que "Override Background: Enabled" esté activo (el botón muestra "Enabled"). El control deslizante de opacidad no tiene efecto visible si el fondo está deshabilitado.

## Pasos

1. En el diálogo Configuración de Marcas, localice la fila **Background Opacity:**
2. Arrastre el control deslizante hacia la izquierda para disminuir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaca).
3. La lectura numérica junto al control deslizante se actualiza inmediatamente para reflejar el valor actual.
4. Cierre el diálogo. El cambio se guarda automáticamente en `SpotsBackgroundOpacity`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido |
|---|---|---|
| Control deslizante **Background Opacity:** | 48 | 0 – 100 |
| Alternar **Override Background: Enabled** | Enabled | Enabled / Disabled |
| Alternar **Override Background: Auto** | Enabled | Enabled / Disabled |
| Selector de color de fondo de marcas | `#000000` | Cualquier color |
| Alternar **Spot Lines:** | Enabled | Enabled / Disabled |

## Consejos

- Un valor de 0 hace que el fondo sea completamente transparente; el texto de las marcas seguirá apareciendo pero sin relleno de fondo.
- Un valor de 100 hace que el fondo sea completamente opaco. Esto puede ocultar señales débiles debajo de una etiqueta de marca.
- Cuando "Override Background: Auto" está habilitado, AetherSDR selecciona automáticamente el color de fondo para contraste. El control deslizante de opacidad aún se aplica sobre ese color seleccionado automáticamente.
- Si desea un color de fondo específico, deshabilite primero "Override Background: Auto", luego use el selector de color de fondo de marcas para elegir un color antes de ajustar la opacidad.
- La alternancia **Spot Lines:** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Esta configuración se almacena en `IsSpotsLinesEnabled`. Desactívela durante concursos para reducir el desorden visual.

## Solución de problemas

- **Mover el control deslizante no tiene efecto** — Confirme que "Override Background: Enabled" muestre "Enabled". Si muestra "Disabled", haga clic para habilitar el fondo y luego ajuste el control deslizante.

## Relacionado

- [Descripción general de Configuración de Marcas](overview.md)
- [Elija un color de fondo personalizado para las marcas](pick-a-custom-background-color-for-spots.md)
- [Forzar un solo color de texto para las marcas](force-a-single-spot-text-color.md)
- [Activar o desactivar las marcas](turn-spots-on-or-off.md)
