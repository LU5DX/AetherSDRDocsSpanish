# Sintonizar el radio a una frecuencia (escribir MHz en el indicador)

Escriba una frecuencia directamente en el indicador VFO para resintonizar el slice activo. Use esta opción cuando conozca la frecuencia exacta y desee ir a ella de inmediato sin hacer clic en el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls aparecerá en blanco si no hay conexión.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón **RX** de la bandeja en la barra lateral derecha para mostrarlo.
- El slice no debe tener el bloqueo de sintonía activado. Si se muestra el ícono 🔒, el slice ignorará los cambios de frecuencia. Consulte [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md).

## Pasos

1. En el applet RX Controls, confirme que la pestaña del slice correcto esté seleccionada (A hasta H). Si tiene más de un slice, haga clic en la pestaña correspondiente para activarlo.
2. Haga clic en el **Frequency label** — el indicador de frecuencia con puntos (por ejemplo, `14.225.000`). Al hacer clic, se activa el modo de edición y el indicador se reemplaza por un campo de texto.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz. El campo acepta valores de 0.001 a 54.000 MHz. Si el slice está en una antena con transverter, se aceptan valores de hasta 450.000 MHz.
4. Presione **Enter**. El radio se sintoniza a la frecuencia ingresada y el panadapter se recentra sobre ella.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido |
|---|---|---|---|
| **Frequency label** | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para entrar al modo de edición. | `0.000.000` | — |
| **Frequency edit** | Campo de texto que aparece al hacer clic en el indicador. Ingrese MHz y presione Enter para sintonizar y recentrar. Admite escalado automático en kHz/Hz. | — | 0.001–54.000 MHz (hasta 450.000 MHz con antena transverter) |
| **STEP** | Define el tamaño del paso de sintonía usado por los botones `<` / `>` y la rueda del ratón. La lista de pasos depende del modo actual. | 100 Hz | SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; otros modos varían |

## Consejos

- Después de ingresar una frecuencia, el panadapter se recentra automáticamente para mantener el VFO visible. Si prefiere que el panadapter no siga al VFO, desactive la opción **View > Pan Follows VFO**.
- Para ajustes pequeños después de escribir una frecuencia, use la rueda del ratón sobre el **Frequency label** o haga clic en los botones `<` / `>` junto a **STEP** para desplazarse en incrementos del tamaño de paso actual.
- Para evitar resintonizar accidentalmente un slice mientras ajusta otros controles, active el bloqueo de sintonía haciendo clic en el ícono 🔓 hasta que muestre 🔒.

## Solución de problemas

- **Presionar Enter no tiene efecto** — Es posible que el slice tenga el bloqueo de sintonía activado (se muestra 🔒 en la fila de encabezado). Haga clic en 🔒 para desbloquearlo y vuelva a ingresar la frecuencia.
- **El campo de entrada de frecuencia no aparece** — Es posible que la conexión con el radio se haya perdido. Verifique el estado de la conexión y vuelva a conectarse mediante **Settings > Connect to Radio...** si es necesario.
- **La frecuencia ingresada no es aceptada** — El valor puede estar fuera de rango. La entrada válida es 0.001–54.000 MHz (o hasta 450.000 MHz con antena transverter). Confirme que la antena del slice sea la correcta.

## Temas relacionados

- [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Seleccionar un ancho de filtro predefinido para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
