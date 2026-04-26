# Usar RIT para desplazar la frecuencia de recepción de una estación con deriva

RIT (Receive Incremental Tuning) desplaza únicamente la frecuencia de recepción en un pequeño margen, sin modificar la frecuencia de transmisión ni el dial del VFO. Úselo cuando una estación con la que está trabajando haya derivado ligeramente de su frecuencia de sintonía.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles RX Controls no están disponibles sin una conexión al radio.
- Abra el applet RX Controls. Si no es visible, haga clic en el botón RX del panel lateral derecho.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.

## Pasos

1. En el applet RX Controls, haga clic en RIT para activar Receive Incremental Tuning. El botón queda presionado.
2. Use las flechas `<` y `>` junto al cuadro de desplazamiento RIT, o gire la rueda del ratón sobre él, para ajustar el desplazamiento. Cada paso mueve la frecuencia de recepción 10 Hz.
3. Continúe ajustando hasta que la estación con deriva quede centrada en la banda de paso.
4. Para devolver la frecuencia de recepción a desplazamiento cero, haga clic en RIT 0.
5. Para desactivar RIT por completo, haga clic nuevamente en RIT.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango/Paso |
|---|---|---|---|
| RIT | Activa o desactiva Receive Incremental Tuning. | Off | — |
| RIT offset | Establece el desplazamiento RIT en Hz. Ajuste con `<` / `>` o la rueda del ratón. | +0 Hz | Pasos de 10 Hz |
| RIT 0 | Pone el desplazamiento RIT a cero de inmediato sin desactivar RIT. | — | — |

## Consejos

- RIT afecta únicamente la frecuencia de recepción. Su frecuencia de transmisión permanece en el dial del VFO, de modo que su señal transmitida se mantiene en la frecuencia que espera la otra estación.
- Hacer clic en RIT 0 borra el desplazamiento pero deja RIT habilitado, por lo que puede volver a aplicar un desplazamiento sin necesidad de reactivar la función.
- El cuadro de desplazamiento RIT offset no tiene un límite máximo documentado en el catálogo; use el desplazamiento mínimo que lleve la estación a la banda de paso en lugar de volver a sintonizar el VFO.

## Solución de problemas

- **RIT no produce ningún efecto audible** — Confirme que RIT aparece como activo (botón presionado). Si el slice está bloqueado (se muestra el candado 🔒), el bloqueo puede impedir cambios de frecuencia; haga clic en el candado para desbloquear el slice primero.
- **El desplazamiento vuelve a +0 Hz** — Hacer clic en RIT 0 es una acción puntual que siempre restablece el valor a cero. Si desea mantener un desplazamiento, no haga clic en RIT 0.

## Relacionado

- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquear el slice para evitar una resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Descripción general de RX Controls](overview.md)
