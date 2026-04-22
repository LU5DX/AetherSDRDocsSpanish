# Cambiar entre múltiples slices usando la fila de pestañas A..H

El applet RX Controls puede vincularse a cualquier slice activo en el radio. Use la fila de pestañas de slices para moverse entre los slices A hasta H sin salir del applet.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. La fila de pestañas de slices no se muestra cuando el radio reporta un único slice.
- Deben existir al menos dos slices en el radio. Cree slices adicionales desde el panadapter antes de usar este procedimiento. Consulte [Entendiendo los slices y VFOs](../../getting-started/concepts/understanding-slices.md).

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
2. Ubique la fila de pestañas de slices en la parte superior del applet. Contiene un botón por cada slice activo, etiquetado **A**, **B**, **C**, y así sucesivamente, hasta **H**.
3. Haga clic en la pestaña con la letra del slice que desea controlar. El applet se vincula inmediatamente a ese slice.
4. Confirme el cambio: el **Slice badge** en la fila de encabezado se actualiza para mostrar la letra seleccionada, con el color correspondiente a la identidad del slice.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX. | — | 1–8 botones, limitado por el número máximo de slices del radio | — |
| Slice badge | Muestra la letra del slice vinculado actualmente. | A | A / B / C / D / E / F / G / H | — |

## Consejos

- La fila de pestañas se oculta por completo cuando el número máximo de slices del radio es 1. Aparece automáticamente una vez que se crea un segundo slice.
- La letra de cada pestaña tiene el color correspondiente a la identidad del slice, coincidiendo con el slice badge y los marcadores del panadapter, lo que facilita identificar los slices de un vistazo.
- Cambiar de pestaña no afecta cuál slice es el slice de TX. Para cambiar el slice de TX, haga clic en el botón **TX (badge)** en el encabezado del applet después de cambiar de pestaña.

## Relacionado

- [Entendiendo los slices y VFOs](../../getting-started/concepts/understanding-slices.md)
- [Descripción general de RX Controls](overview.md)
- [Bloquear el slice para evitar un resintonizado accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
