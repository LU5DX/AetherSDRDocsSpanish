# Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR ofrece cuatro motores de reducción de ruido del lado del cliente — NR2, NR4, DFNR y MNR — cada uno adecuado para diferentes condiciones de señal y tipos de ruido. Esta página explica qué hace cada motor y cómo decidir cuál usar, y muestra dónde configurarlo.

## Antes de comenzar

- No se requiere conexión de radio para abrir o ajustar AetherDSP Settings.
- MNR está disponible únicamente en macOS.
- DFNR utiliza DeepFilterNet3; confirme que su sistema cumple los requisitos de CPU antes de habilitarlo con alta atenuación.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña del motor que desea usar: **NR2**, **NR4**, **MNR** o **DFNR**.
3. Ajuste los controles de ese motor (consulte la tabla a continuación).
4. Para restablecer cualquier motor a los valores de fábrica, haga clic en **Reset Defaults** en la parte inferior de su pestaña (disponible en NR2 y NR4).

## Qué hace cada control

### Pestaña NR2

NR2 es un motor de reducción de ruido musical en el dominio de la frecuencia. Úselo cuando desee un control preciso sobre cuán agresivamente se suprime el ruido en relación con la fidelidad de la voz.

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Gain Method | Botón de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botón de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | Casilla de verificación | Activado | — | `NR2AeFilter` |
| Reduction Depth: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |

**Gain Method** selecciona el mapeo de la curva de ganancia aplicado a cada bin de frecuencia. Gamma se ajusta a los patrones típicos de amplitud de voz y es el valor predeterminado. Trained usa un modelo construido a partir de muestras reales de voz y ruido, lo que puede ofrecer mejor rendimiento con tipos de ruido reconocibles. Linear y Log ofrecen mapeos progresivamente más simples.

**NPE Method** selecciona cómo NR2 estima el piso de ruido. OSMS rastrea el piso mediante un mínimo progresivo y funciona bien con ruido estacionario. MMSE minimiza el error de estimación esperado. NSTAT se adapta al ruido que cambia con el tiempo.

**AE Filter (artifact elimination)** aplica un postfiltro que reduce los artefactos de timbre y ruido musical. Déjelo activado a menos que esté evaluando la salida sin procesar de NR2.

**Reduction Depth:** establece cuánto puede atenuar el ruido NR2. Los valores más altos suprimen más ruido, pero aumentan el riesgo de distorsión de la voz.

**Smoothing:** controla con qué rapidez reacciona la estimación de ruido a los cambios. Los valores más altos son más estables, pero se adaptan más lentamente.

**Voice Threshold:** establece el umbral de probabilidad de presencia de voz por debajo del cual un bin se trata como ruido. Los valores más bajos preservan la voz débil, pero pueden dejar pasar más ruido.

---

### Pestaña NR4

NR4 utiliza la biblioteca libspecbleach. Expone controles separados para el método de estimación de ruido, el seguimiento adaptativo y el modelado espectral. Use NR4 cuando desee una reducción calibrada explícitamente en dB y control sobre el color del ruido residual.

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Noise Estimation Method | Botón de opción | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Activado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Control deslizante | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

**Noise Estimation Method** selecciona el estimador del piso de ruido. SPP-MMSE equilibra la estimación de ruido con la preservación de la voz. Brandt usa suavizado recursivo a través de bandas de frecuencia críticas y maneja bien el ruido no estacionario. Martin rastrea los mínimos espectrales progresivos y es robusto para pisos de ruido que varían lentamente.

**Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido. Desactívelo solo si el piso de ruido es estable y desea fijar una estimación inicial.

**Reduction (dB):** establece la atenuación máxima que aplicará NR4. 10 dB es un punto de partida conservador; aumente hacia 40 dB para ruido intenso, aceptando mayor procesamiento.

**Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido. 0 significa que no hay suavizado adicional más allá del que proporciona el método de estimación.

**Whitening (%):** aplana la forma espectral del ruido residual. Los valores más altos hacen que el ruido restante suene más uniforme en lugar de tonal.

**Masking Depth:** controla la profundidad con la que se aplica el enmascaramiento espectral a los bins de ruido.

**Suppression:** establece la intensidad general de supresión de NR4 en todo el espectro.

---

### Pestaña DFNR

DFNR ejecuta DeepFilterNet3, un supresor basado en redes neuronales. Requiere más CPU que NR2 o NR4, pero puede manejar de manera eficaz el ruido complejo y no estacionario. Use DFNR cuando los otros motores dejen ruido estructurado audible.

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación máxima de ruido que aplicará DeepFilterNet3. 0 es modo de paso; 100 es el máximo. Reduzca este valor si escucha audio con procesamiento excesivo o sonido hueco.

**Post-Filter Beta** aplica un postfiltro adicional sobre la salida de la red neuronal para una supresión extra. 0.00 desactiva el postfiltro. Auméntelo con precaución; los valores más altos pueden introducir artefactos.

---

### Pestaña MNR (solo macOS)

MNR es un reductor de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Solo funciona en macOS.

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | (leído del motor de audio) | — | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** activa o desactiva el motor. Su estado inicial refleja el estado actual del motor de audio.

**Strength** ajusta la agresividad. 0 es suave; 100 es la supresión máxima. `MnrStrength` se almacena como un valor normalizado entre 0.00 y 1.00.

---

## Consejos

- Comience con NR2 en los ajustes predeterminados (Gamma / OSMS / AE activado / Reduction Depth 1.50) para trabajo de voz SSB típico. Preserva la naturalidad de la voz mejor que un corte plano en dB.
- Si el piso de ruido cambia durante un contacto (QSB, aperturas de banda), habilite **Adaptive Noise Estimation** en NR4 o cambie **NPE Method** en NR2 a NSTAT.
- Use **Whitening (%)** en NR4 para reducir el ruido residual tonal o "chispeante" sin aumentar la reducción general.
- Establezca **Attenuation Limit** de DFNR en un valor más bajo (40–60) antes de experimentar hacia arriba; en 100 aplica la supresión neural máxima, lo que puede hacer que las señales débiles suenen procesadas.
- En macOS, puede combinar MNR con NR2 o NR4 si es necesario, pero comience con un solo motor a la vez para escuchar lo que aporta cada uno.
- Haga clic en **Reset Defaults** en la pestaña NR2 o NR4 en cualquier momento para volver a los valores de fábrica mostrados en las tablas anteriores.

## Solución de problemas

- **La voz suena hueca o robótica** — La reducción es demasiado alta. En NR2, baje **Reduction Depth:** por debajo de 1.50. En NR4, reduzca **Reduction (dB):** o baje **Suppression:**. En DFNR, reduzca **Attenuation Limit**.
- **Persiste ruido musical o timbre después de NR2** — Confirme que **AE Filter (artifact elimination)** esté marcado.
- **Los controles de MNR están desactivados** — MNR es solo para macOS. En Linux o Windows, la pestaña está presente, pero el motor no está disponible.
- **DFNR no tiene efecto** — Verifique que **Attenuation Limit** esté por encima de 0. Un valor de 0 es modo de paso.
- **La estimación de ruido de NR4 se desvía en una banda silenciosa** — Desmarque **Adaptive Noise Estimation** para fijar la estimación, o cambie **Noise Estimation Method** a Martin, que está diseñado para pisos que varían lentamente.

## Relacionado

- [Descripción general de AetherDSP Settings](../../features/aether-dsp/overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el método NR
