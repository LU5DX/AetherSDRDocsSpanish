# Configuración de AetherDSP

El cuadro de diálogo Configuración de AetherDSP (se abre mediante `Settings > AetherDSP Settings...`) ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Permite al operador ajustar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se pueden seleccionar mediante una fila de botones en la parte superior; al hacer clic en un botón también se activa o desactiva ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ajustar la configuración DSP.
- Seleccione un motor de reducción de ruido haciendo clic en su botón en la fila de pestañas del cuadro de diálogo.

## Controles comunes

| Control                        | Comportamiento                                                                                                   | Notas                                                                                   |
|--------------------------------|------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Barra de título — AetherDSP Settings | Barra de título con degradado de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo.          | Coincide con la familia de estilos de NetworkDiagnosticsDialog y AetherialAudioStrip.   |
| — (Minimizar)                  | Minimiza el cuadro de diálogo.                                                                                   |                                                                                         |
| □ (Maximizar)                  | Maximiza o restaura el cuadro de diálogo.                                                                        |                                                                                         |
| × (Cerrar)                     | Cierra el cuadro de diálogo.                                                                                     |                                                                                         |
| Arrastrar para mover           | Haga clic y arrastre la barra de título para mover el cuadro de diálogo.                                         | Haga doble clic en la barra de título para cambiar entre maximizar/restaurar.            |
| Redimensionar en 8 direcciones | Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. | Zona de clic de redimensionamiento de 6 px alrededor del widget de contenido interno.   |

## Pestaña NR2 (Reducción de ruido musical)

Al seleccionar la pestaña NR2 se activa o desactiva el motor NR2. Cuando NR2 está activado, AudioEngine se pone en cascada con exclusión, deshabilitando DFNR y otros módulos mutuamente excluyentes.

### Controles de NR2

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|----------------------|-----------------|------------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Gain Method                    | Gamma                | Linear, Log, Gamma, Trained | `NR2GainMethod`        | Selecciona la asignación de la curva de ganancia utilizada por NR2.                                    | Se almacena como entero 0-3 coincidiendo con el orden anterior.                        |
| NPE Method                     | OSMS                 | OSMS, MMSE, NSTAT | `NR2NpeMethod`         | Selecciona el estimador de potencia de ruido.                                                          | Se almacena como entero 0-2.                                                            |
| AE Filter (eliminación de artefactos) | Verdadero            | —                 | `NR2AeFilter`          | Activa o desactiva el post-filtro antiartefacto.                                                       |                                                                                        |
| Reduction:                     | 1.50                 | 0.50-2.00         | `NR2GainMax`           | Establece la profundidad máxima de reducción de NR2.                                                   | El deslizador almacena el valor*100 internamente.                                       |
| Smoothing:                     | 0.85                 | 0.50-0.98         | `NR2GainSmooth`        | Controla la suavidad con la que la estimación de ruido sigue los cambios.                              |                                                                                        |
| Threshold:                     | 0.20                 | 0.05-0.50         | `NR2Qspp`              | Establece el umbral de probabilidad de presencia de voz.                                               |                                                                                        |
| Reset Defaults (icono ↺)      | —                    | —                 | —                      | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20).      | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA). |

## Pestaña NR4 (libspecbleach)

Al seleccionar la pestaña NR4 se activa o desactiva el motor NR4.

### Controles de NR4

| Control                        | Valor predeterminado | Rango válido              | Clave de configuración          | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|----------------------|---------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Noise Estimation:              | MMSE                 | MMSE, Brandt, Martin      | `NR4NoiseEstimationMethod`       | Selecciona el estimador de suelo de ruido utilizado por NR4.                                           | Se almacena como entero 0-2.                                                            |
| Adaptive Noise Estimation      | Verdadero            | —                         | `NR4AdaptiveNoise`               | Habilita la reestimación continua del suelo de ruido.                                                  |                                                                                        |
| Reduction (dB):                | 10.0                 | 0.0-40.0                 | `NR4ReductionAmount`             | Establece la reducción máxima de ruido de NR4 en dB.                                                    | El deslizador almacena el valor*10.                                                     |
| Smoothing (%):                 | 0                    | 0-100                    | `NR4SmoothingFactor`             | Suavizado en el dominio del tiempo de la estimación de ruido de NR4.                                   |                                                                                        |
| Whitening (%):                 | 0                    | 0-100                    | `NR4WhiteningFactor`             | Aplana la forma espectral del ruido residual.                                                          |                                                                                        |
| Masking Depth:                 | 0.50                 | 0.00-1.00                | `NR4MaskingDepth`                | Controla la profundidad del enmascaramiento espectral.                                                  |                                                                                        |
| Suppression:                   | 0.50                 | 0.00-1.00                | `NR4SuppressionStrength`         | Fuerza de supresión general de NR4.                                                                   |                                                                                        |
| Reset Defaults (icono ↺)      | —                    | —                        | —                                | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50).      | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA). |

## Pestaña MNR (MMSE-Wiener de macOS)

Al seleccionar la pestaña MNR se activa o desactiva el motor MNR. El botón de MNR aparece atenuado en las compilaciones de Windows/Linux — el motor no tiene backend en esas plataformas.

### Controles de MNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|----------------------|-----------------|------------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Enable MNR (solo macOS)        | —                    | —               | `MnrEnabled`           | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.                       | El estado inicial se lee en vivo de AudioEngine::mnrEnabled().                          |
| Strength                       | 100                  | 0-100           | `MnrStrength`          | Ajusta la agresividad de MNR (0 suave, 100 máximo).                                                    | Se persiste como valor normalizado 0.00-1.00.                                           |

## Pestaña DFNR (DeepFilterNet3)

Al seleccionar la pestaña DFNR se activa o desactiva el motor DeepFilterNet3.

### Controles de DFNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|----------------------|-----------------|------------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Attenuation Limit              | 100                  | 0-100 dB        | `DfnrAttenLimit`       | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.  |                                                                                        |
| Post-Filter Beta               | 0.00                 | 0.00-0.30       | `DfnrPostFilterBeta`   | Aplica un post-filtro adicional para una supresión extra.                                              | El deslizador almacena el valor*100 internamente.                                       |

## Pestaña RN2 (RNNoise)

Al seleccionar la pestaña RN2 se activa o desactiva el motor RN2. Esta página es puramente informativa — no tiene parámetros ajustables.

## Pestaña BNR (NVIDIA)

Al seleccionar la pestaña BNR se activa o desactiva el motor BNR. La intensidad se controla desde el menú superpuesto. El botón de BNR aparece atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- Para señales fuertes y limpias donde la fidelidad es importante, reduzca **Attenuation Limit** hacia 0 para limitar cuánto puede alterar el motor el audio.
- Para señales débiles o muy degradadas por ruido, establezca **Attenuation Limit** en 100 y combínelo con un **Post-Filter Beta** distinto de cero para la supresión más agresiva.
- Al usar NR2, comience con los valores predeterminados (Gamma/OSMS/AE activado, 1.50/0.85/0.20) y ajuste **Reduction:** y **Smoothing:** para encontrar el mejor equilibrio.

## Solución de problemas

- **El audio no se ve afectado después de mover el deslizador** — Confirme que está en la pestaña correcta y que el motor de reducción de ruido correspondiente está activo. Cada motor tiene controles separados y no se ve afectado por la configuración de otros motores.
- **La pestaña MNR está atenuada** — MNR solo está disponible en compilaciones de macOS.
- **La pestaña BNR está atenuada** — El SDK de NVIDIA Broadcast no está detectado en su sistema.

## Relacionado

- [Configure DFNR post-filter beta for extra suppression](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Choosing the right noise reduction: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [AetherDSP Settings overview](overview.md)
