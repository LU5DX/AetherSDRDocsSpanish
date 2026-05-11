# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo a los operadores definir el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de alternancia en la parte superior; al hacer clic en una alternancia también se activa o desvía ese motor.

## Abrir el diálogo

1. Haga clic en **Settings > AetherDSP Settings...**.
2. Se abre el diálogo. Dependiendo de la configuración **FramelessWindow** (habilitada por defecto), el diálogo aparece como una ventana sin marco con una barra de título personalizada o con el marco de ventana estándar del sistema operativo.

El diálogo se puede mover haciendo clic y arrastrando la barra de título (modo sin marco) o la barra de título del sistema operativo (modo estándar). Haga doble clic en la barra de título para alternar maximizar/restaurar. Redimensione haciendo clic y arrastrando cualquier borde o esquina (zona de redimensión de 6 píxeles) en modo sin marco.

## Controles del diálogo

En modo sin marco, la barra de título contiene tres botones de control de ventana y un glifo de agarre:

| Botón | Acción |
|--------|--------|
| **⋮⋮ (glifo de agarre)** | Indicador de referencia visual en el lado izquierdo de la barra de título. |
| **— (Minimizar)** | Minimiza el diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el diálogo. |
| **× (Cerrar)** | Cierra el diálogo. |

## Pestañas de selección del motor DSP

Haga clic en cualquiera de las seis pestañas (NR2, NR4, MNR, DFNR, RN2, BNR) para seleccionar la página de ese motor. Al hacer clic en una pestaña también se activa o desvía el motor correspondiente.

### Disponibilidad de pestañas

- **MNR** — Atenuada en compilaciones de Windows/Linux. El motor MNR no tiene implementación en esas plataformas.
- **NR4** — Atenuada en compilaciones de Windows compiladas sin LLVM (clang-cl). Requiere LLVM de llvm.org para compilar sus VLA de C99.
- **BNR** — Atenuada en compilaciones sin el SDK NVIDIA Broadcast.
- **RN2** — Puramente informativa; no tiene parámetros ajustables.

## Pestaña NR2

NR2 proporciona reducción de ruido musical. Selecciónela haciendo clic en la alternancia **NR2**.

### Controles de NR2

| Control | Tipo | Valor predeterminado | Rango | Clave de Configuración |
|---------|------|---------|-------|-------------|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` (almacenado como entero 0-3) |
| **NPE Method** | Botones de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` (almacenado como entero 0-2) |
| **AE Filter (eliminación de artefactos)** | Casilla de verificación | Verdadero | - | `NR2AeFilter` |
| **Reduction:** | Deslizador | 1.50 | 0.50-2.00 | `NR2GainMax` (almacenado como valor*100) |
| **Smoothing:** | Deslizador | 0.85 | 0.50-0.98 | `NR2GainSmooth` |
| **Threshold:** | Deslizador | 0.20 | 0.05-0.50 | `NR2Qspp` |
| **Reset Defaults (icono ↺)** | Botón pulsador | - | - | - |

### Descripciones de Gain Method

- **Linear** — Utiliza una escala de amplitud de audio lineal para el cálculo de ganancia.
- **Log** — Utiliza una escala de amplitud logarítmica, que comprime el rango dinámico.
- **Gamma** — Modela la ganancia en una distribución gamma que coincide con los patrones típicos de amplitud del habla. Este es el valor predeterminado.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de habla y ruido.

### Descripciones de NPE Method

- **OSMS** — Suavizado óptimo y estadísticas mínimas.
- **MMSE** — Estimación de error cuadrático medio mínimo.
- **NSTAT** — Estimador basado en estadísticas de ruido.

### Reset Defaults (NR2)

Restaura la pestaña NR2 a Gamma/OSMS/AE activado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Pestaña NR4

NR4 proporciona reducción de ruido basada en libspecbleach. Selecciónela haciendo clic en la alternancia **NR4**.

### Controles de NR4

| Control | Tipo | Valor predeterminado | Rango | Clave de Configuración |
|---------|------|---------|-------|-------------|
| **Noise Estimation:** | Botones de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` (almacenado como entero 0-2) |
| **Adaptive Noise Estimation** | Casilla de verificación | Verdadero | - | `NR4AdaptiveNoise` |
| **Reduction (dB):** | Deslizador | 10.0 | 0.0-40.0 | `NR4ReductionAmount` (almacenado como valor*10) |
| **Smoothing (%):** | Deslizador | 0 | 0-100 | `NR4SmoothingFactor` |
| **Whitening (%):** | Deslizador | 0 | 0-100 | `NR4WhiteningFactor` |
| **Masking Depth:** | Deslizador | 0.50 | 0.00-1.00 | `NR4MaskingDepth` |
| **Suppression:** | Deslizador | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` |
| **Reset Defaults (icono ↺)** | Botón pulsador | - | - | - |

### Reset Defaults (NR4)

Restaura la pestaña NR4 a MMSE/adaptativo activado, Reduction 10 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

## Pestaña MNR (solo macOS)

MNR proporciona reducción de ruido MMSE-Wiener en macOS con suavizado de ganancia asimétrico. Haga clic en la alternancia **MNR** para acceder a sus controles.

**Nota:** La alternancia MNR está atenuada en compilaciones de Windows/Linux.

### Controles de MNR

| Control | Tipo | Valor predeterminado | Rango | Clave de Configuración |
|---------|------|---------|-------|-------------|
| **Enable MNR (solo macOS)** | Casilla de verificación | - | - | `MnrEnabled` (estado inicial leído en vivo de AudioEngine) |
| **Strength** | Deslizador | 100 | 0-100 | `MnrStrength` (persistido como normalizado 0.00-1.00) |

## Pestaña DFNR

DFNR proporciona reducción de ruido DeepFilterNet3. Selecciónela haciendo clic en la alternancia **DFNR**.

### Controles de DFNR

| Control | Tipo | Valor predeterminado | Rango | Clave de Configuración |
|---------|------|---------|-------|-------------|
| **Attenuation Limit** | Deslizador | 100 | 0-100 dB | `DfnrAttenLimit` (0 = paso directo, 100 = máximo) |
| **Post-Filter Beta** | Deslizador | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` (almacenado como valor*100) |

## Pestaña RN2

RN2 utiliza el motor RNNoise. Esta pestaña es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

BNR utiliza el SDK NVIDIA Broadcast. El control de intensidad está disponible desde el menú superpuesto. La alternancia BNR está atenuada en compilaciones sin el SDK NVIDIA Broadcast.

## Consejos

- **NR2** — El método de ganancia **Gamma** con NPE **OSMS** es el valor predeterminado y funciona bien para la mayoría de los contactos de voz en SSB. Comience aquí si no está seguro.
- **NR4** — La estimación de ruido **MMSE** con estimación de ruido adaptativa habilitada proporciona un buen rendimiento de referencia.
- **DFNR** — Attenuation Limit en 100 proporciona la máxima supresión. Los valores más bajos permiten que pase más ruido.
- **MNR** (solo macOS) — Strength en 100 proporciona la máxima agresividad. Redúzcalo para obtener un audio con un sonido más natural.
- Después de cambiar el método de ganancia o el método NPE, reajuste los deslizadores de reducción, suavizado y umbral para que coincidan con las nuevas características.
- Cada pestaña tiene su propio botón **Reset Defaults** para restaurar los parámetros de ese motor a la configuración de fábrica.

## Relacionados

- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Habilitar NR2 en una slice](enable-nr2-on-a-slice.md)
- [Habilitar NR4 en una slice](enable-nr4-on-a-slice.md)
