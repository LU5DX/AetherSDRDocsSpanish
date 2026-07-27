# Ajustar la opacidad del fondo de las marcas

Use esta página para controlar qué tan transparente u opaco aparece el fondo detrás de las etiquetas de las marcas en el panadapter. Reducir la opacidad permite que el espectro se vea a través; aumentarla facilita la lectura del texto de las marcas sobre señales ocupadas.

## Antes de comenzar

- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en la superposición de marcas en el panadapter.
- Confirme que la palanca "Override Background: Enabled" muestre el texto "Enabled" y fondo verde. El control deslizante de opacidad no tiene efecto visible si el fondo está deshabilitado.

## Pasos

1. En el cuadro de diálogo Spot Settings, localice la fila **Background Opacity:**.
2. Arrastre el control deslizante hacia la izquierda para reducir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaco).
3. La lectura numérica junto al control deslizante se actualiza inmediatamente para reflejar el valor actual.
4. Cierre el cuadro de diálogo. El cambio se guarda automáticamente en `SpotsBackgroundOpacity`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido |
|---|---|---|
| Control deslizante **Background Opacity:** | 48 | 0 – 100 |
| Palanca **Override Background:** | Enabled | Enabled / Disabled |
| Palanca **Override Background: Auto** | Enabled | Enabled / Disabled |
| Selector de color de fondo de marcas | `#000000` | Cualquier color |
| Palanca **Spots:** | Enabled | Enabled / Disabled |
| Palanca **Memories:** | Disabled | Enabled / Disabled |
| Control deslizante **Levels:** | 3 | 1 – 10 |
| Control deslizante **Position:** | 50 | 0 – 100 |
| Control deslizante **Font Size:** | 16 | 8 – 32 |
| Control deslizante **Spot Lifetime:** | Varía | 10 seg – 24 hrs (pasos no lineales) |
| Palanca **Override Colors:** | Disabled | Enabled / Disabled |
| Selector de color de texto de marcas | `#FFFF00` | Cualquier color |
| Palanca **Spot Lines:** | Enabled | Enabled / Disabled |
| Botón **Clear All Spots** | N/A | N/A |

## Consejos

- Un valor de 0 hace que el fondo sea completamente transparente; el texto de las marcas aún aparecerá pero sin relleno de respaldo.
- Un valor de 100 hace que el fondo sea completamente opaco. Esto puede ocultar señales débiles debajo de una etiqueta de marca.
- Cuando "Override Background: Auto" está habilitado, AetherSDR selecciona automáticamente el color de fondo para contraste. El control deslizante de opacidad aún se aplica sobre ese color seleccionado automáticamente.
- Si desea un color de fondo específico, deshabilite primero "Override Background: Auto", luego use el selector de color de fondo de marcas para elegir un color antes de ajustar la opacidad.
- La palanca **Spot Lines:** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Esta configuración se almacena en `IsSpotsLinesEnabled`. Desactívela durante concursos para reducir el desorden visual.
- Los botones de palanca muestran texto "Enabled" o "Disabled" e indicadores de color de fondo verde/rojo para mostrar el estado.

## Solución de problemas

- **Mover el control deslizante no tiene efecto** — Confirme que la palanca "Override Background:" muestre "Enabled" con fondo verde. Si muestra "Disabled" con fondo rojo, haga clic para habilitar el fondo y luego ajuste el control deslizante.
- **Los botones de palanca muestran el estado incorrecto** — Cada botón de palanca actualiza su texto automáticamente al hacer clic. Si el texto no coincide con el color de fondo, cierre y vuelva a abrir el cuadro de diálogo Spot Settings para actualizar.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Seleccionar un color de fondo personalizado para marcas](pick-a-custom-background-color-for-spots.md)
- [Forzar un solo color de texto para marcas](force-a-single-spot-text-color.md)
- [Activar o desactivar marcas](turn-spots-on-or-off.md)
