# Configuración de AetherDSP

Esta página explica cómo ajustar los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se seleccionan mediante botones de alternancia en la parte superior del diálogo; al hacer clic en un botón también se activa o desvía ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar estos ajustes.
- El motor de reducción de ruido seleccionado ya debe estar activo en un slice del receptor para que los cambios tengan efecto audible de inmediato.
- MNR solo está disponible en compilaciones para macOS. El botón de alternancia MNR está atenuado en Windows y Linux.
- BNR solo está disponible en compilaciones con el SDK de NVIDIA Broadcast. El botón de alternancia BNR está atenuado en otros casos.
- NR4 requiere LLVM (clang-cl) en Windows. El botón de alternancia NR4 está atenuado en compilaciones de Windows compiladas sin LLVM. Instale LLVM desde llvm.org y recompile para habilitar NR4.
- DFNR requiere que DeepFilterNet esté configurado y que AetherSDR se haya recompilado. El botón de alternancia DFNR está deshabilitado si el motor no está disponible.

## Abrir el diálogo

Haga clic en `Settings > AetherDSP Settings...`.

## Descripción general del diálogo

El diálogo de Configuración de AetherDSP presenta una barra de título personalizada con un fondo degradado. De izquierda a derecha contiene:

- Un glifo de agarre (⋮⋮) — solo indicador visual
- El título del diálogo "AetherDSP Settings"
- Botón **—** (Minimizar) — minimiza el diálogo
- Botón **□** (Maximizar) — maximiza o restaura el diálogo
- Botón **×** (Cerrar) — cierra el diálogo

Arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. Arrastre cualquier borde o esquina para redimensionar el diálogo (redimensionamiento de 8 ejes con una zona de interacción de 6 píxeles).

El diálogo almacena su tamaño y posición entre sesiones usando la clave de geometría `AetherDspDialogGeometry`.

## Seleccionar y activar un motor de reducción de ruido

Seis botones de alternancia están dispuestos en una fila en la parte superior del diálogo. Al hacer clic en un botón:

1. Selecciona la página de parámetros de ese motor
2. Activa el motor (si estaba desviado) o lo desvía (si estaba activo)

Cuando NR2 está activado, el AudioEngine aplica exclusividad en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

Cada botón de alternancia tiene un nombre accesible para lectores de pantalla y automatización, siguiendo el patrón "NR2 noise-reduction method" (método de reducción de ruido NR2), "NR4 noise-reduction method" (método de reducción de ruido NR4), etc.

Motores disponibles:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Motor basado en libspecbleach (requiere LLVM en Windows)
- **MNR** — Motor MMSE-Wiener de macOS (solo macOS)
- **RN2** — Motor basado en RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** — Motor del SDK de NVIDIA Broadcast (solo SDK de NVIDIA)
- **DFNR** — Motor DeepFilterNet3

## Parámetros de NR2

En la pestaña NR2, use estos controles:

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------|-------------|-------------|-------------|
| **Gain Method** | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0-3. |
| **NPE Method** | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| **AE Filter (artifact elimination)** | On | On / Off | `NR2AeFilter` | Activa o desactiva el post-filtro antiartefactos. |
| **Use Original Geometry** | Off | On / Off | `NR2UseOriginalGeometry` | Cuando está habilitado, utiliza la geometría de ganancia espectral NR2 original en lugar de la curva alternativa más plana. |
| **Reduction:** | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El control deslizante almacena el valor*100 internamente. |
| **Reduction Floor:** | 0.10 | 0.00–1.00 | `NR2GainFloor` | Establece la ganancia mínima de reducción de ruido que siempre se aplica, incluso en tramos dominados por voz. |
| **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. |
| **Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de NR2 a sus valores predeterminados: Gamma/OSMS/AE activados, Use Original Geometry desactivado, Reduction 1.50, Reduction Floor 0.10, Smoothing 0.85, Threshold 0.20.

## Parámetros de NR4

En la pestaña NR4, use estos controles:

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------|-------------|-------------|-------------|
| **Noise Estimation:** | MMSE | MMSE / Brandt / Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido utilizado por NR4. Se almacena como entero 0-2. |
| **Adaptive Noise Estimation** | On | On / Off | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| **Reduction (dB):** | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. El control deslizante almacena el valor*10. |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4. |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión de NR4. |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de NR4 a sus valores predeterminados: MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.

## Parámetros de MNR (solo macOS)

En la pestaña MNR, use estos controles:

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------|-------------|-------------|-------------|
| **Enable MNR (macOS only)** | Off | On / Off | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo del AudioEngine. |
| **Strength** | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se persiste como valor normalizado 0.00–1.00. |

La pestaña y el botón de alternancia MNR están atenuados en compilaciones de Windows y Linux; el motor no tiene backend en esas plataformas.

## Parámetros de DFNR

En la pestaña DFNR, use estos controles:

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|---------|-------------|-------------|-------------|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para una supresión extra. El control deslizante almacena el valor*100 internamente. |

## Pestaña RN2

La pestaña RN2 es solo informativa. Muestra el modelo RNNoise actualmente activo, pero no proporciona parámetros ajustables. El motor se controla exclusivamente a través del botón de alternancia de la barra de herramientas principal del receptor.

## Pestaña BNR

La pestaña BNR muestra el modelo NVIDIA Broadcast actualmente activo. La intensidad se controla desde el menú superpuesto, no desde este diálogo. El botón de alternancia BNR está atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Soporte de temas

A partir de v26.6.1, el diálogo de Configuración de AetherDSP utiliza el sistema de temas para el estilo. El fondo del diálogo y los colores del texto siguen el tema activo. Todos los controles deslizantes utilizan el estilo de control deslizante principal del tema en lugar de colores fijos. Los temas personalizados pueden anular la apariencia a través de las variables de plantilla `{{color.background.0}}` y `{{color.text.primary}}`.

## Consejos

- Para operación de voz en SSB con NR2, comience con **Reduction:** en `1.50` y **Threshold:** en `0.20`. Si la voz suena recortada o hueca, baje **Reduction:** hacia `1.00`.
- **Reduction Floor:** establece una ganancia mínima que siempre se aplica. Un valor de `0.10` significa que incluso en tramos dominados por voz, al menos el 10% de reducción de ruido está activa. Establézcalo en `0.00` para permitir el paso completo durante la voz.
- Bajar **Threshold:** por debajo de `0.15` puede hacer que el ruido residual se filtre durante las pausas del habla porque más señal se clasifica como voz. Auméntelo si nota esto.
- Si la estimación de ruido reacciona demasiado lentamente al ruido explosivo, baje **Smoothing:** hacia `0.60`. Si la puerta de ruido suena entrecortada, súbalo hacia `0.95`.
- Se recomienda dejar **AE Filter (artifact elimination)** habilitado para la mayoría de las condiciones; desactívelo solo si nota que el propio post-filtro introduce artefactos.
- **Use Original Geometry** habilita la curva de ganancia espectral NR2 original. Actívelo si prefiere el carácter de reducción de ruido más antiguo; desactívelo para la respuesta más plana más nueva que puede preservar más componentes de la voz.
- Para NR4, comience con los ajustes predeterminados y ajuste **Reduction (dB):** primero. Aumente **Masking Depth:** y **Suppression:** solo si es necesario para condiciones particularmente ruidosas.
- MNR en macOS funciona mejor con **Strength** entre 60-80 para SSB; valores más altos pueden introducir artefactos.

## Solución de problemas

- **La voz suena hueca o sobreprocesada** — **Reduction:** es demasiado alto o **Threshold:** es demasiado alto. Baje **Reduction:** y/o baje **Threshold:** para que se conserven más componentes de la voz.
- **El ruido aún es audible durante las pausas del habla** — **Threshold:** es demasiado bajo, lo que hace que las pausas se clasifiquen como voz. Suba **Threshold:** hacia `0.30`–`0.40`.
- **La estimación de ruido reacciona lentamente o el piso de ruido suena inestable** — Ajuste **Smoothing:** (vea Consejos arriba). También verifique que el **NPE Method** seleccionado se adapte a su tipo de ruido; NSTAT se adapta mejor al ruido no estacionario.
- **El botón de alternancia MNR está atenuado** — Está en Windows o Linux. MNR requiere macOS.
- **El botón de alternancia BNR está atenuado** — El SDK de NVIDIA Broadcast no está instalado o no se detecta.
- **El botón de alternancia NR4 está atenuado en Windows** — LLVM (clang-cl) no está instalado. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.
- **El botón de alternancia DFNR está atenuado** — DeepFilterNet no está configurado o AetherSDR no se recompiló con soporte DFNR.
- **No se encuentra el diálogo después de minimizarlo** — Verifique la barra de tareas/muelle. El diálogo se minimiza como cualquier otra ventana.

## Relacionado

- [Reset NR2 or NR4 parameters to defaults](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Switch NR2 gain method between Linear, Log, Gamma and Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Change NR2 noise power estimator (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Choosing the right noise reduction: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
