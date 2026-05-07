# Configuración de AetherDSP

Utilice el cuadro de diálogo **Configuración de AetherDSP** para ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se pueden seleccionar mediante una fila de botones de alternancia en la parte superior; al hacer clic en un botón de alternancia también se activa o desvía ese motor.

## Abrir la Configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.

El cuadro de diálogo se abre con la pestaña de reducción de ruido actualmente activa seleccionada.

## Marco del cuadro de diálogo (v0.9.8)

El cuadro de diálogo Configuración de AetherDSP utiliza una barra de título personalizada sin marco con un fondo de degradado azul y el título del diálogo "AetherDSP Settings" en texto negrita de 10 px. Un glifo de agarre (⋮⋮) aparece a la izquierda. Tres botones de control de ventana se encuentran a la derecha:

- **— (Minimizar)** — Minimiza el diálogo.
- **□ (Maximizar)** — Maximiza o restaura el diálogo. Al hacer doble clic en la barra de título también se alterna entre maximizar y restaurar.
- **× (Cerrar)** — Cierra el diálogo.

Arrastre la barra de título para mover el diálogo. Cambie el tamaño del diálogo arrastrando cualquier borde o esquina (redimensionamiento en 8 direcciones, zona de impacto de redimensionamiento de 12 px).

## Comportamiento del selector de pestañas

Las seis pestañas en la parte superior (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de pestañas como controles de activación/desactivación del motor. Al hacer clic en una pestaña, se selecciona esa página y se activa el motor DSP correspondiente. Cuando se activa un nuevo motor, AetherSDR aplica una exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

**Notas de plataforma:**

- **MNR (solo macOS)** — La pestaña MNR está atenuada en las compilaciones para Windows y Linux porque el motor MMSE-Wiener de macOS no tiene backend en esas plataformas.
- **BNR** — La pestaña BNR está atenuada en compilaciones sin el SDK de NVIDIA Broadcast.
- **RN2** — La pestaña RN2 es puramente informativa y no tiene parámetros ajustables.

## Pestaña NR2

Utilice el motor NR2 (reducción de ruido musical) para la supresión de ruido que evita artefactos musicales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Método de Ganancia | Gamma | Lineal \| Log \| Gamma \| Entrenado | `NR2GainMethod` |
| Método NPE | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| Filtro AE (eliminación de artefactos) | Habilitado | — | `NR2AeFilter` |
| Reducción: | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Suavizado: | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Umbral: | 0.20 | 0.05–0.50 | `NR2Qspp` |

### Restablecer valores predeterminados de NR2

1. Seleccione la pestaña **NR2**.
2. Haga clic en **Restablecer Valores Predeterminados** (icono ↺).

Todos los controles de NR2 vuelven a Gamma, OSMS, Filtro AE habilitado, Reducción 1.50, Suavizado 0.85, Umbral 0.20.

## Pestaña NR4

Utilice el motor NR4 (libspecbleach) para la reducción de ruido centrada en el habla con estimación de ruido adaptativa.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Estimación de Ruido: | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Estimación de Ruido Adaptativa | Habilitado | — | `NR4AdaptiveNoise` |
| Reducción (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Profundidad de Enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

### Restablecer valores predeterminados de NR4

1. Seleccione la pestaña **NR4**.
2. Haga clic en **Restablecer Valores Predeterminados** (icono ↺).

Todos los controles de NR4 vuelven a MMSE, Estimación de Ruido Adaptativa habilitada, Reducción 10.0 dB, Suavizado 0, Blanqueamiento 0, Profundidad de Enmascaramiento 0.50, Supresión 0.50.

## Pestaña MNR (solo macOS)

Utilice el motor MNR (macOS MMSE-Wiener) para la reducción de ruido con suavizado de ganancia asimétrico. Esta pestaña solo está disponible en compilaciones para macOS.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Habilitar MNR (solo macOS) | — | — | `MnrEnabled` |
| Intensidad | 100 | 0–100 | `MnrStrength` |

**Habilitar MNR** — Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine.
**Intensidad** — Ajusta la agresividad de MNR (0 suave, 100 máximo). Se persiste como valor normalizado 0.00–1.00.

## Pestaña DFNR

Utilice el motor DeepFilterNet3 para la reducción de ruido basada en redes neuronales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Límite de Atenuación | 100 | 0–100 dB | `DfnrAttenLimit` |
| Beta del Post-Filtro | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Límite de Atenuación** — Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.
**Beta del Post-Filtro** — Aplica un post-filtro adicional para una supresión extra. El control deslizante almacena el valor×100 internamente.

## Consejos

- **Restablecer Valores Predeterminados** afecta solo a la pestaña donde se hace clic. Restablecer NR2 no altera la configuración de NR4, y viceversa.
- Los cambios surten efecto de inmediato. Si un motor de reducción de ruido está activo en una franja de recepción en ese momento, escuchará el cambio de comportamiento del motor tan pronto como ajuste cualquier control.
- Los seis conmutadores DSP actúan como selectores exclusivos y controles de activación/desactivación del motor simultáneamente. Activar un motor puede desactivar otros módulos mutuamente excluyentes.

## Relacionado

- [Ajustar la profundidad de reducción y el umbral de NR2](tune-nr2-reduction-depth-and-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Lineal, Log, Gamma y Entrenado](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
