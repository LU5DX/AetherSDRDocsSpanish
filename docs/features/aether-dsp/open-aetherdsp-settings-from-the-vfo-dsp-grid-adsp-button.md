# Abrir la configuración de AetherDSP desde el botón ADSP de la cuadrícula DSP del VFO

Abre el diálogo de configuración de AetherDSP para que pueda ajustar los parámetros de reducción de ruido del lado del cliente sin tener que navegar por el sistema de menús.

## Antes de comenzar

- Debe haber una sección activa en el panadapter para que la cuadrícula DSP del VFO sea visible.

## Pasos

1. En la cuadrícula DSP del VFO por sección, localice el botón **ADSP**.
2. Haga clic en **ADSP**.

Se abrirá el diálogo de configuración de AetherDSP, mostrando las pestañas del motor de reducción de ruido (NR2, NR4, MNR, DFNR, RN2, BNR).

## Consejos

- El mismo diálogo también se puede abrir desde el menú: **Settings > AetherDSP Settings...**, o haciendo doble clic en el mosaico ADSP de la barra RX Chain.
- Vuelva a hacer clic en el botón **ADSP** mientras el diálogo está abierto — esto no activa ni desactiva el diálogo; lo trae al frente si ya está abierto. Para omitir toda la reducción de ruido del lado del cliente, consulte [Omitir todo el grupo de NR del cliente desde el mosaico ADSP de la cadena RX](bypass-the-entire-client-nr-cluster-from-the-rx-chain-adsp-tile.md).

## Controles del diálogo

El diálogo de configuración de AetherDSP proporciona seis pestañas de motores de reducción de ruido. Haga clic en una pestaña para seleccionarla; al hacer clic en la pestaña también se activa o se omite ese motor.

### NR2 (reducción de ruido musical)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|---------------------|-------|----------------------|-------------|
| NR2 (pestaña) | pestaña | — | — | — | Selecciona la página NR2. Al hacer clic se activa o se omite el motor NR2. Cuando está activado, AudioEngine encadena la exclusión, desactivando DFNR y otros módulos mutuamente excluyentes. |
| Método de ganancia | botón de opción | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Se almacena como entero 0-3. |
| Método NPE | botón de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| Filtro AE | casilla de verificación | Verdadero | — | `NR2AeFilter` | Activa o desactiva el filtro posterior contra artefactos. |
| Reducción: | control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. Valores más altos suprimen más ruido pero pueden distorsionar el habla. |
| Piso de ganancia | control deslizante | — | 0.00–1.00 | `NR2GainFloor` | Establece el piso de ganancia mínimo para la reducción NR2. Valores más cercanos a 1.00 permiten menos atenuación, preservando más audio pero reduciendo la supresión de ruido. |
| Suavizado: | control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. Valores más altos proporcionan una adaptación más estable pero más lenta. |
| Umbral: | control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. Valores más bajos preservan el habla suave pero pueden dejar pasar más ruido. |
| Usar geometría original | casilla de verificación | — | — | `NR2UseOriginalGeometry` | Activa el cálculo de geometría de reducción de ruido original en lugar del algoritmo actualizado. |
| Restablecer valores predeterminados (icono ↺) | botón de pulsación | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, piso de ganancia predeterminado, Suavizado 0.85, Umbral 0.20. |

### NR4 (NR espectral libspecbleach)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|---------------------|-------|----------------------|-------------|
| NR4 (pestaña) | pestaña | — | — | — | Selecciona la página NR4. |
| Estimación de ruido: | botón de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2. |
| Estimación de ruido adaptativa | casilla de verificación | Verdadero | — | `NR4AdaptiveNoise` | Activa la reestimación continua del piso de ruido. |
| Reducción (dB): | control deslizante | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. Valores más altos eliminan más ruido pero pueden afectar el habla. |
| Suavizado (%): | control deslizante | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4. Valores más altos producen una reducción más estable pero más lenta. |
| Blanqueamiento (%): | control deslizante | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual para que suene más uniforme. |
| Profundidad de enmascaramiento: | control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. Valores más altos suprimen más ruido en regiones de frecuencia enmascaradas. |
| Supresión: | control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión NR4. |
| Restablecer valores predeterminados (icono ↺) | botón de pulsación | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50. |

### MNR (MMSE-Wiener de macOS)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|---------------------|-------|----------------------|-------------|
| MNR (pestaña) | pestaña | — | — | — | Selecciona la página MNR. La activación de MNR está atenuada en las compilaciones de Windows y Linux — el motor requiere un backend de macOS. |
| Activar MNR | casilla de verificación | — | — | `MnrEnabled` | Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine. |
| Intensidad | control deslizante | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva como valor normalizado de 0.00 a 1.00. |

### RN2 (RNNoise)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|---------------------|-------|----------------------|-------------|
| RN2 (pestaña) | pestaña | — | — | — | Selecciona la página RN2. Esta página es puramente informativa — no tiene parámetros ajustables. |

### BNR (NVIDIA Broadcast)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|---------------------|-------|----------------------|-------------|
| BNR (pestaña) | pestaña | — | — | — | Selecciona la página BNR. La intensidad se controla desde el menú superpuesto. La activación de BNR está atenuada en las compilaciones sin el SDK de NVIDIA Broadcast. |

### DFNR (DeepFilterNet3)

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---------|------|---------------------|-------|----------------------|-------------|
| DFNR (pestaña) | pestaña | — | — | — | Selecciona la página DeepFilterNet3. La activación de DFNR está atenuada si DeepFilterNet no estaba disponible en el momento de la compilación. |
| Límite de atenuación | control deslizante | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo, 100 = máximo. |
| Beta del filtro posterior | control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro posterior adicional para una supresión extra. El control deslizante almacena el valor * 100 internamente. |

## Comportamiento de la ventana del diálogo

El diálogo utiliza un estilo de ventana sin marco con una barra de título personalizada. La geometría y el estado del diálogo se conservan entre sesiones mediante la clave de configuración `AetherDspDialogGeometry`. Los colores de fondo y de texto del diálogo siguen el tema activo.

- **Barra de título**: Barra de título degradada de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo.
- **Minimizar (—)**: Minimiza el diálogo.
- **Maximizar (□)**: Maximiza o restaura el diálogo.
- **Cerrar (×)**: Cierra el diálogo.
- **Arrastrar para mover**: Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar.
- **Redimensionar en 8 ejes**: Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de impacto de redimensionamiento es de 6 píxeles alrededor del widget de contenido interno.

## Notas de plataforma

- **NR4** requiere LLVM (clang-cl) en Windows para compilar sus VLA de C99. Si LLVM no estaba instalado cuando se compiló AetherSDR, la activación de NR4 está atenuada y muestra la información sobre herramientas: "NR4 requiere LLVM (clang-cl) en Windows. Instale LLVM desde llvm.org y recompile para activar NR4."
- **MNR** solo está disponible en macOS. En las compilaciones de Windows y Linux, la activación de MNR está atenuada con la información sobre herramientas: "MNR solo está disponible en macOS."
- **BNR** requiere el SDK de NVIDIA Broadcast en tiempo de compilación. En las compilaciones sin él, la activación de BNR está atenuada.
- **DFNR** requiere que DeepFilterNet esté configurado y que AetherSDR se recompile. Si DeepFilterNet no estaba disponible en el momento de la compilación, la activación de DFNR está atenuada.
