# Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR proporciona seis motores de reducción de ruido del lado del cliente. Esta página describe qué hace cada motor, cuándo usarlo y dónde encontrar sus controles, para que pueda elegir el más adecuado para sus condiciones de operación.

## Antes de comenzar

- Abra la configuración de AetherDSP mediante `Settings > AetherDSP Settings...`.
- El motor NR que configure aquí es solo del lado del cliente; no requiere una conexión a la radio.
- La posición y el tamaño de la ventana de diálogo se restauran automáticamente cada vez que la abre. La clase base `PersistentDialog` guarda la geometría con la clave `AetherDspDialogGeometry`.

## Pasos

1. Vaya a `Settings > AetherDSP Settings...`.
2. Haga clic en el botón de alternancia del motor que desea usar: **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** o **BNR**. Al hacer clic en un botón de alternancia, también se activa o se desvía ese motor.
3. Ajuste los controles en esa pestaña (consulte la tabla a continuación).
4. Haga clic en el botón **×** (Cerrar) o presione Escape para cerrar el diálogo. La configuración se guarda automáticamente.

## Controles de la ventana

El diálogo proporciona la gestión de ventana estándar a través de la barra de título:

| Control | Comportamiento |
|---|---|
| Barra de título — AetherDSP Settings | Barra de título con degradado de 18 px con el glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. |
| Redimensionar en 8 ejes | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Una zona de impacto de redimensionamiento de 6 px rodea el widget de contenido interno. |

## Qué hace cada control

### NR2 — Reducción de ruido musical

Un reductor de ruido en el dominio de la frecuencia diseñado para minimizar los artefactos tonales "birdie" comunes en la sustracción espectral. Buena opción inicial para voz SSB en QRN moderado.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction: | Deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | Deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults (icono ↺) | Botón | — | — | — |

**Gain Method** selecciona cómo NR2 asigna las estimaciones de ruido a la reducción de ganancia. Gamma coincide con los patrones típicos de amplitud del habla y es el predeterminado. Trained utiliza un modelo construido a partir de muestras reales de voz y ruido. Linear y Log intercambian precisión perceptual por una computación más simple.

**NPE Method** selecciona el estimador de potencia de ruido. OSMS (Optimal Smoothing Minimum Statistics) rastrea el piso de ruido utilizando un mínimo móvil y es adecuado para ruido que varía lentamente. MMSE minimiza el error de estimación esperado. NSTAT se adapta al ruido que cambia rápidamente con el tiempo.

**AE Filter (eliminación de artefactos)** aplica un postfiltro para reducir el timbre y los artefactos musicales. Déjelo habilitado a menos que esté experimentando con valores de Reduction muy bajos.

**Reduction:** controla la supresión máxima. Los valores más altos eliminan más ruido pero corren el riesgo de distorsionar la voz. 1.50 es el valor predeterminado.

**Smoothing:** controla la suavidad con la que la estimación de ruido sigue los cambios. Los valores más altos son más estables pero más lentos para adaptarse.

**Threshold:** es el umbral de probabilidad de presencia de voz. Los valores más bajos protegen la voz suave pero pueden permitir que pase más ruido.

**Reset Defaults (icono ↺)** restaura: Gamma / OSMS / AE Filter activado / 1.50 / 0.85 / 0.20.

---

### NR4 — libspecbleach

Un motor de blanqueo espectral separado con su propio estimador de ruido y controles de conformación adicionales. Es útil cuando NR2 deja ruido residual o cuando desea objetivos de reducción calibrados en dB.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
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

**Reduction (dB):** establece la reducción máxima en dB. Comience con 10 dB y aumente si el ruido persiste.

**Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.

**Whitening (%):** aplana la forma espectral del ruido residual después de la reducción.

**Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.

**Suppression:** establece la fuerza de supresión general. Los valores más altos son más agresivos.

**Reset Defaults (icono ↺)** restaura: MMSE / Adaptive activado / 10.0 dB / 0 / 0 / 0.50 / 0.50.

**Nota de plataforma:** NR4 requiere LLVM (clang-cl) en Windows. Si la alternancia **NR4** está deshabilitada y muestra una información sobre herramientas acerca de LLVM, instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

---

### DFNR — DeepFilterNet3

Un filtro de ruido basado en redes neuronales. Adecuado para ruido de banda ancha fuerte donde los métodos espectrales convencionales se quedan cortos. Tiene el mayor costo de CPU de los seis motores.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Attenuation Limit | Deslizador | 100 dB | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación máxima de ruido que aplicará DeepFilterNet3. 0 es paso directo; 100 es atenuación máxima. Reduzca este valor si el filtro neuronal suprime en exceso las señales débiles.

**Post-Filter Beta** agrega una etapa de supresión adicional sobre la salida del filtro neuronal. Déjelo en 0.00 a menos que quede ruido residual después de ajustar Attenuation Limit.

---

### MNR — Solo macOS

Un reductor de ruido MMSE-Wiener con suavizado de ganancia asimétrico, disponible solo en macOS.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Enable MNR (solo macOS) | Casilla de verificación | (leído del motor de audio) | — | `MnrEnabled` |
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

**Enable MNR (solo macOS)** activa o desactiva el motor. El estado inicial refleja el estado actual del motor de audio.

**Strength** establece la agresividad. 0 es el más suave; 100 es el máximo. Se conserva internamente como un valor normalizado de 0.00–1.00.

MNR no está disponible en Linux o Windows. La alternancia **MNR** aparece atenuada en esas plataformas: el motor no tiene un backend allí.

---

### RN2 — RNNoise

La pestaña **RN2** es solo informativa. RNNoise no tiene parámetros ajustables en la configuración de AetherDSP. Habilite o deshabilite el motor desde el menú superpuesto.

---

### BNR — NVIDIA

La pestaña **BNR** es solo informativa. La intensidad de BNR se controla desde el menú superpuesto, no desde la configuración de AetherDSP. La alternancia BNR aparece atenuada en las compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- Ejecute solo un motor de reducción de ruido a la vez. Encadenar múltiples motores puede causar artefactos en el habla y aumentar la carga de la CPU. Las seis alternancias DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de habilitación/deshabilitación del motor. Cuando se activa NR2, AudioEngine ejecuta una exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.
- Para voz SSB con ruido de banda moderado, comience con NR2 en sus valores predeterminados antes de probar NR4 o DFNR.
- Si está en macOS y prefiere una carga de CPU más ligera, MNR es la opción de menor consumo.
- El Attenuation Limit de DFNR en 100 dB puede suprimir señales muy débiles junto con el ruido. Redúzcalo a 40–60 dB en trayectorias marginales.
- En la pestaña NR2, si la voz suena hueca o "subacuática", reduzca **Reduction:** hacia 0.80–1.00 o cambie **Gain Method** de Gamma a Log.
- Use **Reset Defaults (icono ↺)** en la pestaña NR2 o NR4 para recuperar un punto de partida conocido después de cambios experimentales.

## Solución de problemas

- **La voz suena hueca o se escuchan artefactos musicales en NR2** — Reduzca **Reduction:** o asegúrese de que **AE Filter (eliminación de artefactos)** esté habilitado.
- **NR4 no reduce el ruido lo suficiente** — Aumente **Reduction (dB):** y habilite **Adaptive Noise Estimation** si está desactivado.
- **DFNR elimina señales débiles junto con el ruido** — Baje **Attenuation Limit** de 100 a 40–60 dB.
- **La pestaña MNR está presente pero no tiene efecto** — MNR es solo para macOS. En Linux o Windows, use NR2, NR4 o DFNR en su lugar.
- **La alternancia NR4 está deshabilitada en Windows** — NR4 requiere LLVM (clang-cl). Instale LLVM desde llvm.org y reconstruya AetherSDR.
- **La configuración de NR2 o NR4 no se conservó después de reiniciar** — La configuración se guarda automáticamente en cada cambio de control. Si los valores se revierten, haga clic en **Reset Defaults (icono ↺)** y vuelva a ingresar los valores deseados para forzar un guardado.

## Relacionados

- [Descripción general de la configuración de AetherDSP](../../features/aether-dsp/overview.md)
- [Ajustar la profundidad de reducción de NR2 y el umbral de voz](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](../../features/aether-dsp/adjust-nr4-reduction-amount-in-db.md)
