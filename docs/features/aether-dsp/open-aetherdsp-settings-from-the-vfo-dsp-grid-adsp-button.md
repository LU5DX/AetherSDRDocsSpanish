# Abrir la Configuración de AetherDSP desde el botón ADSP de la cuadrícula DSP del VFO

Abre el cuadro de diálogo Configuración de AetherDSP para que pueda ajustar los parámetros de reducción de ruido del lado del cliente sin tener que navegar por el sistema de menús.

## Antes de comenzar

- Debe haber un slice activo en el panadapter para que la cuadrícula DSP del VFO sea visible.

## Pasos

1. En la cuadrícula DSP del VFO por slice, localice el botón **ADSP**.
2. Haga clic en **ADSP**.

Se abrirá el cuadro de diálogo Configuración de AetherDSP, que muestra las pestañas del motor de reducción de ruido (NR2, NR4, MNR, DFNR, RN2, BNR).

## Consejos

- También puede abrir el mismo cuadro de diálogo desde el menú: **Settings > AetherDSP Settings...**, o haciendo doble clic en el mosaico ADSP en la barra de la cadena RX.
- Vuelva a hacer clic en el botón **ADSP** mientras el cuadro de diálogo está abierto; esto no alterna el cuadro de diálogo, sino que trae al frente un diálogo ya abierto. Para omitir toda la reducción de ruido del lado del cliente, consulte [Omitir todo el clúster de NR del cliente desde el mosaico ADSP de la cadena RX](bypass-the-entire-client-nr-cluster-from-the-rx-chain-adsp-tile.md).

## Controles del cuadro de diálogo

El cuadro de diálogo Configuración de AetherDSP proporciona seis pestañas de motor de reducción de ruido. Haga clic en una pestaña para seleccionarla; al hacer clic en la pestaña también se activa o se omite ese motor.

### NR2 (reducción de ruido musical)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------------|-------|------------------------|-------------|
| NR2 (pestaña) | pestaña | — | — | — | Selecciona la página NR2. Al hacer clic se activa o se omite el motor NR2. Cuando está activado, AudioEngine se encadena con exclusión, desactivando DFNR y otros módulos mutuamente excluyentes. |
| Gain Method | radio_button | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Se almacena como entero 0-3. |
| NPE Method | radio_button | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| AE Filter | checkbox | Verdadero | — | `NR2AeFilter` | Activa o desactiva el post-filtro anti-artefacto. |
| Reduction: | slider | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. |
| Smoothing: | slider | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. |
| Threshold: | slider | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |
| Reset Defaults (icono ↺) | push_button | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, 1.50/0.85/0.20. |

### NR4 (NR espectral libspecbleach)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------------|-------|------------------------|-------------|
| NR4 (pestaña) | pestaña | — | — | — | Selecciona la página NR4. |
| Noise Estimation: | radio_button | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2. |
| Adaptive Noise Estimation | checkbox | Verdadero | — | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| Reduction (dB): | slider | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la cantidad máxima de reducción de ruido NR4 en dB. |
| Smoothing (%): | slider | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4. |
| Whitening (%): | slider | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| Masking Depth: | slider | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| Suppression: | slider | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión NR4. |
| Reset Defaults (icono ↺) | push_button | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50. |

### MNR (MMSE-Wiener de macOS)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------------|-------|------------------------|-------------|
| MNR (pestaña) | pestaña | — | — | — | Selecciona la página MNR. La alternancia MNR está atenuada en las compilaciones de Windows y Linux: el motor requiere un backend de macOS. |
| Enable MNR | checkbox | — | — | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. |
| Strength | slider | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máxima). Se persiste normalizado 0.00–1.00. |

### RN2 (RNNoise)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------------|-------|------------------------|-------------|
| RN2 (pestaña) | pestaña | — | — | — | Selecciona la página RN2. Esta página es puramente informativa: no tiene parámetros ajustables. |

### BNR (NVIDIA Broadcast)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------------|-------|------------------------|-------------|
| BNR (pestaña) | pestaña | — | — | — | Selecciona la página BNR. La intensidad se controla desde el menú superpuesto. La alternancia BNR está atenuada en las compilaciones sin el SDK de NVIDIA Broadcast. |

### DFNR (DeepFilterNet3)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------------|-------|------------------------|-------------|
| DFNR (pestaña) | pestaña | — | — | — | Selecciona la página DeepFilterNet3. |
| Attenuation Limit | slider | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo, 100 = máximo. |
| Post-Filter Beta | slider | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para una supresión extra. |

## Comportamiento del marco del cuadro de diálogo

El cuadro de diálogo admite modos de ventana sin marco y nativo, controlados por la preferencia del usuario en **Settings > Configuration** (clave de configuración `FramelessWindow`). Cuando el modo sin marco está activo, el marco cambia en consecuencia:

- **Barra de título**: Barra de título degradada sin marco de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del cuadro de diálogo.
- **Minimize (—)**: Minimiza el cuadro de diálogo.
- **Maximize (□)**: Maximiza o restaura el cuadro de diálogo.
- **Close (×)**: Cierra el cuadro de diálogo.
- **Arrastrar para mover**: Haga clic y arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar.
- **Redimensionar en 8 ejes**: Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de impacto de redimensionamiento es de 6 px alrededor del widget de contenido interior.

Cuando el modo de ventana nativa está activo, se utiliza el marco de ventana estándar del sistema operativo.

## Notas de plataforma

- **NR4** requiere LLVM (clang-cl) en Windows para compilar sus VLA de C99. Si LLVM no estaba instalado cuando se compiló AetherSDR, la alternancia NR4 está atenuada y muestra el tooltip: "NR4 requires LLVM (clang-cl) on Windows. Install LLVM from llvm.org and rebuild to enable NR4."
- **MNR** solo está disponible en macOS. En las compilaciones de Windows y Linux, la alternancia MNR está atenuada con el tooltip: "MNR is only available on macOS."
- **BNR** requiere el SDK de NVIDIA Broadcast en tiempo de compilación. En las compilaciones sin él, la alternancia BNR está atenuada.
