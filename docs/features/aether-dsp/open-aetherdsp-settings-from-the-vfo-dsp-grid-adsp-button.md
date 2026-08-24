# Abrir la configuración de AetherDSP desde el botón ADSP de la cuadrícula DSP del VFO

Abre el diálogo de Configuración de AetherDSP para que pueda ajustar los parámetros de reducción de ruido del lado del cliente sin tener que navegar por el sistema de menús.

## Antes de comenzar

- Debe haber un slice activo en el panadapter para que la cuadrícula DSP del VFO sea visible.

## Pasos

1. En la cuadrícula DSP del VFO por slice, localice el botón **ADSP**.
2. Haga clic en **ADSP**.

Se abre el diálogo de Configuración de AetherDSP, que muestra las pestañas del motor de reducción de ruido (NR2, NR4, MNR, DFNR, RN2, BNR).

## Consejos

- El mismo diálogo también puede abrirse desde el menú: **Settings > AetherDSP Settings...**, o haciendo doble clic en el mosaico ADSP en la tira de la cadena RX.
- Haga clic en el botón **ADSP** nuevamente mientras el diálogo está abierto: esto no alterna el diálogo; trae al frente un diálogo ya abierto. Para omitir toda la reducción de ruido del lado del cliente, consulte [Omitir todo el grupo NR del cliente desde el mosaico ADSP de la cadena RX](bypass-the-entire-client-nr-cluster-from-the-rx-chain-adsp-tile.md).

## Controles del diálogo

El diálogo de Configuración de AetherDSP proporciona seis pestañas de motor de reducción de ruido. Haga clic en una pestaña para seleccionarla; al hacer clic en la pestaña también se activa o se omite ese motor.

### NR2 (reducción de ruido musical)

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------|-------|------------------------|-------------|
| NR2 (pestaña) | pestaña | — | — | — | Selecciona la página NR2. Al hacer clic se activa u omite el motor NR2. Cuando está activado, AudioEngine activa la exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes. |
| Método de ganancia | botón de radio | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Se almacena como entero 0-3. |
| Método NPE | botón de radio | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| Filtro AE | casilla de verificación | Verdadero | — | `NR2AeFilter` | Alterna el post-filtro anti-artefactos. |
| Reducción: | deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. Los valores más altos suprimen más ruido pero pueden distorsionar el habla. |
| Suavizado: | deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. Los valores más altos proporcionan una adaptación más estable pero más lenta. |
| Umbral: | deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de habla. Los valores más bajos preservan el habla silenciosa pero pueden dejar pasar más ruido. |
| Restablecer valores predeterminados (icono ↺) | botón de pulsación | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, Reducción 1.50, Suavizado 0.85, Umbral 0.20. |

### NR4 (NR espectral libspecbleach)

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------|-------|------------------------|-------------|
| NR4 (pestaña) | pestaña | — | — | — | Selecciona la página NR4. |
| Estimación de ruido: | botón de radio | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido. Se almacena como entero 0-2. |
| Estimación adaptativa de ruido | casilla de verificación | Verdadero | — | `NR4AdaptiveNoise` | Habilita la re-estimación continua del piso de ruido. |
| Reducción (dB): | deslizador | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. Los valores más altos eliminan más ruido pero pueden afectar el habla. |
| Suavizado (%): | deslizador | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4. Los valores más altos producen una reducción más estable pero más lenta. |
| Blanqueamiento (%): | deslizador | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual para que suene más uniforme. |
| Profundidad de enmascaramiento: | deslizador | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. Los valores más altos suprimen más ruido en regiones de frecuencia enmascaradas. |
| Supresión: | deslizador | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Intensidad general de supresión NR4. |
| Restablecer valores predeterminados (icono ↺) | botón de pulsación | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50. |

### MNR (MMSE-Wiener de macOS)

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------|-------|------------------------|-------------|
| MNR (pestaña) | pestaña | — | — | — | Selecciona la página MNR. El conmutador MNR aparece atenuado en las compilaciones de Windows y Linux: el motor requiere un backend de macOS. |
| Habilitar MNR | casilla de verificación | — | — | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine. |
| Intensidad | deslizador | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se guarda como valor normalizado 0.00–1.00. |

### RN2 (RNNoise)

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------|-------|------------------------|-------------|
| RN2 (pestaña) | pestaña | — | — | — | Selecciona la página RN2. |
| Piso de ruido (mezcla seca RN2) | deslizador | 0 | 0–100 | — | Establece el porcentaje de la señal original que RN2 deja bajo el audio con reducción de ruido. Cero produce supresión total (silencio entre frases); 10–20% mantiene un piso silencioso constante para que el receptor siga sonando vivo. Afecta solo al audio recibido; el eliminador de ruido de transmisión no cambia. Se guarda mediante Rn2SettingsModel y se expone a la cadena DSP a través de la señal rn2DryMixChanged de AetherDspWidget. |

### BNR (NVIDIA Broadcast)

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------|-------|------------------------|-------------|
| BNR (pestaña) | pestaña | — | — | — | Selecciona la página BNR. La intensidad se controla desde el menú superpuesto. El conmutador BNR aparece atenuado en compilaciones sin el SDK de NVIDIA Broadcast. |

### DFNR (DeepFilterNet3)

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|----------------|-------|------------------------|-------------|
| DFNR (pestaña) | pestaña | — | — | — | Selecciona la página DeepFilterNet3. El conmutador DFNR aparece atenuado si DeepFilterNet no estaba disponible al momento de la compilación. |
| Límite de atenuación | deslizador | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo, 100 = máximo. |
| Beta de post-filtro | deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para una supresión extra. El deslizador almacena el valor * 100 internamente. |

## Comportamiento del marco del diálogo

El diálogo utiliza un estilo de ventana sin marco con una barra de título personalizada. La geometría y el estado del diálogo se guardan entre sesiones mediante la clave de configuración `AetherDspDialogGeometry`. Los colores de fondo y de texto del diálogo siguen el tema activo.

- **Barra de título**: barra de título de degradado de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo.
- **Minimizar (—)**: Minimiza el diálogo.
- **Maximizar (□)**: Maximiza o restaura el diálogo.
- **Cerrar (×)**: Cierra el diálogo.
- **Arrastrar para mover**: Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar.
- **Redimensionar en 8 ejes**: Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de acción de redimensionamiento es de 6 px alrededor del widget de contenido interno.

## Notas de plataforma

- **NR4** requiere LLVM (clang-cl) en Windows para compilar sus VLA de C99. Si LLVM no está instalado cuando se compiló AetherSDR, el conmutador NR4 aparece atenuado y muestra la información sobre herramientas: "NR4 requires LLVM (clang-cl) on Windows. Install LLVM from llvm.org and rebuild to enable NR4."
- **MNR** solo está disponible en macOS. En las compilaciones de Windows y Linux, el conmutador MNR aparece atenuado con la información sobre herramientas: "MNR is only available on macOS."
- **BNR** requiere el SDK de NVIDIA Broadcast al momento de la compilación. En compilaciones sin él, el conmutador BNR aparece atenuado.
- **DFNR** requiere que DeepFilterNet esté configurado y que AetherSDR se recompile. Si DeepFilterNet no estaba disponible al momento de la compilación, el conmutador DFNR aparece atenuado.
