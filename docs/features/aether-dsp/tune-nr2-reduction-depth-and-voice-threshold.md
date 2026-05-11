# Configuración de AetherDSP

Esta página explica cómo ajustar los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se seleccionan mediante botones de alternancia en la parte superior del diálogo; al hacer clic en un botón también se activa o desactiva ese motor.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para cambiar estos ajustes.
- El motor de reducción de ruido seleccionado ya debe estar activo en un slice del receptor para que los cambios tengan efecto audible de inmediato.
- MNR solo está disponible en versiones para macOS. El botón de alternancia de MNR aparece atenuado en Windows y Linux.
- BNR solo está disponible en versiones que incluyen el SDK de NVIDIA Broadcast. De lo contrario, el botón de alternancia de BNR aparece atenuado.
- NR4 requiere LLVM (clang-cl) en Windows. El botón de alternancia de NR4 aparece atenuado en versiones de Windows compiladas sin LLVM. Instale LLVM desde llvm.org y recompile para habilitar NR4.

## Abrir el diálogo

Haga clic en `Settings > AetherDSP Settings...`.

## Resumen del diálogo

El diálogo Configuración de AetherDSP tiene una barra de título que se adapta a la configuración de aplicación **FramelessWindow**. Cuando el modo sin marco está habilitado (valor predeterminado), se muestra una barra de título personalizada que coincide con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip. La barra de título tiene 18 px de alto con un fondo de degradado azul. De izquierda a derecha contiene:

- Un glifo de agarre (⋮⋮) — solo indicador visual
- El título del diálogo "AetherDSP Settings"
- Botón **—** (Minimizar) — minimiza el diálogo
- Botón **□** (Maximizar) — maximiza o restaura el diálogo
- Botón **×** (Cerrar) — cierra el diálogo

Arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Arrastre cualquier borde o esquina para redimensionar el diálogo (redimensionamiento de 8 ejes con una zona de detección de 6 px). Cuando el modo sin marco está deshabilitado, se usan las decoraciones de ventana estándar del sistema operativo.

El diálogo guarda su tamaño y posición entre sesiones.

## Seleccionar y activar un motor de reducción de ruido

Seis botones de alternancia están dispuestos en una fila en la parte superior del diálogo. Al hacer clic en un botón:

1. Selecciona la página de parámetros de ese motor
2. Activa el motor (si estaba desactivado) o lo desactiva (si estaba activo)

Cuando se activa NR2, el AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

Motores disponibles:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Motor basado en libspecbleach (requiere LLVM en Windows)
- **MNR** — Motor MMSE-Wiener de macOS (solo macOS)
- **RN2** — Motor basado en RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** — Motor del SDK de NVIDIA Broadcast (solo SDK de NVIDIA)
- **DFNR** — Motor DeepFilterNet3

## Parámetros de NR2

En la pestaña NR2, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------------|--------------|-----------------|-------------|
| **Gain Method** | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0-3. |
| **NPE Method** | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| **AE Filter (artifact elimination)** | On | On / Off | `NR2AeFilter` | Activa o desactiva el filtro posterior antirruido. |
| **Reduction:** | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción de NR2. El control deslizante almacena el valor*100 internamente. |
| **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. |
| **Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de NR2 a sus valores predeterminados: Gamma/OSMS/AE activado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Parámetros de NR4

En la pestaña NR4, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------------|--------------|-----------------|-------------|
| **Noise Estimation:** | MMSE | MMSE / Brandt / Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido utilizado por NR4. Se almacena como entero 0-2. |
| **Adaptive Noise Estimation** | On | On / Off | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| **Reduction (dB):** | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido de NR4 en dB. El control deslizante almacena el valor*10. |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido de NR4. |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión de NR4. |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de NR4 a sus valores predeterminados: MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.

## Parámetros de MNR (solo macOS)

En la pestaña MNR, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------------|--------------|-----------------|-------------|
| **Enable MNR (macOS only)** | Off | On / Off | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine. |
| **Strength** | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se persiste como valor normalizado 0.00–1.00. |

La pestaña y el botón de alternancia de MNR aparecen atenuados en versiones de Windows y Linux; el motor no tiene backend en esas plataformas.

## Parámetros de DFNR

En la pestaña DFNR, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------------|--------------|-----------------|-------------|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro posterior adicional para una supresión extra. El control deslizante almacena el valor*100 internamente. |

## Consejos

- Para operación de voz SSB con NR2, comience con **Reduction:** en `1.50` y **Threshold:** en `0.20`. Si la voz suena recortada o hueca, reduzca **Reduction:** hacia `1.00`.
- Reducir **Threshold:** por debajo de `0.15` puede provocar que el ruido residual se filtre durante las pausas del habla, ya que más señal se clasifica como voz. Auméntelo si nota esto.
- Si la estimación de ruido reacciona demasiado lentamente al ruido de ráfagas, reduzca **Smoothing:** hacia `0.60`. Si la compuerta de ruido suena entrecortada, auméntela hacia `0.95`.
- Se recomienda mantener el **AE Filter (artifact elimination)** activado para la mayoría de las condiciones; desactívelo solo si nota que el filtro posterior introduce artefactos.
- Para NR4, comience con los ajustes predeterminados y ajuste primero **Reduction (dB):**. Aumente **Masking Depth:** y **Suppression:** solo si es necesario para condiciones particularmente ruidosas.
- MNR en macOS funciona mejor con **Strength** entre 60-80 para SSB; valores más altos pueden introducir artefactos.

## Solución de problemas

- **La voz suena hueca o sobreprocesada** — **Reduction:** es demasiado alto o **Threshold:** es demasiado alto. Reduzca **Reduction:** y/o reduzca **Threshold:** para preservar más componentes de la voz.
- **El ruido sigue siendo audible durante las pausas del habla** — **Threshold:** es demasiado bajo, lo que hace que las pausas se clasifiquen como voz. Aumente **Threshold:** hacia `0.30`–`0.40`.
- **La estimación de ruido reacciona lentamente o el piso de ruido suena inestable** — Ajuste **Smoothing:** (consulte Consejos más arriba). También verifique que el **NPE Method** seleccionado sea adecuado para su tipo de ruido; NSTAT se adapta mejor al ruido no estacionario.
- **El botón de alternancia de MNR aparece atenuado** — Está en Windows o Linux. MNR requiere macOS.
- **El botón de alternancia de BNR aparece atenuado** — El SDK de NVIDIA Broadcast no está instalado o no se detecta.
- **El botón de alternancia de NR4 aparece atenuado en Windows** — LLVM (clang-cl) no está instalado. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.
- **No se encuentra el diálogo después de minimizarlo** — Revise la barra de tareas o el dock. El diálogo se minimiza como cualquier otra ventana.

## Relacionados

- [Restablecer parámetros de NR2 o NR4 a valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
