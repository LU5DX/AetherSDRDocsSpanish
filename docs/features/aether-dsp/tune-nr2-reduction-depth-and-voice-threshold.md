# Configuración de AetherDSP

Esta página explica cómo ajustar los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se seleccionan mediante botones de alternancia en la parte superior del cuadro de diálogo; al hacer clic en un botón también se activa o se omite ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar estos ajustes.
- El motor de reducción de ruido seleccionado ya debe estar activo en un slice del receptor para que los cambios tengan efecto audible de inmediato.
- MNR solo está disponible en las compilaciones para macOS. El botón de alternancia de MNR aparece atenuado en Windows y Linux.
- BNR solo está disponible en las compilaciones que incluyen el SDK de NVIDIA Broadcast. De lo contrario, el botón de alternancia de BNR aparece atenuado.
- NR4 requiere LLVM (clang-cl) en Windows. El botón de alternancia de NR4 aparece atenuado en las compilaciones de Windows compiladas sin LLVM. Instale LLVM desde llvm.org y recompile para habilitar NR4.

## Cómo abrir el cuadro de diálogo

Haga clic en `Settings > AetherDSP Settings...`.

## Descripción general del cuadro de diálogo

El cuadro de diálogo de configuración de AetherDSP cuenta con una barra de título personalizada con un fondo degradado azul. De izquierda a derecha contiene:

- Un glifo de agarre (⋮⋮) — solo indicador visual
- El título del cuadro de diálogo "AetherDSP Settings"
- Botón **—** (Minimizar) — minimiza el cuadro de diálogo
- Botón **□** (Maximizar) — maximiza o restaura el cuadro de diálogo
- Botón **×** (Cerrar) — cierra el cuadro de diálogo

Arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Arrastre cualquier borde o esquina para cambiar el tamaño del cuadro de diálogo (redimensionamiento en 8 direcciones con una zona de impacto de 6 px).

El cuadro de diálogo almacena su tamaño y posición entre sesiones utilizando la clave de geometría `AetherDspDialogGeometry`.

## Cómo seleccionar y activar un motor de reducción de ruido

Seis botones de alternancia están dispuestos en una fila en la parte superior del cuadro de diálogo. Al hacer clic en un botón:

1. Selecciona la página de parámetros de ese motor
2. Activa el motor (si estaba omitido) o lo omite (si estaba activo)

Cuando se activa NR2, el AudioEngine utiliza exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

Motores disponibles:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Motor basado en libspecbleach (requiere LLVM en Windows)
- **MNR** — Motor MMSE-Wiener de macOS (solo macOS)
- **RN2** — Motor basado en RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** — Motor del SDK de NVIDIA Broadcast (solo SDK de NVIDIA)
- **DFNR** — Motor DeepFilterNet3

## Parámetros de NR2

En la pestaña NR2, use estos controles:

| Control | Valor predeterminado | Rango válido | Clave de configuración | Descripción |
|---------|---------|-------------|-------------|-------------|
| **Gain Method** | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0-3. |
| **NPE Method** | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| **AE Filter (artifact elimination)** | On | On / Off | `NR2AeFilter` | Activa o desactiva el postfiltro antiartefactos. |
| **Reduction:** | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción de NR2. El control deslizante almacena el valor*100 internamente. |
| **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que el estimador de ruido sigue los cambios. |
| **Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de NR2 a sus valores predeterminados: Gamma/OSMS/AE activado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Parámetros de NR4

En la pestaña NR4, use estos controles:

| Control | Valor predeterminado | Rango válido | Clave de configuración | Descripción |
|---------|---------|-------------|-------------|-------------|
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

| Control | Valor predeterminado | Rango válido | Clave de configuración | Descripción |
|---------|---------|-------------|-------------|-------------|
| **Enable MNR (macOS only)** | Off | On / Off | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo del AudioEngine. |
| **Strength** | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva como valor normalizado 0.00–1.00. |

La pestaña y el botón de alternancia de MNR aparecen atenuados en las compilaciones de Windows y Linux; el motor no tiene backend en esas plataformas.

## Parámetros de DFNR

En la pestaña DFNR, use estos controles:

| Control | Valor predeterminado | Rango válido | Clave de configuración | Descripción |
|---------|---------|-------------|-------------|-------------|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un postfiltro adicional para una supresión extra. El control deslizante almacena el valor*100 internamente. |

## Consejos

- Para operación de voz en SSB con NR2, comience con **Reduction:** en `1.50` y **Threshold:** en `0.20`. Si el habla suena recortada o hueca, reduzca **Reduction:** hacia `1.00`.
- Reducir **Threshold:** por debajo de `0.15` puede hacer que el ruido residual irrumpa durante las pausas del habla porque una mayor parte de la señal se clasifica como habla. Si nota esto, súbalo.
- Si la estimación de ruido reacciona demasiado lentamente al ruido explosivo, reduzca **Smoothing:** hacia `0.60`. Si la puerta de ruido suena entrecortada, súbalo hacia `0.95`.
- Se recomienda mantener habilitado **AE Filter (artifact elimination)** para la mayoría de las condiciones; desactívelo solo si nota que el postfiltro introduce artefactos por sí mismo.
- Para NR4, comience con los ajustes predeterminados y ajuste **Reduction (dB):** primero. Aumente **Masking Depth:** y **Suppression:** solo si es necesario para condiciones particularmente ruidosas.
- MNR en macOS funciona mejor con **Strength** entre 60 y 80 para SSB; los valores más altos pueden introducir artefactos.

## Solución de problemas

- **El habla suena hueca o sobreprocesada** — **Reduction:** es demasiado alto o **Threshold:** es demasiado alto. Reduzca **Reduction:** y/o baje **Threshold:** para que se conserven más componentes del habla.
- **El ruido todavía es audible durante las pausas del habla** — **Threshold:** es demasiado bajo, lo que hace que las pausas se clasifiquen como habla. Aumente **Threshold:** hacia `0.30`–`0.40`.
- **La estimación de ruido reacciona lentamente o el piso de ruido suena inestable** — Ajuste **Smoothing:** (consulte los Consejos anteriores). También verifique que el **NPE Method** seleccionado se adapte a su tipo de ruido; NSTAT se adapta mejor al ruido no estacionario.
- **El botón de alternancia de MNR está atenuado** — Está en Windows o Linux. MNR requiere macOS.
- **El botón de alternancia de BNR está atenuado** — El SDK de NVIDIA Broadcast no está instalado o no se detecta.
- **El botón de alternancia de NR4 está atenuado en Windows** — LLVM (clang-cl) no está instalado. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.
- **No puedo encontrar el cuadro de diálogo después de minimizarlo** — Verifique la barra de tareas o el dock. El cuadro de diálogo se minimiza como cualquier otra ventana.

## Relacionado

- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
