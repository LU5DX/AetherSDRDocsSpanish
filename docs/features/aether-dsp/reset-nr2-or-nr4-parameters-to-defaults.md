# Restablecer los parámetros de NR2 o NR4 a los valores predeterminados

Use esta página para restaurar todos los controles de reducción de ruido NR2 o NR4 a sus valores de fábrica con un solo clic, descartando cualquier ajuste experimental que haya realizado.

## Antes de comenzar

- Abra `Settings > AetherDSP Settings...` para acceder al diálogo AetherDSP Settings.

## Pasos

### Restablecer los valores predeterminados de NR2

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Haga clic en **Reset Defaults**.

Todos los controles de NR2 vuelven a los valores indicados en la tabla a continuación.

### Restablecer los valores predeterminados de NR4

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Haga clic en **Reset Defaults**.

Todos los controles de NR4 vuelven a los valores indicados en la tabla a continuación.

## Qué hace cada control

### Valores predeterminados de NR2 restaurados por Reset Defaults

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Gain Method | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Activado | — | `NR2AeFilter` |
| Reduction Depth: | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | 0.20 | 0.05–0.50 | `NR2Qspp` |

### Valores predeterminados de NR4 restaurados por Reset Defaults

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Noise Estimation Method | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Activado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

## Sugerencias

- **Reset Defaults** afecta únicamente la pestaña en la que se encuentra en ese momento. Al hacer clic en ella desde la pestaña NR2 no se modifica ningún ajuste de NR4, y viceversa.
- Los cambios surten efecto de inmediato; los valores actualizados se guardan en AppSettings en el momento en que los controles deslizantes y los botones se mueven.

## Relacionado

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
