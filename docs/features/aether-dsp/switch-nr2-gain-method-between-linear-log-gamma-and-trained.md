# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo al operador equilibrar la relación entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o se omite ese motor.

## Abrir el diálogo

1. Haga clic en **Settings > AetherDSP Settings...**.
2. El diálogo se abre con una barra de título degradada sin marco de 18 px que contiene un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo.

El diálogo se puede mover haciendo clic y arrastrando la barra de título. Haga doble clic en la barra de título para alternar entre maximizar/restaurar. Cambie el tamaño haciendo clic y arrastrando cualquier borde o esquina (zona de cambio de tamaño de 6 px).

## Controles del diálogo

La barra de título contiene tres botones de control de ventana y un glifo de agarre:

| Botón                      | Acción                                                                                                                                                                                                                    | Notas                                                                                                                                                                           |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **⋮⋮ (Glifo de agarre)**    | Indicador de referencia visual a la izquierda de la barra de título.                                                                                                                                                      |                                                                                                                                                                                 |
| **— (Minimizar)**           | Minimiza el diálogo.                                                                                                                                                                                                      |                                                                                                                                                                                 |
| **□ (Maximizar)**           | Maximiza o restaura el diálogo.                                                                                                                                                                                           |                                                                                                                                                                                 |
| **× (Cerrar)**              | Cierra el diálogo.                                                                                                                                                                                                        |                                                                                                                                                                                 |
| Noise Floor (RN2 dry mix)   | Establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce supresión total (silencio entre frases); 10-20 % mantiene un piso de ruido constante y bajo para que el receptor siga sonando vivo. | Afecta solo al audio recibido; el denoizador de transmisión no cambia. Se guarda mediante Rn2SettingsModel y se expone a la cadena DSP a través de la señal rn2DryMixChanged de AetherDspWidget. |

## Pestañas de selección del motor DSP

Haga clic en cualquiera de las seis pestañas (NR2, NR4, MNR, DFNR, RN2, BNR) para seleccionar la página de ese motor. Al hacer clic en una pestaña también se activa o se omite el motor correspondiente. Cuando se activa NR2, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

### Disponibilidad de pestañas

- **MNR** — Atenuada en compilaciones para Windows/Linux. El motor MNR no tiene backend en esas plataformas.
- **BNR** — Atenuada en compilaciones sin el SDK de NVIDIA Broadcast.
- **RN2** — Control deslizante de Noise Floor ajustable (nuevo en v26.8.4); antes era puramente informativo.
- **DFNR** — Atenuada en compilaciones sin el SDK de DeepFilterNet.

## Pestaña NR2

NR2 proporciona reducción de ruido musical. Selecciónela haciendo clic en el conmutador **NR2**.

### Controles de NR2

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---------|------|----------------|-------|------------------------|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` (almacenada como entero 0-3) |
| **NPE Method** | Botones de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` (almacenada como entero 0-2) |
| **AE Filter (eliminación de artefactos)** | Casilla de verificación | True | - | `NR2AeFilter` |
| **Reduction:** | Control deslizante | 1.50 | 0.50-2.00 | `NR2GainMax` (almacenada como valor*100) |
| **Smoothing:** | Control deslizante | 0.85 | 0.50-0.98 | `NR2GainSmooth` |
| **Threshold:** | Control deslizante | 0.20 | 0.05-0.50 | `NR2Qspp` |
| **Reset Defaults (ícono ↺)** | Botón pulsador | - | - | - |

### Descripciones de Gain Method

- **Linear** — Usa una escala de amplitud de audio lineal para el cálculo de la ganancia.
- **Log** — Usa una escala de amplitud logarítmica, que comprime el rango dinámico.
- **Gamma** — Modela la ganancia según una distribución gamma que coincide con los patrones típicos de amplitud del habla. Este es el predeterminado.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de habla y ruido.

### Descripciones de NPE Method

- **OSMS** — Suavizado óptimo y estadísticas mínimas.
- **MMSE** — Estimación de error cuadrático medio mínimo.
- **NSTAT** — Estimador basado en estadísticas de ruido.

### Reset Defaults (NR2)

Restaura la pestaña NR2 a Gamma/OSMS/AE activado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Pestaña NR4

NR4 proporciona reducción de ruido basada en libspecbleach. Selecciónela haciendo clic en el conmutador **NR4**.

### Controles de NR4

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---------|------|----------------|-------|------------------------|
| **Noise Estimation:** | Botones de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` (almacenada como entero 0-2) |
| **Adaptive Noise Estimation** | Casilla de verificación | True | - | `NR4AdaptiveNoise` |
| **Reduction (dB):** | Control deslizante | 10.0 | 0.0-40.0 | `NR4ReductionAmount` (almacenada como valor*10) |
| **Smoothing (%):** | Control deslizante | 0 | 0-100 | `NR4SmoothingFactor` |
| **Whitening (%):** | Control deslizante | 0 | 0-100 | `NR4WhiteningFactor` |
| **Masking Depth:** | Control deslizante | 0.50 | 0.00-1.00 | `NR4MaskingDepth` |
| **Suppression:** | Control deslizante | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` |
| **Reset Defaults (ícono ↺)** | Botón pulsador | - | - | - |

### Reset Defaults (NR4)

Restaura la pestaña NR4 a MMSE/adaptativo activado, Reduction 10 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

## Pestaña MNR (solo macOS)

MNR proporciona reducción de ruido MMSE-Wiener en macOS con suavizado de ganancia asimétrico. Haga clic en el conmutador **MNR** para acceder a sus controles.

**Nota:** El conmutador MNR está atenuado en compilaciones para Windows/Linux.

### Controles de MNR

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---------|------|----------------|-------|------------------------|
| **Strength** | Control deslizante | 100 | 0-100 | `MnrStrength` (guardada como valor normalizado 0.00-1.00) |

## Pestaña DFNR

DFNR proporciona reducción de ruido DeepFilterNet3. Selecciónela haciendo clic en el conmutador **DFNR**.

**Nota:** El conmutador DFNR está atenuado en compilaciones sin el SDK de DeepFilterNet.

### Controles de DFNR

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---------|------|----------------|-------|------------------------|
| **Attenuation Limit** | Control deslizante | 100 | 0-100 dB | `DfnrAttenLimit` (0 = paso directo, 100 = máximo) |
| **Post-Filter Beta** | Control deslizante | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` (almacenada como valor*100) |
| **Reset Defaults (ícono ↺)** | Botón pulsador | - | - | - |

## Pestaña RN2

RN2 proporciona reducción de ruido basada en RNNoise. Selecciónela haciendo clic en el conmutador **RN2**.

### Controles de RN2

| Control | Tipo | Predeterminado | Rango | Clave de configuración |
|---------|------|----------------|-------|------------------------|
| **Noise Floor (RN2 dry mix)** | Control deslizante | 0 | 0-100 | - |

El control deslizante Noise Floor establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce supresión total (silencio entre frases); 10-20 % mantiene un piso de ruido constante y bajo para que el receptor siga sonando vivo. Afecta solo al audio recibido; el denoizador de transmisión no cambia.

### Reset Defaults (RN2)

Restaura la pestaña RN2 a Noise Floor 0.

## Pestaña BNR

BNR usa el SDK de NVIDIA Broadcast. El control de intensidad está disponible desde el menú superpuesto. El conmutador BNR está atenuado en compilaciones sin el SDK de NVIDIA Broadcast. No tiene parámetros ajustables — Reset Defaults no realiza ninguna acción aquí.

## Consejos

- **NR2** — El método de ganancia **Gamma** con NPE **OSMS** es el predeterminado y funciona bien para la mayoría de los contactos de voz en SSB. Comience aquí si no está seguro.
- **NR4** — La estimación de ruido **MMSE** con estimación adaptativa de ruido activada proporciona un buen rendimiento de referencia.
- **DFNR** — Attenuation Limit en 100 ofrece la máxima supresión. Los valores más bajos permiten que pase más ruido.
- **MNR** (solo macOS) — Strength en 100 proporciona la máxima agresividad. Redúzcalo para obtener un audio con un sonido más natural.
- **RN2** — Establezca Noise Floor en 10-20 % para mantener el receptor sonando vivo entre frases; ajústelo a 0 para una supresión máxima.
- Después de cambiar el método de ganancia o el método NPE, reajuste los controles deslizantes de reducción, suavizado y umbral para que coincidan con las nuevas características.
- Cada pestaña tiene su propio botón **Reset Defaults** para restaurar los parámetros de ese motor a los valores de fábrica.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- Activar NR2 en un slice
- Activar NR4 en un slice
