# Habilitar o deshabilitar la estimación adaptativa de ruido de NR4

Esta página explica cómo activar o desactivar la re-estimación continua del piso de ruido de NR4. Con la estimación adaptativa de ruido habilitada, NR4 rastrea los cambios en el entorno de ruido en tiempo real; deshabilitarla fija la estimación del piso de ruido en una instantánea estática, lo que puede ser adecuado para condiciones de ruido muy estables.

## Antes de comenzar

- AetherSDR no necesita estar conectado a un radio para ajustar la configuración DSP.
- NR4 debe estar ya activo en su slice de recepción para que estos cambios tengan un efecto audible.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation** para habilitar o deshabilitar la re-estimación continua del piso de ruido.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR4AdaptiveNoise`.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Adaptive Noise Estimation** | Habilitado (marcado) | Marcado / desmarcado | `NR4AdaptiveNoise` |
| **Noise Estimation Method** | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

## Consejos

- Si el piso de ruido en su banda es estable y consistente, desmarcar **Adaptive Noise Estimation** puede evitar que el estimador siga los cambios en el nivel de señal y clasifique erróneamente el habla como ruido.
- Si el piso de ruido varía rápidamente — por ejemplo, durante aperturas de banda o con ruido impulsivo — deje **Adaptive Noise Estimation** marcado para que NR4 pueda seguir las condiciones cambiantes.
- El selector **Noise Estimation Method** (SPP-MMSE, Brandt, Martin) determina cómo NR4 construye su modelo de ruido, independientemente de si el modo adaptativo está activado o desactivado. Cambiar el método puede afectar qué tan bien la estimación estática o adaptativa rastrea su piso de ruido.
- Haga clic en **Reset Defaults** en la pestaña NR4 para restablecer todos los controles de NR4 a sus valores de fábrica (adaptativo activado, SPP-MMSE, 10 dB, 0, 0, 0.50, 0.50).

## Relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
