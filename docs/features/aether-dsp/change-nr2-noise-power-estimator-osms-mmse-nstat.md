# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP permite ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), lo que permite al operador ajustar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de botones de alternancia en la parte superior; al hacer clic en un botón de alternancia también se activa o desvía ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El motor DSP debe estar activo en un receptor para que los cambios tengan efecto audible de inmediato.

## Cómo abrir el diálogo

1. Haga clic en `Settings > AetherDSP Settings...`.

El diálogo aparece como una ventana sin marco con una barra de título degradada. Recuerda su tamaño y posición entre sesiones.

## Descripción general de los controles del diálogo

| Control | Descripción |
|---------|-------------|
| Barra de título | Barra de título degradada sin marco de 18 px con un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. |
| — (Minimizar) | Minimiza el diálogo. |
| □ (Maximizar) | Maximiza o restaura el diálogo. |
| × (Cerrar) | Cierra el diálogo. |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar entre maximizar y restaurar. |
| Redimensión de 8 ejes | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensión. Zona de clic para redimensionar de 6 px alrededor del widget de contenido interno. |

## Pestaña NR2

La pestaña NR2 controla el motor de reducción de ruido musical.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **NR2 (pestaña)** | Pestaña | — | — | Selecciona la página NR2. Al hacer clic en el botón de alternancia NR2 también se activa o desvía el motor NR2. |
| **Gain Method** | Botón de opción (Linear, Log, Gamma, Trained) | Gamma | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como un entero 0-3. |
| **NPE Method** | Botón de opción (OSMS, MMSE, NSTAT) | OSMS | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como un entero 0-2. |
| **AE Filter (artifact elimination)** | Casilla de verificación | True | `NR2AeFilter` | Activa o desactiva el filtro posterior contra artefactos. |
| **Reduction:** | Deslizador, 0.50–2.00 | 1.50 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El deslizador almacena el valor*100 internamente. |
| **Smoothing:** | Deslizador, 0.50–0.98 | 0.85 | `NR2GainSmooth` | Controla qué tan suavemente el estimado de ruido sigue los cambios. |
| **Threshold:** | Deslizador, 0.05–0.50 | 0.20 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de habla. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20). |

### Cambio del método NPE

1. Haga clic en la pestaña **NR2**.
2. En el grupo **NPE Method**, seleccione uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR2NpeMethod`.

## Pestaña NR4

La pestaña NR4 controla el motor de reducción de ruido libspecbleach.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **NR4 (pestaña)** | Pestaña | — | — | Selecciona la página NR4. |
| **Noise Estimation:** | Botón de opción (MMSE, Brandt, Martin) | MMSE | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como un entero 0-2. |
| **Adaptive Noise Estimation** | Casilla de verificación | True | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| **Reduction (dB):** | Deslizador, 0.0–40.0 | 10.0 | `NR4ReductionAmount` | Establece la reducción máxima en dB. El deslizador almacena el valor*10. |
| **Smoothing (%):** | Deslizador, 0–100 | 0 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo del estimado de ruido. |
| **Whitening (%):** | Deslizador, 0–100 | 0 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| **Masking Depth:** | Deslizador, 0.00–1.00 | 0.50 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| **Suppression:** | Deslizador, 0.00–1.00 | 0.50 | `NR4SuppressionStrength` | Fuerza de supresión general. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50). |

## Pestaña MNR (solo macOS)

La pestaña MNR controla el motor de reducción de ruido MMSE-Wiener de macOS. El botón de alternancia MNR aparece atenuado en las compilaciones de Windows/Linux; el motor no tiene backend en esas plataformas.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **MNR (pestaña)** | Pestaña | — | — | Selecciona la página MNR. |
| **Enable MNR (macOS only)** | Casilla de verificación | Se lee en vivo desde AudioEngine | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. |
| **Strength** | Deslizador, 0–100 | 100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva como valor normalizado 0.00-1.00. |

## Pestaña RN2 (informativa)

La pestaña RN2 muestra la página de RNNoise. Es puramente informativa y no tiene parámetros ajustables. El motor RN2 se habilita mediante el botón de alternancia en la parte superior del diálogo.

## Pestaña BNR (NVIDIA)

La pestaña BNR controla el motor de reducción de ruido NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto. El botón de alternancia BNR aparece atenuado en compilaciones sin el SDK de NVIDIA Broadcast.

## Pestaña DFNR

La pestaña DFNR controla el motor de reducción de ruido DeepFilterNet3.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **DFNR (pestaña)** | Pestaña | — | — | Selecciona la página de DeepFilterNet3. |
| **Attenuation Limit** | Deslizador, 0–100 dB | 100 | `DfnrAttenLimit` | Establece la atenuación máxima del ruido. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | Deslizador, 0.00–0.30 | 0.00 | `DfnrPostFilterBeta` | Aplica un filtro posterior adicional para una supresión extra. El deslizador almacena el valor*100 internamente. |

## Notas

- Los seis botones de alternancia DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de habilitación/deshabilitación del motor. Cuando se activa NR2, AudioEngine ejecuta una exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.
- El diálogo utiliza `PersistentDialog`, que guarda y restaura automáticamente su geometría entre sesiones. La posición y el tamaño del diálogo se conservan mediante la clave de configuración `AetherDspDialogGeometry`.
- Todos los deslizadores de este diálogo utilizan el estilo de deslizador primario adaptable al tema, adaptándose al tema de color actual.

## Consejos

- NR2: OSMS funciona bien para ruido de fondo constante, como silbido atmosférico o ruido blanco. NSTAT es mejor para pisos de ruido que cambian rápidamente.
- NR2: Si cambiar el método NPE introduce más artefactos de ruido musical, active **AE Filter (artifact elimination)**.
- NR4: La estimación adaptativa de ruido ayuda a rastrear condiciones de ruido cambiantes. Desactívela si el piso de ruido es estable.
- DFNR: Post-Filter Beta añade supresión adicional, pero puede introducir artefactos en valores más altos.
- Haga clic en el botón Reset Defaults (↺) en cualquier pestaña para restaurar todos los parámetros de esa pestaña a sus valores predeterminados de fábrica.

## Solución de problemas

- **Cambiar parámetros no produce diferencia audible** — Confirme que el motor DSP está habilitado en el receptor. El diálogo de Configuración de AetherDSP ajusta los parámetros, pero no activa el motor por sí mismo; el motor debe activarse desde los controles del receptor.
- **La pestaña MNR está atenuada o no disponible** — MNR solo está disponible en macOS. Las compilaciones de Windows y Linux no incluyen el backend de MNR.
- **La pestaña BNR está atenuada** — El SDK de NVIDIA Broadcast no está instalado en este sistema.

## Relacionados

- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
