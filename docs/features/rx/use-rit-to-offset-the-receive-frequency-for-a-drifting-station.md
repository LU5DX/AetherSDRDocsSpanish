# Usar RIT para desplazar la frecuencia de recepción cuando una estación deriva

RIT (Receive Incremental Tuning) desplaza únicamente la frecuencia de recepción sin alterar la frecuencia de transmisión. Úselo cuando la estación con la que está operando derive ligeramente de su frecuencia de dial y desee seguirla sin mover el VFO.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. RIT es un control por slice (canal de recepción) y requiere un slice activo.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón de bandeja **RX** en la barra lateral derecha.

## Pasos

1. En el applet RX Controls, haga clic en **RIT** para activar Receive Incremental Tuning. El botón queda enclavado en posición activa.
2. Use los botones **<** y **>** a los lados del spinbox **RIT offset**, o gire la rueda del ratón sobre el spinbox, para desplazar la frecuencia de recepción. Cada paso mueve 10 Hz.
3. Continúe ajustando hasta que la estación que deriva quede centrada en la banda de paso.
4. Para volver a cero, haga clic en **RIT 0**.
5. Para desactivar RIT por completo, haga clic en **RIT** nuevamente para desenclavarlo.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| **RIT** | Botón alternante. Activa o desactiva Receive Incremental Tuning para el slice activo. | Off |
| **RIT offset** | Spinbox que muestra el desplazamiento RIT actual en Hz. Ajústelo con **<** / **>** o la rueda del ratón. | +0 Hz |
| **RIT 0** | Botón pulsador. Pone a cero el desplazamiento RIT de inmediato sin desactivar RIT. | — |

## Consejos

- Los pasos del desplazamiento RIT son fijos: 10 Hz por clic o detención de la rueda. Para correcciones mayores, haga clic o desplace la rueda varias veces.
- Al hacer clic en **RIT 0** se pone el desplazamiento a cero, pero RIT permanece activo; así puede aplicar un nuevo desplazamiento sin necesidad de desactivar y volver a activar la función.
- Si necesita desplazar la frecuencia de transmisión en lugar de la de recepción, use **XIT**: sus controles funcionan de la misma manera. Consulte [Usar XIT para desplazar la frecuencia de transmisión sin modificar RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md).

## Solución de problemas

- **El botón RIT no responde** — Es posible que el slice esté bloqueado. Verifique si el ícono de candado (🔒) aparece en el encabezado del applet. Si es así, haga clic en él para desbloquear el slice. Consulte [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md).
- **La frecuencia de recepción no se desplaza con RIT activo** — Confirme que la pestaña de slice correcta (A–H) esté seleccionada en el applet. RIT se aplica únicamente al slice al que está vinculado el applet en ese momento.

## Relacionados

- [Usar XIT para desplazar la frecuencia de transmisión sin modificar RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
