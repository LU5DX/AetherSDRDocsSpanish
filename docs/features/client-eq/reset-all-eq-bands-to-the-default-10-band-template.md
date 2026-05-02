# Restablecer todas las bandas del ecualizador a la plantilla predeterminada de 10 bandas

Use este procedimiento para descartar todas las ediciones de bandas del ecualizador TX o RX y devolver el ecualizador a la configuración de fábrica de 10 bandas. Esto también restablece el número de bandas y la familia de filtros a sus valores predeterminados.

## Antes de comenzar

- El editor flotante del canal de EQ que desea restablecer (TX o RX) debe estar abierto. Consulte [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier canal](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md) si aún no está abierto.

## Pasos

1. En la barra de título del editor flotante, confirme que se encuentra en el canal correcto — el título de la ventana indica "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Haga clic en Reset en la franja de encabezado del editor.

Todas las bandas se reemplazan inmediatamente con la plantilla predeterminada de 10 bandas. El número de bandas se restaura a 10 y el combo Filter family se restablece a Butterworth. La configuración se guarda de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento tras el restablecimiento |
|---|---|---|
| Reset | — | Reemplaza todas las bandas con la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y establece Filter family en Butterworth. Guarda de inmediato. |
| Filter family | Butterworth | Se restablece a Butterworth. Se aplica solo a los tipos de filtro HP y LP; las bandas de tipo peak y shelf no se ven afectadas por este selector. Se persiste como `ClientEqTxFilterFamily` (TX) o `ClientEqRxFilterFamily` (RX). |
| Band count | 10 | Se restaura a 10 mediante Reset. Se persiste como `ClientEqTxBandCount` (TX) o `ClientEqRxBandCount` (RX). |

## Consejos

- Reset afecta únicamente al canal que se muestra en la ventana del editor actual. Para restablecer el otro canal, abra el otro editor y repita el procedimiento.
- El Output Fader (ganancia maestra post-EQ, persistida como `ClientEqTxMasterGain` o `ClientEqRxMasterGain`) no se modifica con Reset. Haga doble clic en el fader para devolverlo a 0 dB de forma independiente si es necesario.

## Temas relacionados

- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier canal](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Cambiar la familia de filtros HP/LP (Butterworth, Chebyshev, Bessel, Elliptic)](change-the-hp-lp-filter-family-butterworth-chebyshev-bessel-elliptic.md)
- [Ajustar la ganancia de salida post-EQ con el Output Fader](adjust-post-eq-output-gain-with-the-output-fader.md)
- [Cambiar el tipo de filtro de una banda haciendo clic en su icono en la fila de iconos](change-a-band-s-filter-type-by-clicking-its-icon-in-the-icon-row.md)
