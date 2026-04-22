# Descripción general de la configuración de AetherDSP

El diálogo AetherDSP Settings expone los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR. Úselo para equilibrar la supresión de ruido con la fidelidad de voz en cuatro motores configurables: NR2, NR4, MNR y DFNR.

## Antes de comenzar

- No se requiere conexión a una radio. El diálogo puede abrirse en cualquier momento.
- Identifique qué motor de reducción de ruido desea ajustar. Consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md) si no está seguro.

## Cómo funciona

Abra el diálogo con `Settings > AetherDSP Settings...`. El diálogo contiene seis pestañas — **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** y **BNR** — cada una cubre un motor de procesamiento independiente. Los cambios surten efecto de inmediato y se guardan automáticamente; no se requiere ningún botón Save. Cada pestaña también incluye un botón **Reset Defaults** (NR2 y NR4) para restaurar los valores de fábrica.

### Pestaña NR2

NR2 es un motor de reducción de ruido musical en el dominio de la frecuencia. Aplica una curva de ganancia para suprimir el ruido intentando preservar la voz.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Gain Method | Botón de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botón de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | Casilla de verificación | Activado | — | `NR2AeFilter` |
| Reduction Depth: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |

- **Gain Method** selecciona el mapeo de la curva de ganancia que se aplica durante la reducción de ruido. Gamma coincide con los patrones típicos de amplitud de voz y es el valor predeterminado. Linear y Log ofrecen mapeos más simples; Trained utiliza un modelo entrenado con muestras reales de voz y ruido.
- **NPE Method** selecciona el estimador de potencia de ruido. OSMS (Optimal Smoothing Minimum Statistics) rastrea el piso de ruido mediante un mínimo continuo. MMSE minimiza el error de estimación esperado. NSTAT se adapta al ruido que cambia con el tiempo.
- **AE Filter (artifact elimination)** activa o desactiva un postfiltro que reduce el repique y los artefactos de ruido musical comunes en la reducción de ruido en el dominio de la frecuencia.
- **Reduction Depth:** establece la reducción de ganancia máxima que NR2 puede aplicar. Valores más altos suprimen más ruido, pero aumentan el riesgo de distorsión de voz.
- **Smoothing:** controla la rapidez con que la estimación de ruido sigue los cambios de señal. Valores más altos producen una estimación más estable, pero de adaptación más lenta.
- **Voice Threshold:** establece el umbral de probabilidad de presencia de voz. Valores más bajos preservan la voz débil, pero pueden permitir que pase más ruido.
- **Reset Defaults** restaura todos los controles de NR2 a: Gain Method = Gamma, NPE Method = OSMS, AE Filter activado, Reduction Depth = 1.50, Smoothing = 0.85, Voice Threshold = 0.20.

### Pestaña NR4

NR4 utiliza la biblioteca libspecbleach para la reducción de ruido basada en sustracción espectral. Ofrece un control más directo sobre la profundidad de reducción en dB.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Noise Estimation Method | Botón de opción | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Activado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Control deslizante | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

- **Noise Estimation Method** selecciona el estimador del piso de ruido. SPP-MMSE equilibra la estimación de ruido con la preservación de voz. Brandt utiliza suavizado recursivo entre bandas de frecuencia críticas, adecuado para ruido no estacionario. Martin utiliza mínimos espectrales continuos, adecuado para pisos de ruido de variación lenta.
- **Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido a medida que cambian las condiciones.
- **Reduction (dB):** establece la reducción de ruido máxima que NR4 aplicará, en decibelios.
- **Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.
- **Whitening (%):** aplana la forma espectral del ruido residual tras la reducción.
- **Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado durante la supresión.
- **Suppression:** establece la fuerza de supresión general de NR4.
- **Reset Defaults** restaura todos los controles de NR4 a: Noise Estimation Method = SPP-MMSE, Adaptive Noise Estimation activado, Reduction = 10.0 dB, Smoothing = 0, Whitening = 0, Masking Depth = 0.50, Suppression = 0.50.

### Pestaña MNR

MNR es un reductor de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Solo está disponible en macOS.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | Leído desde el motor de audio | — | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

- **Enable MNR (macOS only)** activa o desactiva el motor MNR. El estado inicial refleja el estado actual del motor de audio.
- **Strength** ajusta la agresividad. 0 es suave; 100 es la supresión máxima. Se guarda internamente como un valor normalizado de 0.00–1.00.

### Pestaña DFNR

DFNR utiliza el modelo de aprendizaje profundo DeepFilterNet3 para la reducción de ruido.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

- **Attenuation Limit** establece la atenuación de ruido máxima que DeepFilterNet3 aplicará. 0 es paso directo (passthrough); 100 es la atenuación máxima.
- **Post-Filter Beta** aplica un postfiltro adicional sobre la salida de DeepFilterNet3 para una supresión extra. 0.00 desactiva el postfiltro.

### Pestaña RN2

La pestaña RN2 cubre el motor RNNoise. Es únicamente informativa; no hay parámetros ajustables en esta pestaña.

### Pestaña BNR

La pestaña BNR cubre el motor de reducción de ruido de NVIDIA. La intensidad de BNR se controla desde el menú superpuesto (overlay menu), no desde este diálogo.

## Consejos

- Ajuste un parámetro a la vez y observe el efecto en una señal en vivo antes de cambiar otro.
- En la pestaña NR2, si escucha artefactos de ruido musical tras aumentar Reduction Depth, asegúrese de que **AE Filter (artifact elimination)** esté activado.
- En la pestaña NR4, si el piso de ruido cambia rápidamente (por ejemplo, en operación móvil), active **Adaptive Noise Estimation** y pruebe el estimador Brandt o SPP-MMSE.
- **Reset Defaults** en la pestaña NR2 o NR4 es una forma rápida de recuperar un punto de partida conocido como válido sin necesidad de volver a abrir el diálogo desde cero.

## Relacionados

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz en NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación adaptativa de ruido en NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión en NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Activar MNR en macOS y configurar su intensidad](enable-mnr-on-macos-and-set-its-strength.md)
- [Configurar el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Configurar el beta del postfiltro de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
