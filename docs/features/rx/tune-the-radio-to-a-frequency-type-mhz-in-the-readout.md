# Sintonizar el radio a una frecuencia (escribir MHz en el indicador)

Escriba una frecuencia directamente en el indicador VFO para resintonizar el slice (canal de recepción) activo. Use este método cuando desee saltar a una frecuencia específica en lugar de hacer clic en el panadapter o desplazar el control de paso.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Si no lo está, vaya a `Settings > Connect to Radio...` y establezca una conexión.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón **RX** de la bandeja en la barra lateral derecha para mostrarlo.
- El slice que desea sintonizar no debe estar bloqueado. Un candado cerrado (🔒) en el encabezado del applet indica que el slice está bloqueado e ignorará los cambios de frecuencia. Consulte [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña correcta (**A**, **B**, **C**, etc.) en el applet RX Controls para activarla.
2. Haga clic en la **Frequency label** (el indicador con puntos, p. ej. `14.225.000`). La etiqueta cambia a un campo de texto editable.
3. Escriba la frecuencia en MHz, por ejemplo `14.225` o `7.074`. El campo acepta valores de 0.001 a 54.000 MHz. Si el slice está en una antena de transverter, el campo acepta hasta 450.000 MHz.
4. Presione **Enter**. El slice se sintoniza a la frecuencia ingresada y el panadapter se recentra en ella.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Frequency label** | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para entrar en modo de edición. | `0.000.000` | — | — |
| **Frequency edit** | Campo de texto que aparece al hacer clic en la etiqueta. Ingrese MHz y presione Enter para sintonizar y recentrar. Admite escalado automático kHz/Hz. | — | 0.001–54.000 MHz (hasta 450.000 MHz en XVTR) | — |
| **STEP** | Establece el tamaño del paso de sintonía usado al desplazar o usar los botones **<** / **>**. Recorre una lista por modo. | 100 Hz (índice 2) | SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; FM: 50–12500 Hz (ver lista de modos) | — |
| **Filter width presets** | Botones que aplican un ancho de filtro preestablecido para el modo actual. Haga clic derecho en un botón para guardar el ancho actual como ese preajuste. Oculto en los modos FM, NFM y DFM. | — | USB/LSB: 1800–3300 Hz; CW: 50–400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` |

## Consejos

- Si ingresa un valor sin punto decimal, AetherSDR aplica escalado automático kHz/Hz. Por ejemplo, ingresar `14225` se interpreta como 14.225 MHz.
- Después de sintonizar, el panadapter se recentra automáticamente. Para desactivar esto, desmarque `View > Pan Follows VFO`.
- Para ajuste fino después de ingresar una frecuencia, use los botones **<** / **>** del control **STEP** o la rueda del ratón sobre el indicador de frecuencia.

## Solución de problemas

- **Hacer clic en la etiqueta de frecuencia no hace nada** — El slice puede estar bloqueado. Verifique si el icono del candado en el encabezado del applet muestra 🔒. Si es así, haga clic en él para desbloquear el slice.
- **La frecuencia vuelve inmediatamente después de presionar Enter** — El valor ingresado puede estar fuera del rango válido (0.001–54.000 MHz en un puerto de antena estándar). Verifique la frecuencia e inténtelo de nuevo. Si el slice está en una antena de transverter, se aceptan valores de hasta 450.000 MHz.
- **La Frequency label no es visible** — Es posible que el applet RX Controls esté contraído u oculto. Haga clic en el botón **RX** de la bandeja en la barra lateral derecha para alternarlo.

## Relacionados

- [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un ancho de filtro preestablecido para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Entendiendo los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
