# Configuración de AetherDSP

Utilice el diálogo **AetherDSP Settings** para ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR). Los seis módulos DSP se pueden seleccionar mediante una fila de botones en la parte superior; al hacer clic en un botón también se activa o se omite ese motor.

## Abrir AetherDSP Settings

1. Haga clic en `Settings > AetherDSP Settings...`.

El diálogo se abre con la pestaña de reducción de ruido actualmente activa seleccionada.

## Marco del diálogo

El diálogo AetherDSP Settings utiliza una barra de título degradada sin marco de 18 px con un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo "AetherDSP Settings". Tres botones de control de ventana se encuentran a la derecha:

- **— (Minimizar)** — Minimiza el diálogo.
- **□ (Maximizar)** — Maximiza o restaura el diálogo. Al hacer doble clic en la barra de título también se alterna entre maximizar/restaurar.
- **× (Cerrar)** — Cierra el diálogo.

El diálogo tiene una zona de ajuste de tamaño de 6 px alrededor del widget de contenido interno. Arrastre la barra de título para mover el diálogo. Cambie el tamaño del diálogo arrastrando cualquier borde o esquina (ajuste de tamaño en 8 ejes). La geometría del diálogo se conserva entre sesiones bajo la clave de configuración `AetherDspDialogGeometry`.

El diálogo utiliza un estilo temático aplicado a través de `ThemeManager` en lugar de una hoja de estilos fija.

## Comportamiento del selector de pestañas

Las seis pestañas en la parte superior (NR2, NR4, MNR, DFNR, RN2, BNR) funcionan tanto como selectores de pestañas como controles de activación/desactivación del motor. Al hacer clic en una pestaña se selecciona esa página y se activa el motor DSP correspondiente. Cuando se activa un nuevo motor, AetherSDR aplica la exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

Cada botón de alternancia tiene un nombre de objeto con el formato `dspMethodBtn` seguido del texto de la etiqueta (por ejemplo, `dspMethodBtnNR2`), y un nombre accesible que incluye la etiqueta y "método de reducción de ruido". Esto permite que los lectores de pantalla y las herramientas de automatización identifiquen cada botón.

El último método de reducción de ruido del lado del cliente activo se conserva bajo la clave de configuración `LastClientNr`. En las compilaciones sin el backend de DFNR, cualquier preferencia de DFNR almacenada se borra automáticamente.

**Notas de plataforma:**

- **MNR (solo macOS)** — La pestaña MNR está atenuada en las compilaciones de Windows y Linux porque el motor MMSE-Wiener de macOS no tiene backend en esas plataformas.
- **BNR** — La pestaña BNR está atenuada en las compilaciones sin el SDK de NVIDIA Broadcast.
- **DFNR** — La pestaña DFNR muestra una información sobre herramientas "DFNR requires DeepFilterNet to be set up and AetherSDR rebuilt." en las compilaciones sin el backend de DFNR.

## Pestaña NR2

Utilice el motor NR2 (reducción de ruido musical) para la supresión de ruido que evita los artefactos musicales.

### Controles

| Control                          | Predeterminado | Rango válido | Clave de configuración |
|----------------------------------|---------|-------------|---------------------|
| Método de ganancia               | Gamma   | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| Método NPE                       | OSMS    | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| Filtro AE (eliminación de artefactos) | Activado | —           | `NR2AeFilter`       |
| Reducción:                       | 1.50    | 0.50–2.00   | `NR2GainMax`        |
| Suavizado:                       | 0.85    | 0.50–0.98   | `NR2GainSmooth`     |
| Umbral:                          | 0.20    | 0.05–0.50   | `NR2Qspp`           |

**Método de ganancia** — Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0–3 que coincide con el orden anterior.
**Método NPE** — Selecciona el estimador de potencia de ruido. Se almacena como entero 0–2.
**Filtro AE** — Activa el post-filtro anti-artefactos.
**Reducción:** — Establece la profundidad máxima de reducción de NR2. El control deslizante almacena el valor×100 internamente.
**Suavizado:** — Controla con qué suavidad la estimación de ruido sigue los cambios.
**Umbral:** — Establece el umbral de probabilidad de presencia de voz.

### Restablecer valores predeterminados de NR2

1. Seleccione la pestaña **NR2**.
2. Haga clic en **Reset Defaults** (icono ↺).

Todos los controles de NR2 vuelven a Gamma, OSMS, filtro AE activado, Reducción 1.50, Suavizado 0.85, Umbral 0.20.

## Pestaña NR4

Utilice el motor NR4 (libspecbleach) para la reducción de ruido centrada en la voz con estimación de ruido adaptativa.

### Controles

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Estimación de ruido: | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Estimación de ruido adaptativa | Activado | — | `NR4AdaptiveNoise` |
| Reducción (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Suavizado (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Blanqueamiento (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Profundidad de enmascaramiento: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Supresión: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

**Estimación de ruido:** — Selecciona el estimador de piso de ruido utilizado por NR4. Se almacena como entero 0–2.
**Estimación de ruido adaptativa** — Activa la reestimación continua del piso de ruido.
**Reducción (dB):** — Establece la reducción máxima de ruido de NR4 en dB. El control deslizante almacena el valor×10.
**Suavizado (%):** — Suavizado en el dominio del tiempo de la estimación de ruido de NR4.
**Blanqueamiento (%):** — Aplana la forma espectral del ruido residual.
**Profundidad de enmascaramiento:** — Controla la profundidad del enmascaramiento espectral.
**Supresión:** — Fuerza general de supresión de NR4.

### Restablecer valores predeterminados de NR4

1. Seleccione la pestaña **NR4**.
2. Haga clic en **Reset Defaults** (icono ↺).

Todos los controles de NR4 vuelven a MMSE, Estimación de ruido adaptativa activada, Reducción 10.0 dB, Suavizado 0, Blanqueamiento 0, Profundidad de enmascaramiento 0.50, Supresión 0.50.

## Pestaña MNR (solo macOS)

Utilice el motor MNR (MMSE-Wiener de macOS) para la reducción de ruido con suavizado de ganancia asimétrico. Esta pestaña solo está disponible en las compilaciones de macOS.

### Controles

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Activar MNR (solo macOS) | — | — | `MnrEnabled` |
| Intensidad | 100 | 0–100 | `MnrStrength` |

**Activar MNR** — Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine.
**Intensidad** — Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva como valor normalizado 0.00–1.00.

### Restablecer valores predeterminados de MNR

1. Seleccione la pestaña **MNR**.
2. Haga clic en **Reset Defaults** (icono ↺).

El control deslizante de Intensidad vuelve a 100.

## Pestaña DFNR

Utilice el motor DeepFilterNet3 para la reducción de ruido basada en redes neuronales.

### Controles

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Límite de atenuación | 100 | 0–100 dB | `DfnrAttenLimit` |
| Beta del post-filtro | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Límite de atenuación** — Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.
**Beta del post-filtro** — Aplica un post-filtro adicional para una mayor supresión. El control deslizante almacena el valor×100 internamente.

### Restablecer valores predeterminados de DFNR

1. Seleccione la pestaña **DFNR**.
2. Haga clic en **Reset Defaults** (icono ↺).

El Límite de atenuación vuelve a 100 y la Beta del post-filtro vuelve a 0.00.

En las compilaciones sin el backend de DFNR, la pestaña DFNR muestra una información sobre herramientas: "DFNR requires DeepFilterNet to be set up and AetherSDR rebuilt."

## Pestaña RN2

Utilice el motor RN2 (RNNoise) para la supresión de ruido en tiempo real basada en redes neuronales.

### Controles

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Piso de ruido (mezcla seca de RN2) | 0 | 0–100 | — |

**Piso de ruido (mezcla seca de RN2)** — Establece el porcentaje de la señal original que RN2 deja bajo el audio con reducción de ruido. Cero produce una supresión total (silencio entre frases); 10–20% mantiene un piso de quietud constante para que el receptor siga sonando vivo. Afecta solo al audio recibido; el eliminador de ruido de transmisión no cambia. Se conserva mediante Rn2SettingsModel y se expone a la cadena DSP a través de la señal `rn2DryMixChanged` de AetherDspWidget.

### Restablecer valores predeterminados de RN2

1. Seleccione la pestaña **RN2**.
2. Haga clic en **Reset Defaults** (icono ↺).

El control deslizante de Piso de ruido vuelve a 0.

## Pestaña BNR

La pestaña BNR (NVIDIA Broadcast) utiliza el SDK de NVIDIA Broadcast para la reducción de ruido basada en IA. La intensidad se controla desde el menú superpuesto. La pestaña BNR está atenuada en las compilaciones sin el SDK de NVIDIA Broadcast. Esta pestaña no tiene parámetros ajustables, por lo que **Reset Defaults** no hace nada.

## Consejos

- **Reset Defaults** afecta solo a la pestaña en la que hace clic. Restablecer NR2 no altera la configuración de NR4, y viceversa.
- Los cambios surten efecto de inmediato. Si un motor de reducción de ruido está activo en un slice de recepción en ese momento, escuchará el cambio de comportamiento del motor tan pronto como ajuste cualquier control.
- Los seis botones DSP funcionan simultáneamente como selectores exclusivos y controles de activación/desactivación del motor. Activar un motor puede desactivar otros módulos mutuamente excluyentes.
- Cuando AetherSDR se reinicia, restaura el último método de reducción de ruido del lado del cliente activo almacenado bajo la clave de configuración `LastClientNr`.
- Para RN2, establecer el Piso de ruido en 10–20% mantiene un piso de quietud constante para que el receptor siga sonando vivo entre frases, mientras que 0% produce una supresión total.

## Relacionados

- Ajuste la profundidad de reducción y el umbral de NR2
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Establecer la mezcla seca del piso de ruido de RN2](set-rn2-noise-floor-dry-mix.md)
