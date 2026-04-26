# Habilitar o deshabilitar la estimación adaptativa de ruido de NR4

La estimación adaptativa de ruido de NR4 recalcula continuamente el piso de ruido a medida que cambian las condiciones de banda. Habilitarla ayuda a mantener una reducción de ruido precisa en señales con ruido variable o no estacionario; deshabilitarla congela la estimación del piso de ruido, lo que puede ser útil en bandas muy estables y silenciosas.

## Antes de comenzar

- AetherDSP Settings no requiere conexión a un radio. Puede ajustar la configuración de NR4 en cualquier momento.
- NR4 debe estar activo en su cadena de recepción para que estos ajustes tengan efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation**.
   - Marcado (predeterminado): NR4 recalcula continuamente el piso de ruido.
   - Desmarcado: la estimación del piso de ruido queda congelada en su último valor calculado.

El ajuste surte efecto de inmediato y se guarda como `NR4AdaptiveNoise`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Adaptive Noise Estimation** | Habilitado | On / Off | `NR4AdaptiveNoise` | Habilita el recálculo continuo del piso de ruido. |
| **Noise Estimation Method** | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` | Selecciona el algoritmo que realiza la estimación del piso de ruido que el modo adaptativo actualiza continuamente. |
| **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` | Reducción de ruido máxima aplicada por NR4. |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido de NR4. |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Intensidad general de supresión de NR4. |
| **Reset Defaults** | — | — | — | Restaura los valores predeterminados de NR4: SPP-MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50. |

## Consejos

- La estimación adaptativa de ruido funciona en combinación con el **Noise Estimation Method** seleccionado. Si cambia el método, el rastreador adaptativo se reinicia con la estimación inicial de ese algoritmo.
- En bandas estables y de bajo ruido donde las señales son consistentes, deshabilitar la estimación adaptativa y confiar en un piso de ruido congelado puede reducir las fluctuaciones de ganancia innecesarias durante las pausas en la voz.
- Si el piso de ruido cambia con frecuencia (por ejemplo, al cambiar entre bandas o durante actividad solar), mantenga la estimación adaptativa habilitada.

## Solución de problemas

- **La reducción de ruido parece bombear o respirar durante las pausas en la voz** — intente aumentar **Smoothing (%):** o deshabilitar **Adaptive Noise Estimation** para estabilizar la estimación del piso de ruido.
- **El ruido no se suprime tras un cambio en las condiciones** — si la estimación adaptativa está deshabilitada, la estimación congelada del piso de ruido puede ya no corresponder al ruido real. Vuelva a habilitar **Adaptive Noise Estimation** o haga clic en **Reset Defaults** para restaurar un estado conocido.

## Relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
