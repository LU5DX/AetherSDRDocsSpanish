# Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Transmit Incremental Tuning) permite desplazar la frecuencia de transmisión un número fijo de hercios mientras la frecuencia de recepción permanece en el VFO. Esto es útil al trabajar en split, para compensar un desplazamiento de TX solicitado por la otra estación, o para ajustarse a la frecuencia de una red sin resintonizar el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles XIT solo están activos cuando hay una conexión con el radio.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón RX del panel lateral derecho.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para habilitar Transmit Incremental Tuning. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean el spinbox de desplazamiento XIT para avanzar en incrementos de 10 Hz.
   - Coloque el cursor sobre el spinbox de desplazamiento XIT y gire la rueda del ratón para avanzar en incrementos de 10 Hz.
4. Para restablecer el desplazamiento de TX a cero sin deshabilitar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic en XIT nuevamente para que el botón deje de estar iluminado.

## Qué hace cada control

| Control | Función | Valor predeterminado | Paso / Rango |
|---|---|---|---|
| XIT | Activa o desactiva Transmit Incremental Tuning. | Desactivado | — |
| Desplazamiento XIT | Establece el desplazamiento de frecuencia de TX en hercios. Se ajusta con los botones **<** / **>** o la rueda del ratón. | +0 Hz | 10 Hz por paso |
| XIT 0 | Restablece el desplazamiento XIT a +0 Hz sin desactivar XIT. | — | — |

## Consejos

- RIT y XIT son independientes. Puede usar ambos simultáneamente: RIT desplaza la frecuencia de recepción, XIT desplaza la frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, configure el desplazamiento XIT antes de transmitir; permanece establecido hasta que haga clic en XIT 0 o deshabilite XIT.
- Para poner a cero el desplazamiento rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y volver a activar XIT.

## Solución de problemas

- **Los controles XIT aparecen en gris** — El radio no está conectado. Use `Settings > Connect to Radio...` para establecer la conexión y vuelva a intentarlo.
- **La frecuencia de TX no se desplaza como se esperaba** — Confirme que el slice correcto esté seleccionado usando las pestañas de slice (A..H). XIT actúa únicamente sobre el slice actualmente asignado.

## Relacionados

- [Usar RIT para desplazar la frecuencia de recepción ante una estación con deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de RX Controls](overview.md)
