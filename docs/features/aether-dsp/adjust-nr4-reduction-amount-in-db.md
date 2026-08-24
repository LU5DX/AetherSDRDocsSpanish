# Configuración de AetherDSP

El diálogo **AetherDSP Settings** (`Settings > AetherDSP Settings...`) controla los motores de reducción de ruido del lado del cliente integrados en AetherSDR: NR2, NR4, MNR, RN2, BNR y DFNR. Puede abrirlo en cualquier momento; no se requiere una conexión de radio para cambiar estos parámetros. Todos los valores se guardan automáticamente al cerrar el diálogo. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o se omite ese motor.

El diálogo utiliza una barra de título personalizada sin marco con controles de ventana que coinciden con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip. La posición y el tamaño del diálogo se guardan automáticamente entre sesiones. Arrastre la barra de título para mover el diálogo; haga doble clic en la barra de título para alternar maximizar/restaurar. Arrastre cualquier borde o esquina para cambiar el tamaño (zona de redimensionamiento de 6 px alrededor del widget de contenido interno).

El diálogo y todos sus controles usan el tema actual de AetherSDR. El fondo del diálogo utiliza el conjunto de colores de tema `dialog/aetherDsp`, y los deslizadores usan la función de estilo `applyPrimarySliderStyle()` en lugar de una hoja de estilo oscura codificada.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Decida qué motor de reducción de ruido está activo para su slice antes de ajustar sus parámetros. Ajustar un motor deshabilitado no tiene efecto audible.

## Abrir el diálogo

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Se abre el diálogo **AetherDSP Settings**. Seleccione la pestaña del motor que desea ajustar.

---

## Pestaña NR2

NR2 es el motor de reducción de ruido musical. Haga clic en la pestaña **NR2** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                          |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Gain Method**                      | Botones de opción                                                                                            | Gamma                                                                                                          |
| **NPE Method**                       | Botones de opción                                                                                            | OSMS                                                                                                           |
| **AE Filter (artifact elimination)** | Casilla de verificación                                                                                      | Habilitado                                                                                                     |
| **Reduction:**                       | Deslizador                                                                                                   | 1.50                                                                                                           |
| **Smoothing:**                       | Deslizador                                                                                                   | 0.85                                                                                                           |
| **Threshold:**                       | Deslizador                                                                                                   | 0.20                                                                                                           |
| **Reset Defaults (ícono ↺)**         | Botón (ícono plano)                                                                                          | —                                                                                                              |

### Descripciones de los controles

**Gain Method** selecciona la asignación de la curva de ganancia que usa NR2. `NR2GainMethod` se almacena como un entero: Linear = 0, Log = 1, Gamma = 2, Trained = 3. Gamma es adecuado para la mayoría de los modos de voz.

**NPE Method** selecciona el estimador de potencia de ruido. `NR2NpeMethod` se almacena como un entero: OSMS = 0, MMSE = 1, NSTAT = 2.

**AE Filter (artifact elimination)** activa o desactiva el post-filtro anti-artefactos (`NR2AeFilter`). Déjelo habilitado a menos que esté probando específicamente la salida cruda de NR2.

**Reduction:** (`NR2GainMax`) establece la profundidad máxima de reducción que NR2 puede aplicar. Los valores más altos suprimen más ruido, pero pueden afectar la naturalidad del habla.

**Smoothing:** (`NR2GainSmooth`) controla la suavidad con la que la estimación de ruido sigue los cambios. Los valores más altos producen un seguimiento más suave pero más lento.

**Threshold:** (`NR2Qspp`) establece el umbral de probabilidad de presencia de voz por debajo del cual NR2 trata el audio como ruido. Súbalo si se suprime el habla; bájelo si el ruido se filtra durante las pausas.

**Reset Defaults (ícono ↺)** restaura la pestaña NR2 a sus valores de fábrica: Gain Method = Gamma, NPE Method = OSMS, AE Filter = habilitado, Reduction = 1.50, Smoothing = 0.85, Threshold = 0.20.

### Pasos — ajustar la profundidad de reducción de NR2

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Arrastre el deslizador **Reduction:** al valor deseado (predeterminado 1.50).
4. Cierre el diálogo. El valor se guarda automáticamente.

---

## Pestaña NR4

NR4 utiliza la biblioteca libspecbleach. En Windows, NR4 requiere LLVM (clang-cl) para compilar; si LLVM no está instalado, el conmutador NR4 aparece atenuado con una información sobre herramientas que indica que debe instalar LLVM desde llvm.org y recompilar. Haga clic en la pestaña **NR4** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                          |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Noise Estimation:**                | Botones de opción                                                                                            | MMSE                                                                                                           |
| **Adaptive Noise Estimation**        | Casilla de verificación                                                                                      | Habilitado                                                                                                     |
| **Reduction (dB):**                  | Deslizador                                                                                                   | 10.0                                                                                                           |
| **Smoothing (%):**                   | Deslizador                                                                                                   | 0                                                                                                              |
| **Whitening (%):**                   | Deslizador                                                                                                   | 0                                                                                                              |
| **Masking Depth:**                   | Deslizador                                                                                                   | 0.50                                                                                                           |
| **Suppression:**                     | Deslizador                                                                                                   | 0.50                                                                                                           |
| **Reset Defaults (ícono ↺)**         | Botón (ícono plano)                                                                                          | —                                                                                                              |

### Descripciones de los controles

**Noise Estimation:** selecciona el estimador de piso de ruido que usa NR4. `NR4NoiseEstimationMethod` se almacena como un entero: MMSE = 0, Brandt = 1, Martin = 2.

**Adaptive Noise Estimation** (`NR4AdaptiveNoise`) habilita la reestimación continua del piso de ruido. Actívelo cuando el piso de ruido varíe rápidamente.

**Reduction (dB):** (`NR4ReductionAmount`) establece la reducción máxima de ruido que NR4 aplica en decibeles. En 0.0 dB NR4 no aplica atenuación; en 40.0 dB aplica la supresión máxima disponible. El valor predeterminado de 10.0 dB es adecuado para la mayoría de las condiciones de SSB.

**Smoothing (%):** (`NR4SmoothingFactor`) aplica suavizado en el dominio del tiempo a la estimación de ruido de NR4. Si aumentar `NR4ReductionAmount` causa ruido musical, intente aumentar esto primero.

**Whitening (%):** (`NR4WhiteningFactor`) aplana la forma espectral del ruido residual después de la supresión.

**Masking Depth:** (`NR4MaskingDepth`) controla la profundidad del enmascaramiento espectral.

**Suppression:** (`NR4SuppressionStrength`) establece la fuerza general de supresión de NR4.

**Reset Defaults (ícono ↺)** restaura la pestaña NR4 a sus valores de fábrica: Noise Estimation = MMSE, Adaptive Noise Estimation = habilitado, Reduction = 10.0 dB, Smoothing = 0, Whitening = 0, Masking Depth = 0.50, Suppression = 0.50.

### Pasos — ajustar la cantidad de reducción de NR4

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Arrastre el deslizador **Reduction (dB):** hacia la izquierda para disminuir la supresión o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del deslizador.
4. Cierre el diálogo. El valor se guarda automáticamente.

### Consejos

- Comience cerca del valor predeterminado de 10.0 dB y aumente en pasos pequeños mientras monitorea la calidad del audio. Los valores superiores a 25–30 dB pueden introducir artefactos de procesamiento en señales más débiles.
- **Smoothing (%)** y **Suppression:** interactúan con la cantidad de reducción. Si aumentar `NR4ReductionAmount` causa ruido musical, intente aumentar primero el suavizado.
- Active **Adaptive Noise Estimation** cuando el piso de ruido varíe rápidamente para que NR4 reestime el piso continuamente.

---

## Pestaña MNR

MNR es el motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Está disponible solo en macOS. En las compilaciones de Windows y Linux, el conmutador MNR aparece atenuado: el motor no tiene backend en esas plataformas. Haga clic en la pestaña **MNR** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                          |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Enable MNR (macOS only)**          | Casilla de verificación                                                                                      | Leído del motor de audio                                                                                      |
| **Strength**                         | Deslizador                                                                                                   | 100                                                                                                            |

### Descripciones de los controles

**Enable MNR (macOS only)** (`MnrEnabled`) habilita el motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial de la casilla refleja el estado actual del motor de audio en el momento en que se abre el diálogo.

**Strength** (`MnrStrength`) ajusta la agresividad de MNR. 0 es supresión leve; 100 es supresión máxima. El valor se guarda internamente como un rango normalizado de 0.00–1.00.

---

## Pestaña RN2

La pestaña **RN2** (motor RNNoise) aloja un deslizador de **Noise Floor**. Establece el porcentaje de la señal original que permanece mezclado debajo del audio denoizado. Cero produce una supresión completa (silencio entre frases); 10–20% mantiene un piso de ruido constante y bajo para que el receptor siga sonando vivo.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                          |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Noise Floor (RN2 dry mix)**        | Deslizador                                                                                                   | 0                                                                                                              |

### Descripciones de los controles

**Noise Floor (RN2 dry mix)** (`Rn2SettingsModel`) mezcla un porcentaje de la señal original debajo del audio denoizado. Afecta solo al audio recibido; el denoizador de transmisión no cambia. El rango del deslizador es de 0–100%, donde 0 proporciona supresión completa.

### Pasos — ajustar el piso de ruido de RN2

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **RN2**.
3. Arrastre el deslizador **Noise Floor** al porcentaje deseado. Los valores más bajos dan una supresión más fuerte; los valores más altos mantienen más de la señal original en la salida.
4. Cierre el diálogo. El valor se guarda automáticamente.

---

## Pestaña BNR

La pestaña **BNR** muestra información sobre el motor de reducción de ruido de NVIDIA. La intensidad de BNR se controla desde el menú superpuesto (overlay), no desde este diálogo. En las compilaciones sin el SDK de NVIDIA Broadcast, el conmutador BNR aparece atenuado.

---

## Pestaña DFNR

DFNR utiliza la red neuronal DeepFilterNet3 para la reducción de ruido. Haga clic en la pestaña **DFNR** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                          |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Attenuation Limit**                | Deslizador                                                                                                   | 100                                                                                                            |
| **Post-Filter Beta**                 | Deslizador                                                                                                   | 0.00                                                                                                           |

### Descripciones de los controles

**Attenuation Limit** (`DfnrAttenLimit`) establece la atenuación máxima de ruido que DeepFilterNet3 puede aplicar. En 0, la salida pasa sin cambios; en 100 se aplica la atenuación máxima.

**Post-Filter Beta** (`DfnrPostFilterBeta`) aplica un post-filtro adicional para una supresión extra más allá de lo que DeepFilterNet3 proporciona por sí solo. En 0.00 el post-filtro está inactivo. El valor se almacena internamente multiplicado por 100.

---

## Solución de problemas

- **El deslizador no tiene efecto audible** — confirme que el motor cuya pestaña está ajustando es el motor de reducción de ruido activo para su slice. Habilitar otro motor simultáneamente puede enmascarar su contribución.
- **El habla suena hueca o distorsionada con valores altos de reducción de NR4** — baje **Reduction (dB):** y active **Adaptive Noise Estimation** para que la estimación del piso de ruido se mantenga precisa.
- **Los controles de MNR están atenuados** — MNR está disponible solo en macOS. En Linux y Windows, la pestaña MNR es informativa.
- **El conmutador NR4 está atenuado en Windows** — NR4 requiere LLVM (clang-cl) para compilar. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.
- **Los cambios parecen restablecerse** — cada pestaña tiene un botón **Reset Defaults**. Verifique que no lo haya hecho clic accidentalmente.
- **La apariencia del deslizador no coincide con las capturas de pantalla** — el diálogo ahora usa un estilo de deslizador con tema mediante `applyPrimarySliderStyle()`. Los colores de los deslizadores siguen el tema actual en lugar de un esquema de colores codificado. Para cambiar la apariencia de los deslizadores, cambie su tema activo en la configuración de temas de AetherSDR.

---

## Relacionado

- [Habilitar o deshabilitar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
