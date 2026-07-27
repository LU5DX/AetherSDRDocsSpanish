# Configuración de AetherDSP

La configuración de AetherDSP proporciona control avanzado sobre los motores de reducción de ruido del lado del cliente de AetherSDR: NR2, NR4, MNR, DFNR, RN2 y BNR. Cada motor se selecciona mediante una fila de interruptores en la parte superior del diálogo; al hacer clic en un interruptor se selecciona la página de ese motor y se activa o desactiva el motor.

## Abrir la configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Se abre el diálogo.

## Controles del diálogo

El diálogo de configuración de AetherDSP utiliza un marco personalizado sin bordes con una barra de título degradada, botones de minimizar/maximizar/cerrar, arrastrar para mover y redimensionamiento en 8 ejes. La geometría del diálogo se guarda y restaura entre sesiones.

| Control | Comportamiento |
|---------|---------------|
| Barra de título - Configuración de AetherDSP | Barra de título degradada de 18 px con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo |
| — (Minimizar) | Minimiza el diálogo |
| □ (Maximizar) | Maximiza o restaura el diálogo |
| × (Cerrar) | Cierra el diálogo |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar entre maximizar y restaurar |
| Redimensionamiento en 8 ejes | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección. Zona de redimensionamiento de 6 px alrededor del widget de contenido interno |

## Pestaña NR2

El motor NR2 (reducción de ruido musical) utiliza un enfoque de sustracción espectral con métodos de ganancia configurables y estimadores de potencia de ruido.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------|-------|------------------------|----------------|
| Método de ganancia | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia. Se almacena como entero 0-3 |
| Método NPE | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2 |
| Filtro AE (eliminación de artefactos) | Activado | Activado/Desactivado | `NR2AeFilter` | Activa o desactiva el postfiltro antiartefacto |
| Reducción: | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El deslizador almacena el valor*100 internamente |
| Suavizado: | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios |
| Umbral: | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz |
| Usar geometría original | Desactivado | Activado/Desactivado | `NR2UseOriginalGeometry` | Cuando está activado, utiliza la geometría de la curva de ganancia NR2 original en lugar de la geometría mejorada más reciente. Desactivado por defecto para obtener el mejor rendimiento |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR2: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20, Usar geometría original desactivado |

## Pestaña NR4

El motor NR4 utiliza la librería libspecbleach para la reducción de ruido. Ofrece métodos de estimación de ruido configurables y controles de procesamiento espectral.

**Nota:** En Windows, NR4 requiere que LLVM (clang-cl) esté instalado al compilar el código fuente. Si LLVM no está presente, el interruptor NR4 aparece atenuado y muestra la información sobre herramientas "NR4 requires LLVM (clang-cl) on Windows. Install LLVM from llvm.org and rebuild to enable NR4."

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------|-------|------------------------|----------------|
| Estimación de ruido: | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2 |
| Estimación de ruido adaptativa | Activado | Activado/Desactivado | `NR4AdaptiveNoise` | Activa la reestimación continua del piso de ruido |
| Reducción (dB): | 10.0 | 0.0–40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. El deslizador almacena el valor*10 |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4 |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual |
| Profundidad de enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Fuerza general de supresión NR4 |
| Restablecer valores predeterminados (icono ↺) | — | — | — | Restaura los valores predeterminados de NR4: MMSE, adaptativo activado, 10 dB, 0, 0, 0.50, 0.50 |

## Pestaña MNR (solo macOS)

El motor MNR (MMSE-Wiener de macOS) solo está disponible en compilaciones de macOS. Proporciona un suavizado de ganancia asimétrico para la reducción de ruido. El interruptor MNR aparece atenuado en las compilaciones de Windows y Linux; el motor no tiene un backend en esas plataformas.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------|-------|------------------------|----------------|
| Activar MNR (solo macOS) | Desactivado | Activado/Desactivado | `MnrEnabled` | Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo del AudioEngine |
| Intensidad | 100 | 0–100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máxima). Se guarda como valor normalizado 0.00–1.00 |

## Pestaña DFNR

El motor DFNR (DeepFilterNet3) utiliza un modelo de aprendizaje profundo para la reducción de ruido.

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------|-------|------------------------|----------------|
| Límite de atenuación | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido (0 = paso directo, 100 = máxima) |
| Beta del postfiltro | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un postfiltro adicional para una supresión extra. El deslizador almacena el valor*100 internamente |

## Pestaña RN2

La pestaña RN2 (RNNoise) es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

La intensidad de la pestaña BNR (NVIDIA) se controla desde el menú superpuesto. El interruptor BNR aparece atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Selección de motor y exclusión mutua

Los seis interruptores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores de página y controles de activación/desactivación del motor. Cuando NR2 está activado, el AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes. Solo un motor puede estar activo a la vez.

## Persistencia

El motor de reducción de ruido del lado del cliente utilizado por última vez se guarda en `LastClientNr` y se restaura en el siguiente inicio. Si el motor guardado (por ejemplo, DFNR) no está disponible en la compilación actual, la preferencia se elimina silenciosamente.

## Consejos

- **Profundidad de enmascaramiento:** y **Supresión:** en la pestaña NR4 interactúan: aumentar ambos juntos produce la máxima reducción de ruido pero el mayor riesgo de distorsión de la voz. Auméntelos gradualmente y pruebe con una señal en vivo o grabada.
- Si la voz suena demasiado procesada o hueca, reduzca primero **Profundidad de enmascaramiento:** y luego **Supresión:** hasta que recupere la naturalidad.
- La casilla **Estimación de ruido adaptativa** afecta la rapidez con que NR4 sigue un piso de ruido cambiante, lo que a su vez afecta cómo suenan ambos deslizadores en la práctica.
- La casilla **Usar geometría original** en la pestaña NR2 revierte a la geometría de la curva de ganancia heredada utilizada en versiones anteriores de AetherSDR. Déjela desactivada para obtener los mejores resultados a menos que tenga una razón específica para usar la curva original.
- Haga clic en **Restablecer valores predeterminados** en cualquier pestaña para devolver todos los parámetros de esa pestaña a sus valores de fábrica.

## Solución de problemas

- **La voz suena hueca o bajo el agua después de subir los deslizadores** — Ambos deslizadores con valores altos pueden suprimir en exceso los componentes espectrales que se superponen con la voz. Reduzca primero **Profundidad de enmascaramiento:** y luego **Supresión:** hasta que recupere la naturalidad.
- **El piso de ruido sigue siendo audible incluso con la configuración al máximo** — Asegúrese de que **Estimación de ruido adaptativa** esté activada para que NR4 pueda reestimar continuamente el piso de ruido. También considere aumentar **Reducción (dB):** .
- **El deslizador vuelve a su posición o se niega a moverse** — Haga clic directamente en la manija del deslizador en lugar de hacer clic en la ranura.
- **El interruptor NR4 aparece atenuado en Windows** — El motor NR4 requiere LLVM (clang-cl) para compilar sus VLA de C99. Instale LLVM desde llvm.org y reconstruya AetherSDR para activar NR4.
- **El motor de reducción de ruido utilizado por última vez no se restaura entre sesiones** — Si el motor guardado (por ejemplo, DFNR) no está compilado en la compilación actual, la preferencia se elimina silenciosamente. Seleccione un motor disponible y reinicie para guardar la nueva preferencia.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
