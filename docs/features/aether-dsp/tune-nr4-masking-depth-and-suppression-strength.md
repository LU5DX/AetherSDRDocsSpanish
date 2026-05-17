# Configuración de AetherDSP

La configuración de AetherDSP proporciona control avanzado sobre los motores de reducción de ruido del lado del cliente de AetherSDR: NR2, NR4, MNR, DFNR, RN2 y BNR. Cada motor se selecciona mediante una fila de botones de alternancia en la parte superior del diálogo; al hacer clic en un botón se selecciona la página de ese motor y se activa o desvía el motor.

## Cómo abrir la Configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Se abrirá el diálogo.

## Controles del diálogo

El diálogo de Configuración de AetherDSP utiliza un marco personalizado sin bordes con una barra de título degradada, botones de minimizar/maximizar/cerrar, arrastrar para mover y redimensionamiento en 8 ejes. La geometría del diálogo se guarda y restaura entre sesiones.

| Control | Comportamiento |
|---------|----------------|
| Barra de título — AetherDSP Settings | Barra de título degradada de 18 píxeles con un icono de agarre (⋮⋮) a la izquierda y el título del diálogo |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar entre maximizar y restaurar |
| Redimensionamiento en 8 ejes | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección. Zona de redimensionamiento de 6 píxeles alrededor del widget de contenido interno |

## Pestaña NR2

El motor NR2 (reducción de ruido musical) utiliza un enfoque de sustracción espectral con métodos de ganancia configurables y estimadores de potencia de ruido.

| Control | Predeterminado | Rango | Clave de Configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Método de Ganancia | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Se almacena como entero 0-3 |
| Método NPE | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2 |
| Filtro AE (eliminación de artefactos) | Activado | On/Off | `NR2AeFilter` | Activa o desactiva el post-filtro antiartefacto |
| Reducción: | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El deslizador almacena el valor*100 internamente |
| Suavizado: | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios |
| Umbral: | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20 |

## Pestaña NR4

El motor NR4 utiliza la biblioteca libspecbleach para la reducción de ruido. Ofrece métodos configurables de estimación de ruido y controles de procesamiento espectral.

**Nota:** En Windows, NR4 requiere que LLVM (clang-cl) esté instalado al compilar el código fuente. Si LLVM no está presente, el botón de alternancia NR4 se atenúa y muestra la información sobre herramientas "NR4 requires LLVM (clang-cl) on Windows. Install LLVM from llvm.org and rebuild to enable NR4."

| Control | Predeterminado | Rango | Clave de Configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Estimación de Ruido: | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2 |
| Estimación Adaptativa de Ruido | Activada | On/Off | `NR4AdaptiveNoise` | Activa la reestimación continua del piso de ruido |
| Reducción (dB): | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. El deslizador almacena el valor*10 |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4 |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual |
| Profundidad de Enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza de supresión general de NR4 |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50 |

## Pestaña MNR (solo macOS)

El motor MNR (MMSE-Wiener de macOS) solo está disponible en compilaciones para macOS. Proporciona un suavizado de ganancia asimétrico para la reducción de ruido. El botón de alternancia MNR está atenuado en compilaciones de Windows y Linux; el motor no tiene un backend en esas plataformas.

| Control | Predeterminado | Rango | Clave de Configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Activar MNR (solo macOS) | Desactivado | On/Off | `MnrEnabled` | Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine |
| Intensidad | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se guarda normalizado como 0.00–1.00 |

## Pestaña DFNR

El motor DFNR (DeepFilterNet3) utiliza un modelo de aprendizaje profundo para la reducción de ruido.

| Control | Predeterminado | Rango | Clave de Configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Límite de Atenuación | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido (0 = paso directo, 100 = máximo) |
| Beta del Post-Filtro | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para una supresión extra. El deslizador almacena el valor*100 internamente |

## Pestaña RN2

La pestaña RN2 (RNNoise) es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

La intensidad de la pestaña BNR (NVIDIA) se controla desde el menú superpuesto. El botón de alternancia BNR está atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Selección de motor y exclusión mutua

Los seis botones de alternancia DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores de página y controles de activación/desactivación del motor. Cuando se activa NR2, AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes. Solo un motor puede estar activo a la vez.

## Consejos

- **Profundidad de Enmascaramiento:** y **Supresión:** en la pestaña NR4 interactúan: aumentar ambos juntos produce la máxima reducción de ruido pero el mayor riesgo de distorsión del habla. Auméntelos gradualmente y pruebe con una señal en vivo o grabada.
- Si el habla suena sobreprocesada o hueca, reduzca primero **Profundidad de Enmascaramiento:**, luego **Supresión:** hasta que recupere la naturalidad.
- La casilla de verificación **Estimación Adaptativa de Ruido** afecta la rapidez con la que NR4 sigue un piso de ruido cambiante, lo que a su vez afecta cómo suenan ambos deslizadores en la práctica.
- Haga clic en **Restablecer valores predeterminados** en cualquier pestaña para devolver todos los parámetros de esa pestaña a sus valores de fábrica.

## Solución de problemas

- **El habla suena hueca o bajo el agua después de subir los deslizadores** — Ambos deslizadores en valores altos pueden suprimir en exceso los componentes espectrales que se superponen con el habla. Reduzca primero **Profundidad de Enmascaramiento:**, luego **Supresión:** hasta que recupere la naturalidad.
- **El piso de ruido sigue siendo audible incluso en la configuración máxima** — Asegúrese de que **Estimación Adaptativa de Ruido** esté activada para que NR4 pueda reestimar continuamente el piso de ruido. También considere aumentar **Reducción (dB):** .
- **El deslizador retrocede o se niega a moverse** — Haga clic directamente en el control deslizante en lugar de hacer clic en la ranura.
- **El botón de alternancia NR4 está atenuado en Windows** — El motor NR4 requiere LLVM (clang-cl) para compilar sus VLA C99. Instale LLVM desde llvm.org y recompile AetherSDR para activar NR4.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
