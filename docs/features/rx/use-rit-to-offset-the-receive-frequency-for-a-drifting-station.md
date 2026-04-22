# Usar RIT para desplazar la frecuencia de recepción cuando una estación se desvía

RIT (Sintonía Incremental de Recepción) desplaza únicamente la frecuencia de recepción sin mover la frecuencia de transmisión ni el indicador del VFO. Úselo cuando una estación con la que está trabajando se desvía ligeramente de su frecuencia en dial y desea seguirla sin resintonizar.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles RIT están inactivos sin una conexión de radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la fila RIT.
2. Haga clic en RIT para habilitar la Sintonía Incremental de Recepción. El botón se activa.
3. Use los botones `<` y `>` que flanquean el spinbox de desplazamiento RIT, o gire la rueda del ratón sobre él, para desplazar la frecuencia de recepción. Cada paso mueve el desplazamiento 10 Hz.
4. Lea el desplazamiento actual en el spinbox de desplazamiento RIT. El valor predeterminado es `+0 Hz`.
5. Para volver a cero sin deshabilitar RIT, haga clic en RIT 0.
6. Para desactivar RIT por completo, haga clic nuevamente en RIT para que el botón deje de estar activo.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido / paso | Comportamiento |
|---|---|---|---|---|
| RIT | Botón de alternancia | Off | On / Off | Habilita o deshabilita la Sintonía Incremental de Recepción para el slice activo. |
| Desplazamiento RIT | Spinbox | +0 Hz | Paso: 10 Hz | Establece el desplazamiento de la frecuencia de recepción. Ajuste con `<` / `>` o la rueda del ratón. |
| RIT 0 | Botón de acción | — | — | Pone a cero el desplazamiento RIT de forma inmediata sin desactivar RIT. |

## Consejos

- RIT afecta únicamente al lado de recepción. Su frecuencia de transmisión permanece en la frecuencia del VFO mostrada en el indicador Frequency.
- Si también necesita desplazar la frecuencia de transmisión, use XIT de forma independiente. Los dos desplazamientos son independientes entre sí.
- Para restablecer el desplazamiento y deshabilitar RIT en una sola acción, haga clic en RIT 0 y luego haga clic en RIT.

## Relacionados

- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Descripción general de RX Controls](overview.md)
