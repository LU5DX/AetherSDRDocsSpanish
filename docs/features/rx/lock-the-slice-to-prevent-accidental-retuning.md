# Bloquear el slice para evitar la sintonización accidental

La función de bloqueo de sintonía impide que un slice (canal receptor independiente) responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija mientras opera otros slices o hace clic en el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- Identifique qué slice desea bloquear. Si tiene más de uno, selecciónelo usando la fila de pestañas A..H en la parte superior del applet RX Controls.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
2. Localice el botón 🔓 en la fila de encabezado, inmediatamente a la derecha de la insignia del slice (A, B, C, etc.).
3. Haga clic en 🔓 para bloquear el slice. El ícono cambia a 🔒 y el botón se resalta en azul. El slice ignorará los cambios de frecuencia a partir de ese momento.
4. Para desbloquear, haga clic en 🔒 nuevamente. El ícono vuelve a 🔓 y el slice reanuda la sintonización normal.

## Qué hace cada control

| Control | Predeterminado | Comportamiento |
|---------|----------------|----------------|
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. El ícono alterna entre candado abierto y cerrado. No tiene clave de configuración persistente. |

## Consejos

- El bloqueo se aplica únicamente al slice que se muestra en ese momento en el applet RX Controls. Los demás slices no se ven afectados.
- Si tiene varios slices, use las pestañas de slice (A..H) para cambiar a uno diferente y bloquearlo o desbloquearlo de forma independiente.

## Solución de problemas

- **Al hacer clic en el panadapter o escribir una frecuencia, el slice sigue sintonizándose** — Confirme que el ícono 🔒 esté visible y resaltado en azul. Si el applet muestra un slice distinto al que desea bloquear, seleccione primero la pestaña del slice correcto.
- **El botón 🔓 / 🔒 no está visible** — Es posible que la fila de encabezado haya quedado fuera de vista si el panel del applet es muy pequeño. Redimensione el panel o desplácese hacia arriba dentro del applet.

## Relacionados

- [Cambiar entre varios slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Entender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
