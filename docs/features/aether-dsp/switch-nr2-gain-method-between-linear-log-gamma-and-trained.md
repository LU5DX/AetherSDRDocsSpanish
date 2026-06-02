# Configuración de AetherDSP

El cuadro de diálogo de Configuración de AetherDSP permite ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo a los operadores ajustar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de botones de alternancia en la parte superior; al hacer clic en un botón también se activa o desactiva ese motor.

## Cómo abrir el cuadro de diálogo

1. Haga clic en **Settings > AetherDSP Settings...**.
2. Se abre el cuadro de diálogo con una barra de título degradada de 18 píxeles sin marco que contiene un glifo de agarre (⋮⋮) a la izquierda y el título del cuadro de diálogo.

El cuadro de diálogo se puede mover haciendo clic y arrastrando la barra de título. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Redimensione haciendo clic y arrastrando cualquier borde o esquina (zona de redimensión de 6 píxeles).

## Controles del cuadro de diálogo

La barra de título contiene tres botones de control de ventana y un glifo de agarre:

| Botón | Acción |
|--------|--------|
| **⋮⋮ (Glifo de agarre)** | Indicador visual de referencia en la parte izquierda de la barra de título. |
| **— (Minimizar)** | Minimiza el cuadro de diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el cuadro de diálogo. |
| **× (Cerrar)** | Cierra el cuadro de diálogo. |

## Pestañas de selección del motor DSP

Haga clic en cualquiera de las seis pestañas (NR2, NR4, MNR, DFNR, RN2, BNR) para seleccionar la página de ese motor. Al hacer clic en una pestaña también se activa o desactiva el motor correspondiente. Cuando NR2 está activado, AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

### Disponibilidad de pestañas

- **MNR** — Atenuada en compilaciones para Windows/Linux. El motor MNR no tiene soporte en esas plataformas.
- **BNR** — Atenuada en compilaciones sin el SDK de NVIDIA Broadcast.
- **RN2** — Solo informativa; no tiene parámetros ajustables.

## Pestaña NR2

NR2 proporciona reducción de ruido musical. Selecciónela haciendo clic en la alternancia **NR2**.

### Controles de NR2

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---------|------|---------|-------|-------------|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` (almacenado como entero 0-3) |
| **NPE Method** | Botones de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` (almacenado como entero 0-2) |
| **AE Filter (eliminación de artefactos)** | Casilla de verificación | Activado | - | `NR2AeFilter` |
| **Reduction:** | Control deslizante | 1.50 | 0.50-2.00 | `NR2GainMax` (almacenado como valor*100) |
| **Smoothing:** | Control deslizante | 0.85 | 0.50-0.98 | `NR2GainSmooth` |
| **Threshold:** | Control deslizante | 0.20 | 0.05-0.50 | `NR2Qspp` |
| **Restablecer valores predeterminados (icono ↺)** | Botón de pulsación | - | - | - |

### Descripciones de Gain Method

- **Linear** — Utiliza una escala de amplitud de audio lineal para el cálculo de la ganancia.
- **Log** — Utiliza una escala de amplitud logarítmica, que comprime el rango dinámico.
- **Gamma** — Modela la ganancia según una distribución gamma que se ajusta a los patrones típicos de amplitud del habla. Esta es la opción predeterminada.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de habla y ruido.

### Descripciones de NPE Method

- **OSMS** — Suavizado óptimo y estadísticas mínimas.
- **MMSE** — Estimación de error cuadrático medio mínimo.
- **NSTAT** — Estimador basado en estadísticas de ruido.

### Restablecer valores predeterminados (NR2)

Restaura la pestaña NR2 a Gamma/OSMS/AE activado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Pestaña NR4

NR4 proporciona reducción de ruido basada en libspecbleach. Selecciónela haciendo clic en la alternancia **NR4**.

### Controles de NR4

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---------|------|---------|-------|-------------|
| **Noise Estimation:** | Botones de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` (almacenado como entero 0-2) |
| **Adaptive Noise Estimation** | Casilla de verificación | Activado | - | `NR4AdaptiveNoise` |
| **Reduction (dB):** | Control deslizante | 10.0 | 0.0-40.0 | `NR4ReductionAmount` (almacenado como valor*10) |
| **Smoothing (%):** | Control deslizante | 0 | 0-100 | `NR4SmoothingFactor` |
| **Whitening (%):** | Control deslizante | 0 | 0-100 | `NR4WhiteningFactor` |
| **Masking Depth:** | Control deslizante | 0.50 | 0.00-1.00 | `NR4MaskingDepth` |
| **Suppression:** | Control deslizante | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` |
| **Restablecer valores predeterminados (icono ↺)** | Botón de pulsación | - | - | - |

### Restablecer valores predeterminados (NR4)

Restaura la pestaña NR4 a MMSE/adaptativo activado, Reduction 10 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

## Pestaña MNR (solo macOS)

MNR proporciona reducción de ruido MMSE-Wiener para macOS con suavizado de ganancia asimétrico. Haga clic en la alternancia **MNR** para acceder a sus controles.

**Nota:** La alternancia MNR está atenuada en compilaciones para Windows/Linux.

### Controles de MNR

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---------|------|---------|-------|-------------|
| **Enable MNR (solo macOS)** | Casilla de verificación | - | - | `MnrEnabled` (el estado inicial se lee en vivo de AudioEngine) |
| **Strength** | Control deslizante | 100 | 0-100 | `MnrStrength` (persistido como normalizado 0.00-1.00) |

## Pestaña DFNR

DFNR proporciona reducción de ruido DeepFilterNet3. Selecciónela haciendo clic en la alternancia **DFNR**.

### Controles de DFNR

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste |
|---------|------|---------|-------|-------------|
| **Attenuation Limit** | Control deslizante | 100 | 0-100 dB | `DfnrAttenLimit` (0 = paso directo, 100 = máximo) |
| **Post-Filter Beta** | Control deslizante | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` (almacenado como valor*100) |

## Pestaña RN2

RN2 utiliza el motor RNNoise. Esta pestaña es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

BNR utiliza el SDK de NVIDIA Broadcast. El control de intensidad está disponible desde el menú superpuesto. La alternancia BNR está atenuada en compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- **NR2** — El método de ganancia **Gamma** con NPE **OSMS** es la opción predeterminada y funciona bien para la mayoría de los contactos de voz en SSB. Comience aquí si no está seguro.
- **NR4** — La estimación de ruido **MMSE** con estimación de ruido adaptativa activada proporciona un buen rendimiento base.
- **DFNR** — El límite de atenuación en 100 proporciona la máxima supresión. Valores más bajos permiten que pase más ruido.
- **MNR** (solo macOS) — La intensidad en 100 proporciona la máxima agresividad. Redúzcala para obtener un audio con un sonido más natural.
- Después de cambiar el método de ganancia o el método NPE, reajuste los controles deslizantes de reducción, suavizado y umbral para que coincidan con las nuevas características.
- Cada pestaña tiene su propio botón **Restablecer valores predeterminados** para restaurar los parámetros de ese motor a los valores de fábrica.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- Activar NR2 en una slice
- Activar NR4 en una slice
