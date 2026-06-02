# Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR proporciona seis motores de reducción de ruido del lado del cliente. Esta página describe qué hace cada motor, cuándo usarlo y dónde encontrar sus controles para que pueda elegir el más adecuado para sus condiciones de operación.

## Antes de empezar

- Abra la configuración de AetherDSP mediante `Settings > AetherDSP Settings...`.
- El motor NR que configure aquí es solo del lado del cliente; no requiere una conexión con la radio.
- La posición y el tamaño de la ventana de diálogo se restauran automáticamente cada vez que la abre. La clase base `PersistentDialog` guarda la geometría con la clave `AetherDspDialogGeometry`.
- El diálogo usa un estilo temático basado en el tema actual de AetherSDR. Los colores se toman del contenedor de tema `dialog/aetherDsp`.

## Pasos

1. Vaya a `Settings > AetherDSP Settings...`.
2. Haga clic en el botón de activación del motor que desea usar: **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** o **BNR**. Al hacer clic en un botón de activación también se activa o se omite ese motor.
3. Ajuste los controles en esa pestaña (consulte la tabla a continuación).
4. Haga clic en el botón **×** (Cerrar) o presione Escape para cerrar el diálogo. Los ajustes se guardan automáticamente.

## Controles de la ventana

El diálogo proporciona gestión de ventana estándar a través de la barra de título:

| Control | Comportamiento |
|---|---|
| Barra de título — AetherDSP Settings | Barra de título de gradiente de 18 píxeles con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. Tematizada mediante el contenedor de tema `dialog/aetherDsp`. |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. |
| Redimensionamiento en 8 direcciones | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Hay una zona de contacto de redimensionamiento de 6 píxeles alrededor del widget de contenido interno. |

## Qué hace cada control

### NR2 — Reducción de ruido musical

Un reductor de ruido en el dominio de la frecuencia diseñado para minimizar los artefactos tonales "birdie" comunes en la sustracción espectral. Buena opción inicial para voz SSB con QRN moderado.

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction: | Deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | Deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Restablecer valores predeterminados (icono ↺) | Botón | — | — | — |

**Gain Method** selecciona cómo NR2 asigna las estimaciones de ruido a la reducción de ganancia. Gamma coincide con los patrones típicos de amplitud del habla y es el valor predeterminado. Trained utiliza un modelo construido a partir de muestras reales de habla y ruido. Linear y Log intercambian precisión perceptual por un cálculo más simple.

**NPE Method** selecciona el estimador de potencia de ruido. OSMS (Optimal Smoothing Minimum Statistics) rastrea el piso de ruido utilizando un mínimo móvil y es adecuado para ruido que varía lentamente. MMSE minimiza el error de estimación esperado. NSTAT se adapta al ruido que cambia rápidamente con el tiempo.

**AE Filter (artifact elimination)** aplica un filtro posterior para reducir el timbre y los artefactos musicales. Déjelo habilitado a menos que esté experimentando con valores muy bajos de Reduction.

**Reduction:** controla la supresión máxima. Los valores más altos eliminan más ruido, pero pueden distorsionar la voz. 1.50 es el valor predeterminado.

**Smoothing:** controla la suavidad con la que la estimación de ruido sigue los cambios. Los valores más altos son más estables pero más lentos para adaptarse.

**Threshold:** es el umbral de probabilidad de presencia de voz. Los valores más bajos protegen el habla suave, pero pueden dejar pasar más ruido.

**Reset Defaults (icono ↺)** restaura: Gamma / OSMS / AE Filter activado / 1.50 / 0.85 / 0.20.

---

### NR4 — libspecbleach

Un motor de blanqueo espectral separado con su propio estimador de ruido y controles de modelado adicionales. Útil cuando NR2 deja ruido residual o cuando desea objetivos de reducción calibrados en dB.

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Noise Estimation: | Botones de opción | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Deslizador | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Deslizador | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Deslizador | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Deslizador | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Deslizador | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Restablecer valores predeterminados (icono ↺) | Botón | — | — | — |

**Noise Estimation:** selecciona el estimador del piso de ruido. MMSE minimiza el error de estimación esperado y es el valor predeterminado. Brandt utiliza suavizado recursivo sobre bandas de frecuencia críticas y es adecuado para ruido no estacionario. Martin utiliza mínimos espectrales móviles y es robusto para pisos de ruido que varían lentamente.

**Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido. Desactívelo solo si el entorno de ruido es estático y desea un piso fijo.

**Reduction (dB):** establece la reducción máxima en dB. Comience con 10 dB y aumente si el ruido persiste.

**Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.

**Whitening (%):** aplana la forma espectral del ruido residual después de la reducción.

**Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.

**Suppression:** establece la fuerza de supresión general. Los valores más altos son más agresivos.

**Reset Defaults (icono ↺)** restaura: MMSE / Adaptativo activado / 10.0 dB / 0 / 0 / 0.50 / 0.50.

**Nota de plataforma:** NR4 requiere LLVM (clang-cl) en Windows. Si el botón de activación **NR4** está deshabilitado y muestra una información sobre herramientas acerca de LLVM, instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

---

### DFNR — DeepFilterNet3

Un filtro de ruido basado en red neuronal. Adecuado para ruido de banda ancha intenso donde los métodos espectrales convencionales se quedan cortos. Tiene el mayor coste de CPU de los seis motores.

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Attenuation Limit | Deslizador | 100 dB | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación máxima de ruido que aplicará DeepFilterNet3. 0 es paso directo; 100 es la atenuación máxima. Reduzca este valor si el filtro neuronal suprime en exceso las señales débiles.

**Post-Filter Beta** añade una etapa de supresión adicional sobre la salida del filtro neuronal. Déjelo en 0.00 a menos que quede ruido residual después de ajustar Attenuation Limit.

---

### MNR — Solo macOS

Un reductor de ruido MMSE-Wiener con suavizado de ganancia asimétrico, disponible solo en macOS.

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (solo macOS) | Casilla de verificación | (leído del motor de audio) | — | `MnrEnabled` |
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** activa o desactiva el motor. El estado inicial refleja el estado actual del motor de audio.

**Strength** establece la agresividad. 0 es el más suave; 100 es el máximo. Se mantiene internamente como un valor normalizado de 0.00 a 1.00.

MNR no está disponible en Linux o Windows. El botón de activación **MNR** está atenuado en esas plataformas; el motor no tiene un backend allí.

---

### RN2 — RNNoise

La pestaña **RN2** es solo informativa. RNNoise no tiene parámetros ajustables en AetherDSP Settings. Active o desactive el motor desde el menú superpuesto.

---

### BNR — NVIDIA

La pestaña **BNR** es solo informativa. La intensidad de BNR se controla desde el menú superpuesto, no desde AetherDSP Settings. El botón de activación BNR está atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- Ejecute solo un motor de reducción de ruido a la vez. Encadenar varios motores puede causar artefactos en el habla y aumenta la carga de la CPU. Los seis botones de activación de DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de activación/desactivación del motor. Cuando se activa NR2, AudioEngine aplica una exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.
- Para voz SSB con ruido de banda moderado, comience con NR2 en sus valores predeterminados antes de probar NR4 o DFNR.
- Si está en macOS y prefiere una carga de CPU más ligera, MNR es la opción de menor consumo.
- El Attenuation Limit de DFNR en 100 dB puede suprimir señales muy débiles junto con el ruido. Redúzcalo a 40–60 dB en rutas marginales.
- En la pestaña NR2, si el habla suena hueca o "subacuática", reduzca **Reduction:** hacia 0.80–1.00 o cambie **Gain Method** de Gamma a Log.
- Use **Reset Defaults (icono ↺)** en la pestaña NR2 o NR4 para recuperar un punto de partida conocido después de cambios experimentales.

## Solución de problemas

- **El habla suena hueca o se escuchan artefactos musicales en NR2** — Reduzca **Reduction:** o confirme que **AE Filter (artifact elimination)** está habilitado.
- **NR4 no reduce el ruido lo suficiente** — Aumente **Reduction (dB):** y active **Adaptive Noise Estimation** si está desactivado.
- **DFNR elimina señales débiles junto con el ruido** — Baje **Attenuation Limit** de 100 hacia 40–60 dB.
- **La pestaña MNR está presente pero no tiene efecto** — MNR es solo para macOS. En Linux o Windows, use NR2, NR4 o DFNR.
- **El botón de activación NR4 está deshabilitado en Windows** — NR4 requiere LLVM (clang-cl). Instale LLVM desde llvm.org y reconstruya AetherSDR.
- **Los ajustes de NR2 o NR4 no se conservaron después de reiniciar** — Los ajustes se guardan automáticamente en cada cambio de control. Si los valores se revierten, haga clic en **Reset Defaults (icono ↺)** y vuelva a ingresar los valores deseados para forzar un guardado.

## Relacionados

- [Resumen de ajustes de AetherDSP](../../features/aether-dsp/overview.md)
- [Ajuste la profundidad de reducción y el umbral de voz de NR2](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambie el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambie el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajuste la cantidad de reducción de NR4 en dB](../../features/aether-dsp/adjust-nr4-reduction-amount-in-db.md)
