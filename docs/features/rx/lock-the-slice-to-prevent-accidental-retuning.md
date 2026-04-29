# Bloquear el slice para evitar un resintonizado accidental

La función de bloqueo de sintonía impide que un slice (receptor virtual) responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin riesgo de mover el VFO al hacer clic en el panadapter o girar la rueda del ratón.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila de encabezado que contiene la insignia del slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de un slice, haga clic en la pestaña correspondiente (de A a H) para seleccionar el slice que desea bloquear.
3. Haga clic en el botón 🔓 de la fila de encabezado. El ícono cambia a 🔒 y se pone azul, confirmando que el slice está bloqueado.
4. Para desbloquear, haga clic en 🔒 nuevamente. El ícono vuelve a 🔓 y el slice retoma la respuesta a los cambios de frecuencia.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. Haga clic nuevamente para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear el slice A mientras el slice B permanece libremente sintonizable.
- El botón de bloqueo siempre es visible en la fila de encabezado, independientemente del modo actual.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
