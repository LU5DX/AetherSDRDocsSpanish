# Configuración de AetherDSP

El cuadro de diálogo de Configuración de AetherDSP ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo al operador afinar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o se desvía ese motor.

## Abrir el cuadro de diálogo

1. Haga clic en **Settings > AetherDSP Settings...**.
2. El cuadro de diálogo se abre como una ventana sin marco con una barra de título personalizada.

El cuadro de diálogo se puede mover haciendo clic y arrastrando la barra de título. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Cambie el tamaño haciendo clic y arrastrando cualquier borde o esquina (zona de redimensionamiento de 6 píxeles).

## Controles del cuadro de diálogo

La barra de título contiene tres botones de control de ventana:

| Botón | Acción |
|--------|--------|
| **— (Minimizar)** | Minimiza el cuadro de diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el cuadro de diálogo. |
| **× (Cerrar)** | Cierra el cuadro de diálogo. |

Un glifo de agarre (⋮⋮) aparece en el lado izquierdo de la barra de título como referencia visual.

## Pestañas de selección del motor DSP

Haga clic en cualquiera de las seis pestañas (NR2, NR4, MNR, DFNR, RN2, BNR) para seleccionar la página de ese motor. Al hacer clic en una pestaña también se activa o se desvía el motor correspondiente.

### Disponibilidad de pestañas

- **MNR** — Atenuado en compilaciones para Windows/Linux. El motor MNR no tiene un backend en esas plataformas.
- **BNR** — Atenuado en compilaciones sin el SDK de NVIDIA Broadcast.
- **RN2** — Puramente informativo; sin parámetros ajustables.

## Pestaña NR2

NR2 proporciona reducción de ruido musical. Selecciónelo haciendo clic en el conmutador **NR2**.

### Controles de NR2

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
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

NR4 proporciona reducción de ruido basada en libspecbleach. Selecciónelo haciendo clic en el conmutador **NR4**.

### Controles de NR4

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
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

MNR proporciona reducción de ruido MMSE-Wiener de macOS con suavizado de ganancia asimétrico. Haga clic en el conmutador **MNR** para acceder a sus controles.

**Nota:** El conmutador MNR está atenuado en compilaciones para Windows/Linux.

### Controles de MNR

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---------|------|---------|-------|-------------|
| **Enable MNR (solo macOS)** | Casilla de verificación | - | - | `MnrEnabled` (estado inicial leído en vivo de AudioEngine) |
| **Strength** | Deslizador | 100 | 0-100 | `MnrStrength` (persistido como normalizado 0.00-1.00) |

## Pestaña DFNR

DFNR proporciona reducción de ruido DeepFilterNet3. Selecciónelo haciendo clic en el conmutador **DFNR**.

### Controles de DFNR

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---------|------|---------|-------|-------------|
| **Attenuation Limit** | Deslizador | 100 | 0-100 dB | `DfnrAttenLimit` (0 = paso directo, 100 = máximo) |
| **Post-Filter Beta** | Deslizador | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` (almacenado como valor*100) |

## Pestaña RN2

RN2 utiliza el motor RNNoise. Esta pestaña es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

BNR utiliza el SDK de NVIDIA Broadcast. El control de intensidad está disponible desde el menú superpuesto. El conmutador BNR está atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- **NR2** — El método de ganancia **Gamma** con NPE **OSMS** es el valor predeterminado y funciona bien para la mayoría de los contactos de voz en SSB. Comience aquí si no está seguro.
- **NR4** — La estimación de ruido **MMSE** con estimación de ruido adaptativa habilitada proporciona un buen rendimiento base.
- **DFNR** — Attenuation Limit en 100 proporciona la máxima supresión. Los valores más bajos permiten que pase más ruido.
- **MNR** (solo macOS) — Strength en 100 proporciona la máxima agresividad. Reduzca para obtener un audio con un sonido más natural.
- Después de cambiar el método de ganancia o el método NPE, reajuste los deslizadores de reducción, suavizado y umbral para que coincidan con las nuevas características.
- Cada pestaña tiene su propio botón **Reset Defaults** para restaurar los parámetros de ese motor a la configuración de fábrica.

## Relacionados

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Habilitar NR2 en una slice](enable-nr2-on-a-slice.md)
- [Habilitar NR4 en una slice](enable-nr4-on-a-slice.md)
