# Descripción general de los ajustes de AetherDSP

Los ajustes de AetherDSP le dan acceso directo a los motores de reducción de ruido del lado del cliente integrados en AetherSDR. Úselos para ajustar el equilibrio entre la supresión de ruido y la fidelidad de voz en cuatro motores configurables: NR2, NR4, MNR y DFNR.

## Antes de comenzar

- No se requiere conexión a un radio para abrir este diálogo ni para modificar sus ajustes.
- Los cambios surten efecto de inmediato y se guardan automáticamente — no existe un botón Save separado.

## Cómo funciona

Abra el diálogo mediante `Settings > AetherDSP Settings...`. Contiene seis pestañas, una por motor. Solo NR2, NR4, MNR y DFNR exponen parámetros ajustables; RN2 y BNR son informativos o se controlan desde otro lugar.

### Pestaña NR2

NR2 es un motor de reducción de ruido musical en el dominio de la frecuencia. Sus controles determinan la agresividad con que suprime el ruido y la precisión con que rastrea la voz.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction Depth: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults | Botón | — | — | — |

**Gain Method** selecciona el mapeo de la curva de ganancia aplicado durante la reducción de ruido. Gamma se ajusta a los patrones típicos de amplitud del habla y es el valor predeterminado. Trained utiliza un modelo construido a partir de muestras reales de voz y ruido.

**NPE Method** selecciona el estimador de potencia de ruido. OSMS rastrea el piso de ruido mediante un mínimo continuo. MMSE minimiza el error de estimación esperado. NSTAT se adapta al ruido que varía con el tiempo.

**AE Filter (artifact elimination)** aplica un postfiltro para reducir el timbre (ringing) y los artefactos musicales frecuentes en la reducción de ruido en el dominio de la frecuencia.

**Reduction Depth:** establece la supresión máxima de ganancia aplicada. Valores más altos eliminan más ruido, pero pueden distorsionar la voz.

**Smoothing:** controla la rapidez con que la estimación de ruido sigue los cambios en la señal. Valores más altos producen una estimación más estable, pero de adaptación más lenta.

**Voice Threshold:** establece el umbral de probabilidad de presencia de voz por debajo del cual NR2 trata la señal como ruido. Valores más bajos preservan la voz débil, pero pueden dejar pasar más ruido.

**Reset Defaults** restaura la pestaña NR2 a: Gain Method = Gamma, NPE Method = OSMS, AE Filter habilitado, Reduction Depth = 1.50, Smoothing = 0.85, Voice Threshold = 0.20.

---

### Pestaña NR4

NR4 utiliza la biblioteca libspecbleach para la reducción de ruido basada en sustracción espectral. Sus controles se expresan en dB y porcentajes.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Noise Estimation Method | Botones de opción | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Control deslizante | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults | Botón | — | — | — |

**Noise Estimation Method** selecciona el estimador del piso de ruido de NR4. SPP-MMSE equilibra la estimación de ruido con la preservación de la voz. Brandt utiliza suavizado recursivo en bandas de frecuencia críticas. Martin utiliza mínimos espectrales continuos, adecuado para pisos de ruido de variación lenta.

**Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido a medida que cambian las condiciones.

**Reduction (dB):** establece la reducción de ruido máxima aplicada, en decibeles.

**Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.

**Whitening (%):** aplana la forma espectral del ruido residual tras la reducción.

**Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado durante la reducción.

**Suppression:** establece la intensidad de supresión general de NR4.

**Reset Defaults** restaura la pestaña NR4 a: Noise Estimation Method = SPP-MMSE, Adaptive Noise Estimation habilitado, Reduction = 10.0 dB, Smoothing = 0, Whitening = 0, Masking Depth = 0.50, Suppression = 0.50.

---

### Pestaña MNR

MNR es un motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Está disponible únicamente en macOS.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | Leído del motor de audio | — | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** activa el motor MNR. Su estado inicial refleja si MNR está actualmente activo en el motor de audio.

**Strength** ajusta la agresividad de MNR. 0 es la configuración más suave; 100 es la supresión máxima. El valor se guarda internamente como un valor normalizado de 0.00–1.00.

---

### Pestaña DFNR

DFNR utiliza el modelo de aprendizaje profundo DeepFilterNet3 para la reducción de ruido.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** limita la atenuación de ruido máxima que aplica DeepFilterNet3. 0 deja pasar la señal sin modificación; 100 permite la atenuación máxima.

**Post-Filter Beta** aplica un postfiltro adicional sobre la salida de DeepFilterNet3 para obtener supresión extra. 0.00 deshabilita el postfiltro.

---

### Pestaña RN2

La pestaña RN2 (motor RNNoise) es solo informativa. No contiene parámetros ajustables.

---

### Pestaña BNR

La pestaña BNR (reducción de ruido NVIDIA) es solo informativa. La intensidad de BNR se controla desde el menú superpuesto (overlay), no desde este diálogo.

---

## Consejos

- Todos los cambios se guardan de inmediato. No es necesario cerrar el diálogo para escuchar el efecto.
- Use **Reset Defaults** en la pestaña NR2 o NR4 para recuperar un punto de partida conocido antes de experimentar.
- En NR2, aumentar **Reduction Depth:** mientras se reduce **Voice Threshold:** incrementa la agresividad, pero también el riesgo de artefactos en la voz. Habilite **AE Filter (artifact elimination)** para mitigar esto.
- En NR4, mantenga **Adaptive Noise Estimation** habilitado para señales donde el piso de ruido varía — por ejemplo, durante condiciones de apertura de banda.
- El rango de **Post-Filter Beta** de DFNR es 0.00–0.30. Los incrementos pequeños tienen un efecto notable; comience en 0.05 y aumente gradualmente.

## Temas relacionados

- [Elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Habilitar MNR en macOS y configurar su intensidad](enable-mnr-on-macos-and-set-its-strength.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Configurar el beta del postfiltro de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
