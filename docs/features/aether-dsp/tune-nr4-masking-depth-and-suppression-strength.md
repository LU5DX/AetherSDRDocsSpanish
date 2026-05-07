# Configuración de AetherDSP

La configuración de AetherDSP proporciona control avanzado sobre los motores de reducción de ruido del lado del cliente de AetherSDR: NR2, NR4, MNR, DFNR, RN2 y BNR. Cada motor se selecciona mediante una fila de botones en la parte superior del diálogo; al hacer clic en un botón se selecciona la página de ese motor y se activa o desactiva el motor.

## Abrir la configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.
2. El diálogo se abre como una ventana sin marco con una barra de título personalizada.

## Controles del diálogo

El diálogo de configuración de AetherDSP utiliza un marco personalizado sin bordes con funcionalidades de redimensionamiento y movimiento añadidas en la versión v0.9.8.

| Control | Comportamiento |
|---------|----------------|
| Barra de título — AetherDSP Settings | Barra de título con degradado de 18 px con un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar entre maximizar y restaurar |
| Redimensionamiento en 8 ejes | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección. Zona de 6 px alrededor del widget de contenido interior |

## Pestaña NR2

El motor NR2 (reducción de ruido musical) utiliza un enfoque de sustracción espectral con métodos de ganancia configurables y estimadores de potencia de ruido.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| Gain Method | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona el mapeo de la curva de ganancia. Se almacena como entero 0-3 |
| NPE Method | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2 |
| AE Filter (eliminación de artefactos) | Activado | On/Off | `NR2AeFilter` | Activa o desactiva el post-filtro antiartefacto |
| Reduction: | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El deslizador almacena el valor*100 internamente |
| Smoothing: | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios |
| Threshold: | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz |
| Reset Defaults (icono ↺) | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20 |

## Pestaña NR4

El motor NR4 utiliza la librería libspecbleach para la reducción de ruido. Ofrece métodos configurables de estimación de ruido y controles de procesamiento espectral.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| Noise Estimation: | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2 |
| Adaptive Noise Estimation | Activado | On/Off | `NR4AdaptiveNoise` | Activa la reestimación continua del piso de ruido |
| Reduction (dB): | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. El deslizador almacena el valor*10 |
| Smoothing (%): | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4 |
| Whitening (%): | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual |
| Masking Depth: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral |
| Suppression: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Intensidad general de supresión NR4 |
| Reset Defaults (icono ↺) | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50 |

## Pestaña MNR (solo macOS)

El motor MNR (MMSE-Wiener para macOS) está disponible únicamente en las compilaciones de macOS. Proporciona un suavizado de ganancia asimétrico para la reducción de ruido.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| Enable MNR (macOS only) | Desactivado | On/Off | `MnrEnabled` | Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo del AudioEngine |
| Strength | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se persiste como valor normalizado 0.00–1.00 |

## Pestaña DFNR

El motor DFNR (DeepFilterNet3) utiliza un modelo de aprendizaje profundo para la reducción de ruido.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido (0 = paso directo, 100 = máxima) |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para una supresión extra. El deslizador almacena el valor*100 internamente |

## Pestaña RN2

La pestaña RN2 (RNNoise) es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

La intensidad de la pestaña BNR (NVIDIA) se controla desde el menú superpuesto. El botón BNR aparece atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Selección de motor y exclusión mutua

Los seis botones DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de página como controles de activación/desactivación del motor. Cuando NR2 se activa, el AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes. Solo un motor puede estar activo a la vez.

## Consejos

- **Masking Depth:** y **Suppression:** en la pestaña NR4 interactúan entre sí: elevar ambos al máximo produce la mayor reducción de ruido pero también el mayor riesgo de distorsión de la voz. Auméntelos gradualmente y pruebe con una señal en vivo o grabada.
- Si la voz suena demasiado procesada o hueca, reduzca primero **Masking Depth:** y luego **Suppression:** hasta que recupere la naturalidad.
- La casilla **Adaptive Noise Estimation** afecta la rapidez con la que NR4 sigue un piso de ruido cambiante, lo que a su vez afecta cómo suenan ambos deslizadores en la práctica.
- Haga clic en **Reset Defaults** en cualquier pestaña para restaurar todos los parámetros de esa pestaña a sus valores de fábrica.

## Solución de problemas

- **La voz suena hueca o como bajo el agua después de subir los deslizadores** — Ambos deslizadores con valores altos pueden suprimir en exceso componentes espectrales que se superponen con la voz. Reduzca primero **Masking Depth:** y luego **Suppression:** hasta que recupere la naturalidad.
- **El piso de ruido sigue siendo audible incluso con la configuración máxima** — Asegúrese de que **Adaptive Noise Estimation** esté activado para que NR4 pueda reestimar continuamente el piso de ruido. También considere aumentar **Reduction (dB):** .
- **El deslizador vuelve a su posición o se niega a moverse** — Haga clic directamente en el mango del deslizador en lugar de hacer clic en la ranura.

## Relacionados

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
