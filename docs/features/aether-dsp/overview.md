# Descripción general de AetherDSP Settings

AetherDSP Settings le brinda un control preciso sobre los motores de reducción de ruido del lado del cliente en AetherSDR. Use este diálogo para ajustar el equilibrio entre la supresión de ruido y la fidelidad de voz en cuatro motores configurables: NR2, NR4, MNR y DFNR.

## Antes de comenzar

- No se requiere conexión a una radio para abrir o ajustar AetherDSP Settings.
- Cada motor debe habilitarse por separado (desde el panel de applets o el menú de superposición) antes de que su configuración surta efecto.

## Cómo funciona

Abra el diálogo mediante `Settings > AetherDSP Settings...`. El diálogo contiene seis pestañas — **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** y **BNR** — cada una cubre un motor de reducción de ruido diferente. La configuración se guarda inmediatamente al cambiar cualquier control; no se requiere botón Apply ni OK.

### Pestaña NR2

NR2 es un motor de reducción de ruido musical en el dominio de la frecuencia. Sus parámetros controlan la agresividad con que se suprime el ruido y cómo el motor distingue entre voz y ruido.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction Depth: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |

- **Gain Method** selecciona el mapeo de la curva de ganancia aplicado durante la reducción de ruido. Gamma se adapta a los patrones de amplitud típicos de la voz; Trained usa un modelo construido a partir de muestras reales de voz y ruido.
- **NPE Method** selecciona el estimador de potencia de ruido. OSMS rastrea el piso de ruido mediante un mínimo continuo; MMSE minimiza el error de estimación esperado; NSTAT se adapta a ruido que cambia con el tiempo.
- **AE Filter (eliminación de artefactos)** activa o desactiva un postfiltro que reduce el timbre residual y los artefactos musicales comunes en el procesamiento de dominio de frecuencia.
- **Reduction Depth:** establece la profundidad máxima de supresión. Valores más altos suprimen más ruido, pero pueden distorsionar la voz.
- **Smoothing:** controla la rapidez con que la estimación de ruido sigue los cambios. Valores más altos dan una adaptación más estable pero más lenta.
- **Voice Threshold:** establece el umbral de probabilidad de presencia de voz. Valores más bajos preservan la voz débil, pero pueden dejar pasar más ruido.
- **Reset Defaults** restaura NR2 a: Gamma, OSMS, AE Filter activado, Reduction Depth 1.50, Smoothing 0.85, Voice Threshold 0.20.

### Pestaña NR4

NR4 utiliza la biblioteca libspecbleach para la reducción de ruido basada en sustracción espectral, con control independiente sobre la intensidad de supresión y la forma espectral.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Noise Estimation Method | Botones de opción | SPP-MMSE | SPP-MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Control deslizante | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

- **Noise Estimation Method** selecciona cómo NR4 estima el piso de ruido. SPP-MMSE equilibra la estimación de ruido con la preservación de voz; Brandt usa suavizado recursivo en bandas críticas; Martin usa mínimos espectrales continuos.
- **Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido a medida que cambian las condiciones.
- **Reduction (dB):** establece la reducción máxima de ruido en decibeles.
- **Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.
- **Whitening (%):** aplana la forma espectral del ruido residual.
- **Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.
- **Suppression:** establece la intensidad de supresión general de NR4.
- **Reset Defaults** restaura NR4 a: SPP-MMSE, Adaptive Noise Estimation activado, Reduction 10.0 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

### Pestaña MNR

MNR es un motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Está disponible únicamente en macOS.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | (leído del motor de audio) | — | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

- **Enable MNR (macOS only)** activa o desactiva el motor. El estado inicial refleja lo que el motor de audio reporta en el momento en que se abre el diálogo.
- **Strength** establece la agresividad desde suave (0) hasta máxima (100). El valor se persiste como un valor normalizado de 0.00 a 1.00.

### Pestaña DFNR

DFNR utiliza la red neuronal DeepFilterNet3 para la supresión profunda de ruido.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

- **Attenuation Limit** limita la atenuación máxima que aplica DeepFilterNet3. 0 es paso directo (passthrough); 100 es el máximo.
- **Post-Filter Beta** aplica un filtro de postprocesamiento adicional para una supresión extra más allá de la que proporciona la red neuronal.

### Pestaña RN2

La pestaña RN2 cubre el motor RNNoise. Es solo informativa; no hay parámetros ajustables en esta pestaña.

### Pestaña BNR

La pestaña BNR cubre la reducción de ruido de NVIDIA. La intensidad se controla desde el menú de superposición, no desde este diálogo.

## Consejos

- Los cambios surten efecto de inmediato; puede monitorear el audio mientras ajusta los controles deslizantes.
- En la pestaña NR2, reducir **Voice Threshold:** por debajo de su valor predeterminado (0.20) ayuda a recuperar voz débil o de baja potencia, pero puede aumentar el paso de ruido.
- En la pestaña NR4, dejar **Smoothing (%):** y **Whitening (%):** en 0 produce la salida con sonido más natural; auméntelos solo si el ruido residual resulta molesto.
- Use **Reset Defaults** en la pestaña NR2 o NR4 para recuperar una línea base conocida como correcta antes de experimentar.

## Relacionados

- [Elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Habilitar MNR en macOS y establecer su intensidad](enable-mnr-on-macos-and-set-its-strength.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Configurar el beta del postfiltro de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
