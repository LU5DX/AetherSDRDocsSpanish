# Descripción general de la configuración de AetherDSP

La configuración de AetherDSP le brinda un control detallado sobre los motores de reducción de ruido del lado del cliente de AetherSDR. Use este diálogo para ajustar el equilibrio entre la supresión de ruido y la fidelidad de la voz en seis motores configurables: NR2, NR4, MNR, DFNR, RN2 y BNR.

## Antes de comenzar

- No se requiere conexión de radio para abrir o ajustar la configuración de AetherDSP.
- Cada motor debe activarse por separado (desde el panel de applets o el menú superpuesto) antes de que su configuración surta efecto.

## Cómo funciona

Abra el diálogo a través de `Settings > AetherDSP Settings...`. El diálogo contiene seis pestañas — **NR2**, **NR4**, **MNR**, **DFNR**, **RN2** y **BNR** —, cada una correspondiente a un motor de reducción de ruido diferente. Al hacer clic en una pestaña también se activa o se pasa por alto ese motor; los seis conmutadores de DSP actúan como selectores exclusivos y controles de activación/desactivación del motor. La configuración se guarda inmediatamente cuando cambia cualquier control; no se necesita un botón Aplicar o Aceptar.

El diálogo tiene una barra de título degradada sin marco de 18 px con un glifo de agarre (⋮⋮) a la izquierda y botones de control de ventana (—, □, ×) a la derecha, que coinciden con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip. Los controles dentro del diálogo los proporciona un `AetherDspWidget` incrustado en modo diálogo, con todas las fuentes escaladas a 13 px. La posición y el tamaño del diálogo se conservan entre sesiones mediante la clave de configuración `AetherDspDialogGeometry`. El fondo y los colores del diálogo siguen el tema actual a través de `ThemeManager`.

### Pestaña NR2

NR2 es un motor de reducción de ruido musical en el dominio de la frecuencia. Sus parámetros controlan qué tan agresivamente se suprime el ruido y cómo el motor identifica la voz frente al ruido.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Habilitado | — | `NR2AeFilter` |
| Reduction: | Deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | Deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — (sin clave) |

- **Gain Method** selecciona la asignación de la curva de ganancia aplicada durante la reducción de ruido. Gamma coincide con los patrones de amplitud de voz típicos; Trained utiliza un modelo basado en muestras reales de voz y ruido.
- **NPE Method** selecciona el estimador de potencia de ruido. OSMS rastrea el piso de ruido utilizando un mínimo móvil; MMSE minimiza el error de estimación esperado; NSTAT se adapta al ruido que cambia con el tiempo.
- **AE Filter (eliminación de artefactos)** activa un filtro posterior que reduce los artefactos de timbre y musicales comunes en el procesamiento en el dominio de la frecuencia.
- **Reduction:** establece la profundidad máxima de supresión. Los valores más altos suprimen más ruido, pero corren el riesgo de distorsionar la voz.
- **Smoothing:** controla la rapidez con la que la estimación de ruido rastrea los cambios. Los valores más altos brindan una adaptación más estable pero más lenta.
- **Threshold:** establece el umbral de probabilidad de presencia de voz. Los valores más bajos preservan la voz baja, pero pueden permitir que pase más ruido.
- **Reset Defaults** restaura NR2 a: Gamma, OSMS, AE Filter activado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

### Pestaña NR4

NR4 utiliza la biblioteca libspecbleach para la reducción de ruido basada en sustracción espectral, con control independiente sobre la fuerza de supresión y la forma espectral. En Windows, NR4 requiere el conjunto de herramientas LLVM (clang-cl) para compilar los arreglos de longitud variable de C99 de libspecbleach. Si AetherSDR se compiló sin LLVM, el conmutador NR4 está deshabilitado y una información sobre herramientas explica la dependencia faltante.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Noise Estimation: | Botones de opción | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Deslizador | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Deslizador | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Deslizador | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Deslizador | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Deslizador | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — (sin clave) |

- **Noise Estimation:** selecciona el estimador del piso de ruido. MMSE equilibra la estimación de ruido con la preservación de la voz; Brandt utiliza un suavizado recursivo en bandas críticas; Martin utiliza mínimos espectrales móviles.
- **Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido a medida que cambian las condiciones.
- **Reduction (dB):** establece la reducción máxima de ruido en decibelios.
- **Smoothing (%):** aplica un suavizado en el dominio del tiempo a la estimación de ruido.
- **Whitening (%):** aplana la forma espectral del ruido residual.
- **Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado.
- **Suppression:** establece la fuerza de supresión general de NR4.
- **Reset Defaults** restaura NR4 a: MMSE, Adaptive Noise Estimation activado, Reduction 10.0 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

### Pestaña MNR

MNR es un motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Solo está disponible en macOS; en las compilaciones de Windows y Linux, el conmutador MNR aparece atenuado porque el motor no tiene backend en esas plataformas.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Enable MNR (solo macOS) | Casilla de verificación | (leído del motor de audio) | — | `MnrEnabled` |
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

- **Enable MNR (solo macOS)** activa o desactiva el motor. El estado inicial refleja lo que el motor de audio informa en el momento en que se abre el diálogo.
- **Strength** establece la agresividad desde suave (0) hasta máxima (100). El valor se persiste como una cifra normalizada de 0.00 a 1.00.

### Pestaña DFNR

DFNR utiliza la red neuronal DeepFilterNet3 para la supresión profunda de ruido.

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Attenuation Limit | Deslizador | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

- **Attenuation Limit** limita la atenuación máxima que aplica DeepFilterNet3. 0 es paso directo; 100 es el máximo.
- **Post-Filter Beta** aplica un filtro de posprocesamiento adicional para una supresión extra más allá de lo que proporciona la red neuronal.

### Pestaña RN2

La pestaña RN2 cubre el motor RNNoise. Es solo informativa; no hay parámetros ajustables en esta pestaña.

### Pestaña BNR

La pestaña BNR cubre la reducción de ruido de NVIDIA. La intensidad se controla desde el menú superpuesto, no desde este diálogo. En las compilaciones sin el SDK de NVIDIA Broadcast, el conmutador BNR aparece atenuado.

## Controles de ventana

La barra de título personalizada del diálogo proporciona estos controles:

| Control | Comportamiento |
|---|---|
| Glifo de agarre (⋮⋮) | Solo indicador visual; haga clic y arrastre cualquier parte de la barra de título para mover el diálogo |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Doble clic en la barra de título | Alterna entre maximizar y restaurar |

## Redimensionamiento

Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección del redimensionamiento. Una zona de acción de redimensionamiento de 6 px se extiende hacia adentro desde cada borde.

## Consejos

- Los cambios surten efecto de inmediato; puede monitorear el audio mientras ajusta los deslizadores.
- En la pestaña NR2, reducir **Threshold:** por debajo de su valor predeterminado (0.20) ayuda a recuperar la voz débil o de baja potencia, pero puede aumentar la fuga de ruido.
- En la pestaña NR4, dejar **Smoothing (%)** y **Whitening (%)** en 0 proporciona la salida con sonido más natural; auméntelos solo si el ruido residual es objetable.
- Use **Reset Defaults** en la pestaña NR2 o NR4 para recuperar una línea base conocida antes de experimentar.

## Relacionados

- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Activar MNR en macOS y establecer su intensidad](enable-mnr-on-macos-and-set-its-strength.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Configurar el beta del filtro posterior de DFNR para una supresión extra](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
