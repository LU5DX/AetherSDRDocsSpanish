# Cambiar entre múltiples slices usando la fila de pestañas A..H

El applet RX Controls muestra una fila de pestañas con letras — de la A a la H — cuando el radio tiene más de un slice activo. Al hacer clic en una pestaña, se vincula el applet RX Controls completo a ese slice, permitiéndole ajustar su frecuencia, modo, filtro y otros parámetros de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La fila de pestañas requiere una conexión activa con el radio.
- Deben existir al menos dos slices en el radio. La fila de pestañas se oculta cuando solo hay un slice activo.

## Pasos

1. Abra el applet RX Controls en el panel de applets. Si no está visible, haga clic en el botón RX del panel lateral derecho.
2. Localice la fila de pestañas de slices en la parte superior del applet RX Controls. Las pestañas están etiquetadas A, B, C, y así sucesivamente hasta la H, con una pestaña por cada slice activo.
3. Haga clic en la letra correspondiente al slice que desea controlar (por ejemplo, B para cambiar al slice B).
4. Confirme el cambio: el indicador de slice debajo de la fila de pestañas se actualiza con la letra del slice seleccionado, y todos los controles del applet — modo, frecuencia, ancho de filtro, antena, etc. — reflejan el estado actual de ese slice.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX Controls. | La fila se oculta cuando el radio reporta un solo slice. Aparecen entre 1 y 8 pestañas, limitadas por el número máximo de slices del radio. |
| Indicador de slice | Muestra la letra del slice actualmente vinculado (A/B/C/D/E/F/G/H). | El color corresponde a la identidad del slice. Se actualiza inmediatamente al hacer clic en una pestaña. |

No existe ninguna clave de configuración persistente asociada a la selección de pestañas de slice. Los preajustes de ancho de filtro se almacenan por modo bajo `FilterPresets`.

## Consejos

- La fila de pestañas solo aparece cuando `maxSlices` es mayor que 1. Si no ve pestañas, el radio actualmente tiene configurado un único slice.
- Cambiar de pestaña no modifica nada en el radio; solo cambia qué slice está visualizando y editando el applet RX Controls local.
- Cada slice conserva su propio modo, frecuencia, filtro, antena, AGC y configuración de RIT/XIT. Cambiar de pestaña permite inspeccionar o ajustar un slice sin afectar a los demás.

## Relacionado

- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
- [Descripción general de RX Controls](overview.md)
- [Sintonizar el radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
