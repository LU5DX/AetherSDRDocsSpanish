# Configuración de AetherDSP

Use el diálogo **Configuración de AetherDSP** para ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se seleccionan mediante una fila de botones en la parte superior; al hacer clic en un botón también se activa o se omite ese motor.

## Cómo abrir la Configuración de AetherDSP

1. Haga clic en `Settings > AetherDSP Settings...`.

El diálogo se abre con la pestaña de reducción de ruido actualmente activa seleccionada.

## Elementos del diálogo

El diálogo de Configuración de AetherDSP usa una barra de título sin marco con degradado de 18 px, un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo "AetherDSP Settings". Tres botones de control de ventana se encuentran a la derecha:

- **— (Minimizar)** — Minimiza el diálogo.
- **□ (Maximizar)** — Maximiza o restaura el diálogo. Al hacer doble clic en la barra de título también se alterna entre maximizar y restaurar.
- **× (Cerrar)** — Cierra el diálogo.

El diálogo tiene una zona de ajuste de tamaño de 6 px alrededor del widget de contenido interno. Arrastre la barra de título para mover el diálogo. Cambie el tamaño del diálogo arrastrando cualquier borde o esquina (redimensionamiento de 8 ejes). La geometría del diálogo se conserva entre sesiones bajo la clave de configuración `AetherDspDialogGeometry`.

El diálogo usa un estilo temático aplicado a través de `ThemeManager` en lugar de una hoja de estilo fija.

## Comportamiento del selector de pestañas

Las seis pestañas en la parte superior (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de pestaña como controles de activación/desactivación del motor. Al hacer clic en una pestaña se selecciona esa página y se activa el motor DSP correspondiente. Cuando se activa un nuevo motor, AetherSDR aplica una exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

Cada botón de selección tiene un nombre de objeto en el formato `dspMethodBtn` seguido del texto de la etiqueta (por ejemplo, `dspMethodBtnNR2`), y un nombre accesible que incluye la etiqueta y "método de reducción de ruido". Esto permite que los lectores de pantalla y las herramientas de automatización identifiquen cada botón.

El último método de reducción de ruido activo del lado del cliente se conserva bajo la clave de configuración `LastClientNr`. En compilaciones sin el backend DFNR, cualquier preferencia DFNR almacenada se borra automáticamente.

**Notas de plataforma:**

- **MNR (solo macOS)** — La pestaña MNR está atenuada en compilaciones de Windows y Linux porque el motor macOS MMSE-Wiener no tiene backend en esas plataformas.
- **BNR** — La pestaña BNR está atenuada en compilaciones sin el SDK de NVIDIA Broadcast.
- **DFNR** — La pestaña DFNR muestra una información sobre herramientas "DFNR requiere que DeepFilterNet esté configurado y que AetherSDR se reconstruya." en compilaciones sin el backend DFNR.
- **RN2** — La pestaña RN2 es puramente informativa y no tiene parámetros ajustables.

## Pestaña NR2

Use el motor NR2 (reducción de ruido musical) para la supresión de ruido que evita los artefactos musicales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Método de ganancia | Gamma | Lineal \| Log \| Gamma \| Entrenado | `NR2GainMethod` |
| Método NPE | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| Filtro AE (eliminación de artefactos) | Habilitado | — | `NR2AeFilter` |
| Reducción: | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Suavizado: | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Umbral: | 0.20 | 0.05–0.50 | `NR2Qspp` |

### Restablecer valores predeterminados de NR2

1. Seleccione la pestaña **NR2**.
2. Haga clic en **Reset Defaults** (icono ↺).

Todos los controles de NR2 vuelven a Gamma, OSMS, filtro AE habilitado, Reducción 1.50, Suavizado 0.85, Umbral 0.20.

## Pestaña NR4

Use el motor NR4 (libspecbleach) para la reducción de ruido centrada en el habla con estimación de ruido adaptativa.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Estimación de ruido: | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Estimación de ruido adaptativa | Habilitado | — | `NR4AdaptiveNoise` |
| Reducción (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Profundidad de enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

### Restablecer valores predeterminados de NR4

1. Seleccione la pestaña **NR4**.
2. Haga clic en **Reset Defaults** (icono ↺).

Todos los controles de NR4 vuelven a MMSE, Estimación de ruido adaptativa habilitada, Reducción 10.0 dB, Suavizado 0, Blanqueamiento 0, Profundidad de enmascaramiento 0.50, Supresión 0.50.

## Pestaña MNR (solo macOS)

Use el motor MNR (macOS MMSE-Wiener) para la reducción de ruido con suavizado de ganancia asimétrico. Esta pestaña solo está disponible en compilaciones de macOS.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Habilitar MNR (solo macOS) | — | — | `MnrEnabled` |
| Intensidad | 100 | 0–100 | `MnrStrength` |

**Habilitar MNR** — Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde el motor de audio.
**Intensidad** — Ajusta la agresividad de MNR (0 suave, 100 máxima). Se conserva como valor normalizado 0.00–1.00.

## Pestaña DFNR

Use el motor DeepFilterNet3 para la reducción de ruido basada en redes neuronales.

### Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Límite de atenuación | 100 | 0–100 dB | `DfnrAttenLimit` |
| Beta del post-filtro | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Límite de atenuación** — Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.
**Beta del post-filtro** — Aplica un post-filtro adicional para una supresión extra. El deslizador almacena el valor×100 internamente.

En compilaciones sin el backend DFNR, la pestaña DFNR muestra una información sobre herramientas: "DFNR requiere que DeepFilterNet esté configurado y que AetherSDR se reconstruya."

## Pestaña RN2

La pestaña RN2 (RNNoise) es puramente informativa y no tiene parámetros ajustables. Cuando RN2 está activo, utiliza un modelo de red neuronal para la supresión de ruido en tiempo real sin ajustes configurables por el usuario.

## Pestaña BNR

La pestaña BNR (NVIDIA Broadcast) usa el SDK de NVIDIA Broadcast para la reducción de ruido basada en IA. La intensidad se controla desde el menú superpuesto. La pestaña BNR está atenuada en compilaciones sin el SDK de NVIDIA Broadcast.

## Consejos

- **Reset Defaults** afecta solo a la pestaña en la que hace clic. Restablecer NR2 no altera la configuración de NR4, y viceversa.
- Los cambios surten efecto de inmediato. Si un motor de reducción de ruido está activo en una franja de recepción en ese momento, escuchará que el comportamiento del motor cambia tan pronto como ajuste cualquier control.
- Los seis botones DSP actúan como selectores exclusivos y controles de activación/desactivación del motor simultáneamente. Activar un motor puede desactivar otros módulos mutuamente excluyentes.
- Cuando AetherSDR se reinicia, restaura el último método de reducción de ruido del lado del cliente activo almacenado bajo la clave de configuración `LastClientNr`.

## Relacionados

- Ajustar la profundidad de reducción y el umbral de NR2
- [Cambiar el método de ganancia de NR2 entre Lineal, Log, Gamma y Entrenado](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
