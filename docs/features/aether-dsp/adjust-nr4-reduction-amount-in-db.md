# Configuración de AetherDSP

El diálogo **Configuración de AetherDSP** (`Settings > AetherDSP Settings...`) controla los motores de reducción de ruido del lado del cliente integrados en AetherSDR: NR2, NR4, MNR, RN2, BNR y DFNR. Puede abrirlo en cualquier momento; no se requiere una conexión de radio para cambiar estos parámetros. Todos los valores se guardan automáticamente al cerrar el diálogo. Los seis módulos DSP se seleccionan mediante una fila de botones de alternancia en la parte superior; al hacer clic en un botón también se activa o se desactiva ese motor.

El diálogo utiliza una barra de título personalizada sin marco con controles de ventana que coinciden con la familia cromática de NetworkDiagnosticsDialog y AetherialAudioStrip. Arrastre la barra de título para mover el diálogo; haga doble clic para alternar maximizar/restaurar. Arrastre cualquier borde o esquina para cambiar el tamaño.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Decida qué motor de reducción de ruido está activo para su slice antes de ajustar sus parámetros. Ajustar un motor deshabilitado no tiene efecto audible.

## Abrir el diálogo

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Se abre el diálogo **Configuración de AetherDSP**. Seleccione la pestaña del motor que desea ajustar.

---

## Pestaña NR2

NR2 es el motor de reducción de ruido musical. Haga clic en la pestaña **NR2** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                           |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Gain Method**                      | Botones de opción                                                                                            | Gamma                                                                                                          |
| **NPE Method**                       | Botones de opción                                                                                            | OSMS                                                                                                           |
| **AE Filter (eliminación de artefactos)** | Casilla de verificación                                                                                     | Habilitado                                                                                                     |
| **Reduction:**                       | Deslizador                                                                                                   | 1.50                                                                                                           |
| **Smoothing:**                       | Deslizador                                                                                                   | 0.85                                                                                                           |
| **Threshold:**                       | Deslizador                                                                                                   | 0.20                                                                                                           |
| **Restablecer valores predeterminados (icono ↺)** | Botón (icono plano)                                                                                          | —                                                                                                              |

### Descripciones de los controles

**Gain Method** selecciona la asignación de la curva de ganancia que utiliza NR2. `NR2GainMethod` se almacena como un entero: Linear = 0, Log = 1, Gamma = 2, Trained = 3. Gamma es adecuado para la mayoría de los modos de voz.

**NPE Method** selecciona el estimador de potencia de ruido. `NR2NpeMethod` se almacena como un entero: OSMS = 0, MMSE = 1, NSTAT = 2.

**AE Filter (eliminación de artefactos)** activa o desactiva el post-filtro antiartefactos (`NR2AeFilter`). Manténgalo habilitado a menos que esté probando específicamente la salida NR2 sin procesar.

**Reduction:** (`NR2GainMax`) establece la profundidad máxima de reducción que NR2 puede aplicar. Los valores más altos suprimen más ruido, pero pueden afectar la naturalidad del habla.

**Smoothing:** (`NR2GainSmooth`) controla la rapidez con la que la estimación de ruido sigue los cambios de la señal. Los valores más altos producen un seguimiento más suave pero más lento.

**Threshold:** (`NR2Qspp`) establece el umbral de probabilidad de presencia de voz por debajo del cual NR2 trata el audio como ruido. Aumente este valor si se suprime el habla; redúzcalo si el ruido se cuela durante las pausas.

**Restablecer valores predeterminados (icono ↺)** restaura la pestaña NR2 a sus valores de fábrica: Gain Method = Gamma, NPE Method = OSMS, AE Filter = habilitado, Reduction = 1.50, Smoothing = 0.85, Threshold = 0.20.

### Pasos: ajustar la profundidad de reducción de NR2

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Arrastre el deslizador **Reduction:** al valor deseado (predeterminado 1.50).
4. Cierre el diálogo. El valor se guarda automáticamente.

---

## Pestaña NR4

NR4 utiliza la librería libspecbleach. Haga clic en la pestaña **NR4** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                           |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Noise Estimation:**                | Botones de opción                                                                                            | MMSE                                                                                                           |
| **Adaptive Noise Estimation**        | Casilla de verificación                                                                                      | Habilitado                                                                                                     |
| **Reduction (dB):**                  | Deslizador                                                                                                   | 10.0                                                                                                           |
| **Smoothing (%):**                   | Deslizador                                                                                                   | 0                                                                                                              |
| **Whitening (%):**                   | Deslizador                                                                                                   | 0                                                                                                              |
| **Masking Depth:**                   | Deslizador                                                                                                   | 0.50                                                                                                           |
| **Suppression:**                     | Deslizador                                                                                                   | 0.50                                                                                                           |
| **Restablecer valores predeterminados (icono ↺)** | Botón (icono plano)                                                                                          | —                                                                                                              |

### Descripciones de los controles

**Noise Estimation:** selecciona el estimador de piso de ruido que utiliza NR4. `NR4NoiseEstimationMethod` se almacena como un entero: MMSE = 0, Brandt = 1, Martin = 2.

**Adaptive Noise Estimation** (`NR4AdaptiveNoise`) habilita la reestimación continua del piso de ruido. Habilite esta opción cuando el piso de ruido varíe rápidamente.

**Reduction (dB):** (`NR4ReductionAmount`) establece la reducción máxima de ruido que NR4 aplica en decibelios. A 0.0 dB, NR4 no aplica atenuación; a 40.0 dB, aplica la supresión máxima disponible. El valor predeterminado de 10.0 dB es adecuado para la mayoría de las condiciones de SSB.

**Smoothing (%):** (`NR4SmoothingFactor`) aplica suavizado en el dominio del tiempo a la estimación de ruido de NR4. Si al aumentar `NR4ReductionAmount` se produce ruido musical, intente aumentar este valor primero.

**Whitening (%):** (`NR4WhiteningFactor`) aplana la forma espectral del ruido residual después de la supresión.

**Masking Depth:** (`NR4MaskingDepth`) controla la profundidad del enmascaramiento espectral.

**Suppression:** (`NR4SuppressionStrength`) establece la fuerza general de supresión de NR4.

**Restablecer valores predeterminados (icono ↺)** restaura la pestaña NR4 a sus valores de fábrica: Noise Estimation = MMSE, Adaptive Noise Estimation = habilitado, Reduction = 10.0 dB, Smoothing = 0, Whitening = 0, Masking Depth = 0.50, Suppression = 0.50.

### Pasos: ajustar la cantidad de reducción de NR4

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Arrastre el deslizador **Reduction (dB):** hacia la izquierda para disminuir la supresión o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del deslizador.
4. Cierre el diálogo. El valor se guarda automáticamente.

### Consejos

- Comience cerca del valor predeterminado de 10.0 dB y aumente en pasos pequeños mientras monitorea la calidad del audio. Los valores por encima de 25–30 dB pueden introducir artefactos de procesamiento en señales más débiles.
- **Smoothing (%):** y **Suppression:** interactúan con la cantidad de reducción. Si al aumentar `NR4ReductionAmount` se produce ruido musical, intente aumentar primero el suavizado.
- Habilite **Adaptive Noise Estimation** cuando el piso de ruido varíe rápidamente para que NR4 reestime el piso continuamente.

---

## Pestaña MNR

MNR es el motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. Está disponible solo en macOS. En las compilaciones para Windows y Linux, el botón de alternancia MNR está atenuado; el motor no tiene backend en esas plataformas. Haga clic en la pestaña **MNR** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                           |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Enable MNR (solo macOS)**          | Casilla de verificación                                                                                      | Leído del motor de audio                                                                                      |
| **Strength**                         | Deslizador                                                                                                   | 100                                                                                                            |

### Descripciones de los controles

**Enable MNR (solo macOS)** (`MnrEnabled`) habilita el motor de reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial de la casilla de verificación refleja el estado actual del motor de audio en el momento en que se abre el diálogo.

**Strength** (`MnrStrength`) ajusta la agresividad de MNR. 0 es supresión leve; 100 es supresión máxima. El valor se conserva internamente como un rango normalizado de 0.00 a 1.00.

---

## Pestaña RN2

La pestaña **RN2** muestra información sobre el motor RNNoise. No hay parámetros ajustables en esta pestaña.

---

## Pestaña BNR

La pestaña **BNR** muestra información sobre el motor de reducción de ruido de NVIDIA. La intensidad de BNR se controla desde el menú superpuesto, no desde este diálogo. En las compilaciones sin el SDK NVIDIA Broadcast, el botón de alternancia BNR está atenuado.

---

## Pestaña DFNR

DFNR utiliza la red neuronal DeepFilterNet3 para la reducción de ruido. Haga clic en la pestaña **DFNR** para acceder a sus controles.

### Controles

| Control                              | Tipo                                                                                                         | Valor predeterminado                                                                                           |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **Attenuation Limit**                | Deslizador                                                                                                   | 100                                                                                                            |
| **Post-Filter Beta**                 | Deslizador                                                                                                   | 0.00                                                                                                           |

### Descripciones de los controles

**Attenuation Limit** (`DfnrAttenLimit`) establece la atenuación máxima de ruido que DeepFilterNet3 puede aplicar. En 0, la salida pasa sin cambios; en 100, se aplica la atenuación máxima.

**Post-Filter Beta** (`DfnrPostFilterBeta`) aplica un post-filtro adicional para una supresión extra más allá de la que DeepFilterNet3 proporciona por sí solo. En 0.00, el post-filtro está inactivo. El valor se almacena internamente multiplicado por 100.

---

## Solución de problemas

- **El deslizador no tiene efecto audible** — confirme que el motor cuya pestaña está ajustando es el motor de reducción de ruido activo para su slice. Habilitar otro motor simultáneamente puede enmascarar su contribución.
- **El habla suena hueca o distorsionada con valores altos de reducción de NR4** — reduzca **Reduction (dB):** y habilite **Adaptive Noise Estimation** para que la estimación del piso de ruido se mantenga precisa.
- **Los controles de MNR están atenuados** — MNR está disponible solo en macOS. En Linux y Windows, la pestaña MNR es informativa.
- **Los cambios parecen restablecerse** — cada pestaña tiene un botón **Restablecer valores predeterminados**. Verifique que no lo haya presionado accidentalmente.

---

## Relacionado

- [Enable or disable NR4 adaptive noise estimation](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Tune NR4 masking depth and suppression strength](tune-nr4-masking-depth-and-suppression-strength.md)
- [Reset NR2 or NR4 parameters to defaults](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Choosing the right noise reduction: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
