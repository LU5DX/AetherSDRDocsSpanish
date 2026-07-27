# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP (abierto mediante `Settings > AetherDSP Settings...`) ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Permite a los operadores equilibrar la supresión de ruido con la fidelidad de la voz. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o desvía ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ajustar la configuración de DSP.
- Seleccione un motor de reducción de ruido haciendo clic en su conmutador en la fila de pestañas del diálogo.

## Controles comunes

| Control                        | Comportamiento                                                                                             | Notas                                                                                   |
|--------------------------------|------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Barra de título — AetherDSP Settings | Barra de título de 18 px con degradado y glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. | Coincide con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip.    |
| — (Minimizar)                   | Minimiza el diálogo.                                                                                      |                                                                                         |
| □ (Maximizar)                   | Maximiza o restaura el diálogo.                                                                          |                                                                                         |
| × (Cerrar)                      | Cierra el diálogo.                                                                                         |                                                                                         |
| Arrastrar para mover            | Haga clic y arrastre la barra de título para mover el diálogo.                                           | Haga doble clic en la barra de título para alternar entre maximizar y restaurar.        |
| Redimensionar en 8 ejes         | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección. | Zona de captura de redimensionamiento de 6 px alrededor del widget de contenido interno. |

## Pestaña NR2 (Reducción de ruido musical)

Seleccionar la pestaña NR2 activa o desvía el motor NR2. Cuando NR2 está activado, AudioEngine lo prioriza en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

### Controles de NR2

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|----------------|-----------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Gain Method                    | Gamma         | Linear, Log, Gamma, Trained | `NR2GainMethod`       | Selecciona la asignación de la curva de ganancia utilizada por NR2.                                                        | Se almacena como entero 0-3 en el orden anterior.                                        |
| NPE Method                     | OSMS          | OSMS, MMSE, NSTAT | `NR2NpeMethod`        | Selecciona el estimador de potencia de ruido.                                                                 | Se almacena como entero 0-2.                                                                |
| AE Filter (eliminación de artefactos) | True          | —              | `NR2AeFilter`         | Activa el filtro posterior antiartefactos.                                                          |                                                                                        |
| Reduction:                     | 1,50          | 0,50-2,00      | `NR2GainMax`          | Establece la profundidad máxima de reducción de NR2.                                                              | El control deslizante almacena el valor*100 internamente.                                                    |
| Gain Floor                     | 0,00          | 0,00-0,50      | `NR2GainFloor`        | Establece el piso de ganancia mínimo para el procesamiento de NR2.                                                 | Añadido en v26.7.4.                                                                      |
| Smoothing:                     | 0,85          | 0,50-0,98      | `NR2GainSmooth`       | Controla la suavidad con la que la estimación de ruido sigue los cambios.                                                                                        |                                                                                        |
| Threshold:                     | 0,20          | 0,05-0,50      | `NR2Qspp`             | Establece el umbral de probabilidad de presencia de voz.                                                    |                                                                                        |
| Use Original Spatial Geometry  | True          | —              | `NR2UseOriginalGeometry` | Activa el uso de la geometría espacial original en lugar de la configuración en cascada.                 | Añadido en v26.7.4.                                                                      |
| Restablecer valores predeterminados (icono ↺) | —              | —              | —                     | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activado, 1,50/0,00/0,85/0,20, Use Original Geometry activado). | Se muestra como un botón de icono plano con una flecha antihoraria (U+21BA).                   |

## Pestaña NR4 (libspecbleach)

Seleccionar la pestaña NR4 activa o desvía el motor NR4.

### Controles de NR4

| Control                        | Valor predeterminado | Rango válido              | Clave de configuración          | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|--------------------------|--------------------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Noise Estimation:              | MMSE          | MMSE, Brandt, Martin     | `NR4NoiseEstimationMethod`     | Selecciona el estimador de piso de ruido utilizado por NR4.                                                      | Se almacena como entero 0-2.                                                                |
| Adaptive Noise Estimation      | True          | —                        | `NR4AdaptiveNoise`             | Habilita la reestimación continua del piso de ruido.                                            |                                                                                        |
| Reduction (dB):                | 10,0          | 0,0-40,0                | `NR4ReductionAmount`           | Establece la reducción máxima de ruido de NR4 en dB.                                                         | El control deslizante almacena el valor*10.                                                                |
| Smoothing (%):                 | 0             | 0-100                   | `NR4SmoothingFactor`           | Suavizado en el dominio del tiempo de la estimación de ruido de NR4.                                                    |                                                                                        |
| Whitening (%):                 | 0             | 0-100                   | `NR4WhiteningFactor`           | Aplana la forma espectral del ruido residual.                                                         |                                                                                        |
| Masking Depth:                 | 0,50          | 0,00-1,00               | `NR4MaskingDepth`              | Controla la profundidad del enmascaramiento espectral.                                                                |                                                                                        |
| Suppression:                   | 0,50          | 0,00-1,00               | `NR4SuppressionStrength`       | Fuerza de supresión general de NR4.                                                               |                                                                                        |
| Restablecer valores predeterminados (icono ↺) | —              | —                        | —                              | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0,50, 0,50).                              | Se muestra como un botón de icono plano con una flecha antihoraria (U+21BA).                   |

## Pestaña MNR (MMSE-Wiener de macOS)

Seleccionar la pestaña MNR activa o desvía el motor MNR. El conmutador MNR está atenuado en las compilaciones de Windows/Linux; el motor no tiene backend en esas plataformas.

### Controles de MNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|----------------|------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Enable MNR (solo macOS)        | —             | —              | `MnrEnabled`     | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.                            | El estado inicial se lee en vivo desde AudioEngine::mnrEnabled().                               |
| Strength                       | 100           | 0-100          | `MnrStrength`    | Ajusta la agresividad de MNR (0 suave, 100 máximo).                                                   | Se conserva normalizado como 0,00-1,00.                                                     |

## Pestaña DFNR (DeepFilterNet3)

Seleccionar la pestaña DFNR activa o desvía el motor DeepFilterNet3. DFNR solo está disponible cuando AetherSDR se recompila después de configurar DeepFilterNet.

### Controles de DFNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|----------------|-----------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Attenuation Limit              | 100           | 0-100 dB       | `DfnrAttenLimit`      | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.       |                                                                                        |
| Post-Filter Beta               | 0,00          | 0,00-0,30      | `DfnrPostFilterBeta`  | Aplica un filtro posterior adicional para una supresión extra.                                        | El control deslizante almacena el valor*100 internamente.                                                    |

## Pestaña RN2 (RNNoise)

Seleccionar la pestaña RN2 activa o desvía el motor RN2. Esta página es puramente informativa: no tiene parámetros ajustables.

## Pestaña BNR (NVIDIA)

Seleccionar la pestaña BNR activa o desvía el motor BNR. La intensidad se controla desde el menú superpuesto. El conmutador BNR está atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- Para señales fuertes y limpias donde la fidelidad es importante, reduzca **Attenuation Limit** hacia 0 para limitar cuánto puede alterar el motor el audio.
- Para señales débiles o muy degradadas por ruido, establezca **Attenuation Limit** en 100 y combínelo con un **Post-Filter Beta** distinto de cero para la supresión más agresiva.
- Al usar NR2, comience con los valores predeterminados (Gamma/OSMS/AE activado, 1,50/0,00/0,85/0,20) y ajuste **Reduction:**, **Gain Floor** y **Smoothing:** para encontrar el mejor equilibrio.
- El control **Gain Floor** evita que el motor NR2 aplique una atenuación excesiva a señales muy débiles; los valores más altos conservan más ruido de fondo, los valores más bajos permiten una supresión más profunda.

## Solución de problemas

- **El audio no parece verse afectado después de mover el control deslizante** — Confirme que está en la pestaña correcta y que el motor de reducción de ruido correspondiente está activo. Cada motor tiene controles separados y no se ve afectado por la configuración de otros motores.
- **La pestaña MNR está atenuada** — MNR solo está disponible en compilaciones de macOS.
- **La pestaña BNR está atenuada** — El SDK de NVIDIA Broadcast no se detecta en su sistema.
- **La pestaña DFNR muestra la información sobre herramientas "DFNR no disponible"** — DFNR requiere que se configure DeepFilterNet y que se recompile AetherSDR.

## Relacionado

- [Configurar el beta del filtro posterior de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de la configuración de AetherDSP](overview.md)
