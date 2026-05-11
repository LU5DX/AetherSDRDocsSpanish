# Configuración de AetherDSP

El cuadro de diálogo Configuración de AetherDSP (se abre mediante `Settings > AetherDSP Settings...`) ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Permite al operador definir el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o se desvía ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ajustar la configuración DSP.
- Seleccione un motor de reducción de ruido haciendo clic en su conmutador en la fila de pestañas del cuadro de diálogo.

## Controles comunes

| Control                         | Comportamiento                                                                                              | Notas                                                                                    |
|---------------------------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Barra de título — AetherDSP Settings | Barra de título con degradado de 18 px, un asa de agarre (⋮⋮) a la izquierda y el título del cuadro de diálogo. La visibilidad de la barra de título se controla mediante el ajuste FramelessWindow. | Coincide con la familia de ventanas de NetworkDiagnosticsDialog y AetherialAudioStrip. |
| — (Minimizar)                   | Minimiza el cuadro de diálogo.                                                                              |                                                                                          |
| □ (Maximizar)                   | Maximiza o restaura el cuadro de diálogo.                                                                   |                                                                                          |
| × (Cerrar)                      | Cierra el cuadro de diálogo.                                                                                |                                                                                          |
| Arrastrar para mover            | Haga clic y arrastre la barra de título para mover el cuadro de diálogo.                                    | Haga doble clic en la barra de título para alternar entre maximizar y restaurar.         |
| Redimensionar en 8 ejes         | Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. | Zona de redimensionamiento de 12 px alrededor de los bordes del cuadro de diálogo (solo cuando el modo sin marco está habilitado). |

## Pestaña NR2 (Reducción de ruido musical)

Al seleccionar la pestaña NR2 se activa o se desvía el motor NR2. Cuando NR2 está activado, AudioEngine aplica una exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

### Controles de NR2

| Control                        | Valor predeterminado | Rango válido   | Clave de ajuste   | Comportamiento                                                                                               | Notas                                                                                         |
|--------------------------------|----------------------|----------------|-------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Gain Method                    | Gamma                | Linear, Log, Gamma, Trained | `NR2GainMethod`   | Selecciona la asignación de la curva de ganancia utilizada por NR2.                                          | Se almacena como un entero 0-3 que coincide con el orden anterior.                           |
| NPE Method                     | OSMS                 | OSMS, MMSE, NSTAT | `NR2NpeMethod`    | Selecciona el estimador de potencia de ruido.                                                                | Se almacena como un entero 0-2.                                                              |
| AE Filter (eliminación de artefactos) | Verdadero           | —                | `NR2AeFilter`     | Activa o desactiva el postfiltro antirruido.                                                                   |                                                                                               |
| Reduction:                     | 1.50                 | 0.50-2.00       | `NR2GainMax`      | Establece la profundidad máxima de reducción de NR2.                                                           | El deslizador almacena el valor*100 internamente.                                            |
| Smoothing:                     | 0.85                 | 0.50-0.98       | `NR2GainSmooth`   | Controla la suavidad con la que la estimación de ruido sigue los cambios.                                      |                                                                                               |
| Threshold:                     | 0.20                 | 0.05-0.50       | `NR2Qspp`         | Establece el umbral de probabilidad de presencia de voz.                                                        |                                                                                               |
| Restablecer valores predeterminados (icono ↺) | —                    | —              | —                 | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20).               | Se representa como un botón de icono plano con una flecha antihoraria (U+21BA).              |

## Pestaña NR4 (libspecbleach)

Al seleccionar la pestaña NR4 se activa o se desvía el motor NR4. En Windows, NR4 requiere que LLVM (clang-cl) esté instalado; la pestaña se atenúa con una información sobre herramientas cuando no está disponible.

### Controles de NR4

| Control                        | Valor predeterminado | Rango válido             | Clave de ajuste               | Comportamiento                                                                                               | Notas                                                                                         |
|--------------------------------|----------------------|--------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Noise Estimation:              | MMSE                 | MMSE, Brandt, Martin     | `NR4NoiseEstimationMethod`     | Selecciona el estimador de suelo de ruido utilizado por NR4.                                                  | Se almacena como un entero 0-2.                                                              |
| Adaptive Noise Estimation      | Verdadero            | —                        | `NR4AdaptiveNoise`            | Habilita la reestimación continua del suelo de ruido.                                                         |                                                                                               |
| Reduction (dB):                | 10.0                 | 0.0-40.0                | `NR4ReductionAmount`           | Establece la reducción máxima de ruido de NR4 en dB.                                                          | El deslizador almacena el valor*10.                                                            |
| Smoothing (%):                 | 0                    | 0-100                   | `NR4SmoothingFactor`           | Suavizado en el dominio del tiempo de la estimación de ruido de NR4.                                           |                                                                                               |
| Whitening (%):                 | 0                    | 0-100                   | `NR4WhiteningFactor`           | Aplana la forma espectral del ruido residual.                                                                  |                                                                                               |
| Masking Depth:                 | 0.50                 | 0.00-1.00               | `NR4MaskingDepth`              | Controla la profundidad del enmascaramiento espectral.                                                         |                                                                                               |
| Suppression:                   | 0.50                 | 0.00-1.00               | `NR4SuppressionStrength`       | Fuerza de supresión general de NR4.                                                                           |                                                                                               |
| Restablecer valores predeterminados (icono ↺) | —                    | —                        | —                              | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50).               | Se representa como un botón de icono plano con una flecha antihoraria (U+21BA).              |

## Pestaña MNR (MMSE-Wiener de macOS)

Al seleccionar la pestaña MNR se activa o se desvía el motor MNR. El conmutador MNR está atenuado en las compilaciones de Windows/Linux; el motor no tiene un backend en esas plataformas.

### Controles de MNR

| Control                        | Valor predeterminado | Rango válido   | Clave de ajuste   | Comportamiento                                                                                               | Notas                                                                                         |
|--------------------------------|----------------------|----------------|-------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Enable MNR (solo macOS)        | —                    | —              | `MnrEnabled`      | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrica.                             | El estado inicial se lee en vivo desde AudioEngine::mnrEnabled().                            |
| Strength                       | 100                  | 0-100          | `MnrStrength`     | Ajusta la agresividad de MNR (0 suave, 100 máximo).                                                           | Se guarda normalizado como 0.00-1.00.                                                         |

## Pestaña DFNR (DeepFilterNet3)

Al seleccionar la pestaña DFNR se activa o se desvía el motor DeepFilterNet3.

### Controles de DFNR

| Control                        | Valor predeterminado | Rango válido   | Clave de ajuste      | Comportamiento                                                                                               | Notas                                                                                         |
|--------------------------------|----------------------|----------------|----------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Attenuation Limit              | 100                  | 0-100 dB       | `DfnrAttenLimit`     | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.          |                                                                                               |
| Post-Filter Beta               | 0.00                 | 0.00-0.30      | `DfnrPostFilterBeta` | Aplica un postfiltro adicional para una supresión extra.                                                      | El deslizador almacena el valor*100 internamente.                                            |

## Pestaña RN2 (RNNoise)

Al seleccionar la pestaña RN2 se activa o se desvía el motor RN2. Esta página es puramente informativa: no tiene parámetros ajustables.

## Pestaña BNR (NVIDIA)

Al seleccionar la pestaña BNR se activa o se desvía el motor BNR. La intensidad se controla desde el menú superpuesto. El conmutador BNR está atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- Para señales fuertes y limpias en las que sea importante preservar la fidelidad, reduzca **Attenuation Limit** hacia 0 para limitar cuánto puede modificar el motor el audio.
- Para señales débiles o muy degradadas por el ruido, establezca **Attenuation Limit** en 100 y combínelo con un **Post-Filter Beta** distinto de cero para la supresión más agresiva.
- Al usar NR2, comience con los valores predeterminados (Gamma/OSMS/AE activado, 1.50/0.85/0.20) y ajuste **Reduction:** y **Smoothing:** para encontrar el mejor equilibrio.

## Solución de problemas

- **El audio no se ve afectado después de mover el deslizador** — Confirme que está en la pestaña correcta y que el motor de reducción de ruido correspondiente está activo. Cada motor tiene controles separados y no se ve afectado por la configuración de otros motores.
- **La pestaña MNR está atenuada** — MNR solo está disponible en las compilaciones de macOS.
- **La pestaña BNR está atenuada** — El SDK de NVIDIA Broadcast no se detecta en su sistema.
- **La pestaña NR4 está atenuada en Windows** — NR4 requiere que LLVM (clang-cl) esté instalado. Instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

## Relacionado

- [Configure DFNR post-filter beta for extra suppression](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Choosing the right noise reduction: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [AetherDSP Settings overview](overview.md)
