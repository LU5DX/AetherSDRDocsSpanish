# Configuración de AetherDSP

La configuración de AetherDSP proporciona control avanzado sobre los motores de reducción de ruido del lado del cliente de AetherSDR: NR2, NR4, MNR, DFNR, RN2 y BNR. Cada motor se selecciona mediante una fila de botones de alternancia en la parte superior del diálogo; al hacer clic en un botón se selecciona la página de ese motor y se activa o desvía el motor.

## Abrir la configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Se abre el diálogo.

## Controles del diálogo

El diálogo de configuración de AetherDSP utiliza un marco personalizado sin bordes con una barra de título degradada, botones de minimizar/maximizar/cerrar, arrastrar para mover y redimensionamiento en 8 ejes. La geometría del diálogo se mantiene y se restaura entre sesiones.

| Control | Comportamiento |
|---------|----------------|
| Barra de título — AetherDSP Settings | Barra de título degradada de 18 px con icono de agarre (⋮⋮) a la izquierda y el título del diálogo |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar entre maximizar y restaurar |
| Redimensionamiento en 8 ejes | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección. Zona de redimensionamiento de 6 px alrededor del widget de contenido interno |

## Pestaña NR2

El motor NR2 (reducción de ruido musical) utiliza un enfoque de sustracción espectral con métodos de ganancia y estimadores de potencia de ruido configurables.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------------|-------|------------------------|----------------|
| Método de ganancia | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Se almacena como entero 0-3 |
| Método NPE | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2 |
| Filtro AE (eliminación de artefactos) | Habilitado | Activado/Desactivado | `NR2AeFilter` | Activa/desactiva el filtro posterior antiartefacto |
| Reducción: | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El control deslizante almacena el valor*100 internamente |
| Suavizado: | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios |
| Umbral: | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20 |

## Pestaña NR4

El motor NR4 utiliza la biblioteca libspecbleach para la reducción de ruido. Ofrece métodos de estimación de ruido configurables y controles de procesamiento espectral.

**Nota:** En Windows, NR4 requiere que LLVM (clang-cl) esté instalado al compilar el código fuente. Si LLVM no está presente, el botón de alternancia NR4 aparece atenuado y muestra la información sobre herramientas "NR4 requiere LLVM (clang-cl) en Windows. Instale LLVM desde llvm.org y recompile para habilitar NR4."

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------------|-------|------------------------|----------------|
| Estimación de ruido: | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido. Se almacena como entero 0-2 |
| Estimación de ruido adaptativa | Habilitado | Activado/Desactivado | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido |
| Reducción (dB): | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. El control deslizante almacena el valor*10 |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4 |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual |
| Profundidad de enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión NR4 |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50 |

## Pestaña MNR (solo macOS)

El motor MNR (MMSE-Wiener de macOS) está disponible únicamente en las compilaciones de macOS. Proporciona un suavizado de ganancia asimétrica para la reducción de ruido. El botón de alternancia MNR aparece atenuado en las compilaciones de Windows y Linux; el motor no tiene un backend en esas plataformas.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------------|-------|------------------------|----------------|
| Habilitar MNR (solo macOS) | Deshabilitado | Activado/Desactivado | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrica. El estado inicial se lee en vivo desde AudioEngine |
| Intensidad | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se mantiene normalizado 0.00–1.00 |

## Pestaña DFNR

El motor DFNR (DeepFilterNet3) utiliza un modelo de aprendizaje profundo para la reducción de ruido.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------------|-------|------------------------|----------------|
| Límite de atenuación | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido (0 = paso directo, 100 = máximo) |
| Beta del filtro posterior | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro posterior adicional para una supresión extra. El control deslizante almacena el valor*100 internamente |

## Pestaña RN2

La pestaña RN2 (RNNoise) es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

La intensidad de la pestaña BNR (NVIDIA) se controla desde el menú superpuesto. El botón de alternancia BNR aparece atenuado en las compilaciones sin el NVIDIA Broadcast SDK.

## Selección de motor y exclusión mutua

Los seis botones de alternancia de DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de página como controles de activación/desactivación del motor. Cuando se activa NR2, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes. Solo un motor puede estar activo a la vez.

## Consejos

- **Profundidad de enmascaramiento:** y **Supresión:** en la pestaña NR4 interactúan: aumentar ambos juntos produce la máxima reducción de ruido pero el mayor riesgo de distorsión de la voz. Auméntelos gradualmente y pruébelos en una señal en vivo o grabada.
- Si la voz suena demasiado procesada o hueca, reduzca primero **Profundidad de enmascaramiento:**, luego **Supresión:** hasta que recupere la naturalidad.
- La casilla **Estimación de ruido adaptativa** afecta la rapidez con la que NR4 sigue un piso de ruido cambiante, lo que a su vez afecta cómo suenan ambos controles deslizantes en la práctica.
- Haga clic en **Restablecer valores predeterminados** en cualquier pestaña para devolver todos los parámetros de esa pestaña a sus valores de fábrica.

## Solución de problemas

- **La voz suena hueca o bajo el agua después de subir los controles deslizantes** — Ambos controles deslizantes en valores altos pueden suprimir en exceso los componentes espectrales que se superponen con la voz. Reduzca primero **Profundidad de enmascaramiento:**, luego **Supresión:** hasta que recupere la naturalidad.
- **El piso de ruido aún es audible incluso en la configuración máxima** — Asegúrese de que **Estimación de ruido adaptativa** esté habilitada para que NR4 pueda reestimar continuamente el piso de ruido. Considere también aumentar **Reducción (dB):** .
- **El control deslizante retrocede o se niega a moverse** — Haga clic directamente en el control del deslizante en lugar de hacer clic en la ranura.
- **El botón de alternancia NR4 aparece atenuado en Windows** — El motor NR4 requiere LLVM (clang-cl) para compilar sus VLA C99. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
