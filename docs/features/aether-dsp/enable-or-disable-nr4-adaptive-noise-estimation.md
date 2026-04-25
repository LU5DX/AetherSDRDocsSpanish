# Habilitar o deshabilitar la estimación adaptativa de ruido de NR4

La estimación adaptativa de ruido de NR4 remide continuamente el piso de ruido a medida que las condiciones cambian en la banda. Habilitarla permite que el motor siga las interferencias variables; deshabilitarla congela la estimación del piso de ruido, lo que puede ser útil cuando el ruido de fondo es muy estable y uniforme.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar este ajuste.
- Abra el diálogo AetherDSP Settings mediante `Settings > AetherDSP Settings...`.

## Pasos

1. Vaya a `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation**.
   - Marcada (predeterminado): NR4 re-estima continuamente el piso de ruido.
   - Desmarcada: la estimación del piso de ruido queda congelada en el valor capturado la última vez que se inició NR4.

El ajuste se guarda de inmediato. No se necesita confirmación ni reinicio.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| **Noise Estimation Method** (botones de opción: SPP-MMSE, Brandt, Martin) | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| **Adaptive Noise Estimation** (casilla de verificación) | Habilitado | On / Off | `NR4AdaptiveNoise` |
| **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| **Reset Defaults** (botón) | — | — | — |

## Consejos

- Si el carácter del ruido en su frecuencia cambia rápidamente (ruido de pulsos, ráfagas de QRM), mantenga **Adaptive Noise Estimation** habilitada para que el estimador pueda seguir el piso cambiante.
- Si nota que el estimador de ruido atenúa señales durante una transmisión prolongada de una estación débil, intente deshabilitar **Adaptive Noise Estimation** para evitar que el motor trate la señal entrante como parte del piso de ruido.
- Al hacer clic en **Reset Defaults** en la pestaña NR4 se restauran todos los parámetros de NR4 a sus valores predeterminados, incluida la re-habilitación de **Adaptive Noise Estimation**.

## Solución de problemas

- **Las señales deseadas se están suprimiendo junto con el ruido** — es posible que el estimador adaptativo esté clasificando una señal débil o constante como ruido. Desmarque **Adaptive Noise Estimation** para congelar la estimación del piso de ruido.
- **La supresión de ruido deja de seguir el piso después de un tiempo** — verifique que **Adaptive Noise Estimation** esté marcada. Si el carácter del ruido ha cambiado significativamente desde que se inició AetherSDR, la estimación congelada puede ya no corresponder al piso actual.

## Relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
