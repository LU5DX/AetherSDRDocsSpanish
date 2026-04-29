# Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR ofrece cuatro motores de reducción de ruido del lado del cliente. Esta página describe qué hace cada motor, cuándo usarlo y dónde encontrar sus controles, para que pueda elegir el más adecuado según sus condiciones de operación.

## Antes de comenzar

- Abra AetherDSP Settings mediante `Settings > AetherDSP Settings...`.
- El motor NR que configure aquí es exclusivamente del lado del cliente; no requiere conexión a un equipo de radio.

## Pasos

1. Vaya a `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña del motor que desee usar: **NR2**, **NR4**, **DFNR** o **MNR**.
3. Ajuste los controles de esa pestaña (consulte la tabla a continuación).
4. Cierre el diálogo. Los ajustes se guardan automáticamente.

## Qué hace cada control

### NR2 — reducción de ruido musical

Un reductor de ruido en el dominio de la frecuencia diseñado para minimizar los artefactos tonales tipo "birdie" comunes en la sustracción espectral. Es una buena opción inicial para voz SSB con QRN moderado.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction Depth: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults | Botón | — | — | — |

**Gain Method** selecciona cómo NR2 mapea las estimaciones de ruido a la reducción de ganancia. Gamma se ajusta a los patrones típicos de amplitud del habla y es el valor predeterminado. Trained utiliza un modelo construido a partir de muestras reales de voz y ruido. Linear y Log intercambian precisión perceptual por un cálculo más simple.

**NPE Method** selecciona el estimador de potencia de ruido. OSMS (Optimal Smoothing Minimum Statistics) rastrea el piso de ruido usando un mínimo continuo y es adecuado para ruido que varía lentamente. MMSE minimiza el error de estimación esperado. NSTAT se adapta a ruido que cambia rápidamente con el tiempo.

**AE Filter (artifact elimination)** aplica un postfiltro para reducir el timbre y los artefactos musicales. Déjelo habilitado a menos que esté experimentando con valores muy bajos de Reduction Depth.

**Reduction Depth:** controla la supresión máxima. Valores más altos eliminan más ruido, pero pueden distorsionar la voz. El valor predeterminado es 1.50.

**Smoothing:** controla la rapidez con que la estimación de ruido sigue los cambios. Valores más altos son más estables, pero se adaptan más lentamente.

**Voice Threshold:** es el umbral de probabilidad de presencia de voz. Valores más bajos protegen la voz débil, pero pueden dejar pasar más ruido.

**Reset Defaults** restaura: Gamma / OSMS / AE Filter activado / 1.50 / 0.85 / 0.20.

---

### NR4 — libspecbleach

Un motor de blanqueo espectral independiente con su propio estimador de ruido y controles de forma adicionales. Resulta útil cuando NR2 deja ruido residual o cuando se desean objetivos de reducción calibrados en dB.

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

**Noise Estimation Method** — SPP-MMSE equilibra la estimación de ruido con la preservación de la voz. Brandt utiliza suavizado recursivo sobre bandas de frecuencia críticas y es adecuado para ruido no estacionario. Martin utiliza mínimos espectrales continuos y es robusto para pisos de ruido que varían lentamente.

**Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido. Deshabilítelo solo si el entorno de ruido es estático y desea un piso fijo.

**Reduction (dB):** establece la reducción máxima en dB. Comience con 10 dB y aumente si el ruido persiste.

**Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.

**Whitening (%):** aplana la forma espectral del ruido residual después de la reducción.

**Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.

**Suppression:** establece la intensidad de supresión general. Valores más altos son más agresivos.

**Reset Defaults** restaura: SPP-MMSE / Adaptive activado / 10.0 dB / 0 / 0 / 0.50 / 0.50.

---

### DFNR — DeepFilterNet3

Un filtro de ruido basado en redes neuronales. Es adecuado para ruido de banda ancha intenso donde los métodos espectrales convencionales son insuficientes. Tiene el mayor costo de CPU de los cuatro motores.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 dB | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación de ruido máxima que aplicará DeepFilterNet3. 0 es paso directo (passthrough); 100 es atenuación máxima. Reduzca este valor si el filtro neuronal suprime en exceso señales débiles.

**Post-Filter Beta** agrega una etapa de supresión adicional sobre la salida del filtro neuronal. Déjelo en 0.00 a menos que quede ruido residual después de ajustar Attenuation Limit.

---

### MNR — solo macOS

Un reductor de ruido MMSE-Wiener con suavizado de ganancia asimétrico, disponible únicamente en macOS.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | (leído del motor de audio) | — | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** activa o desactiva el motor. El estado inicial refleja el estado actual del motor de audio.

**Strength** establece la agresividad. 0 es la más suave; 100 es la máxima. Se almacena internamente como un valor normalizado de 0.00 a 1.00.

MNR no está disponible en Linux ni en Windows. La pestaña **MNR** sigue presente, pero **Enable MNR (macOS only)** no tendrá efecto en sistemas que no sean macOS.

## Consejos

- Ejecute solo un motor de reducción de ruido a la vez. Encadenar varios motores puede causar artefactos en la voz y aumenta la carga de CPU.
- Para voz SSB con ruido de banda moderado, comience con NR2 en sus valores predeterminados antes de probar NR4 o DFNR.
- Si usa macOS y prefiere una menor carga de CPU, MNR es la opción con menor consumo de recursos.
- El Attenuation Limit de DFNR en 100 dB puede suprimir señales muy débiles junto con el ruido. Redúzcalo a 40–60 dB en trayectos marginales.
- En la pestaña NR2, si la voz suena hueca o "bajo el agua", reduzca **Reduction Depth:** hacia 0.80–1.00 o cambie **Gain Method** de Gamma a Log.
- Use **Reset Defaults** en las pestañas NR2 o NR4 para recuperar un punto de partida conocido y válido después de cambios experimentales.

## Solución de problemas

- **La voz suena hueca o se perciben artefactos musicales en NR2** — Reduzca **Reduction Depth:** o confirme que **AE Filter (artifact elimination)** esté habilitado.
- **NR4 no reduce suficientemente el ruido** — Aumente **Reduction (dB):** y habilite **Adaptive Noise Estimation** si está desactivado.
- **DFNR elimina señales débiles junto con el ruido** — Baje **Attenuation Limit** de 100 hacia 40–60 dB.
- **La pestaña MNR está presente pero no tiene efecto** — MNR es exclusivo de macOS. En Linux o Windows, use NR2, NR4 o DFNR en su lugar.
- **Los ajustes de NR2 o NR4 no se conservaron tras el reinicio** — Los ajustes se guardan automáticamente en cada cambio de control. Si los valores se revierten, haga clic en **Reset Defaults** y vuelva a ingresar los valores deseados para forzar el guardado.

## Relacionado

- [Descripción general de AetherDSP Settings](../../features/aether-dsp/overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](../../features/aether-dsp/adjust-
