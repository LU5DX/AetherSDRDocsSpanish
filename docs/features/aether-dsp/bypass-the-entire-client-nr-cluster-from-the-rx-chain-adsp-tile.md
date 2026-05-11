# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP proporciona configuración avanzada para todos los motores de reducción de ruido del lado del cliente en AetherSDR. Incluye seis módulos DSP: NR2, NR4, MNR, DFNR, RN2 y BNR.

## Cómo abrir el diálogo

- Desde la tira de la cadena RX, haga doble clic en el mosaico **ADSP**.
- Desde la cuadrícula DSP del VFO, haga clic en el botón **ADSP**.

## Ventana del diálogo

El diálogo tiene una barra de título sin marco con un glifo de agarre (⋮⋮) a la izquierda. La barra de título incluye tres botones:

- — (Minimizar) — Minimiza el diálogo.
- □ (Maximizar) — Maximiza o restaura el diálogo.
- × (Cerrar) — Cierra el diálogo.

Arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Arrastre cualquier borde o esquina para cambiar el tamaño (zona de cambio de tamaño de 6 píxeles).

### Modo sin marco

La Configuración de AetherDSP usa el modo sin marco de forma predeterminada. Para cambiar entre ventanas sin marco y decoraciones nativas:

1. Abra **Settings > Appearance** desde el menú principal.
2. Active o desactive **Frameless Windows**.
3. El cambio surtirá efecto la próxima vez que se abra la Configuración de AetherDSP.

## Fila de alternancia

La parte superior del diálogo contiene seis botones de alternancia que sirven tanto como selectores de pestañas como controles de activación/desactivación del motor:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Reducción de ruido espectral libspecbleach
- **MNR** — Reducción de ruido MMSE-Wiener de macOS (atenuado en Windows/Linux)
- **DFNR** — Reducción de ruido neuronal DeepFilterNet3
- **RN2** — Reducción de ruido neuronal RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** — Reducción de ruido neuronal NVIDIA Broadcast (atenuado sin NVIDIA Broadcast SDK)

Al hacer clic en un botón de alternancia se activa ese motor y se selecciona su pestaña. Al hacer clic nuevamente se desactiva el motor. Solo un motor puede estar activo a la vez — NR2, NR4 y DFNR son mutuamente excluyentes. MNR y BNR pueden apilarse en algunas compilaciones.

## Pestaña NR2

Controles para el motor de reducción de ruido musical.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-----------------|----------------|
| Gain Method | Botón de opción | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia (almacenado como entero 0-3). |
| NPE Method | Botón de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido (almacenado como entero 0-2). |
| AE Filter (eliminación de artefactos) | Casilla de verificación | Verdadero | — | `NR2AeFilter` | Activa/desactiva el postfiltro antiartefactos. |
| Reduction: | Deslizador | 1.50 | 0.50-2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. |
| Smoothing: | Deslizador | 0.85 | 0.50-0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. |
| Threshold: | Deslizador | 0.20 | 0.05-0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20). |

## Pestaña NR4

Controles para el motor de reducción de ruido espectral libspecbleach.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-----------------|----------------|
| Noise Estimation: | Botón de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido (almacenado como entero 0-2). |
| Adaptive Noise Estimation | Casilla de verificación | Verdadero | — | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| Reduction (dB): | Deslizador | 10.0 | 0.0-40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. |
| Smoothing (%): | Deslizador | 0 | 0-100 | `NR4SmoothingFactor` | Suavizado en el dominio temporal de la estimación de ruido NR4. |
| Whitening (%): | Deslizador | 0 | 0-100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| Masking Depth: | Deslizador | 0.50 | 0.00-1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| Suppression: | Deslizador | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` | Fuerza general de supresión NR4. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50). |

**Nota:** NR4 requiere LLVM (clang-cl) en Windows. La alternancia se atenúa si LLVM no está instalado. Instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

## Pestaña MNR

Controles para el motor de reducción de ruido MMSE-Wiener de macOS. Esta pestaña y sus controles solo están disponibles en compilaciones de macOS.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-----------------|----------------|
| Enable MNR (solo macOS) | Casilla de verificación | — | — | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. |
| Strength | Deslizador | 100 | 0-100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). |

## Pestaña DFNR

Controles para el motor de reducción de ruido neuronal DeepFilterNet3.

**Nota:** DeepFilterNet3 es un sistema avanzado de reducción de ruido basado en redes neuronales que utiliza aprendizaje profundo para suprimir el ruido mientras preserva la calidad de la voz. Puede requerir recursos significativos de CPU.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-----------------|----------------|
| Attenuation Limit | Deslizador | 100 | 0-100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = supresión máxima. |
| Post-Filter Beta | Deslizador | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` | Aplica un postfiltro adicional para una supresión extra. |

**Disponible en v26.5.1.** DFNR reemplaza las implementaciones anteriores de reducción de ruido neuronal.

## Pestaña RN2

Selecciona la página de reducción de ruido neuronal RNNoise. Esta pestaña es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

Selecciona la página de reducción de ruido neuronal NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto. La alternancia se atenúa en compilaciones sin NVIDIA Broadcast SDK.

## Cómo omitir todos los motores NR del cliente

Para deshabilitar rápidamente toda la reducción de ruido del lado del cliente sin abrir el diálogo de Configuración de AetherDSP:

1. Localice el mosaico **ADSP** en la tira de la cadena RX.
2. Haga doble clic en el mosaico **ADSP** para abrir la Configuración de AetherDSP.
3. En la fila de alternancia en la parte superior, haga clic en cada alternancia de reducción de ruido activa (encendida) para desactivarla.
4. Continúe hasta que todas las alternancias estén atenuadas.

El mosaico ADSP se actualiza para reflejar el estado de omisión. Ahora ningún motor NR del cliente está activo, lo que devuelve el audio a la transmisión de audio sin procesar desde la radio.

## Consejos

- Las seis alternancias DSP (NR2, NR4, MNR, DFNR, RN2, BNR) sirven tanto como selectores de pestañas como controles de activación/desactivación del motor.
- NR2, NR4 y DFNR son mutuamente excluyentes — solo uno puede estar activo a la vez.
- MNR y BNR pueden apilarse con otros motores en algunas compilaciones.
- El botón Reset Defaults (icono ↺) en cada pestaña restaura los parámetros de ese motor a sus valores predeterminados.
- Los ajustes se conservan entre sesiones.
