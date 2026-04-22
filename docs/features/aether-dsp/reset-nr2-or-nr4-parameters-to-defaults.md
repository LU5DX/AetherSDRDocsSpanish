# Restablecer los parámetros de NR2 o NR4 a los valores predeterminados

Use esta página para restaurar todos los controles de NR2 o NR4 a sus valores de fábrica con un solo clic, deshaciendo cualquier cambio experimental sin necesidad de ajustar cada control individualmente.

## Antes de comenzar

- Abra `Settings > AetherDSP Settings...` para acceder al diálogo AetherDSP Settings.
- Identifique el motor que desea restablecer: NR2 o NR4 (o ambos).

## Pasos

### Restablecer NR2

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Haga clic en **Reset Defaults**.

Todos los controles de NR2 vuelven a sus valores predeterminados de inmediato.

### Restablecer NR4

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Haga clic en **Reset Defaults**.

Todos los controles de NR4 vuelven a sus valores predeterminados de inmediato.

## Qué hace cada control

### Valores predeterminados de NR2 restaurados por Reset Defaults

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Gain Method | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Habilitado | — | `NR2AeFilter` |
| Reduction Depth: | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | 0.20 | 0.05–0.50 | `NR2Qspp` |

### Valores predeterminados de NR4 restaurados por Reset Defaults

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Noise Estimation Method | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

## Sugerencias

- **Reset Defaults** afecta únicamente la pestaña que se muestra en ese momento. Al hacer clic en ella desde la pestaña NR2 no se modifican los ajustes de NR4, y viceversa.
- Los cambios surten efecto de inmediato; no hay confirmación ni posibilidad de deshacer. Si desea conservar una configuración que funciona correctamente, anote los valores actuales antes de hacer clic en **Reset Defaults**.

## Relacionado

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
