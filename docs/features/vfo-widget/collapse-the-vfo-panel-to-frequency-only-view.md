# Contraer el panel VFO a vista de frecuencia únicamente

Cuando el espacio en pantalla es limitado, puede contraer el panel VFO a una barra compacta que muestra solo la frecuencia del slice (canal de recepción). El estado contraído se guarda por slice y persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO del slice en la pantalla del espectro.

## Pasos

1. Localice el badge del slice en el área de encabezado del panel VFO. El badge muestra el identificador del slice (por ejemplo, **A** o **B**).
2. Haga clic en el badge del slice. El panel se contrae a una barra compacta de solo frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier lugar de la barra contraída.

## Qué hace cada control

| Control | Valor predeterminado | Ajuste persistido |
|---|---|---|
| Alternancia de contracción | Expandido | `SliceFlagCollapsed_{N}` |

El ajuste `SliceFlagCollapsed_{N}` se almacena por slice, donde `{N}` es el número de slice. Contraer un slice no afecta a los demás slices.

## Consejos

- En vista contraída, desplazar la rueda del ratón sobre la barra sintoniza la frecuencia del slice según el tamaño de paso actual — igual que al desplazar sobre la pantalla de frecuencia en el panel completo.
- En vista contraída, hacer clic en el badge TX que aparece en la barra alterna la asignación TX de ese slice. Hacer clic en cualquier otro lugar de la barra expande el panel.
- El panel se desplaza automáticamente hacia el lado derecho del marcador VFO si al expandirse quedaría recortado por el borde de la ventana. Este comportamiento aplica tanto en estado expandido como contraído.

## Relacionado

- [Descripción general del panel VFO](overview.md)
- [Sintonizar el radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Cambiar el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Ocultar o mostrar las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
