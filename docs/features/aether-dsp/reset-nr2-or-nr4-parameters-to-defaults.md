# Configuración de AetherDSP

Utilice el diálogo **Configuración de AetherDSP** para ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se seleccionan mediante una fila de interruptores en la parte superior; al hacer clic en un interruptor también se activa o se omite ese motor.

## Cómo abrir la Configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.

Se abre el diálogo con la pestaña de reducción de ruido actualmente activa seleccionada.

## Interfaz del diálogo

El diálogo Configuración de AetherDSP utiliza una barra de título sin marco con un fondo degradado azul y el título del diálogo "AetherDSP Settings" en negrita de 10 px. A la izquierda aparece un glifo de agarre (⋮⋮). A la derecha se encuentran tres botones de control de ventana:

- **— (Minimizar)** — Minimiza el diálogo.
- **□ (Maximizar)** — Maximiza o restaura el diálogo. Al hacer doble clic en la barra de título también se alterna entre maximizar y restaurar.
- **× (Cerrar)** — Cierra el diálogo.

El diálogo tiene una zona de redimensionamiento de 6 píxeles alrededor del widget de contenido interior. Arrastre la barra de título para mover el diálogo. Redimensione el diálogo arrastrando cualquier borde o esquina (redimensionamiento en 8 direcciones). La geometría del diálogo se conserva entre sesiones bajo la clave de configuración `AetherDspDialogGeometry`.

## Comportamiento del selector de pestañas

Las seis pestañas en la parte superior (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de pestaña como controles de activación/desactivación del motor. Al hacer clic en una pestaña se selecciona esa página y se activa el motor DSP correspondiente. Cuando se activa un nuevo motor, AetherSDR aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

**Notas de plataforma:**

- **MNR (solo macOS)** — La pestaña MNR está atenuada en las compilaciones de Windows y Linux porque el motor MMSE-Wiener de macOS no tiene soporte en esas plataformas.
- **NR4 (solo Windows con LLVM)** — La pestaña NR4 está atenuada en las compilaciones de Windows compiladas sin clang-cl (LLVM). Instale LLVM desde llvm.org y recompile para habilitar NR4.
- **BNR** — La pestaña BNR está atenuada en compilaciones sin el NVIDIA Broadcast SDK.
- **RN2** — La pestaña RN2 es puramente informativa y no tiene parámetros ajustables.

## Pestaña NR2

Utilice el motor NR2 (reducción de ruido musical) para la supresión de ruido que evita artefactos musicales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Método de ganancia | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| Método NPE | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| Filtro AE (eliminación de artefactos) | Habilitado | — | `NR2AeFilter` |
| Reducción: | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Suavizado: | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Umbral: | 0.20 | 0.05–0.50 | `NR2Qspp` |

### Restablecer valores predeterminados de NR2

1. Seleccione la pestaña **NR2**.
2. Haga clic en **Restablecer valores predeterminados** (icono ↺).

Todos los controles de NR2 vuelven a Gamma, OSMS, filtro AE habilitado, Reducción 1.50, Suavizado 0.85, Umbral 0.20.

## Pestaña NR4

Utilice el motor NR4 (libspecbleach) para la reducción de ruido centrada en el habla con estimación adaptativa de ruido. Esta pestaña está atenuada en las compilaciones de Windows compiladas sin clang-cl (LLVM).

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Estimación de ruido: | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Estimación adaptativa de ruido | Habilitado | — | `NR4AdaptiveNoise` |
| Reducción (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Profundidad de enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

### Restablecer valores predeterminados de NR4

1. Seleccione la pestaña **NR4**.
2. Haga clic en **Restablecer valores predeterminados** (icono ↺).

Todos los controles de NR4 vuelven a MMSE, Estimación adaptativa de ruido habilitada, Reducción 10.0 dB, Suavizado 0, Blanqueamiento 0, Profundidad de enmascaramiento 0.50, Supresión 0.50.

## Pestaña MNR (solo macOS)

Utilice el motor MNR (MMSE-Wiener de macOS) para la reducción de ruido con suavizado de ganancia asimétrico. Esta pestaña solo está disponible en compilaciones de macOS.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Habilitar MNR (solo macOS) | — | — | `MnrEnabled` |
| Intensidad | 100 | 0–100 | `MnrStrength` |

**Habilitar MNR** — Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine.
**Intensidad** — Ajusta la agresividad de MNR (0 suave, 100 máxima). Se conserva como valor normalizado de 0.00 a 1.00.

## Pestaña DFNR

Utilice el motor DeepFilterNet3 para la reducción de ruido basada en redes neuronales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Límite de atenuación | 100 | 0–100 dB | `DfnrAttenLimit` |
| Beta del postfiltro | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Límite de atenuación** — Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máxima.
**Beta del postfiltro** — Aplica un postfiltro adicional para una supresión extra. El control deslizante almacena el valor multiplicado por 100 internamente.

## Consejos

- **Restablecer valores predeterminados** afecta solo a la pestaña donde hace clic. Restablecer NR2 no altera la configuración de NR4, y viceversa.
- Los cambios surten efecto inmediatamente. Si un motor de reducción de ruido está activo en un slice de recepción en ese momento, escuchará que el comportamiento del motor cambia tan pronto como ajuste cualquier control.
- Los seis interruptores DSP actúan simultáneamente como selectores exclusivos y controles de activación/desactivación del motor. Activar un motor puede deshabilitar otros módulos mutuamente excluyentes.

## Relacionados

- [Ajustar la profundidad de reducción y el umbral de NR2](tune-nr2-reduction-depth-and-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
