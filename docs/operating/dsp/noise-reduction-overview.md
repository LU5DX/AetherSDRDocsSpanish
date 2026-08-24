# Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR proporciona seis motores de reducción de ruido del lado del cliente. Esta página describe qué hace cada motor, cuándo usarlo y dónde encontrar sus controles para que pueda elegir el adecuado según sus condiciones de operación.

## Antes de comenzar

- Abra AetherDSP Settings mediante `Settings > AetherDSP Settings...`.
- El motor NR que configure aquí es solo del lado del cliente; no requiere conexión con la radio.
- La posición y el tamaño de la ventana del diálogo se restauran automáticamente cada vez que la abre. La clase base `PersistentDialog` guarda la geometría bajo la clave `AetherDspDialogGeometry`.
- El diálogo utiliza un estilo con temas basado en el tema actual de AetherSDR. Los colores se obtienen del contenedor de temas `dialog/aetherDsp`.

## Pasos

1. Vaya a `Settings > AetherDSP Settings...`.
2. Haga clic en el botón de alternancia del motor que desea usar: **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** o **BNR**. Al hacer clic en una alternancia también se activa o se desvía ese motor.
3. Ajuste los controles en esa pestaña (consulte la tabla a continuación).
4. Haga clic en el botón **×** (Close) o presione Escape para cerrar el diálogo. La configuración se guarda automáticamente.

## Controles de la ventana

El diálogo proporciona administración estándar de ventanas mediante la barra de título:

| Control                        | Comportamiento                                                                                                                                                                                                  | Notas                                                                                                                                                                     |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Barra de título — AetherDSP Settings | Barra de título con degradado de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. Con temas mediante el contenedor de temas `dialog/aetherDsp`.                                          |                                                                                                                                                                           |
| — (Minimizar)                  | Minimiza el diálogo                                                                                                                                                                                             |                                                                                                                                                                           |
| □ (Maximizar)                  | Maximiza o restaura el diálogo                                                                                                                                                                                  |                                                                                                                                                                           |
| × (Cerrar)                     | Cierra el diálogo                                                                                                                                                                                               |                                                                                                                                                                           |
| Arrastrar para mover           | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar.                                                                          |                                                                                                                                                                           |
| Redimensionar en 8 ejes        | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Una zona de redimensionamiento de 6 px rodea el widget de contenido interno. |                                                                                                                                                                           |
| Noise Floor (RN2 dry mix)      | Establece el porcentaje de la señal original que RN2 deja bajo el audio con ruido eliminado. Cero produce supresión total (silencio entre frases); 10-20 % mantiene un piso silencioso constante para que el receptor siga sonando vivo. | Afecta solo al audio recibido; el eliminador de ruido de transmisión no cambia. Se conserva mediante Rn2SettingsModel y se expone a la cadena DSP mediante la señal rn2DryMixChanged de AetherDspWidget. |

## Qué hace cada control

### NR2 — reducción de ruido musical

Un reductor de ruido en el dominio de la frecuencia diseñado para minimizar los artefactos tonales "de pájaro" comunes en la sustracción espectral. Buena opción inicial para voz SSB con QRN moderado.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Gain Method | Botones de radio | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de radio | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction: | Deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Gain Floor: | Deslizador | 0.0010 | 0.0001–0.1000 | `NR2GainFloor` |
| Smoothing: | Deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | Deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults (icono ↺) | Botón | — | — | — |

**Gain Method** selecciona cómo NR2 asigna las estimaciones de ruido a la reducción de ganancia. Gamma coincide con los patrones típicos de amplitud del habla y es el predeterminado. Trained utiliza un modelo construido con muestras reales de voz y ruido. Linear y Log intercambian precisión perceptiva por un cálculo más simple.

**NPE Method** selecciona el estimador de potencia de ruido. OSMS (Optimal Smoothing Minimum Statistics) rastrea el piso de ruido usando un mínimo móvil y es adecuado para ruido que varía lentamente. MMSE minimiza el error esperado de estimación. NSTAT se adapta a ruido que cambia rápidamente con el tiempo.

**AE Filter (artifact elimination)** aplica un post-filtro para reducir zumbidos y artefactos musicales. Déjelo habilitado a menos que esté experimentando con valores muy bajos de Reduction.

**Reduction:** controla la supresión máxima. Los valores más altos eliminan más ruido pero arriesgan distorsión del habla. 1.50 es el predeterminado.

**Gain Floor:** establece la ganancia mínima que NR2 aplicará. Los valores más bajos permiten una supresión de ruido más profunda pero pueden introducir artefactos en pasajes muy silenciosos. Aumente este valor si escucha efectos de bombeo o respiración.

**Smoothing:** controla la suavidad con la que la estimación de ruido rastrea los cambios. Los valores más altos son más estables pero se adaptan más lentamente.

**Threshold:** es el umbral de probabilidad de presencia de habla. Los valores más bajos protegen el habla silenciosa pero pueden permitir que pase más ruido.

**Reset Defaults (icono ↺)** restaura: Gamma / OSMS / AE Filter activado / 1.50 / 0.0010 / 0.85 / 0.20.

---

### NR4 — libspecbleach

Un motor separado de blanqueamiento espectral con su propio estimador de ruido y controles adicionales de modelado. Útil cuando NR2 deja ruido residual o cuando desea objetivos de reducción calibrados en dB.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Noise Estimation: | Botones de radio | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Deslizador | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Deslizador | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Deslizador | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Deslizador | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Deslizador | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults (icono ↺) | Botón | — | — | — |

**Noise Estimation:** selecciona el estimador del piso de ruido. MMSE minimiza el error esperado de estimación y es el predeterminado. Brandt utiliza suavizado recursivo sobre bandas de frecuencia críticas y es adecuado para ruido no estacionario. Martin utiliza mínimos espectrales móviles y es robusto para pisos de ruido que varían lentamente.

**Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido. Desactívelo solo si el entorno de ruido es estático y desea un piso fijo.

**Reduction (dB):** establece la reducción máxima en dB. Comience en 10 dB y aumente si el ruido persiste.

**Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación de ruido.

**Whitening (%):** aplana la forma espectral del ruido residual después de la reducción.

**Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.

**Suppression:** establece la fuerza general de supresión. Los valores más altos son más agresivos.

**Reset Defaults (icono ↺)** restaura: MMSE / Adaptive activado / 10.0 dB / 0 / 0 / 0.50 / 0.50.

**Nota de plataforma:** NR4 requiere LLVM (clang-cl) en Windows. Si la alternancia **NR4** está deshabilitada y muestra una información sobre herramientas acerca de LLVM, instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

---

### DFNR — DeepFilterNet3

Un filtro de ruido basado en redes neuronales. Adecuado para ruido de banda ancha fuerte donde los métodos espectrales convencionales no son suficientes. Tiene el mayor costo de CPU de los seis motores.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Attenuation Limit | Deslizador | 100 dB | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación máxima de ruido que aplicará DeepFilterNet3. 0 es paso directo; 100 es atenuación máxima. Reduzca este valor si el filtro neuronal suprime en exceso señales débiles.

**Post-Filter Beta** agrega una etapa de supresión adicional sobre la salida del filtro neuronal. Déjelo en 0.00 a menos que quede ruido residual después de ajustar Attenuation Limit.

---

### MNR — solo macOS

Un reductor de ruido MMSE-Wiener con suavizado de ganancia asimétrico, disponible solo en macOS.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

**Strength** establece la agresividad. 0 es el más suave; 100 es el máximo. Se conserva internamente como un valor normalizado de 0.00–1.00.

MNR no está disponible en Linux ni Windows. La alternancia **MNR** aparece atenuada en esas plataformas — el motor no tiene backend allí.

---

### RN2 — RNNoise

Un reductor de ruido basado en redes neuronales optimizado para voz en tiempo real. La pestaña **RN2** aloja el control **Noise Floor**, que determina cuánta de la señal original se mezcla de vuelta bajo el audio con ruido eliminado.

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Noise Floor (RN2 dry mix) | Deslizador | 0 | 0–100 | — |

**Noise Floor (RN2 dry mix)** establece el porcentaje de la señal original que RN2 deja bajo el audio con ruido eliminado. Cero produce supresión total (silencio entre frases); 10–20 % mantiene un piso silencioso constante para que el receptor siga sonando vivo. El control afecta solo al audio recibido; el eliminador de ruido de transmisión no cambia.

---

### BNR — NVIDIA

La pestaña **BNR** es solo informativa. La intensidad de BNR se controla desde el menú superpuesto, no desde AetherDSP Settings. La alternancia BNR aparece atenuada en compilaciones sin el NVIDIA Broadcast SDK.

## Consejos

- Ejecute solo un motor de reducción de ruido a la vez. Encadenar varios motores puede causar artefactos en el habla y agrega carga de CPU. Las seis alternancias DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de habilitación/deshabilitación del motor. Cuando NR2 está activado, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.
- Para voz SSB con ruido de banda moderado, comience con NR2 en sus valores predeterminados antes de probar NR4 o DFNR.
- Si está en macOS y prefiere una carga de CPU más ligera, MNR es la opción de menor sobrecarga.
- El Attenuation Limit de DFNR en 100 dB puede suprimir señales muy débiles junto con el ruido. Redúzcalo a 40–60 dB en rutas marginales.
- En la pestaña NR2, si el habla suena hueca o "bajo el agua", baje **Reduction:** hacia 0.80–1.00 o cambie **Gain Method** de Gamma a Log.
- Si NR2 produce un efecto de bombeo, aumente **Gain Floor:** del valor predeterminado 0.0010 hacia 0.0100.
- En la pestaña RN2, si el receptor suena muerto entre frases, suba **Noise Floor** a 10–20 % para que un fondo silencioso permanezca audible.
- Use **Reset Defaults (icono ↺)** en la pestaña NR2 o NR4 para recuperar un punto de partida conocido y bueno después de cambios experimentales.

## Solución de problemas

- **El habla suena hueca o se escuchan artefactos musicales en NR2** — Reduzca **Reduction:** o confirme que **AE Filter (artifact elimination)** está habilitado.
- **NR2 tiene un efecto de bombeo o respiración** — Aumente **Gain Floor:** o reduzca **Reduction:**.
- **NR4 no reduce el ruido lo suficiente** — Aumente **Reduction (dB):** y habilite **Adaptive Noise Estimation** si está desactivado.
- **DFNR elimina señales débiles junto con el ruido** — Baje **Attenuation Limit** de 100 hacia 40–60 dB.
- **La pestaña MNR está presente pero no tiene efecto** — MNR es solo para macOS. En Linux o Windows, use NR2, NR4 o DFNR en su lugar.
- **La alternancia NR4 está deshabilitada en Windows** — NR4 requiere LLVM (clang-cl). Instale LLVM desde llvm.org y reconstruya AetherSDR.
- **La salida de RN2 es silenciosa entre frases y el receptor suena muerto** — Suba **Noise Floor** en la pestaña RN2 a 10–20 %.
- **La configuración de NR2 o NR4 no se conservó después de reiniciar** — La configuración se guarda automáticamente en cada cambio de control. Si los valores revierten, haga clic en **Reset Defaults (icono ↺)** y vuelva a ingresar los valores deseados para forzar un guardado.

## Relacionados

- [AetherDSP Settings overview](../../features/aether-dsp/overview.md)
- [Tune NR2 reduction depth and voice threshold](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Switch NR2 gain method between Linear, Log, Gamma and Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Change NR2 noise power estimator (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Adjust NR4 reduction amount in dB](../../features/aether-dsp/adjust-nr4-reduction-amount-in-db.md)
