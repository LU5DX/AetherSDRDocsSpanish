# Configuración de AetherDSP

El cuadro de diálogo Configuración de AetherDSP permite ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), lo que permite al operador encontrar el equilibrio ideal entre la supresión de ruido y la fidelidad de la voz. Los seis módulos DSP se seleccionan mediante una fila de botones en la parte superior; al hacer clic en un botón también se activa o se desactiva ese motor.

## Cómo abrir el cuadro de diálogo

1. Haga clic en **Settings > AetherDSP Settings...**.
2. El cuadro de diálogo se abre con una barra de título degradada de 18 px sin marco que contiene un glifo de agarre (⋮⋮) a la izquierda y el título del cuadro de diálogo.

El cuadro de diálogo se puede mover haciendo clic y arrastrando la barra de título. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Cambie el tamaño haciendo clic y arrastrando cualquier borde o esquina (zona de cambio de tamaño de 6 px).

## Controles del cuadro de diálogo

La barra de título contiene tres botones de control de ventana y un glifo de agarre:

| Botón | Acción |
|-------|--------|
| **⋮⋮ (Glifo de agarre)** | Indicador de referencia visual en el lado izquierdo de la barra de título. |
| **— (Minimizar)** | Minimiza el cuadro de diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el cuadro de diálogo. |
| **× (Cerrar)** | Cierra el cuadro de diálogo. |

## Pestañas de selección del motor DSP

Haga clic en cualquiera de las seis pestañas (NR2, NR4, MNR, DFNR, RN2, BNR) para seleccionar la página de ese motor. Al hacer clic en una pestaña también se activa o se desactiva el motor correspondiente.

### Disponibilidad de pestañas

- **MNR** — Atenuada en las compilaciones para Windows/Linux. El motor MNR no tiene una implementación interna en esas plataformas.
- **BNR** — Atenuada en las compilaciones sin el NVIDIA Broadcast SDK.
- **RN2** — Solo informativa; no tiene parámetros ajustables.

## Pestaña NR2

NR2 proporciona reducción de ruido musical. Selecciónela haciendo clic en el botón **NR2**.

### Controles de NR2

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---------|------|----------------------|-------|------------------------|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` (almacenado como entero 0-3) |
| **NPE Method** | Botones de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` (almacenado como entero 0-2) |
| **AE Filter (eliminación de artefactos)** | Casilla de verificación | Activado | - | `NR2AeFilter` |
| **Reduction:** | Deslizador | 1.50 | 0.50-2.00 | `NR2GainMax` (almacenado como valor*100) |
| **Smoothing:** | Deslizador | 0.85 | 0.50-0.98 | `NR2GainSmooth` |
| **Threshold:** | Deslizador | 0.20 | 0.05-0.50 | `NR2Qspp` |
| **Reset Defaults (icono ↺)** | Botón pulsador | - | - | - |

### Descripciones de Gain Method

- **Linear** — Utiliza una escala de amplitud de audio lineal para el cálculo de la ganancia.
- **Log** — Utiliza una escala de amplitud logarítmica, que comprime el rango dinámico.
- **Gamma** — Modela la ganancia según una distribución gamma que se ajusta a los patrones típicos de amplitud del habla. Es el valor predeterminado.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de voz y ruido.

### Descripciones de NPE Method

- **OSMS** — Suavizado óptimo y estadísticas mínimas.
- **MMSE** — Estimación de error cuadrático medio mínimo.
- **NSTAT** — Estimador basado en estadísticas de ruido.

### Reset Defaults (NR2)

Restaura la pestaña NR2 a Gamma/OSMS/AE activados, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Pestaña NR4

NR4 proporciona reducción de ruido basada en libspecbleach. Selecciónela haciendo clic en el botón **NR4**.

### Controles de NR4

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---------|------|----------------------|-------|------------------------|
| **Noise Estimation:** | Botones de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` (almacenado como entero 0-2) |
| **Adaptive Noise Estimation** | Casilla de verificación | Activado | - | `NR4AdaptiveNoise` |
| **Reduction (dB):** | Deslizador | 10.0 | 0.0-40.0 | `NR4ReductionAmount` (almacenado como valor*10) |
| **Smoothing (%):** | Deslizador | 0 | 0-100 | `NR4SmoothingFactor` |
| **Whitening (%):** | Deslizador | 0 | 0-100 | `NR4WhiteningFactor` |
| **Masking Depth:** | Deslizador | 0.50 | 0.00-1.00 | `NR4MaskingDepth` |
| **Suppression:** | Deslizador | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` |
| **Reset Defaults (icono ↺)** | Botón pulsador | - | - | - |

### Reset Defaults (NR4)

Restaura la pestaña NR4 a MMSE/estimación adaptativa activada, Reduction 10 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

## Pestaña MNR (solo macOS)

MNR proporciona reducción de ruido MMSE-Wiener en macOS con suavizado de ganancia asimétrico. Haga clic en el botón **MNR** para acceder a sus controles.

**Nota:** El botón MNR está atenuado en las compilaciones para Windows/Linux.

### Controles de MNR

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---------|------|----------------------|-------|------------------------|
| **Enable MNR (solo macOS)** | Casilla de verificación | - | - | `MnrEnabled` (el estado inicial se lee directamente de AudioEngine) |
| **Strength** | Deslizador | 100 | 0-100 | `MnrStrength` (se conserva como valor normalizado 0.00-1.00) |

## Pestaña DFNR

DFNR proporciona reducción de ruido basada en DeepFilterNet3. Selecciónela haciendo clic en el botón **DFNR**.

### Controles de DFNR

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración |
|---------|------|----------------------|-------|------------------------|
| **Attenuation Limit** | Deslizador | 100 | 0-100 dB | `DfnrAttenLimit` (0 = paso directo, 100 = máximo) |
| **Post-Filter Beta** | Deslizador | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` (almacenado como valor*100) |

## Pestaña RN2

RN2 utiliza el motor RNNoise. Esta pestaña es solo informativa y no tiene parámetros ajustables.

## Pestaña BNR

BNR utiliza el NVIDIA Broadcast SDK. El control de intensidad está disponible desde el menú superpuesto. El botón BNR está atenuado en las compilaciones sin el NVIDIA Broadcast SDK.

## Consejos

- **NR2** — El método de ganancia **Gamma** con NPE **OSMS** es el valor predeterminado y funciona bien para la mayoría de los contactos de voz en SSB. Comience aquí si no está seguro.
- **NR4** — La estimación de ruido **MMSE** con la estimación de ruido adaptativa activada proporciona un buen rendimiento base.
- **DFNR** — Un Attenuation Limit de 100 ofrece la máxima supresión. Los valores más bajos permiten que pase más ruido.
- **MNR** (solo macOS) — Un Strength de 100 proporciona la máxima agresividad. Redúzcalo para obtener un audio con un sonido más natural.
- Después de cambiar el método de ganancia o el método NPE, reajuste los deslizadores de reducción, suavizado y umbral para que se ajusten a las nuevas características.
- Cada pestaña tiene su propio botón **Reset Defaults** para restaurar los parámetros de ese motor a la configuración de fábrica.

## Relacionados

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Activar NR2 en un slice](enable-nr2-on-a-slice.md)
- [Activar NR4 en un slice](enable-nr4-on-a-slice.md)
