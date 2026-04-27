# Cambiar entre múltiples slices usando la fila de pestañas A..H

El FLEX-8600 admite hasta ocho slices de recepción simultáneos. La fila de pestañas A..H en la parte superior del applet RX Controls permite cambiar a qué slice está vinculado el applet, para que pueda ver y ajustar el modo, la frecuencia, el filtro y otros parámetros de cada slice de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet RX Controls requiere una conexión de radio activa.
- El radio debe tener más de un slice activo. La fila de pestañas se oculta cuando solo existe un slice.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.

## Pasos

1. Observe la parte superior del applet RX Controls para encontrar la fila horizontal de pestañas con letras (A, B, C, y así sucesivamente, hasta H).
2. Haga clic en la letra de la pestaña correspondiente al slice que desea inspeccionar o controlar.
3. Confirme el cambio: el **Slice badge** en la fila de encabezado se actualiza para mostrar la letra del slice recién seleccionado, con el color de su identidad de slice.
4. Todos los controles debajo de la fila de pestañas — modo, frecuencia, filtro, AGC, ganancia AF y otros — ahora reflejan y controlan el slice seleccionado.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX Controls. | — | 1–8 pestañas, limitado por el número máximo de slices del radio | — |
| Slice badge | Muestra la letra del slice vinculado actualmente, con el color de su identidad de slice. | A | A / B / C / D / E / F / G / H | — |

## Consejos

- La fila de pestañas se oculta por completo cuando el radio indica un número máximo de slices de 1. Si no ve ninguna pestaña, solo hay un slice configurado en el radio.
- Cada slice conserva su propio modo, frecuencia, preajustes de filtro, configuración de AGC y selección de antena. Cambiar de pestaña no altera los parámetros de ningún slice; solo cambia qué slice muestra el applet.
- Los preajustes de ancho de filtro se guardan por modo mediante la configuración `FilterPresets`. Los preajustes que guarde en el slice A en modo USB se aplican al modo USB en todos los slices.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
- [Sintonizar el radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Bloquear el slice para evitar una resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
