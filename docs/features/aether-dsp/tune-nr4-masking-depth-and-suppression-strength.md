# Configuración de AetherDSP

Configuración de AetherDSP proporciona control avanzado sobre los motores de reducción de ruido del lado del cliente de AetherSDR: NR2, NR4, MNR, DFNR, RN2 y BNR. Cada motor se selecciona mediante una fila de conmutadores en la parte superior del diálogo; al hacer clic en un conmutador se selecciona la página de ese motor y se activa o se omite el motor.

## Abrir Configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Se abre el diálogo.

## Controles del diálogo

El diálogo Configuración de AetherDSP utiliza un marco personalizado sin bordes con una barra de título en degradado, botones de minimizar/maximizar/cerrar, arrastre para mover y redimensionado en 8 ejes. La geometría del diálogo se conserva y se restaura entre sesiones.

| Control                        | Comportamiento                                                                                                                                                                                                 | Notas                                                                                                                                                                      |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Barra de título — AetherDSP Settings | Barra de título en degradado de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo                                                                                                                               |                                                                                                                                                                            |
| — (Minimizar)                   | Minimiza el diálogo                                                                                                                                                                                         |                                                                                                                                                                            |
| □ (Maximizar)                   | Maximiza o restaura el diálogo                                                                                                                                                                             |                                                                                                                                                                            |
| × (Cerrar)                      | Cierra el diálogo                                                                                                                                                                                            |                                                                                                                                                                            |
| Arrastrar para mover                   | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar entre maximizar/restaurar                                                                                                                     |                                                                                                                                                                            |
| Redimensionado en 8 ejes                  | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección. Zona de redimensionado de 6 px alrededor del widget de contenido interno                                                                      |                                                                                                                                                                            |
| Piso de ruido (mezcla seca RN2)      | Establece el porcentaje de la señal original que RN2 deja bajo el audio con reducción de ruido. El valor cero produce supresión total (silencio entre frases); el 10-20% mantiene un piso de ruido bajo constante para que el receptor siga sonando vivo. | Afecta solo al audio recibido; el eliminador de ruido de transmisión no cambia. Se conserva mediante Rn2SettingsModel y se expone a la cadena DSP mediante la señal rn2DryMixChanged de AetherDspWidget. |

## Pestaña NR2

El motor NR2 (reducción de ruido musical) utiliza un enfoque de sustracción espectral con métodos de ganancia y estimadores de potencia de ruido configurables.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| Método de ganancia | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Se almacena como entero 0-3 |
| Método NPE | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2 |
| Filtro AE (eliminación de artefactos) | Habilitado | Activado/Desactivado | `NR2AeFilter` | Alterna el filtro posterior anti-artefactos |
| Reducción: | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El control deslizante almacena el valor*100 internamente |
| Suavizado: | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con que la estimación de ruido sigue los cambios |
| Umbral: | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20 |

## Pestaña NR4

El motor NR4 utiliza la biblioteca libspecbleach para la reducción de ruido. Ofrece métodos de estimación de ruido configurables y controles de procesamiento espectral.

**Nota:** En Windows, NR4 requiere que LLVM (clang-cl) esté instalado al compilar el código fuente. Si LLVM no está presente, el conmutador NR4 aparece atenuado y muestra la información sobre herramientas "NR4 requires LLVM (clang-cl) on Windows. Install LLVM from llvm.org and rebuild to enable NR4."

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| Estimación de ruido: | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2 |
| Estimación de ruido adaptativa | Habilitado | Activado/Desactivado | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido |
| Reducción (dB): | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. El control deslizante almacena el valor*10 |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio temporal de la estimación de ruido NR4 |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual |
| Profundidad de enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión de NR4 |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50 |

## Pestaña MNR (solo macOS)

El motor MNR (MMSE-Wiener de macOS) está disponible únicamente en las compilaciones de macOS. Proporciona suavizado de ganancia asimétrico para la reducción de ruido. El conmutador MNR aparece atenuado en las compilaciones de Windows y Linux — el motor no tiene backend en esas plataformas.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| Habilitar MNR (solo macOS) | Deshabilitado | Activado/Desactivado | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine |
| Intensidad | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva como valor normalizado 0.00–1.00 |

## Pestaña DFNR

El motor DFNR (DeepFilterNet3) utiliza un modelo de aprendizaje profundo para la reducción de ruido.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| Límite de atenuación | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido (0 = paso directo, 100 = máximo) |
| Beta del filtro posterior | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro posterior adicional para mayor supresión. El control deslizante almacena el valor*100 internamente |

## Pestaña RN2

El motor RN2 (RNNoise) utiliza una red neuronal recurrente para la supresión de ruido. La pestaña aloja el control deslizante de mezcla seca del piso de ruido, que controla el porcentaje de la señal original mezclada bajo el audio con reducción de ruido.

## Pestaña BNR

La intensidad de la pestaña BNR (NVIDIA) se controla desde el menú superpuesto. El conmutador BNR aparece atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.

## Selección de motor y exclusión mutua

Los seis conmutadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) funcionan tanto como selectores de página como controles de habilitación/deshabilitación del motor. Cuando se activa NR2, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes. Solo un motor puede estar activo a la vez.

## Persistencia

El motor de reducción de ruido del lado del cliente utilizado por última vez se conserva en `LastClientNr` y se restaura en el próximo inicio. Si el motor almacenado (por ejemplo, DFNR) no está disponible en la compilación actual, la preferencia se borra silenciosamente.

## Consejos

- **Profundidad de enmascaramiento:** y **Supresión:** en la pestaña NR4 interactúan: aumentar ambos juntos produce la reducción máxima de ruido pero el mayor riesgo de distorsión del habla. Auméntelos de forma incremental y pruébelos con una señal en vivo o grabada.
- Si el habla suena sobreprocesada o hueca, reduzca primero **Profundidad de enmascaramiento:** y luego **Supresión:** hasta que vuelva la naturalidad.
- La casilla **Estimación de ruido adaptativa** afecta la rapidez con que NR4 sigue un piso de ruido cambiante, lo que a su vez afecta cómo suenan ambos controles deslizantes en la práctica.
- En la pestaña RN2, un valor pequeño de **Piso de ruido** (10–20%) mantiene el receptor sonando vivo mientras elimina la mayor parte del ruido de fondo. Un valor de 0 produce supresión total, que puede sonar silenciosa entre frases.
- Haga clic en **Restablecer valores predeterminados** en cualquier pestaña para devolver todos los parámetros de esa pestaña a sus valores de fábrica. En la pestaña RN2, Restablecer valores predeterminados devuelve el control deslizante de Piso de ruido a 0; en la pestaña BNR no tiene efecto.

## Solución de problemas

- **El habla suena hueca o como bajo el agua después de subir los controles deslizantes** — Ambos controles en valores altos pueden suprimir en exceso los componentes espectrales que se superponen con el habla. Reduzca primero **Profundidad de enmascaramiento:** y luego **Supresión:** hasta que vuelva la naturalidad.
- **El piso de ruido sigue siendo audible incluso en la configuración máxima** — Asegúrese de que **Estimación de ruido adaptativa** esté habilitada para que NR4 pueda reestimar continuamente el piso de ruido. Considere también aumentar **Reducción (dB):** .
- **El control deslizante vuelve a su posición o se niega a moverse** — Haga clic directamente en la perilla del control deslizante en lugar de hacer clic en la ranura.
- **El conmutador NR4 aparece atenuado en Windows** — El motor NR4 requiere LLVM (clang-cl) para compilar sus VLA de C99. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.
- **El motor de reducción de ruido utilizado por última vez no se restaura entre sesiones** — Si el motor persistido (por ejemplo, DFNR) no está compilado en la compilación actual, la preferencia se borra silenciosamente. Seleccione un motor disponible y reinicie para conservar la nueva preferencia.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
