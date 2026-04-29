# Sintonizar el radio a una frecuencia (escribir MHz en el indicador)

Escriba una frecuencia directamente en el applet RX Controls para mover el VFO del slice activo a cualquier frecuencia dentro del rango de sintonía del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Si no lo está, vaya a `Settings > Connect to Radio...`.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
- Asegúrese de que el slice que desea sintonizar no esté bloqueado. Si el ícono de candado muestra 🔒, haga clic en él para desbloquearlo antes de continuar (consulte [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña de slice correspondiente (**A**, **B**, **C**, etc.) en la parte superior del applet RX Controls para seleccionar el slice que desea sintonizar.
2. Haga clic en la **Frequency label** (el indicador con puntos, p. ej. `0.000.000`). Este cambia a modo de edición y se convierte en el campo **Frequency edit**.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz.
4. Presione **Enter**. El slice se sintoniza a la frecuencia ingresada y el panadapter se recentra en ella.

Para cancelar sin cambiar la frecuencia, presione **Escape**. El editor se cierra y se restaura la frecuencia anterior.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Frequency label** | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para entrar al modo de edición. | `0.000.000` | — | — |
| **Frequency edit** | Campo de texto. Ingrese una frecuencia en MHz y presione Enter para sintonizar y recentrar. Escape cancela. | — | 0.001–54.000 MHz (hasta 450.000 MHz cuando el slice está en una antena transverter) | — |
| **STEP** | Define el tamaño del paso usado al desplazar la frecuencia con los botones `<` / `>` o la rueda del ratón. | 100 Hz | Lista por modo (p. ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | — |
| **Filter width presets** | Haga clic en un botón de preajuste para aplicar ese ancho de filtro al modo actual. Haga clic derecho en un preajuste para guardar el ancho actual en esa ranura. | — | USB/LSB: 1800–3300 Hz; AM/SAM: 5600–14000 Hz; CW: 50–400 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` |

## Consejos

- No es necesario escribir ceros al final. `14.2` se interpreta como 14.200 MHz.
- Para desplazar la frecuencia en pasos pequeños sin reescribir, use los botones `<` y `>` junto a **STEP**, o desplace la rueda del ratón sobre la **Frequency label** después de sintonizar.
- La lista de tamaños de paso cambia al cambiar de modo. Al cambiar el **Mode combo**, los preajustes de paso se restablecen a valores apropiados para ese modo.

## Solución de problemas

- **El campo Frequency edit no aparece al hacer clic en el indicador** — El slice puede estar bloqueado. Verifique si el ícono de candado muestra 🔒. Si es así, haga clic en él para desbloquearlo y luego haga clic de nuevo en el indicador de frecuencia.
- **La frecuencia que escribí fue ignorada** — Es posible que haya presionado Escape en lugar de Enter, o que haya ingresado un valor fuera del rango válido (0.001–54.000 MHz con una antena estándar, hasta 450.000 MHz con una antena transverter). Vuelva a ingresar el valor y presione Enter.
- **El panadapter no siguió la nueva frecuencia** — Verifique que `View > Pan Follows VFO` esté habilitado.

## Temas relacionados

- [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Entender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
