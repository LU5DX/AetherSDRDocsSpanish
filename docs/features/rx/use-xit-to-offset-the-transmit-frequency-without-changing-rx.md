# Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión un offset fijo sin modificar la frecuencia de recepción. Esto es útil al trabajar en split, responder a una estación DX en una frecuencia ligeramente distinta, o compensar un transceptor en el otro extremo que está un poco desviado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles XIT no están disponibles sin una conexión de radio activa.
- Abra el applet RX Controls haciendo clic en el botón RX de la barra lateral derecha si no está visible.
- Seleccione el slice con el que desea trabajar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, localice la fila XIT cerca de la parte inferior del applet, debajo de la fila RIT.
2. Haga clic en XIT para habilitar el sintonizado incremental de transmisión. El botón se ilumina cuando está activo.
3. Ajuste el offset XIT usando el cuadro de valores del offset XIT:
   - Haga clic en `<` para disminuir el offset en pasos de 10 Hz.
   - Haga clic en `>` para aumentar el offset en pasos de 10 Hz.
   - Desplace la rueda del ratón sobre el cuadro de valores para cambiar el offset en pasos de 10 Hz.
4. Transmita. Su frecuencia de TX se desplazará según el offset XIT mostrado; la frecuencia de RX y la posición del VFO en el panadapter permanecen sin cambios.
5. Para eliminar el offset sin deshabilitar XIT, haga clic en XIT 0. El offset se restablece a +0 Hz.
6. Para deshabilitar XIT por completo, haga clic en XIT nuevamente para que el botón deje de estar activo.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Paso |
|---|---|---|---|
| XIT | Activa o desactiva el sintonizado incremental de transmisión. | Desactivado | — |
| XIT offset | Establece el offset de frecuencia de TX en Hz. Se ajusta con `<` / `>` o la rueda del ratón. | +0 Hz | 10 Hz |
| XIT 0 | Restablece el offset XIT a +0 Hz sin desactivar XIT. | — | — |

## Consejos

- XIT y RIT son independientes. Puede usar ambos al mismo tiempo para desplazar TX y RX por separado en el mismo slice.
- El offset XIT se ajusta en pasos de 10 Hz. Para un offset grande, mantenga presionado el botón `>` o `<`, o gire la rueda del ratón rápidamente.
- Para poner el offset a cero y deshabilitar XIT en una sola secuencia, haga clic en XIT 0 y luego en XIT.

## Relacionado

- [Usar RIT para desplazar la frecuencia de recepción por una estación con deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
