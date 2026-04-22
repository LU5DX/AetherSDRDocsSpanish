# Activar o desactivar la estimación adaptativa de ruido de NR4

La estimación adaptativa de ruido de NR4 recalcula continuamente el piso de ruido a medida que cambian las condiciones de banda. Desactivarla fija el piso de ruido en una estimación constante, lo que puede ser útil con ruido muy estable, pero puede degradar la supresión cuando las condiciones cambian.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar este ajuste.
- Abra la pestaña **NR4** en AetherDSP Settings. Si aún no se encuentra allí, siga los pasos indicados a continuación.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation** para activarla o desactivarla.

El ajuste surte efecto de inmediato y se guarda automáticamente en `NR4AdaptiveNoise`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Adaptive Noise Estimation** | Casilla de verificación | Activado (True) | On / Off | `NR4AdaptiveNoise` |
| **Noise Estimation Method** | Botón de opción | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| **Reduction (dB):** | Control deslizante | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Smoothing (%):** | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| **Whitening (%):** | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| **Masking Depth:** | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| **Reset Defaults** | Botón | — | — | — |

**Adaptive Noise Estimation** controla si NR4 actualiza continuamente su modelo de piso de ruido. Cuando está activada, NR4 sigue el ruido que varía con el tiempo. Cuando está desactivada, el piso de ruido queda fijo en la estimación capturada en el momento en que NR4 fue inicializado por última vez.

**Noise Estimation Method** selecciona el algoritmo utilizado para estimar el piso de ruido. SPP-MMSE equilibra la estimación de ruido con la preservación de la voz; Brandt aplica suavizado recursivo sobre bandas de frecuencia críticas y es adecuado para ruido no estacionario; Martin utiliza mínimos espectrales en ejecución y es adecuado para pisos de ruido de variación lenta.

## Consejos

- Si el piso de ruido en su banda es estable y percibe artefactos de supresión que siguen la señal, pruebe desactivar **Adaptive Noise Estimation** y seleccione el método Martin, diseñado para pisos de ruido de variación lenta.
- Tras desactivar la estimación adaptativa, aumente **Smoothing (%):** para estabilizar la estimación fija del piso de ruido frente a fluctuaciones de corta duración.
- Haga clic en **Reset Defaults** para restablecer todos los controles de NR4 a sus valores de fábrica (SPP-MMSE, adaptativa activada, 10 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50).

## Temas relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
