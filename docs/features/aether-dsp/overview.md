# Resumen de configuración de AetherDSP

La configuración de AetherDSP le brinda un control detallado sobre los motores de reducción de ruido del lado del cliente en AetherSDR. Use este diálogo para ajustar el equilibrio entre la supresión de ruido y la fidelidad del habla en seis motores configurables: NR2, NR4, MNR, DFNR, RN2 y BNR.

## Antes de comenzar

- No se requiere conexión de radio para abrir o ajustar la configuración de AetherDSP.
- Cada motor debe habilitarse por separado (desde el panel de applets o el menú superpuesto) antes de que sus ajustes surtan efecto.

## Cómo funciona

Abra el diálogo mediante `Settings > AetherDSP Settings...`. El diálogo contiene seis pestañas — **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** y **BNR** — cada una cubre un motor diferente de reducción de ruido. Al hacer clic en una pestaña también se activa o se omite ese motor; los seis conmutadores DSP actúan como selectores exclusivos y controles de habilitación/deshabilitación del motor. Los ajustes se guardan inmediatamente al cambiar cualquier control; no se requiere ningún botón Apply ni OK.

El diálogo tiene una barra de título degradada sin marco de 18 px con un glifo de agarre (⋮⋮) a la izquierda y botones de control de ventana (—, □, ×) a la derecha, que coinciden con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip. Los controles dentro del diálogo los proporciona un `AetherDspWidget` integrado en modo de diálogo, con todas las fuentes escaladas a 13 px. La posición y el tamaño del diálogo se guardan entre sesiones mediante la clave de configuración `AetherDspDialogGeometry`. El fondo y los colores del diálogo siguen el tema actual mediante `ThemeManager`.

Cada botón de conmutación en la fila superior tiene un nombre de objeto de la forma `dspMethodBtnNR2`, `dspMethodBtnNR4`, etc., y un nombre accesible que incluye la etiqueta y "noise-reduction method". Esto permite que los puentes de automatización y las tecnologías de asistencia identifiquen cada control específico del motor.

Cuando selecciona una pestaña DSP, AetherSDR recuerda el último motor de reducción de ruido del lado del cliente usado en la configuración `LastClientNr`. Si esa configuración apunta a `DFNR` en una compilación sin soporte de DeepFilterNet, se borra automáticamente.

### Pestaña NR2

NR2 es un motor de reducción de ruido musical en el dominio de la frecuencia. Sus parámetros controlan cuán agresivamente se suprime el ruido y cómo el motor identifica el habla frente al ruido.

| Control | Tipo | Predeterminado | Rango | Clave guardada |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults (ícono ↺) | Botón de acción | — | — | — (sin clave) |

- **Gain Method** selecciona la asignación de la curva de ganancia aplicada durante la reducción de ruido. Gamma coincide con los patrones típicos de amplitud del habla; Trained usa un modelo creado a partir de muestras reales de habla y ruido.
- **NPE Method** selecciona el estimador de potencia de ruido. OSMS rastrea el piso de ruido usando un mínimo móvil; MMSE minimiza el error de estimación esperado; NSTAT se adapta al ruido que cambia con el tiempo.
- **AE Filter (eliminación de artefactos)** activa un filtro posterior que reduce el timbre y los artefactos musicales comunes en el procesamiento en el dominio de la frecuencia.
- **Reduction:** establece la profundidad máxima de supresión. Los valores más altos suprimen más ruido pero corren el riesgo de distorsionar el habla.
- **Smoothing:** controla la rapidez con la que el estimador de ruido sigue los cambios. Los valores más altos ofrecen una adaptación más estable pero más lenta.
- **Threshold:** establece el umbral de probabilidad de presencia del habla. Los valores más bajos preservan el habla débil pero pueden permitir que pase más ruido.
- **Reset Defaults** restaura NR2 a: Gamma, OSMS, AE Filter activado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

### Pestaña NR4

NR4 usa la biblioteca libspecbleach para la reducción de ruido basada en sustracción espectral, con control independiente sobre la fuerza de supresión y la forma espectral. En Windows, NR4 requiere el conjunto de herramientas LLVM (clang-cl) para compilar los arreglos de longitud variable C99 de libspecbleach. Si AetherSDR se compiló sin LLVM, el conmutador NR4 está deshabilitado y una información sobre herramientas explica la dependencia faltante.

| Control | Tipo | Predeterminado | Rango | Clave guardada |
|---|---|---|---|---|
| Noise Estimation: | Botones de opción | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Control deslizante | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults (ícono ↺) | Botón de acción | — | — | — (sin clave) |

- **Noise Estimation:** selecciona el estimador del piso de ruido. MMSE equilibra la estimación del ruido con la preservación del habla; Brandt usa suavizado recursivo entre bandas críticas; Martin usa mínimos espectrales móviles.
- **Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido a medida que cambian las condiciones.
- **Reduction (dB):** establece la reducción máxima de ruido en decibelios.
- **Smoothing (%):** aplica suavizado en el dominio del tiempo a la estimación del ruido.
- **Whitening (%):** aplana la forma espectral del ruido residual.
- **Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.
- **Suppression:** establece la fuerza general de supresión de NR4.
- **Reset Defaults** restaura NR4 a: MMSE, Adaptive Noise Estimation activado, Reduction 10.0 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

### Pestaña MNR

MNR es un motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Solo está disponible en macOS; en las compilaciones para Windows y Linux, el conmutador MNR está atenuado porque el motor no tiene un backend en esas plataformas.

| Control | Tipo | Predeterminado | Rango | Clave guardada |
|---|---|---|---|---|
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

- **Strength** establece la agresividad desde suave (0) hasta máxima (100). El valor se guarda como una cifra normalizada de 0.00–1.00.

### Pestaña DFNR

DFNR usa la red neuronal DeepFilterNet3 para la supresión profunda de ruido. Si AetherSDR se compiló sin soporte de DeepFilterNet, el conmutador DFNR está deshabilitado y una información sobre herramientas explica la dependencia faltante.

| Control | Tipo | Predeterminado | Rango | Clave guardada |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

- **Attenuation Limit** limita la atenuación máxima que aplica DeepFilterNet3. 0 es paso directo; 100 es el máximo.
- **Post-Filter Beta** aplica un filtro de posprocesamiento adicional para una supresión extra más allá de lo que proporciona la red neuronal.

### Pestaña RN2

La pestaña RN2 cubre el motor RNNoise. Aloja el control deslizante de mezcla seca Noise Floor, que establece la cantidad de la señal original que RN2 deja debajo del audio con eliminación de ruido.

| Control | Tipo | Predeterminado | Rango | Clave guardada |
|---|---|---|---|---|
| Noise Floor | Control deslizante | 0 | 0–100 | — (guardado por Rn2SettingsModel) |

- **Noise Floor** establece el porcentaje de la señal original que RN2 deja debajo del audio con eliminación de ruido. Cero produce una supresión completa (silencio entre frases); 10–20% mantiene un piso de silencio constante para que el receptor siga sonando vivo. Esto afecta solo el audio recibido; el eliminador de ruido de transmisión no cambia.
- **Reset Defaults** restaura la pestaña RN2 a su valor predeterminado de Noise Floor de 0.

### Pestaña BNR

La pestaña BNR cubre la reducción de ruido de NVIDIA. La intensidad se controla desde el menú superpuesto, no desde este diálogo. En las compilaciones sin el SDK de NVIDIA Broadcast, el conmutador BNR está atenuado. No hay parámetros ajustables en esta pestaña, por lo que **Reset Defaults** no realiza ninguna acción.

## Controles de ventana

La barra de título personalizada del diálogo ofrece estos controles:

| Control                   | Comportamiento                                                                                                                                                                                                     | Notas                                                                                                                                                                      |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Glifo de agarre (⋮⋮)       | Solo indicador visual; haga clic y arrastre cualquier parte de la barra de título para mover el diálogo                                                                                                             |                                                                                                                                                                            |
| — (Minimizar)              | Minimiza el diálogo                                                                                                                                                                                                |                                                                                                                                                                            |
| □ (Maximizar)              | Maximiza o restaura el diálogo                                                                                                                                                                                     |                                                                                                                                                                            |
| × (Cerrar)                 | Cierra el diálogo                                                                                                                                                                                                  |                                                                                                                                                                            |
| Doble clic en la barra de título | Alterna entre maximizar/restaurar                                                                                                                                                                                 |                                                                                                                                                                            |

## Cambio de tamaño

Haga clic y arrastre cualquier borde o esquina del diálogo para cambiar su tamaño. El cursor cambia para indicar la dirección del cambio de tamaño. Una zona de golpe de 6 px para cambiar el tamaño se extiende hacia adentro desde cada borde.

## Consejos

- Los cambios surten efecto de inmediato; puede monitorear el audio mientras ajusta los controles deslizantes.
- En la pestaña NR2, reducir **Threshold:** por debajo de su valor predeterminado (0.20) ayuda a recuperar habla débil o de baja potencia, pero puede aumentar la filtración de ruido.
- En la pestaña NR4, dejar **Smoothing (%):** y **Whitening (%):** en 0 ofrece la salida con sonido más natural; auméntelos solo si el ruido residual resulta molesto.
- En la pestaña RN2, use un **Noise Floor** de 10–20% para mantener el receptor sonando vivo entre frases en lugar de quedar completamente en silencio.
- Use **Reset Defaults** en las pestañas NR2, NR4 o RN2 para recuperar una línea base conocida antes de experimentar.

## Relacionados

- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción de NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Habilitar MNR en macOS y establecer su fuerza](enable-mnr-on-macos-and-set-its-strength.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Configurar la beta del filtro posterior de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
