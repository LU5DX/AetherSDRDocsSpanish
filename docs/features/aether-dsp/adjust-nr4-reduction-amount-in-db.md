# Ajustar la cantidad de reducción de NR4 en dB

El ajuste `NR4ReductionAmount` controla la agresividad con la que NR4 atenúa el ruido. Aumentar el valor incrementa la supresión; reducirlo preserva más el carácter original de la señal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio para cambiar este ajuste.
- NR4 debe estar activo en su cadena de recepción para que los cambios tengan un efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Arrastre el control deslizante **Reduction (dB):** hasta el valor deseado. El valor actual se muestra a la derecha del control.
4. Cierre el cuadro de diálogo. El ajuste se guarda automáticamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| **Noise Estimation Method** | SPP-MMSE | SPP-MMSE / Brandt / Martin | `NR4NoiseEstimationMethod` |
| **Adaptive Noise Estimation** | Enabled | On / Off | `NR4AdaptiveNoise` |

**Reduction (dB):** establece la atenuación de ruido máxima que NR4 aplicará. A 0.0 dB no se produce ninguna atenuación. A 40.0 dB, NR4 suprime el ruido hasta 40 dB por debajo del piso de ruido estimado.

## Consejos

- Comience con el valor predeterminado de 10.0 dB y auméntelo en pasos pequeños mientras monitorea la aparición de artefactos en la voz.
- Valores muy altos (por encima de 30 dB) en señales con ruido que cambia rápidamente pueden producir ruido musical o distorsión en la voz. Si esto ocurre, reduzca **Reduction (dB):** o aumente **Smoothing (%):** para estabilizar la estimación de ruido.
- Para restablecer todos los parámetros de NR4 a sus valores de fábrica en un solo paso, haga clic en **Reset Defaults** en la parte inferior de la pestaña NR4. Esto restaura **Reduction (dB):** a 10.0 dB junto con los demás valores predeterminados de NR4.

## Relacionado

- [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
