# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP permite la configuración avanzada de todos los motores de reducción de ruido del lado del cliente en AetherSDR. Incluye seis módulos DSP: NR2, NR4, MNR, DFNR, RN2 y BNR.

## Cómo abrir el diálogo

- En la tira de la cadena RX, haga doble clic en el mosaico **ADSP**.
- En la cuadrícula DSP del VFO, haga clic en el botón **ADSP**.

## Ventana del diálogo

El diálogo tiene una barra de título sin marco con un glifo de agarre (⋮⋮) a la izquierda. La barra de título incluye tres botones:

- — (Minimizar) — Minimiza el diálogo.
- □ (Maximizar) — Maximiza o restaura el diálogo.
- × (Cerrar) — Cierra el diálogo.

Arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. Arrastre cualquier borde o esquina para cambiar el tamaño (zona de cambio de tamaño de 6 píxeles).

La posición y el tamaño del diálogo se guardan automáticamente entre sesiones mediante la clave de configuración `AetherDspDialogGeometry`.

El diálogo utiliza un estilo adaptado al tema aplicado a través de `ThemeManager`. Los colores se derivan del tema de color activo en lugar de valores codificados.

## Fila de conmutación

La parte superior del diálogo contiene seis botones de conmutación que sirven tanto como selectores de pestañas como controles de activación/desactivación del motor:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Reducción de ruido espectral libspecbleach
- **MNR** — Reducción de ruido MMSE-Wiener de macOS (atenuado en Windows/Linux)
- **DFNR** — Reducción de ruido neuronal DeepFilterNet3
- **RN2** — Reducción de ruido neuronal RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** — Reducción de ruido neuronal NVIDIA Broadcast (atenuado sin el SDK de NVIDIA Broadcast)

Al hacer clic en un motor, se activa y se selecciona su pestaña. Al hacer clic nuevamente, se desactiva el motor. Solo un motor puede estar activo a la vez: NR2, NR4 y DFNR son mutuamente excluyentes. MNR y BNR pueden apilarse en algunas compilaciones.

## Pestaña NR2

Controles para el motor de reducción de ruido musical.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Gain Method | Botón de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona el mapeo de la curva de ganancia (almacenado como entero 0-3). |
| NPE Method | Botón de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido (almacenado como entero 0-2). |
| AE Filter (artifact elimination) | Casilla de verificación | True | — | `NR2AeFilter` | Alterna el filtro posterior antiartefacto. |
| Reduction: | Deslizador | 1.50 | 0.50-2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción de NR2. |
| Smoothing: | Deslizador | 0.85 | 0.50-0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. |
| Threshold: | Deslizador | 0.20 | 0.05-0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20). |

Los deslizadores en esta pestaña utilizan un estilo adaptado al tema mediante `applyPrimarySliderStyle()`.

## Pestaña NR4

Controles para el motor de reducción de ruido espectral libspecbleach.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Noise Estimation: | Botón de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido (almacenado como entero 0-2). |
| Adaptive Noise Estimation | Casilla de verificación | True | — | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| Reduction (dB): | Deslizador | 10.0 | 0.0-40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido de NR4 en dB. |
| Smoothing (%): | Deslizador | 0 | 0-100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido de NR4. |
| Whitening (%): | Deslizador | 0 | 0-100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| Masking Depth: | Deslizador | 0.50 | 0.00-1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| Suppression: | Deslizador | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` | Fuerza general de supresión de NR4. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50). |

Los deslizadores en esta pestaña utilizan un estilo adaptado al tema mediante `applyPrimarySliderStyle()`.

**Nota:** NR4 requiere LLVM (clang-cl) en Windows. El conmutador está atenuado si LLVM no está instalado. Instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

## Pestaña MNR

Controles para el motor de reducción de ruido MMSE-Wiener de macOS. Esta pestaña y sus controles solo están disponibles en compilaciones de macOS.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Enable MNR (macOS only) | Casilla de verificación | — | — | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. |
| Strength | Deslizador | 100 | 0-100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). |

## Pestaña DFNR

Controles para el motor de reducción de ruido neuronal DeepFilterNet3.

**Nota:** DeepFilterNet3 es un sistema avanzado de reducción de ruido basado en redes neuronales que utiliza aprendizaje profundo para suprimir el ruido mientras preserva la calidad del habla. Puede requerir recursos significativos de CPU.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Attenuation Limit | Deslizador | 100 | 0-100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = supresión máxima. |
| Post-Filter Beta | Deslizador | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` | Aplica un filtro posterior adicional para una supresión extra. |

## Pestaña RN2

Selecciona la página de reducción de ruido neuronal RNNoise. Esta pestaña es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

Selecciona la página de reducción de ruido neuronal NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto. El conmutador está atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Cómo omitir todos los motores NR del cliente

Para deshabilitar rápidamente toda la reducción de ruido del lado del cliente sin abrir el diálogo de Configuración de AetherDSP:

1. Localice el mosaico **ADSP** en la tira de la cadena RX.
2. Haga doble clic en el mosaico **ADSP** para abrir la Configuración de AetherDSP.
3. En la fila de conmutación en la parte superior, haga clic en cada conmutador de reducción de ruido activo (iluminado) para desactivarlo.
4. Continúe hasta que todos los conmutadores estén atenuados.

El mosaico ADSP se actualiza para reflejar el estado de omisión. Ahora no hay motores NR del cliente activos, lo que devuelve el audio al flujo de audio sin procesar de la porción de la radio.

## Consejos

- Los seis conmutadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) sirven tanto como selectores de pestañas como controles de activación/desactivación del motor.
- NR2, NR4 y DFNR son mutuamente excluyentes: solo uno puede estar activo a la vez.
- MNR y BNR pueden apilarse con otros motores en algunas compilaciones.
- El botón Reset Defaults (icono ↺) en cada pestaña restaura los parámetros de ese motor a sus valores predeterminados.
- La configuración se conserva entre sesiones.
- El diálogo utiliza un estilo adaptado al tema. Los colores se obtienen del tema de color activo en lugar de valores fijos.
