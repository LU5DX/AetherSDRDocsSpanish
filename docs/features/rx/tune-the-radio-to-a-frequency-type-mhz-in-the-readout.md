# Sintonizar el radio en una frecuencia (escribir MHz en el indicador)

Haga clic en el indicador de frecuencia del applet RX Controls para abrir un campo de texto, escriba una frecuencia en MHz y presione Enter para sintonizar el slice en esa frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Si no está conectado, vaya a `Settings > Connect to Radio...`.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho.
- Si el slice está bloqueado, la sintonización se ignora. Desbloquéelo primero — consulte [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña correspondiente (A hasta H) en la parte superior del applet RX Controls para seleccionar el slice que desea sintonizar.
2. Haga clic en la etiqueta de frecuencia — el indicador con puntos que muestra la frecuencia VFO actual (por ejemplo, `14.225.000`). El indicador cambia a un campo de entrada de texto.
3. Escriba la frecuencia deseada en MHz (por ejemplo, `14.225`). El campo acepta valores de 0.001 a 54.000 MHz. Si el slice está en una antena con transverter, se aceptan valores de hasta 450.000 MHz.
4. Presione Enter. El slice se sintoniza en la frecuencia ingresada y el panadapter se recentra en ella.

Para cancelar sin sintonizar, presione Escape. La frecuencia anterior se restaura y el editor se cierra.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido |
|---|---|---|---|
| Etiqueta de frecuencia | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para entrar al modo de edición. | `0.000.000` | — |
| Edición de frecuencia | Campo de texto. Escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar. Presione Escape para cancelar. | — | 0.001–54.000 MHz (hasta 450.000 MHz en una antena con transverter) |
| STEP | Establece el tamaño del paso de sintonización utilizado por los botones `<` / `>` y la rueda del ratón. Haga clic en `<` o `>`, o desplace la rueda del ratón sobre el área del indicador, para subir o bajar la frecuencia en pasos. | 100 Hz | Lista por modo; para SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz |
| 🔓 / 🔒 | Bloquea o desbloquea el slice. Un slice bloqueado ignora los cambios de frecuencia de cualquier origen. | 🔓 (desbloqueado) | — |

## Consejos

- No es necesario escribir ceros iniciales ni ceros finales. Escribir `7.2` sintoniza en 7.200.000 MHz.
- Si sintoniza con la rueda del ratón o los botones STEP `<` / `>` en lugar de escribir, el tamaño del paso lo determina el control STEP. Cambie primero el tamaño del paso si desea incrementos más gruesos o más finos.
- Los presets de filtro se almacenan por modo en `FilterPresets`. Cambiar la frecuencia no altera el ancho de filtro ni el modo actuales.

## Solución de problemas

- **Hacer clic en el indicador de frecuencia no tiene efecto** — Es posible que el slice esté bloqueado. Verifique el botón 🔓 / 🔒 en la fila de encabezado; si muestra 🔒, haga clic en él para desbloquearlo.
- **El radio no sintoniza la frecuencia ingresada** — Confirme que el valor esté dentro del rango válido (0.001–54.000 MHz, o hasta 450.000 MHz en una antena con transverter). Los valores fuera del rango son rechazados y se restaura la frecuencia anterior.
- **El panadapter no sigue la nueva frecuencia** — Verifique que `View > Pan Follows VFO` esté habilitado.

## Relacionados

- [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preset de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
