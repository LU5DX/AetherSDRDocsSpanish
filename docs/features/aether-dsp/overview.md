# Descripción general de AetherDSP Settings

AetherDSP Settings es el centro de control de reducción de ruido del lado del cliente en AetherSDR. Proporciona acceso detallado a cuatro motores DSP — NR2, NR4, MNR y DFNR — para que pueda ajustar el equilibrio entre la supresión de ruido y la fidelidad de la voz sin tocar el radio.

## Antes de comenzar

- No se requiere conexión al radio. AetherDSP Settings puede abrirse en cualquier momento.
- Decida qué motor desea ajustar. Si no está seguro de cuál motor se adapta a su situación, consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md).

## Cómo funciona

Abra AetherDSP Settings mediante `Settings > AetherDSP Settings...`. El diálogo contiene seis pestañas: **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** y **BNR**. Cada pestaña controla un motor de forma independiente. Los cambios surten efecto de inmediato y se guardan automáticamente — no existe un botón global Save.

### Pestaña NR2

NR2 es un motor de reducción de ruido musical en el dominio de la frecuencia. Sus controles permiten seleccionar la curva de ganancia, el estimador de potencia de ruido y la sensibilidad de detección de voz.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | Casilla de verificación | Activado | — | `NR2AeFilter` |
| Reduction Depth: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults | Botón | — | — | — |

**Gain Method** selecciona el mapeo de la curva de ganancia que se aplica durante la reducción de ruido. **NPE Method** selecciona el algoritmo que estima el piso de potencia de ruido. **AE Filter (artifact elimination)** aplica un postfiltro que reduce el repique y los artefactos de ruido musical. **Reduction Depth:** establece la profundidad máxima de supresión — valores más altos suprimen más ruido, pero pueden distorsionar la voz. **Smoothing:** controla la rapidez con que la estimación de ruido sigue los cambios de señal — valores más altos ofrecen una respuesta más estable pero más lenta. **Voice Threshold:** establece el umbral de probabilidad de presencia de voz — valores más bajos preservan la voz débil, pero pueden dejar pasar más ruido.

Haga clic en **Reset Defaults** para restaurar NR2 a: Gamma, OSMS, AE Filter activado, Reduction Depth 1.50, Smoothing 0.85, Voice Threshold 0.20.

### Pestaña NR4

NR4 utiliza la biblioteca libspecbleach para la reducción espectral de ruido. Expone un método de estimación de ruido, un modo adaptativo y varios controles de ajuste fino.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Noise Estimation Method | Botones de opción | SPP-MMSE | SPP-MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Activado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Control deslizante | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults | Botón | — | — | — |

**Noise Estimation Method** selecciona el algoritmo utilizado para estimar el piso de ruido. **Adaptive Noise Estimation** habilita la re-estimación continua a medida que cambian las condiciones. **Reduction (dB):** establece la reducción de ruido máxima aplicada. **Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido. **Whitening (%):** aplana la forma espectral de cualquier ruido residual. **Masking Depth:** controla la profundidad con que se aplica el enmascaramiento espectral. **Suppression:** establece la intensidad general de supresión de NR4.

Haga clic en **Reset Defaults** para restaurar NR4 a: SPP-MMSE, Adaptive Noise Estimation activado, 10.0 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

### Pestaña MNR

MNR es un motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Está disponible solo en macOS.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | Leído desde el motor de audio | — | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** activa el motor. **Strength** ajusta la agresividad: 0 es suave, 100 es la supresión máxima.

### Pestaña DFNR

DFNR utiliza DeepFilterNet3, un supresor de ruido basado en redes neuronales.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 dB | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** limita la atenuación de ruido máxima que aplica DeepFilterNet3. Establecerlo en 0 equivale a modo de paso directo; 100 es la atenuación máxima. **Post-Filter Beta** añade una etapa de postfiltro adicional para una supresión extra más allá de la salida de la red neuronal.

### Pestaña RN2

La pestaña RN2 cubre el motor RNNoise. Es solo informativa — no hay parámetros ajustables en esta pestaña.

### Pestaña BNR

La pestaña BNR cubre el motor de supresión de ruido de NVIDIA. La intensidad se controla desde el menú de superposición (overlay), no desde este diálogo.

## Consejos

- Todos los cambios se guardan de inmediato. No es necesario cerrar el diálogo para que la configuración surta efecto.
- El botón **Reset Defaults** de cada pestaña afecta únicamente los parámetros de esa pestaña, no los demás motores.
- Los controles de la pestaña MNR están activos solo en macOS. En otras plataformas la pestaña es visible, pero el motor no estará disponible.

## Relacionados

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Activar MNR en macOS y configurar su intensidad](enable-mnr-on-macos-and-set-its-strength.md)
- [Configurar el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Configurar el beta del postfiltro de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
