# Use XIT to offset the transmit frequency without changing RX

XIT (Transmit Incremental Tuning) le permite desplazar su frecuencia de transmisión un número fijo de hertz mientras su frecuencia de recepción permanece en el VFO. Esto es útil cuando trabaja en split, compensando un desplazamiento de TX solicitado por la otra estación, o igualando una frecuencia de red sin reajustar el panadapter.

## Before you start

- AetherSDR must be connected to the radio. XIT controls are only active when a radio connection is present.
- Open the RX Controls applet. If it is not visible, click the RX tray button on the right sidebar.
- Select the slice you want to adjust using the slice tabs (A..H) at the top of the applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para activar Transmit Incremental Tuning. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean el spinbox de desplazamiento XIT para avanzar en incrementos de 10 Hz.
   - Pase el mouse sobre el spinbox de desplazamiento XIT y desplácese con la rueda del mouse para avanzar en incrementos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin desactivar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic nuevamente en XIT para que el botón ya no esté iluminado.

## What each control does

| Control    | What it does                                                                                   | Default |
|------------|------------------------------------------------------------------------------------------------|---------|
| XIT        | Toggles Transmit Incremental Tuning on or off.                                                 | Off     |
| XIT offset | Sets the TX frequency offset in hertz. Adjusted with the **<** / **>** buttons or mouse wheel. | +0 Hz   |
| XIT 0      | Resets the XIT offset to +0 Hz without turning XIT off.                                        | —       |

## Consejos

- RIT y XIT son independientes. Puede ejecutar ambos simultáneamente: RIT desplaza su frecuencia de recepción, XIT desplaza su frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, establezca el desplazamiento XIT antes de transmitir; permanecerá establecido hasta que haga clic en XIT 0 o desactive XIT.
- Para poner a cero el desplazamiento rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y reactivar XIT.

## Solución de problemas

- **Los controles XIT están deshabilitados** — La radio no está conectada. Use `Settings > Connect to Radio...` para establecer una conexión, luego intente de nuevo.
- **La frecuencia de TX no se desplaza como se esperaba** — Confirme que la slice correcta está seleccionada usando las tabs de slice (A..H). XIT actúa solo sobre la slice actualmente vinculada.

## Slice tab and badge colors (v0.9.3)

Starting in v0.9.3, the slice tab buttons (A..H) and the slice badge in the top-left of the applet are colored by the SliceColorManager. Each slice has its own color that persists across sessions. The same color is reflected in the VFO widgets and meter strips for that slice. Colors are not configurable from within the RX Controls applet itself; they are managed centrally by SliceColorManager and apply consistently across all widgets that reference a given slice.

## NT mode behavior

The NT mode is treated as a digital mode by the RX Controls applet. Specifically:

- NT follows the same filter width presets and step sizes as DIGU and DIGL.
- The filter width label calculates bandwidth the same way as DIGU (using the high-edge value).
- The SQL button and squelch level slider are disabled when NT is active, because audio is routed via DAX and squelch is not meaningful. If squelch was on when you switched to NT, it is turned off automatically and the previous state is saved for restoration when you leave NT mode.

## Relacionado

- [Use RIT to offset the receive frequency for a drifting station](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Tune the radio to a frequency (type MHz in the readout)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Switch between multiple slices using the A..H tab row](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [RX Controls overview](overview.md)
