# Bloquear el slice para evitar un resintonizado accidental

La función de bloqueo de sintonía (tune-lock) evita que un slice responda a cambios de frecuencia, como clics accidentales en el panadapter o el movimiento de la rueda de desplazamiento. Úsela para mantener estable una frecuencia de monitoreo mientras trabaja con otro slice.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls no funciona sin una conexión de radio.
- El applet RX debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.

## Pasos

1. En la fila de encabezado del applet RX, localice el ícono de candado. Cuando el slice está desbloqueado, el ícono muestra 🔓.
2. Haga clic en 🔓. El ícono cambia a 🔒 y se torna azul. El slice ahora ignora los cambios de frecuencia.
3. Para desbloquear, haga clic en 🔒 nuevamente. El ícono vuelve a 🔓 y la sintonía normal se reanuda.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los comandos de cambio de frecuencia. Haga clic nuevamente para desbloquear. |

## Consejos

- El bloqueo se aplica al slice que se muestra actualmente en el applet RX. Si tiene varios slices, verifique la insignia del slice (A, B, C, …) en la fila de encabezado para confirmar cuál está bloqueando antes de hacer clic.
- Bloquear un slice no afecta su audio, filtro, modo ni configuración de AGC: solo se bloquea la sintonía.

## Relacionado

- [Cambiar entre varios slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Entender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
