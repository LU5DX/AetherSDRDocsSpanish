# Bloquear el slice para evitar la sintonización accidental

Use el control de bloqueo de sintonía en el applet RX Controls para congelar la frecuencia de un slice (receptor independiente) de modo que los clics, el desplazamiento con la rueda del ratón y los comandos de sintonización no puedan resintonizarlo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- Identifique qué slice desea bloquear. Si tiene más de un slice activo, selecciónelo primero mediante la fila de pestañas de slice (A..H).

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón de bandeja **RX** en la barra lateral derecha.
2. Si hay varios slices en uso, haga clic en la pestaña con la letra correspondiente (A hasta H) del slice que desea bloquear.
3. Localice el botón **🔓** en la fila de encabezado, inmediatamente a la derecha del indicador del slice.
4. Haga clic en **🔓**. El ícono cambia a **🔒** y se torna azul. El slice queda bloqueado y comenzará a ignorar los cambios de frecuencia.
5. Para desbloquear, haga clic en **🔒**. El ícono vuelve a **🔓** y el slice acepta la sintonización nuevamente.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **🔓 / 🔒** | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora los cambios de frecuencia de cualquier origen. Cuando está desbloqueado (🔓), la sintonización normal se reanuda. |

## Consejos

- El estado de bloqueo se aplica únicamente al slice en el que se establece. Los demás slices no se ven afectados.
- El indicador con la letra del slice (A, B, C, etc.) y el botón de bloqueo se encuentran ambos en la fila de encabezado. Confirme que el indicador muestre la letra correcta antes de bloquear.

## Temas relacionados

- [Cambiar entre múltiples slices mediante la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Entender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
