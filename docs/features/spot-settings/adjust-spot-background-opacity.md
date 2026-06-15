# Ajustar la opacidad del fondo de las marcas

Use esta página para controlar qué tan transparente u opaco aparece el fondo detrás de las etiquetas de las marcas en el panadapter. Reducir la opacidad permite que el espectro se vea a través del fondo; aumentarla hace que el texto de las marcas sea más legible sobre señales densas.

## Antes de comenzar

- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en la superposición de marcas en el panadapter.
- Confirme que "Override Background: Enabled" esté activo (el botón debe mostrarse como presionado/marcado). El control deslizante de opacidad no tiene efecto visible si el fondo está deshabilitado.

## Pasos

1. En el cuadro de diálogo Spot Settings, localice la fila **Background Opacity:**.
2. Arrastre el control deslizante hacia la izquierda para disminuir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaco).
3. El valor numérico junto al control deslizante se actualiza inmediatamente para reflejar el valor actual.
4. Cierre el cuadro de diálogo. El cambio se guarda automáticamente en `SpotsBackgroundOpacity`.

## Función de cada control

| Control | Valor predeterminado | Rango válido |
|---|---|---|
| Control deslizante **Background Opacity:** | 48 | 0 – 100 |
| Interruptor **Override Background: Enabled** | Activado (marcado) | Activado / Desactivado |
| Interruptor **Override Background: Auto** | Activado (marcado) | Activado / Desactivado |
| Selector de color de fondo de marcas | `#000000` | Cualquier color |
| Interruptor **Spots:** | Activado (marcado) | Activado / Desactivado |
| Interruptor **Memories:** | Desactivado (sin marcar) | Activado / Desactivado |
| Control deslizante **Levels:** | 3 | 1 – 10 |
| Control deslizante **Position:** | 50 | 0 – 100 |
| Control deslizante **Font Size:** | 16 | 8 – 32 |
| Control deslizante **Spot Lifetime:** | Varía | 10 seg – 24 horas (pasos no lineales) |
| Interruptor **Override Colors:** | Desactivado (sin marcar) | Activado / Desactivado |
| Selector de color de texto de marcas | `#FFFF00` | Cualquier color |
| Botón **Clear All Spots** | N/A | N/A |

## Controles adicionales

| Control | Valor predeterminado | Rango válido |
|---|---|---|
| Interruptor **Spots:** | Activado (marcado) | Activado / Desactivado |
| Interruptor **Memories:** | Desactivado (sin marcar) | Activado / Desactivado |
| Control deslizante **Levels:** | 3 | 1 – 10 |
| Control deslizante **Position:** | 50 | 0 – 100 |
| Control deslizante **Font Size:** | 16 | 8 – 32 |
| Control deslizante **Spot Lifetime:** | Varía | 10 seg – 24 horas (pasos no lineales) |
| Interruptor **Override Colors:** | Desactivado (sin marcar) | Activado / Desactivado |
| Selector de color de texto de marcas | `#FFFF00` | Cualquier color |
| Botón **Clear All Spots** | N/A | N/A |

## Consejos

- Un valor de 0 hace que el fondo sea completamente transparente; el texto de las marcas aún aparecerá pero sin relleno de fondo.
- Un valor de 100 hace que el fondo sea completamente opaco. Esto puede ocultar señales débiles debajo de una etiqueta de marca.
- Cuando "Override Background: Auto" está Activado, AetherSDR elige el color de fondo automáticamente para lograr contraste. El control deslizante de opacidad aún se aplica sobre ese color seleccionado automáticamente.
- Si desea un color de fondo específico, desactive primero "Override Background: Auto", luego use el selector de color de fondo de marcas para elegir un color antes de ajustar la opacidad.
- El interruptor **Spot Lines:** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Esta configuración se almacena en `IsSpotsLinesEnabled`. Desactívelo durante concursos para reducir el desorden visual.
- Los botones de alternancia ya no muestran el texto "Enabled" o "Disabled"; usan un estilo de botón marcable con indicadores de color de fondo: verde cuando están activados, rojo cuando están desactivados.

## Solución de problemas

- **Mover el control deslizante no tiene efecto** — Confirme que "Override Background: Enabled" se muestre como presionado/marcado. Si muestra fondo verde (activado), el control deslizante debería funcionar. Si muestra fondo rojo (desactivado), haga clic para activar el fondo y luego ajuste el control deslizante.
- **Los botones de alternancia no muestran cambios de texto** — Este comportamiento es normal. Los botones de alternancia usan un estado marcable con indicadores de color de fondo verde/rojo en lugar de etiquetas de texto.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Seleccionar un color de fondo personalizado para las marcas](pick-a-custom-background-color-for-spots.md)
- [Forzar un solo color de texto para las marcas](force-a-single-spot-text-color.md)
- [Activar o desactivar las marcas](turn-spots-on-or-off.md)
