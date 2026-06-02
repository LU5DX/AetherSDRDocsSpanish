# Configuración de AetherDSP

Use el cuadro de diálogo **AetherDSP Settings** para ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se seleccionan mediante una fila de botones de activación en la parte superior; al hacer clic en un botón también se activa o desactiva ese motor.

## Abrir la configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.

El cuadro de diálogo se abre con la pestaña de reducción de ruido activa actualmente seleccionada.

## Aspecto del cuadro de diálogo

El cuadro de diálogo AetherDSP Settings utiliza una barra de título de degradado sin marco de 18 píxeles con un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo "AetherDSP Settings". Tres botones de control de ventana se encuentran a la derecha:

- **— (Minimize)** — Minimiza el cuadro de diálogo.
- **□ (Maximize)** — Maximiza o restaura el cuadro de diálogo. Al hacer doble clic en la barra de título también se alterna entre maximizar y restaurar.
- **× (Close)** — Cierra el cuadro de diálogo.

El cuadro de diálogo tiene una zona de ajuste de tamaño de 6 píxeles alrededor del widget de contenido interior. Arrastre la barra de título para mover el cuadro de diálogo. Cambie el tamaño del cuadro de diálogo arrastrando cualquier borde o esquina (redimensionamiento en 8 ejes). La geometría del cuadro de diálogo se conserva entre sesiones bajo la clave de configuración `AetherDspDialogGeometry`.

El cuadro de diálogo utiliza un estilo temático aplicado a través de `ThemeManager` en lugar de una hoja de estilo codificada.

## Comportamiento del selector de pestañas

Las seis pestañas en la parte superior (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de pestaña como controles de activación/desactivación del motor. Al hacer clic en una pestaña, se selecciona esa página y se activa el motor DSP correspondiente. Cuando se activa un nuevo motor, AetherSDR aplica una exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

**Notas de plataforma:**

- **MNR (solo macOS)** — La pestaña MNR está atenuada en las versiones de Windows y Linux porque el motor MMSE-Wiener de macOS no tiene backend en esas plataformas.
- **BNR** — La pestaña BNR está atenuada en las versiones sin el NVIDIA Broadcast SDK.
- **RN2** — La pestaña RN2 es puramente informativa y no tiene parámetros ajustables.

## Pestaña NR2

Use el motor NR2 (reducción de ruido musical) para la supresión de ruido que evita los artefactos musicales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Gain Method | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Habilitado | — | `NR2AeFilter` |
| Reduction: | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | 0.20 | 0.05–0.50 | `NR2Qspp` |

### Restablecer valores predeterminados de NR2

1. Seleccione la pestaña **NR2**.
2. Haga clic en **Reset Defaults** (icono ↺).

Todos los controles de NR2 vuelven a Gamma, OSMS, AE Filter habilitado, Reduction 1.50, Smoothing 0.85, Threshold 0.20.

## Pestaña NR4

Use el motor NR4 (libspecbleach) para la reducción de ruido centrada en el habla con estimación de ruido adaptativa.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Noise Estimation: | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

### Restablecer valores predeterminados de NR4

1. Seleccione la pestaña **NR4**.
2. Haga clic en **Reset Defaults** (icono ↺).

Todos los controles de NR4 vuelven a MMSE, Adaptive Noise Estimation habilitado, Reduction 10.0 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50.

## Pestaña MNR (solo macOS)

Use el motor MNR (MMSE-Wiener de macOS) para la reducción de ruido con suavizado de ganancia asimétrico. Esta pestaña solo está disponible en las versiones de macOS.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Enable MNR (solo macOS) | — | — | `MnrEnabled` |
| Strength | 100 | 0–100 | `MnrStrength` |

**Enable MNR** — Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine.
**Strength** — Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva normalizado entre 0.00–1.00.

## Pestaña DFNR

Use el motor DeepFilterNet3 para la reducción de ruido basada en redes neuronales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** — Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.
**Post-Filter Beta** — Aplica un post-filtro adicional para una supresión extra. El control deslizante almacena el valor×100 internamente.

## Pestaña RN2

La pestaña RN2 (RNNoise) es puramente informativa y no tiene parámetros ajustables. Cuando RN2 está activo, utiliza un modelo de red neuronal para la supresión de ruido en tiempo real sin ajustes configurables por el usuario.

## Pestaña BNR

La pestaña BNR (NVIDIA Broadcast) utiliza el NVIDIA Broadcast SDK para la reducción de ruido basada en IA. La intensidad se controla desde el menú superpuesto. La pestaña BNR está atenuada en las versiones sin el NVIDIA Broadcast SDK.

## Consejos

- **Reset Defaults** afecta solo a la pestaña en la que hace clic. Restablecer NR2 no modifica la configuración de NR4, y viceversa.
- Los cambios surten efecto de inmediato. Si un motor de reducción de ruido está activo en una slice de recepción en ese momento, escuchará el cambio de comportamiento del motor tan pronto como ajuste cualquier control.
- Los seis botones de activación DSP actúan como selectores exclusivos y controles de activación/desactivación del motor simultáneamente. Activar un motor puede desactivar otros módulos mutuamente excluyentes.

## Relacionados

- Ajustar la profundidad de reducción y el umbral de NR2
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
