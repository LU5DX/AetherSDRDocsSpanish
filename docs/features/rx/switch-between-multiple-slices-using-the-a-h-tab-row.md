# Cambiar entre múltiples slices mediante la fila de pestañas A..H

El FLEX-8600 admite hasta ocho slices de recepción simultáneos. La fila de pestañas A..H en el applet RX Controls permite moverse entre esos slices para que los controles del applet se apliquen al que usted desee.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. La fila de pestañas no es visible en ningún otro caso.
- El radio debe tener más de un slice activo. La fila de pestañas se oculta cuando solo existe un slice.
- El applet RX Controls debe estar abierto en el Panel de Applets. Si no es visible, haga clic en el botón de bandeja **RX** en la barra lateral derecha.

## Pasos

1. Observe la parte superior del applet RX Controls; encontrará una fila de botones con letras (A, B, C, etcétera).
2. Haga clic en la letra del slice con el que desea trabajar (por ejemplo, **B**).
3. Confirme el cambio: el **Slice badge** (el pequeño cuadrado de color en el extremo izquierdo de la fila de encabezado) se actualiza para mostrar la letra seleccionada, y todos los controles inferiores —frecuencia, modo, filtro, AGC, etcétera— reflejan ahora ese slice.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX. | Entre 1 y 8 botones, limitados por la cantidad máxima de slices del radio. La fila se oculta cuando solo hay un slice. |
| Slice badge | Muestra la letra del slice vinculado actualmente. | El color corresponde a la identidad del slice. Se actualiza de inmediato al hacer clic en una pestaña. |

## Consejos

- La fila de pestañas muestra únicamente tantos botones como slices tenga disponibles el radio, con un máximo de ocho (A hasta H).
- Después de cambiar de slice, verifique el **Slice badge** para confirmar qué slice está activo antes de modificar el modo, la frecuencia o los ajustes del filtro.
- Los presets de ancho de filtro se almacenan por modo bajo la configuración `FilterPresets`. Cambiar de slice no modifica los presets guardados, pero los botones de presets mostrados reflejarán el modo y el filtro del slice recién seleccionado.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Conceptos sobre slices y VFOs](../../getting-started/concepts/understanding-slices.md)
- [Sintonizar el radio a una frecuencia (escriba MHz en el display)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquear el slice para evitar una resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Seleccionar un preset de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
