# Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR proporciona seis motores de reducción de ruido del lado del cliente. Esta página describe lo que hace cada motor, cuándo usarlo y dónde encontrar sus controles para que pueda elegir el adecuado para sus condiciones de operación.

## Antes de empezar

- Abra la configuración de AetherDSP a través de `Settings > AetherDSP Settings...`.
- El motor NR que configure aquí es solo del lado del cliente; no requiere conexión con la radio.
- El diálogo utiliza una barra de título sin marco introducida en v0.9.8. Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. Haga clic y arrastre cualquier borde o esquina para redimensionar el diálogo.

## Pasos

1. Vaya a `Settings > AetherDSP Settings...`.
2. Haga clic en el botón de alternancia del motor que desea usar: **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** o **BNR**. Al hacer clic en una alternancia también se activa o desactiva ese motor.
3. Ajuste los controles en esa pestaña (consulte la tabla a continuación).
4. Haga clic en el botón **×** (Cerrar) o presione Escape para cerrar el diálogo. La configuración se guarda automáticamente.

## Controles de la ventana

El diálogo proporciona gestión de ventanas estándar a través de la barra de título:

| Control | Comportamiento |
|---|---|
| Barra de título — AetherDSP Settings | Barra de título degradada sin marco de 18 px con el glifo de agarre (⋮⋮) a la izquierda y el título del diálogo |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo |
| Redimensionamiento en 8 ejes | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento |

## Qué hace cada control

### NR2 — reducción de ruido musical

Un reductor de ruido en el dominio de la frecuencia diseñado para minimizar los artefactos tonales de "pajarito" comunes en la sustracción espectral. Buena opción inicial para voz en SSB con QRN moderado.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction: | Deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | Deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults (icono ↺) | Botón | — | — | — |

**Gain Method** selecciona cómo NR2 asigna las estimaciones de ruido a la reducción de ganancia. Gamma coincide con los patrones típicos de amplitud del habla y es el predeterminado. Trained utiliza un modelo construido a partir de muestras reales de habla y ruido. Linear y Log intercambian precisión perceptiva por un cálculo más simple.

**NPE Method** selecciona el estimador de potencia de ruido. OSMS (Optimal Smoothing Minimum Statistics) rastrea el piso de ruido utilizando un mínimo móvil y es adecuado para ruido que varía lentamente. MMSE minimiza el error de estimación esperado. NSTAT se adapta al ruido que cambia rápidamente con el tiempo.

**AE Filter (artifact elimination)** aplica un post-filtro para reducir artefactos de timbre y musicales. Déjelo habilitado a menos que esté experimentando con valores de Reduction muy bajos.

**Reduction:** controla la supresión máxima. Valores más altos eliminan más ruido pero arriesgan distorsión del habla. 1.50 es el valor predeterminado.

**Smoothing:** controla la suavidad con la que la estimación de ruido rastrea los cambios. Valores más altos son más estables pero más lentos para adaptarse.

**Threshold:** es el umbral de probabilidad de presencia de habla. Valores más bajos protegen el habla silenciosa pero pueden permitir que pase más ruido.

**Reset Defaults (icono ↺)** restaura: Gamma / OSMS / AE Filter activado / 1.50 / 0.85 / 0.20.

---

### NR4 — libspecbleach

Un motor de blanqueo espectral independiente con su propio estimador de ruido y controles de modelado adicionales. Útil cuando NR2 deja ruido residual o cuando desea objetivos de reducción calibrados en dB.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Noise Estimation: | Botones de opción | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Deslizador | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Deslizador | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Deslizador | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Deslizador | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Deslizador | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults (icono ↺) | Botón | — | — | — |

**Noise Estimation:** selecciona el estimador del piso de ruido. MMSE minimiza el error de estimación esperado y es el predeterminado. Brandt utiliza suavizado recursivo sobre bandas de frecuencia críticas y es adecuado para ruido no estacionario. Martin utiliza mínimos espectrales móviles y es robusto para pisos de ruido que varían lentamente.

**Adaptive Noise Estimation** permite la reestimación continua del piso de ruido. Desactívelo solo si el entorno de ruido es estático y desea un piso fijo.

**Reduction (dB):** establece la reducción máxima en dB. Comience en 10 dB y aumente si el ruido persiste.

**Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.

**Whitening (%):** aplana la forma espectral del ruido residual después de la reducción.

**Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.

**Suppression:** establece la fuerza de supresión general. Valores más altos son más agresivos.

**Reset Defaults (icono ↺)** restaura: MMSE / Adaptive activado / 10.0 dB / 0 / 0 / 0.50 / 0.50.

---

### DFNR — DeepFilterNet3

Un filtro de ruido basado en redes neuronales. Adecuado para ruido de banda ancha fuerte donde los métodos espectrales convencionales se quedan cortos. Tiene el mayor costo de CPU de los seis motores.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Attenuation Limit | Deslizador | 100 dB | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación máxima de ruido que DeepFilterNet3 aplicará. 0 es paso directo; 100 es atenuación máxima. Reduzca este valor si el filtro neuronal sobresuprime señales débiles.

**Post-Filter Beta** añade una etapa de supresión adicional sobre la salida del filtro neuronal. Déjelo en 0.00 a menos que quede ruido residual después de ajustar Attenuation Limit.

---

### MNR — solo macOS

Un reductor de ruido MMSE-Wiener con suavizado de ganancia asimétrico, disponible solo en macOS.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Enable MNR (solo macOS) | Casilla de verificación | (leído del motor de audio) | — | `MnrEnabled` |
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

**Enable MNR (solo macOS)** activa o desactiva el motor. El estado inicial refleja el estado actual del motor de audio.

**Strength** establece la agresividad. 0 es el más suave; 100 es el máximo. Se persiste internamente como un valor normalizado de 0.00–1.00.

MNR no está disponible en Linux o Windows. La alternancia **MNR** está atenuada en esas plataformas; el motor no tiene backend allí.

---

### RN2 — RNNoise

La pestaña **RN2** es solo informativa. RNNoise no tiene parámetros ajustables en AetherDSP Settings. Active o desactive el motor desde el menú superpuesto.

---

### BNR — NVIDIA

La pestaña **BNR** es solo informativa. La intensidad de BNR se controla desde el menú superpuesto, no desde AetherDSP Settings. La alternancia BNR está atenuada en compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- Ejecute solo un motor de reducción de ruido a la vez. Encadenar múltiples motores puede causar artefactos en el habla y aumentar la carga de CPU. Las seis alternancias DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de activación/desactivación del motor. Cuando NR2 está activado, AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.
- Para voz en SSB con ruido de banda moderado, comience con NR2 en sus valores predeterminados antes de probar NR4 o DFNR.
- Si está en macOS y prefiere una carga de CPU más ligera, MNR es la opción de menor consumo.
- El Attenuation Limit de DFNR a 100 dB puede suprimir señales muy débiles junto con el ruido. Redúzcalo a 40–60 dB en trayectos marginales.
- En la pestaña NR2, si el habla suena hueca o "submarina", reduzca **Reduction:** hacia 0.80–1.00 o cambie **Gain Method** de Gamma a Log.
- Use **Reset Defaults (icono ↺)** en la pestaña NR2 o NR4 para recuperar un punto de partida conocido después de cambios experimentales.

## Solución de problemas

- **El habla suena hueca o se escuchan artefactos musicales en NR2** — Reduzca **Reduction:** o confirme que **AE Filter (artifact elimination)** está habilitado.
- **NR4 no reduce suficiente ruido** — Aumente **Reduction (dB):** y active **Adaptive Noise Estimation** si está desactivado.
- **DFNR elimina señales débiles junto con el ruido** — Baje **Attenuation Limit** de 100 hacia 40–60 dB.
- **La pestaña MNR está presente pero no tiene efecto** — MNR es solo para macOS. En Linux o Windows, use NR2, NR4 o DFNR.
- **La configuración de NR2 o NR4 no persiste después de reiniciar** — La configuración se guarda automáticamente en cada cambio de control. Si los valores se revierten, haga clic en **Reset Defaults (icono ↺)** y vuelva a ingresar los valores deseados para forzar un guardado.

## Relacionado

- [AetherDSP Settings overview](../../features/aether-dsp/overview.md)
- [Tune NR2 reduction depth and voice threshold](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Switch NR2 gain method between Linear, Log, Gamma and Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Change NR2 noise power estimator (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Adjust NR4 reduction amount in dB](../../features/aether-dsp/adjust-nr4-reduction-amount-in-db.md)
