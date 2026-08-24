# Configuración de AetherDSP

Esta página explica cómo ajustar los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se pueden seleccionar mediante botones de alternancia en la parte superior del diálogo; al hacer clic en un botón de alternancia también se activa o se omite ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar estos ajustes.
- El motor de reducción de ruido seleccionado ya debe estar activo en un slice de receptor para que los cambios surtan efecto audible de inmediato.
- MNR solo está disponible en compilaciones de macOS. El botón de alternancia de MNR está atenuado en Windows y Linux.
- BNR solo está disponible en compilaciones con el SDK de NVIDIA Broadcast. El botón de alternancia de BNR está atenuado en caso contrario.
- NR4 requiere LLVM (clang-cl) en Windows. El botón de alternancia de NR4 está atenuado en compilaciones de Windows compiladas sin LLVM. Instale LLVM desde llvm.org y recompile para habilitar NR4.
- DFNR requiere que DeepFilterNet esté configurado y que AetherSDR se haya recompilado. El botón de alternancia de DFNR está deshabilitado si el motor no está disponible.

## Abrir el diálogo

Haga clic en `Settings > AetherDSP Settings...`.

## Descripción general del diálogo

El diálogo de Configuración de AetherDSP presenta una barra de título personalizada con un fondo degradado. De izquierda a derecha contiene:

- Un glifo de agarre (⋮⋮) — solo indicador visual
- El título del diálogo "AetherDSP Settings"
- Botón **—** (Minimizar) — minimiza el diálogo
- Botón **□** (Maximizar) — maximiza o restaura el diálogo
- Botón **×** (Cerrar) — cierra el diálogo

Arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. Arrastre cualquier borde o esquina para redimensionar el diálogo (redimensionamiento en 8 ejes con una zona de impacto de 6 px).

El diálogo almacena su tamaño y posición entre sesiones utilizando la clave de geometría `AetherDspDialogGeometry`.

## Seleccionar y activar un motor de reducción de ruido

Seis botones de alternancia están dispuestos en una fila en la parte superior del diálogo. Al hacer clic en un botón de alternancia:

1. Selecciona la página de parámetros de ese motor
2. Activa el motor (si estaba omitido) o lo omite (si estaba activo)

Cuando se activa NR2, AudioEngine activa la exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

Cada botón de alternancia tiene un nombre accesible para lectores de pantalla y automatización, siguiendo el patrón "NR2 noise-reduction method", "NR4 noise-reduction method", etc.

Motores disponibles:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Motor basado en libspecbleach (requiere LLVM en Windows)
- **MNR** — Motor MMSE-Wiener de macOS (solo macOS)
- **RN2** — Motor basado en RNNoise con piso de ruido ajustable
- **BNR** — Motor del SDK de NVIDIA Broadcast (solo SDK de NVIDIA)
- **DFNR** — Motor DeepFilterNet3

## Parámetros de NR2

En la pestaña NR2, use estos controles:

| Control                              | Predeterminado | Rango válido            | Clave de ajuste        | Descripción                                                                                                                         |
|--------------------------------------|----------------|-------------------------|------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Gain Method**                      | Gamma         | Linear / Log / Gamma / Trained | `NR2GainMethod`    | Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0-3 que coincide con el orden anterior. |
| **NPE Method**                       | OSMS          | OSMS / MMSE / NSTAT     | `NR2NpeMethod`         | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2.                                                          |
| **AE Filter (artifact elimination)** | On            | On / Off                | `NR2AeFilter`          | Activa el post-filtro anti-artefactos.                                                                                              |
| **Reduction:**                       | 1.50          | 0.50–2.00               | `NR2GainMax`           | Establece la profundidad máxima de reducción de NR2. El deslizador almacena el valor*100 internamente.                              |
| **Smoothing:**                       | 0.85          | 0.50–0.98               | `NR2GainSmooth`        | Controla la suavidad con la que la estimación de ruido sigue los cambios.                                                           |
| **Threshold:**                       | 0.20          | 0.05–0.50               | `NR2Qspp`              | Establece el umbral de probabilidad de presencia de voz.                                                                            |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de NR2 a sus valores predeterminados: Gamma/OSMS/AE activados, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Parámetros de NR4

En la pestaña NR4, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|----------------|--------------|-----------------|-------------|
| **Noise Estimation:** | MMSE | MMSE / Brandt / Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido utilizado por NR4. Se almacena como entero 0-2. |
| **Adaptive Noise Estimation** | On | On / Off | `NR4AdaptiveNoise` | Habilita la re-estimación continua del piso de ruido. |
| **Reduction (dB):** | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido de NR4 en dB. El deslizador almacena el valor*10. |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido de NR4. |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión de NR4. |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de NR4 a sus valores predeterminados: MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.

## Parámetros de MNR (solo macOS)

En la pestaña MNR, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|----------------|--------------|-----------------|-------------|
| **Enable MNR (macOS only)** | Off | On / Off | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine. |
| **Strength** | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se persiste como valor normalizado 0.00–1.00. |

La pestaña y el botón de alternancia de MNR están atenuados en compilaciones de Windows y Linux — el motor no tiene backend en esas plataformas.

Haga clic en **Reset Defaults** (icono ↺) para restaurar la Strength de MNR a su valor predeterminado de 100. La casilla de verificación Enable MNR no se ve afectada por Reset Defaults.

## Parámetros de DFNR

En la pestaña DFNR, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|----------------|--------------|-----------------|-------------|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para mayor supresión. El deslizador almacena el valor*100 internamente. |

Haga clic en **Reset Defaults** (icono ↺) para restaurar todos los parámetros de DFNR a sus valores predeterminados: Attenuation Limit 100, Post-Filter Beta 0.00.

## Parámetros de RN2

En la pestaña RN2, use estos controles:

| Control | Predeterminado | Rango válido | Clave de ajuste | Descripción |
|---------|----------------|--------------|-----------------|-------------|
| **Noise Floor (RN2 dry mix)** | 0 | 0–100 | — | Establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce supresión total (silencio entre frases); 10-20% mantiene un piso de ruido constante y bajo para que el receptor siga sonando vivo. Afecta solo al audio recibido; el denoizador de transmisión no cambia. |

La pestaña RN2 también muestra el modelo RNNoise actualmente activo. Haga clic en **Reset Defaults** (icono ↺) para restaurar el Noise Floor a su valor predeterminado de 0.

## Pestaña BNR

La pestaña BNR muestra el modelo NVIDIA Broadcast actualmente activo. La intensidad se controla desde el menú superpuesto, no desde este diálogo. El botón de alternancia de BNR está atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Soporte de temas

A partir de la v26.6.1, el diálogo de Configuración de AetherDSP utiliza el sistema de temas para el estilo. El fondo del diálogo y los colores del texto siguen el tema activo. Todos los deslizadores utilizan el estilo de deslizador principal del tema en lugar de colores fijos. Los temas personalizados pueden anular la apariencia mediante las variables de plantilla `{{color.background.0}}` y `{{color.text.primary}}`.

## Consejos

- Para operación de voz SSB con NR2, comience con **Reduction:** en `1.50` y **Threshold:** en `0.20`. Si el habla suena recortada o hueca, baje **Reduction:** hacia `1.00`.
- Bajar **Threshold:** por debajo de `0.15` puede hacer que el ruido residual se filtre durante las pausas del habla porque más señal se clasifica como habla. Súbalo si nota esto.
- Si la estimación de ruido reacciona demasiado lentamente al ruido de ráfagas, baje **Smoothing:** hacia `0.60`. Si la puerta de ruido suena entrecortada, súbalo hacia `0.95`.
- Se recomienda dejar **AE Filter (artifact elimination)** habilitado para la mayoría de las condiciones; desactívelo solo si nota que el post-filtro introduce artefactos.
- Para RN2, un **Noise Floor** de `10`–`20` mantiene el receptor sonando vivo entre frases mientras aún suprime la mayor parte del ruido de fondo. Comience en `0` para máxima supresión y auméntelo solo si el silencio resulta molesto.
- Para NR4, comience con los ajustes predeterminados y ajuste primero **Reduction (dB):**. Aumente **Masking Depth:** y **Suppression:** solo si es necesario para condiciones particularmente ruidosas.
- MNR en macOS funciona mejor con **Strength** entre 60-80 para SSB; valores más altos pueden introducir artefactos.

## Solución de problemas

- **El habla suena hueca o sobreprocesada** — **Reduction:** es demasiado alta o **Threshold:** es demasiado alto. Baje **Reduction:** y/o baje **Threshold:** para que se preserven más componentes del habla.
- **El ruido sigue siendo audible durante las pausas del habla** — **Threshold:** es demasiado bajo, lo que hace que las pausas se clasifiquen como habla. Suba **Threshold:** hacia `0.30`–`0.40`.
- **La estimación de ruido reacciona lentamente o el piso de ruido suena inestable** — Ajuste **Smoothing:** (consulte los Consejos anteriores). También verifique que el **NPE Method** seleccionado se adapte a su tipo de ruido; NSTAT se adapta mejor al ruido no estacionario.
- **La salida de RN2 es completamente silenciosa entre frases y le resulta molesta** — Aumente el deslizador **Noise Floor** a `10`–`20` para mantener un piso de ruido constante y bajo bajo el audio denoizado.
- **El botón de alternancia de MNR está atenuado** — Está en Windows o Linux. MNR requiere macOS.
- **El botón de alternancia de BNR está atenuado** — El SDK de NVIDIA Broadcast no está instalado o no se detecta.
- **El botón de alternancia de NR4 está atenuado en Windows** — LLVM (clang-cl) no está instalado. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.
- **El botón de alternancia de DFNR está atenuado** — DeepFilterNet no está configurado o AetherSDR no se recompiló con soporte para DFNR.
- **No puede encontrar el diálogo después de minimizarlo** — Revise la barra de tareas/muelle. El diálogo se minimiza como cualquier otra ventana.

## Relacionado

- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
