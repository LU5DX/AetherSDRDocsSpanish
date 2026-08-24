# Configuración de AetherDSP

El cuadro de diálogo de Configuración de AetherDSP (se abre mediante `Settings > AetherDSP Settings...`) ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Permite a los operadores equilibrar la compensación entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o se omite ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ajustar la configuración de DSP.
- Seleccione un motor de reducción de ruido haciendo clic en su conmutador en la fila de pestañas del cuadro de diálogo.

## Controles comunes

| Control                        | Comportamiento                                                                                                                                                                                                     | Notas                                                                                                                                                                      |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Barra de título — AetherDSP Settings | Barra de título con degradado de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo.                                                                                                            | Coincide con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip.                                                                                            |
| — (Minimizar)                   | Minimiza el diálogo.                                                                                                                                                                                               |                                                                                                                                                                            |
| □ (Maximizar)                   | Maximiza o restaura el diálogo.                                                                                                                                                                                    |                                                                                                                                                                            |
| × (Cerrar)                      | Cierra el diálogo.                                                                                                                                                                                                 |                                                                                                                                                                            |
| Arrastrar para mover            | Haga clic y arrastre la barra de título para mover el diálogo.                                                                                                                                                     | Haga doble clic en la barra de título para alternar maximizar/restaurar.                                                                                                     |
| Redimensionado de 8 ejes         | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionado.                                                                      | Zona de redimensionado de 6 px alrededor del widget de contenido interno.                                                                                                                      |
| Restablecer valores predeterminados (icono ↺)       | Restaura los valores predeterminados de la pestaña actual. Para RN2, esto restablece el control deslizante de Piso de ruido al 0%. Para BNR, esta es una operación sin efecto (sin parámetros ajustables).                                                                 | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).                                                                                                       |
| Piso de ruido (mezcla seca de RN2)      | Define el porcentaje de la señal original que RN2 deja debajo del audio denoizado. Cero produce supresión total (silencio entre frases); 10-20% mantiene un piso de silencio constante para que el receptor siga sonando vivo. | Afecta solo al audio recibido; el denoizador de transmisión no cambia. Lo persiste Rn2SettingsModel y lo expone a la cadena DSP mediante la señal rn2DryMixChanged de AetherDspWidget. |

## Pestaña NR2 (Reducción de ruido musical)

Seleccionar la pestaña NR2 activa u omite el motor NR2. Cuando NR2 está activado, AudioEngine ejecuta exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

### Controles de NR2

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración           | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|----------------|-----------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Método de ganancia                    | Gamma         | Lineal, Logarítmico, Gamma, Entrenado | `NR2GainMethod`       | Selecciona la asignación de la curva de ganancia utilizada por NR2.                                                        | Se almacena como entero 0-3 en el orden anterior.                                        |
| Método de NPE                     | OSMS          | OSMS, MMSE, NSTAT | `NR2NpeMethod`        | Selecciona el estimador de potencia de ruido.                                                                 | Se almacena como entero 0-2.                                                                |
| Filtro AE (eliminación de artefactos) | True          | —              | `NR2AeFilter`         | Activa el post-filtro anti-artefactos.                                                          |                                                                                        |
| Reducción:                     | 1.50          | 0.50-2.00      | `NR2GainMax`          | Define la profundidad máxima de reducción de NR2.                                                              | El control deslizante almacena valor*100 internamente.                                                    |
| Piso de ganancia                     | 0.00          | 0.00-0.50      | `NR2GainFloor`        | Define el piso de ganancia mínimo para el procesamiento de NR2.                                                 | Añadido en v26.7.4.                                                                      |
| Suavizado:                     | 0.85          | 0.50-0.98      | `NR2GainSmooth`       | Controla con qué suavidad la estimación de ruido sigue los cambios.                                        |                                                                                        |
| Umbral:                     | 0.20          | 0.05-0.50      | `NR2Qspp`             | Define el umbral de probabilidad de presencia de habla.                                                    |                                                                                        |
| Restablecer valores predeterminados (icono ↺)       | —              | —              | —                     | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activados, 1.50/0.00/0.85/0.20).                             | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).                   |

## Pestaña NR4 (libspecbleach)

Seleccionar la pestaña NR4 activa u omite el motor NR4.

### Controles de NR4

| Control                        | Valor predeterminado | Rango válido              | Clave de configuración                    | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|--------------------------|--------------------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Estimación de ruido:              | MMSE          | MMSE, Brandt, Martin     | `NR4NoiseEstimationMethod`     | Selecciona el estimador de piso de ruido utilizado por NR4.                                                      | Se almacena como entero 0-2.                                                                |
| Estimación de ruido adaptativa      | True          | —                        | `NR4AdaptiveNoise`             | Habilita la re-estimación continua del piso de ruido.                                            |                                                                                        |
| Reducción (dB):                | 10.0          | 0.0-40.0                | `NR4ReductionAmount`           | Define la reducción máxima de ruido de NR4 en dB.                                                         | El control deslizante almacena valor*10.                                                                |
| Suavizado (%):                 | 0             | 0-100                   | `NR4SmoothingFactor`           | Suavizado en el dominio del tiempo de la estimación de ruido de NR4.                                                    |                                                                                        |
| Blanqueamiento (%):                 | 0             | 0-100                   | `NR4WhiteningFactor`           | Aplana la forma espectral del ruido residual.                                                         |                                                                                        |
| Profundidad de enmascaramiento:                 | 0.50          | 0.00-1.00               | `NR4MaskingDepth`              | Controla la profundidad del enmascaramiento espectral.                                                                |                                                                                        |
| Supresión:                   | 0.50          | 0.00-1.00               | `NR4SuppressionStrength`       | Fuerza de supresión general de NR4.                                                               |                                                                                        |
| Restablecer valores predeterminados (icono ↺)       | —              | —                        | —                              | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activados, 10 dB, 0, 0, 0.50, 0.50).                              | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).                   |

## Pestaña MNR (MMSE-Wiener de macOS)

Seleccionar la pestaña MNR activa u omite el motor MNR. El conmutador de MNR está atenuado en las versiones para Windows/Linux: el motor no tiene backend en esas plataformas.

### Controles de MNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración      | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|----------------|------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Habilitar MNR (solo macOS)        | —             | —              | `MnrEnabled`     | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.                            | El estado inicial se lee en vivo desde AudioEngine::mnrEnabled().                               |
| Intensidad                       | 100           | 0-100          | `MnrStrength`    | Ajusta la agresividad de MNR (0 suave, 100 máximo).                                                   | Se persiste como valor normalizado 0.00-1.00.                                                     |
| Restablecer valores predeterminados (icono ↺)       | —              | —              | —                | Restaura los valores predeterminados de MNR (intensidad 100).                                                           | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).                   |

## Pestaña DFNR (DeepFilterNet3)

Seleccionar la pestaña DFNR activa u omite el motor DeepFilterNet3. DFNR solo está disponible cuando AetherSDR se recompila después de configurar DeepFilterNet.

### Controles de DFNR

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración           | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|----------------|-----------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Límite de atenuación              | 100           | 0-100 dB       | `DfnrAttenLimit`      | Define la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.       |                                                                                        |
| Beta de post-filtro               | 0.00          | 0.00-0.30      | `DfnrPostFilterBeta`  | Aplica un post-filtro adicional para mayor supresión.                                        | El control deslizante almacena valor*100 internamente.                                                    |
| Restablecer valores predeterminados (icono ↺)       | —              | —              | —                   | Restaura los valores predeterminados de DFNR (100, 0.00).                                                             | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).                   |

## Pestaña RN2 (RNNoise)

Seleccionar la pestaña RN2 activa u omite el motor RN2. Esta página incluye un único parámetro ajustable para controlar cuánta señal original se mezcla debajo del audio denoizado.

### Controles de RN2

| Control                        | Valor predeterminado | Rango válido    | Clave de configuración      | Comportamiento                                                                                        | Notas                                                                                  |
|--------------------------------|---------------|----------------|------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Piso de ruido (mezcla seca de RN2)      | 0             | 0-100          | —                | Define el porcentaje de la señal original que RN2 deja debajo del audio denoizado. Cero produce supresión total (silencio entre frases); 10-20% mantiene un piso de silencio constante para que el receptor siga sonando vivo. | Afecta solo al audio recibido; el denoizador de transmisión no cambia. Lo persiste Rn2SettingsModel y lo expone a la cadena DSP mediante la señal rn2DryMixChanged de AetherDspWidget. Añadido en v26.8.4. |
| Restablecer valores predeterminados (icono ↺)       | —              | —              | —                | Restaura los valores predeterminados de la pestaña RN2 (Piso de ruido 0).                                                      | Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).                   |

## Pestaña BNR (NVIDIA)

Seleccionar la pestaña BNR activa u omite el motor BNR. La intensidad se controla desde el menú superpuesto. El conmutador de BNR está atenuado en las versiones sin el SDK de NVIDIA Broadcast. La pestaña BNR no tiene parámetros ajustables; Restablecer valores predeterminados es una operación sin efecto.

## Consejos

- Para señales fuertes y limpias donde importa preservar la fidelidad, reduzca **Límite de atenuación** hacia 0 para limitar cuánto puede alterar el motor el audio.
- Para señales débiles o muy degradadas por ruido, configure **Límite de atenuación** a 100 y combínelo con un **Beta de post-filtro** distinto de cero para la supresión más agresiva.
- Al usar NR2, comience con los valores predeterminados (Gamma/OSMS/AE activados, 1.50/0.00/0.85/0.20) y ajuste **Reducción:**, **Piso de ganancia** y **Suavizado:** para encontrar el mejor equilibrio.
- El control **Piso de ganancia** evita que el motor NR2 aplique atenuación excesiva a señales muy débiles; los valores más altos conservan más ruido de fondo, los valores más bajos permiten una supresión más profunda.
- Al usar RN2, configure **Piso de ruido** al 10-20% si la salida totalmente suprimida suena demasiado muerta entre frases.
- Para una configuración de NR2 más agresiva, desactive **Filtro AE** y aumente **Reducción:** y **Suavizado:**.

## Solución de problemas

- **El audio no se ve afectado después de mover el control deslizante** — Confirme que está en la pestaña correcta y que el motor de reducción de ruido correspondiente está activo. Cada motor tiene controles separados y no se ve afectado por la configuración de otros motores.
- **La pestaña MNR está atenuada** — MNR solo está disponible en las versiones para macOS.
- **La pestaña BNR está atenuada** — El SDK de NVIDIA Broadcast no se detecta en su sistema.
- **La pestaña DFNR muestra la información sobre herramientas de DFNR no disponible** — DFNR requiere que DeepFilterNet esté configurado y AetherSDR recompilado.
- **El control deslizante de Piso de ruido de RN2 no tiene efecto** — Confirme que RN2 es el motor activo (haga clic en su conmutador) y que el motor RN2 no está omitido.

## Relacionado

- [Configurar el beta de post-filtro de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Resumen de la Configuración de AetherDSP](overview.md)
