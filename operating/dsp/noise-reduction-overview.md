# Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR ofrece cuatro motores de reducción de ruido en el lado del cliente — NR2, NR4, DFNR y MNR — cada uno con diferentes fortalezas. Esta página describe qué hace cada motor y cuándo conviene usar uno en lugar de otro, para que pueda elegir el punto de partida correcto antes de ajustar los parámetros.

## Antes de comenzar

- No se requiere conexión a radio para abrir o ajustar estos ajustes.
- Abra `Settings > AetherDSP Settings...` para acceder a los cuatro motores.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña del motor que desea usar: **NR2**, **NR4**, **DFNR** o **MNR**.
3. Ajuste los controles según sea necesario (consulte la tabla a continuación).
4. Cierre el diálogo. Los ajustes se guardan inmediatamente al cambiar cualquier control.

## Qué hace cada control

### Pestaña NR2 — reducción de ruido musical

NR2 utiliza un enfoque de ganancia espectral para suprimir el ruido. Es ajustable y funciona en todas las plataformas.

| Control | Valor predeterminado | Rango | Clave de ajuste | Qué hace |
|---|---|---|---|---|
| Gain Method | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` | Selecciona el mapeo de la curva de ganancia. Gamma es adecuado para la mayoría de las señales de voz. Trained usa un modelo construido a partir de muestras reales de voz y ruido. |
| NPE Method | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. OSMS rastrea un mínimo continuo; MMSE minimiza el error de estimación; NSTAT se adapta a ruido cambiante. |
| AE Filter (eliminación de artefactos) | On | On / Off | `NR2AeFilter` | Reduce el timbre residual y los artefactos de ruido musical. Déjelo activado a menos que note efectos no deseados. |
| Reduction Depth: | 1.50 | 0.50–2.00 | `NR2GainMax` | Profundidad máxima de supresión. Valores más altos eliminan más ruido, pero pueden distorsionar la voz. |
| Smoothing: | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Velocidad con la que la estimación de ruido rastrea los cambios. Valores más altos son más estables, pero más lentos para adaptarse. |
| Voice Threshold: | 0.20 | 0.05–0.50 | `NR2Qspp` | Umbral de probabilidad de presencia de voz. Valores más bajos preservan la voz débil, pero pueden dejar pasar más ruido. |
| Reset Defaults | — | — | — | Restaura Gain Method a Gamma, NPE Method a OSMS, AE Filter activado y los deslizadores a 1.50 / 0.85 / 0.20. |

### Pestaña NR4 — libspecbleach

NR4 aplica blanqueamiento espectral y funciona bien con ruido continuo y de banda ancha. La profundidad de reducción se expresa en dB, lo que permite un control preciso.

| Control | Valor predeterminado | Rango | Clave de ajuste | Qué hace |
|---|---|---|---|---|
| Noise Estimation Method | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido. SPP-MMSE equilibra la estimación de ruido con la preservación de la voz; Brandt es adecuado para ruido no estacionario; Martin es adecuado para pisos de ruido que varían lentamente. |
| Adaptive Noise Estimation | On | On / Off | `NR4AdaptiveNoise` | Reestima continuamente el piso de ruido a medida que cambian las condiciones. |
| Reduction (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` | Reducción máxima de ruido en dB. |
| Smoothing (%): | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido. |
| Whitening (%): | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual después de la reducción. |
| Masking Depth: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad de enmascaramiento espectral. |
| Suppression: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión de NR4. |
| Reset Defaults | — | — | — | Restaura SPP-MMSE, estimación adaptativa activada, 10 dB, 0, 0, 0.50, 0.50. |

### Pestaña DFNR — DeepFilterNet3

DFNR utiliza una red neuronal profunda (DeepFilterNet3) para la supresión de ruido. Es la opción más agresiva y funciona mejor cuando el piso de ruido es continuo y la señal es voz.

| Control | Valor predeterminado | Rango | Clave de ajuste | Qué hace |
|---|---|---|---|---|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` | Atenuación máxima aplicada por DeepFilterNet3. Establézcalo en 0 para paso directo; 100 para supresión máxima. |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un postfiltro adicional después de DeepFilterNet3 para supresión extra. |

### Pestaña MNR — solo macOS

MNR es un motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico, disponible solo en macOS.

| Control | Valor predeterminado | Rango | Clave de ajuste | Qué hace |
|---|---|---|---|---|
| Enable MNR (macOS only) | (leído del motor de audio) | On / Off | `MnrEnabled` | Habilita MNR. |
| Strength | 100 | 0–100 | `MnrStrength` | Agresividad. 0 es suave; 100 es máximo. Se almacena como un valor normalizado de 0.00–1.00. |

## Consejos

- Use **NR2** cuando desee control detallado sobre la detección de voz y el comportamiento de ganancia, o cuando el ruido sea intermitente.
- Use **NR4** cuando el ruido sea de banda ancha y estable, y desee establecer un objetivo de reducción preciso en dB.
- Use **DFNR** para la supresión más potente en señales de voz, especialmente en presencia de QRM intenso o ruido atmosférico. Comience con **Attenuation Limit** por debajo de 100 y auméntelo solo según sea necesario para evitar el sobreprocesamiento.
- Use **MNR** en macOS cuando prefiera una opción más ligera e integrada con el sistema.
- Solo un motor está activo por ruta de recepción a la vez; el motor activo se selecciona en otro lugar de la interfaz, no en este diálogo. Este diálogo únicamente ajusta los parámetros de cada motor.
- Haga clic en **Reset Defaults** en la pestaña NR2 o NR4 para recuperar una línea base conocida si los ajustes producen artefactos no deseados.

## Relacionados

- [Descripción general de AetherDSP Settings](../../features/aether-dsp/overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz en NR2](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](../../features/aether-dsp/adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](../../features/aether-dsp/enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](../../features/aether-dsp/tune-nr4-masking-depth-and-suppression-strength.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](../../features/aether-dsp/set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Configurar el beta del postfiltro de DFNR para supresión adicional](../../features/aether-dsp/configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Habilitar MNR en macOS y ajustar su intensidad](../../features/aether-dsp/enable-mnr-on-macos-and-set-its-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](../../features/aether-dsp/reset-nr2-or-nr4-parameters-to-defaults.md)
