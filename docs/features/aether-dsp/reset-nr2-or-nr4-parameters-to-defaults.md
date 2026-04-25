# Restablecer los parámetros de NR2 o NR4 a los valores predeterminados

Use esta página para restaurar todos los parámetros de reducción de ruido NR2 o NR4 a sus valores de fábrica con un solo clic. Esto es útil después de experimentar con la configuración y querer un punto de partida limpio.

## Antes de comenzar

- Abra AetherSDR. No se requiere conexión a un equipo de radio.

## Pasos

### Restablecer NR2

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña **NR2**.
3. Haga clic en **Reset Defaults**.

Todos los parámetros de NR2 vuelven a sus valores predeterminados de inmediato.

### Restablecer NR4

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña **NR4**.
3. Haga clic en **Reset Defaults**.

Todos los parámetros de NR4 vuelven a sus valores predeterminados de inmediato.

## Qué hace cada control

### Valores predeterminados de NR2 restaurados por Reset Defaults

| Control | Clave de configuración | Valor predeterminado |
|---|---|---|
| Gain Method | `NR2GainMethod` | Gamma |
| NPE Method | `NR2NpeMethod` | OSMS |
| AE Filter (eliminación de artefactos) | `NR2AeFilter` | Enabled |
| Reduction Depth: | `NR2GainMax` | 1.50 (rango 0.50–2.00) |
| Smoothing: | `NR2GainSmooth` | 0.85 (rango 0.50–0.98) |
| Voice Threshold: | `NR2Qspp` | 0.20 (rango 0.05–0.50) |

### Valores predeterminados de NR4 restaurados por Reset Defaults

| Control | Clave de configuración | Valor predeterminado |
|---|---|---|
| Noise Estimation Method | `NR4NoiseEstimationMethod` | SPP-MMSE |
| Adaptive Noise Estimation | `NR4AdaptiveNoise` | Enabled |
| Reduction (dB): | `NR4ReductionAmount` | 10.0 (rango 0.0–40.0 dB) |
| Smoothing (%): | `NR4SmoothingFactor` | 0 (rango 0–100) |
| Whitening (%): | `NR4WhiteningFactor` | 0 (rango 0–100) |
| Masking Depth: | `NR4MaskingDepth` | 0.50 (rango 0.00–1.00) |
| Suppression: | `NR4SuppressionStrength` | 0.50 (rango 0.00–1.00) |

## Consejos

- **Reset Defaults** se aplica únicamente a la pestaña que se está restableciendo en ese momento. Hacer clic en ella desde la pestaña NR2 no afecta la configuración de NR4, y viceversa.
- Los cambios surten efecto de inmediato; no se requiere confirmación ni ningún paso adicional para guardar.

## Relacionado

- [Descripción general de AetherDSP Settings](overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
