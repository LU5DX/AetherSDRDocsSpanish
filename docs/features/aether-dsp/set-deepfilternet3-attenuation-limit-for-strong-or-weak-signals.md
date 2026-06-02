# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP (accesible mediante `Settings > AetherDSP Settings...`) ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Permite al operador encontrar el equilibrio entre la supresión de ruido y la fidelidad de la voz. Los seis módulos DSP se seleccionan mediante una fila de botones de alternancia en la parte superior; al hacer clic en un botón también se activa o desactiva ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se necesita una conexión de radio para ajustar la configuración DSP.
- Seleccione un motor de reducción de ruido haciendo clic en su botón de alternancia en la fila de pestañas del diálogo.

## Controles comunes

| Control                        | Comportamiento                                                                                              | Notas                                                                                     |
|--------------------------------|-------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| Barra de título — AetherDSP Settings | Barra de título con degradado de 18 píxeles con un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. | Coincide con la familia de estilos de NetworkDiagnosticsDialog y AetherialAudioStrip. |
| — (Minimizar)                  | Minimiza el diálogo.                                                                                        |                                                                                           |
| □ (Maximizar)                  | Maximiza o restaura el diálogo.                                                                             |                                                                                           |
| × (Cerrar)                     | Cierra el diálogo.                                                                                          |                                                                                           |
| Arrastrar para mover           | Haga clic y arrastre la barra de título para mover el diálogo.                                              | Haga doble clic en la barra de título para alternar entre maximizar y restaurar.          |
| Redimensionar en 8 ejes        | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. | Zona de redimensionamiento de 6 píxeles alrededor del widget de contenido interno.        |

## Pestaña NR2 (Reducción de ruido musical)

Seleccionar la pestaña NR2 activa o desactiva el motor NR2. Cuando NR2 está activado, AudioEngine impide el uso simultáneo de DFNR y otros módulos mutuamente excluyentes.

### Controles de NR2

| Control                        | Valor predeterminado | Rango válido      | Clave de configuración | Comportamiento                                                                                     | Notas                                                                                   |
|--------------------------------|----------------------|-------------------|------------------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Gain Method (Método de ganancia) | Gamma                | Linear, Log, Gamma, Trained | `NR2GainMethod`        | Selecciona la asignación de la curva de ganancia utilizada por NR2.                                | Se almacena como entero 0-3 coincidiendo con el orden anterior.                        |
| NPE Method (Método NPE)         | OSMS                 | OSMS, MMSE, NSTAT | `NR2NpeMethod`         | Selecciona el estimador de potencia de ruido.                                                      | Se almacena como entero 0-2.                                                            |
| AE Filter (Filtro AE)           | Activado             | —                 | `NR2AeFilter`          | Activa o desactiva el filtro posterior antirruido.                                                 |                                                                                         |
| Reduction (Reducción):          | 1.50                 | 0.50-2.00         | `NR2GainMax`           | Establece la profundidad máxima de reducción de NR2.                                               | El control deslizante almacena el valor*100 internamente.                               |
| Smoothing (Suavizado):          | 0.85                 | 0.50-0.98         | `NR2GainSmooth`        | Controla la suavidad con la que la estimación de ruido sigue los cambios.                          |                                                                                         |
| Threshold (Umbral):             | 0.20                 | 0.05-0.50         | `NR2Qspp`              | Establece el umbral de probabilidad de presencia de voz.                                           |                                                                                         |
| Reset Defaults (icono ↺)       | —                    | —                 | —                      | Restablece los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20). | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA). |

## Pestaña NR4 (libspecbleach)

Seleccionar la pestaña NR4 activa o desactiva el motor NR4.

### Controles de NR4

| Control                        | Valor predeterminado | Rango válido              | Clave de configuración              | Comportamiento                                                                                     | Notas                                                                                   |
|--------------------------------|----------------------|---------------------------|--------------------------------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Noise Estimation (Estimación de ruido): | MMSE                 | MMSE, Brandt, Martin      | `NR4NoiseEstimationMethod`           | Selecciona el estimador de piso de ruido utilizado por NR4.                                        | Se almacena como entero 0-2.                                                            |
| Adaptive Noise Estimation (Estimación adaptativa de ruido) | Activado              | —                         | `NR4AdaptiveNoise`                   | Activa la reestimación continua del piso de ruido.                                                 |                                                                                         |
| Reduction (dB) (Reducción):     | 10.0                 | 0.0-40.0                 | `NR4ReductionAmount`                 | Establece la reducción máxima de ruido de NR4 en dB.                                               | El control deslizante almacena el valor*10.                                              |
| Smoothing (%) (Suavizado):      | 0                    | 0-100                    | `NR4SmoothingFactor`                 | Suavizado en el dominio del tiempo de la estimación de ruido de NR4.                               |                                                                                         |
| Whitening (%) (Blanqueamiento):| 0                    | 0-100                    | `NR4WhiteningFactor`                 | Aplana la forma espectral del ruido residual.                                                      |                                                                                         |
| Masking Depth (Profundidad de enmascaramiento): | 0.50                 | 0.00-1.00               | `NR4MaskingDepth`                    | Controla la profundidad del enmascaramiento espectral.                                             |                                                                                         |
| Suppression (Supresión):        | 0.50                 | 0.00-1.00               | `NR4SuppressionStrength`             | Fuerza de supresión general de NR4.                                                               |                                                                                         |
| Reset Defaults (icono ↺)       | —                    | —                        | —                                    | Restablece los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50). | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA). |

## Pestaña MNR (MMSE-Wiener de macOS)

Seleccionar la pestaña MNR activa o desactiva el motor MNR. El botón de alternancia de MNR está atenuado en las compilaciones de Windows/Linux; el motor no tiene un backend en esas plataformas.

### Controles de MNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                     | Notas                                                                                   |
|--------------------------------|----------------------|-----------------|------------------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Enable MNR (solo macOS)        | —                    | —               | `MnrEnabled`           | Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.                     | El estado inicial se lee en vivo de AudioEngine::mnrEnabled().                         |
| Strength (Intensidad)           | 100                  | 0-100           | `MnrStrength`          | Ajusta la agresividad de MNR (0 suave, 100 máxima).                                                | Se persiste como valor normalizado 0.00-1.00.                                           |

## Pestaña DFNR (DeepFilterNet3)

Seleccionar la pestaña DFNR activa o desactiva el motor DeepFilterNet3.

### Controles de DFNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                     | Notas                                                                                   |
|--------------------------------|----------------------|-----------------|------------------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Attenuation Limit (Límite de atenuación) | 100          | 0-100 dB        | `DfnrAttenLimit`       | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máxima. |                                                                                         |
| Post-Filter Beta (Beta del filtro posterior) | 0.00        | 0.00-0.30       | `DfnrPostFilterBeta`   | Aplica un filtro posterior adicional para una supresión extra.                                     | El control deslizante almacena el valor*100 internamente.                               |

## Pestaña RN2 (RNNoise)

Seleccionar la pestaña RN2 activa o desactiva el motor RN2. Esta página es puramente informativa: no tiene parámetros ajustables.

## Pestaña BNR (NVIDIA)

Seleccionar la pestaña BNR activa o desactiva el motor BNR. La intensidad se controla desde el menú superpuesto. El botón de alternancia de BNR está atenuado en las compilaciones sin el NVIDIA Broadcast SDK.

## Consejos

- Para señales fuertes y limpias donde la fidelidad es importante, reduzca el **Attenuation Limit** hacia 0 para limitar cuánto puede modificar el motor el audio.
- Para señales débiles o con mucho ruido, establezca **Attenuation Limit** a 100 y combínelo con un **Post-Filter Beta** distinto de cero para la supresión más agresiva.
- Al usar NR2, comience con los valores predeterminados (Gamma/OSMS/AE activado, 1.50/0.85/0.20) y ajuste **Reduction:** y **Smoothing:** para encontrar el mejor equilibrio.

## Solución de problemas

- **El audio no se ve afectado después de mover el control deslizante** — Confirme que está en la pestaña correcta y que el motor de reducción de ruido correspondiente está activo. Cada motor tiene controles separados y no se ve afectado por la configuración de otros motores.
- **La pestaña MNR está atenuada** — MNR solo está disponible en las compilaciones de macOS.
- **La pestaña BNR está atenuada** — El NVIDIA Broadcast SDK no está detectado en su sistema.

## Relacionados

- [Configure DFNR post-filter beta for extra suppression](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Choosing the right noise reduction: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [AetherDSP Settings overview](overview.md)
