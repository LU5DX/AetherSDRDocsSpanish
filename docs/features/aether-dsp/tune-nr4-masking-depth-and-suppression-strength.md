# Configuración de AetherDSP

La configuración de AetherDSP proporciona control avanzado sobre los motores de reducción de ruido del lado del cliente de AetherSDR: NR2, NR4, MNR, DFNR, RN2 y BNR. Cada motor es seleccionable mediante una fila de interruptores en la parte superior del diálogo; al hacer clic en un interruptor se selecciona la página de ese motor y se activa o desvía el motor.

## Cómo abrir la Configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Se abre el diálogo. Su apariencia depende de la configuración **FramelessWindow**: si está habilitada (predeterminado), el diálogo usa un marco personalizado sin bordes; si está deshabilitada, se muestra el marco de ventana estándar del SO.

## Controles del diálogo

El diálogo de Configuración de AetherDSP utiliza un marco personalizado sin bordes (cuando **FramelessWindow** está habilitado) o el marco de ventana estándar del SO (cuando está deshabilitado). Los comportamientos de redimensionamiento y movimiento se adaptan en consecuencia.

| Control | Comportamiento |
|---------|----------------|
| Barra de título — AetherDSP Settings | Barra de título degradada de 18 píxeles con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. Visible solo en modo sin bordes |
| — (Minimizar) | Minimiza el diálogo. Visible solo en modo sin bordes |
| □ (Maximizar) | Maximiza o restaura el diálogo. Visible solo en modo sin bordes |
| × (Cerrar) | Cierra el diálogo. Visible solo en modo sin bordes |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar maximizar/restaurar. Disponible solo en modo sin bordes |
| Redimensionamiento de 8 ejes | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección. Zona de redimensionamiento de 6 píxeles alrededor del widget de contenido interior. Disponible solo en modo sin bordes |

## Pestaña NR2

El motor NR2 (reducción de ruido musical) utiliza un enfoque de sustracción espectral con métodos de ganancia configurables y estimadores de potencia de ruido.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Gain Method | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Almacenado como entero 0-3 |
| NPE Method | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Almacenado como entero 0-2 |
| AE Filter (eliminación de artefactos) | Habilitado | On/Off | `NR2AeFilter` | Activa o desactiva el post-filtro antiartefactos |
| Reduction: | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El control deslizante almacena el valor*100 internamente |
| Smoothing: | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios |
| Threshold: | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz |
| Reset Defaults (icono ↺) | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20 |

## Pestaña NR4

El motor NR4 utiliza la biblioteca libspecbleach para la reducción de ruido. Ofrece métodos de estimación de ruido configurables y controles de procesamiento espectral.

**Nota:** En Windows, NR4 requiere que LLVM (clang-cl) esté instalado al compilar el código fuente. Si LLVM no está presente, el interruptor de NR4 aparece atenuado y muestra la información sobre herramienta "NR4 requires LLVM (clang-cl) on Windows. Install LLVM from llvm.org and rebuild to enable NR4."

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Noise Estimation: | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Almacenado como entero 0-2 |
| Adaptive Noise Estimation | Habilitado | On/Off | `NR4AdaptiveNoise` | Activa la reestimación continua del piso de ruido |
| Reduction (dB): | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. El control deslizante almacena el valor*10 |
| Smoothing (%): | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4 |
| Whitening (%): | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual |
| Masking Depth: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral |
| Suppression: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión NR4 |
| Reset Defaults (icono ↺) | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50 |

## Pestaña MNR (solo macOS)

El motor MNR (MMSE-Wiener para macOS) está disponible solo en compilaciones de macOS. Proporciona suavizado de ganancia asimétrico para la reducción de ruido. El interruptor MNR aparece atenuado en compilaciones de Windows y Linux; el motor no tiene implementación en esas plataformas.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Enable MNR (macOS only) | Deshabilitado | On/Off | `MnrEnabled` | Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo de AudioEngine |
| Strength | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva como valor normalizado 0.00–1.00 |

## Pestaña DFNR

El motor DFNR (DeepFilterNet3) utiliza un modelo de aprendizaje profundo para la reducción de ruido.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido (0 = paso directo, 100 = máximo) |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para mayor supresión. El control deslizante almacena el valor*100 internamente |

## Pestaña RN2

La pestaña RN2 (RNNoise) es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

La intensidad de la pestaña BNR (NVIDIA) se controla desde el menú superpuesto. El interruptor BNR aparece atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Selección de motor y exclusión mutua

Los seis interruptores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de página como controles de activación/desactivación del motor. Cuando NR2 se activa, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes. Solo un motor puede estar activo a la vez.

## Modo sin bordes

El diálogo respeta la configuración de aplicación **FramelessWindow** (almacenada como `"True"` o `"False"` en `AppSettings`). Cuando está habilitada, el diálogo utiliza un marco personalizado sin bordes con una barra de título degradada, botones de minimizar/maximizar/cerrar, arrastrar para mover y redimensionamiento de 8 ejes. Cuando está deshabilitada, se utilizan el marco y los controles de ventana estándar del SO. Cambiar esta configuración surte efecto la próxima vez que se abra el diálogo. El valor predeterminado es `"True"`.

## Consejos

- **Masking Depth:** y **Suppression:** en la pestaña NR4 interactúan: aumentar ambos juntos produce la máxima reducción de ruido pero el mayor riesgo de distorsión del habla. Auméntelos gradualmente y pruébelos con una señal en vivo o grabada.
- Si el habla suena sobreprocesada o hueca, reduzca primero **Masking Depth:**, luego **Suppression:** hasta que regrese la naturalidad.
- La casilla **Adaptive Noise Estimation** afecta la rapidez con que NR4 sigue un piso de ruido cambiante, lo que a su vez afecta cómo suenan ambos controles deslizantes en la práctica.
- Haga clic en **Reset Defaults** en cualquier pestaña para restaurar todos los parámetros de esa pestaña a sus valores de fábrica.

## Solución de problemas

- **El habla suena hueca o como bajo el agua después de subir los controles deslizantes** — Ambos controles en valores altos pueden suprimir en exceso los componentes espectrales que se superponen con el habla. Reduzca primero **Masking Depth:**, luego **Suppression:** hasta que regrese la naturalidad.
- **El piso de ruido sigue siendo audible incluso con la configuración máxima** — Asegúrese de que **Adaptive Noise Estimation** esté habilitado para que NR4 pueda reestimar continuamente el piso de ruido. Considere también aumentar **Reduction (dB):** .
- **El control deslizante vuelve a su posición o se niega a moverse** — Haga clic directamente en la manija del control deslizante en lugar de hacer clic en la ranura.
- **El interruptor NR4 está atenuado en Windows** — El motor NR4 requiere LLVM (clang-cl) para compilar sus VLA de C99. Instale LLVM desde llvm.org y recompile AetherSDR para habilitar NR4.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
