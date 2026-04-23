# Descripción general de AetherDSP Settings

AetherDSP Settings le ofrece control detallado sobre los motores de reducción de ruido del lado del cliente en AetherSDR. Úselo para equilibrar la supresión de ruido y la fidelidad de la voz en cuatro motores de procesamiento independientes: NR2, NR4, MNR y DFNR.

## Antes de comenzar

- No se requiere conexión a un radio para abrir o ajustar AetherDSP Settings.
- Decida qué motor desea configurar. Consulte [Cómo elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md) si no está seguro.

## Cómo funciona

Abra el diálogo en `Settings > AetherDSP Settings...`. Presenta seis pestañas — NR2, NR4, MNR, DFNR, RN2 y BNR — cada una correspondiente a un motor de reducción de ruido independiente. Los ajustes surten efecto de inmediato y se guardan automáticamente; no se requiere ningún paso explícito de guardado. Cada pestaña contiene un botón `Reset Defaults` (donde corresponde) que restaura los parámetros de esa pestaña a sus valores de fábrica.

- **NR2** — Motor en dominio de frecuencia enfocado en la reducción de ruido musical. Ofrece tres controles de algoritmo (Gain Method, NPE Method, AE Filter) y tres deslizadores de nivel.
- **NR4** — Basado en libspecbleach. Proporciona control de reducción calibrado en dB y varios parámetros de modelado espectral.
- **MNR** — Motor MMSE-Wiener disponible solo en macOS.
- **DFNR** — Utiliza la red neuronal DeepFilterNet3. Dos controles establecen la atenuación máxima y el post-filtrado opcional.
- **RN2** — Utiliza RNNoise. Esta pestaña es informativa; no tiene parámetros ajustables.
- **BNR** — Utiliza la reducción de ruido de NVIDIA. La intensidad se controla desde el menú superpuesto (overlay), no desde este diálogo.

## Qué hace cada control

### Pestaña NR2

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction Depth: | Deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults | Botón | — | — | — |

- **Gain Method** — Selecciona el mapeo de curva de ganancia que aplica NR2. Gamma es el valor predeterminado y modela patrones típicos de amplitud de voz. Linear y Log ofrecen escalado de amplitud más simple. Trained usa un modelo construido a partir de muestras de voz y ruido.
- **NPE Method** — Selecciona el estimador de potencia de ruido. OSMS (Optimal Smoothing Minimum Statistics) rastrea el piso de ruido mediante un mínimo continuo. MMSE minimiza el error de estimación esperado. NSTAT se adapta a ruido que cambia con el tiempo.
- **AE Filter (eliminación de artefactos)** — Activa o desactiva un post-filtro anti-artefactos que reduce el ringing y el ruido musical típicos del procesamiento en dominio de frecuencia.
- **Reduction Depth:** — Establece la profundidad máxima de reducción de NR2. Valores más altos suprimen más ruido, pero aumentan el riesgo de distorsión de la voz.
- **Smoothing:** — Controla con qué suavidad la estimación de ruido sigue los cambios de señal. Valores más altos producen una estimación más estable, pero de adaptación más lenta.
- **Voice Threshold:** — Establece el umbral de probabilidad de presencia de voz. Valores más bajos preservan la voz más débil, pero pueden dejar pasar más ruido.
- **Reset Defaults** — Restaura NR2 a: Gain Method = Gamma, NPE Method = OSMS, AE Filter = habilitado, Reduction Depth = 1.50, Smoothing = 0.85, Voice Threshold = 0.20.

### Pestaña NR4

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Noise Estimation Method | Botones de opción | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Deslizador | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Deslizador | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Deslizador | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Deslizador | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Deslizador | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults | Botón | — | — | — |

- **Noise Estimation Method** — Selecciona el estimador de piso de ruido de NR4. SPP-MMSE equilibra la estimación de ruido con la preservación de la voz. Brandt utiliza suavizado recursivo en bandas de frecuencia críticas y maneja bien el ruido no estacionario. Martin aplica mínimos espectrales continuos, adecuado para pisos de ruido de variación lenta.
- **Adaptive Noise Estimation** — Cuando está habilitado, el piso de ruido se re-estima continuamente durante la recepción.
- **Reduction (dB):** — Establece la reducción de ruido máxima que aplicará NR4, en decibeles.
- **Smoothing (%):** — Aplica suavizado en el dominio del tiempo a la estimación de ruido.
- **Whitening (%):** — Aplana la forma espectral del ruido residual después del procesamiento.
- **Masking Depth:** — Controla la profundidad del enmascaramiento espectral aplicado durante la supresión de ruido.
- **Suppression:** — Establece la intensidad general de supresión de NR4.
- **Reset Defaults** — Restaura NR4 a: SPP-MMSE, Adaptive Noise Estimation habilitado, Reduction = 10.0 dB, Smoothing = 0, Whitening = 0, Masking Depth = 0.50, Suppression = 0.50.

### Pestaña MNR

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | Leído del motor de audio | — | `MnrEnabled` |
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

- **Enable MNR (macOS only)** — Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Disponible solo en macOS.
- **Strength** — Establece la agresividad de MNR. 0 es mínima; 100 es la supresión máxima.

### Pestaña DFNR

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Attenuation Limit | Deslizador | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

- **Attenuation Limit** — Establece la atenuación de ruido máxima que aplicará DeepFilterNet3. 0 deja pasar la señal sin procesamiento; 100 aplica atenuación completa.
- **Post-Filter Beta** — Aplica un post-filtro adicional sobre la salida de DeepFilterNet3 para mayor supresión. Déjelo en 0.00 a menos que quede ruido residual después de ajustar Attenuation Limit.

### Pestaña RN2

Esta pestaña es informativa. RNNoise no tiene parámetros ajustables por el usuario en AetherDSP Settings.

### Pestaña BNR

Esta pestaña es informativa. La intensidad de BNR (NVIDIA) se controla desde el menú superpuesto (overlay), no desde este diálogo.

## Consejos

- Todos los cambios se guardan de inmediato. No es necesario cerrar el diálogo para aplicar un ajuste.
- Use `Reset Defaults` en la pestaña NR2 o NR4 para recuperar una línea base conocida antes de comparar cambios de parámetros.
- En la pestaña NR4, comience ajustando solo `Reduction (dB):` y `Suppression:`, dejando Smoothing, Whitening y Masking Depth en sus valores predeterminados, y luego refine desde ahí.
- MNR está disponible solo en macOS. La casilla `Enable MNR (macOS only)` reflejará el estado actual del motor de audio cuando se abra el diálogo.

## Temas relacionados

- [Cómo elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Habilitar MNR en macOS y configurar su intensidad](enable-mnr-on-macos-and-set-its-strength.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-at
