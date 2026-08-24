# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo al operador ajustar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o se omite ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El motor DSP debe estar activo en un receptor para que los cambios surtan efecto audible de inmediato.

## Abrir el diálogo

1. Haga clic en `Settings > AetherDSP Settings...`.

El diálogo aparece como una ventana sin marco con una barra de título degradada. Recuerda su tamaño y posición entre sesiones.

## Descripción general de los controles del diálogo

| Control | Descripción | Notas |
|---------|-------------|-------|
| Barra de título | Barra de título degradada sin marco de 18 px con un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. | Coincide con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip. Añadido en v0.9.8 (refacción #2425). |
| — (Minimizar) | Minimiza el diálogo. | |
| □ (Maximizar) | Maximiza o restaura el diálogo. | |
| × (Cerrar) | Cierra el diálogo. | |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Doble clic para alternar maximizar/restaurar. | |
| Redimensionar en 8 ejes | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. Zona de redimensionamiento de 6 px alrededor del widget de contenido interno. | |
| Noise Floor (mezcla seca RN2) | Establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce supresión total (silencio entre frases); 10-20% mantiene un piso silencioso constante para que el receptor siga sonando vivo. | Afecta solo al audio recibido; el denoizador de transmisión no cambia. Persistido por Rn2SettingsModel y expuesto a la cadena DSP mediante la señal rn2DryMixChanged de AetherDspWidget. Nuevo en v26.8.4. |

## Pestaña NR2

La pestaña NR2 controla el motor de reducción de ruido musical.

### Controles

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---------|------|----------------|------------------------|----------------|
| **NR2 (pestaña)** | Pestaña | — | — | Selecciona la página NR2. Al hacer clic en el botón conmutador NR2 también se activa o se omite el motor NR2. |
| **Gain Method** | Botón de opción (Linear, Log, Gamma, Trained) | Gamma | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0-3. |
| **NPE Method** | Botón de opción (OSMS, MMSE, NSTAT) | OSMS | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| **AE Filter (eliminación de artefactos)** | Casilla de verificación | True | `NR2AeFilter` | Activa el postfiltro antiartefactos. |
| **Reduction:** | Deslizador, 0.50–2.00 | 1.50 | `NR2GainMax` | Establece la profundidad máxima de reducción de NR2. El deslizador almacena valor*100 internamente. |
| **Gain Floor:** | Deslizador, 0.00–1.00 | 0.00 | `NR2GainFloor` | Establece el piso de ganancia mínimo aplicado por NR2. Los valores más altos preservan más ruido ambiente. Añadido en v26.7.4. |
| **Smoothing:** | Deslizador, 0.50–0.98 | 0.85 | `NR2GainSmooth` | Controla con qué suavidad la estimación de ruido sigue los cambios. |
| **Threshold:** | Deslizador, 0.05–0.50 | 0.20 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de habla. |
| Restablecer valores (icono ↺) | Botón pulsador | — | — | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activado, 1.50/0.00/0.85/0.20). |

### Cambiar el método NPE

1. Haga clic en la pestaña **NR2**.
2. En el grupo **NPE Method**, seleccione uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR2NpeMethod`.

### Ajustar el Gain Floor

El deslizador **Gain Floor** (0.00–1.00, predeterminado 0.00) establece la ganancia mínima aplicada por el motor NR2. Un valor de 0.00 permite que el motor atenúe completamente el ruido cuando la probabilidad de presencia de habla es baja. Los valores más altos preservan más ruido ambiente, lo que puede reducir el sonido "deficiente" o "subacuático" que algunos operadores experimentan con la reducción de ruido agresiva.

1. Haga clic en la pestaña **NR2**.
2. Arrastre el deslizador **Gain Floor:** al nivel deseado.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR2GainFloor`.

## Pestaña NR4

La pestaña NR4 controla el motor de reducción de ruido libspecbleach.

### Controles

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---------|------|----------------|------------------------|----------------|
| **NR4 (pestaña)** | Pestaña | — | — | Selecciona la página NR4. |
| **Noise Estimation:** | Botón de opción (MMSE, Brandt, Martin) | MMSE | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2. |
| **Adaptive Noise Estimation** | Casilla de verificación | True | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| **Reduction (dB):** | Deslizador, 0.0–40.0 | 10.0 | `NR4ReductionAmount` | Establece la reducción máxima en dB. El deslizador almacena valor*10. |
| **Smoothing (%):** | Deslizador, 0–100 | 0 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido. |
| **Whitening (%):** | Deslizador, 0–100 | 0 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| **Masking Depth:** | Deslizador, 0.00–1.00 | 0.50 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| **Suppression:** | Deslizador, 0.00–1.00 | 0.50 | `NR4SuppressionStrength` | Fuerza general de supresión. |
| Restablecer valores (icono ↺) | Botón pulsador | — | — | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50). |

## Pestaña MNR (solo macOS)

La pestaña MNR controla el motor de reducción de ruido MMSE-Wiener de macOS. El conmutador MNR está atenuado en las compilaciones para Windows/Linux: el motor no tiene backend en esas plataformas.

### Controles

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---------|------|----------------|------------------------|----------------|
| **MNR (pestaña)** | Pestaña | — | — | Selecciona la página MNR. |
| **Enable MNR (solo macOS)** | Casilla de verificación | Leído en vivo desde AudioEngine | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. |
| **Strength** | Deslizador, 0–100 | 100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se persiste como valor normalizado 0.00-1.00. |

## Pestaña RN2

La pestaña RN2 controla el motor RNNoise. Alberga el deslizador de mezcla seca Noise Floor. El motor RN2 se habilita mediante el botón conmutador en la parte superior del diálogo.

### Controles

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---------|------|----------------|------------------------|----------------|
| **RN2 (pestaña)** | Pestaña | — | — | Selecciona la página RN2. |
| **Noise Floor (mezcla seca RN2)** | Deslizador, 0–100 | 0 | — | Establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce supresión total (silencio entre frases); 10-20% mantiene un piso silencioso constante para que el receptor siga sonando vivo. Persistido por Rn2SettingsModel y expuesto a la cadena DSP mediante la señal rn2DryMixChanged de AetherDspWidget. Nuevo en v26.8.4. |

### Ajustar el Noise Floor

El deslizador **Noise Floor** (0–100, predeterminado 0) establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Un valor de 0 produce supresión total, lo que puede generar silencio entre frases. Un valor de 10–20% mantiene un piso silencioso constante para que el receptor siga sonando vivo.

1. Haga clic en la pestaña **RN2**.
2. Arrastre el deslizador **Noise Floor** al nivel deseado.

La configuración surte efecto de inmediato y es persistida por Rn2SettingsModel.

## Pestaña BNR (NVIDIA)

La pestaña BNR controla el motor de reducción de ruido NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto. El conmutador BNR está atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.

## Pestaña DFNR

La pestaña DFNR controla el motor de reducción de ruido DeepFilterNet3. El conmutador DFNR está atenuado en las compilaciones sin soporte de DeepFilterNet.

### Controles

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---------|------|----------------|------------------------|----------------|
| **DFNR (pestaña)** | Pestaña | — | — | Selecciona la página DeepFilterNet3. |
| **Attenuation Limit** | Deslizador, 0–100 dB | 100 | `DfnrAttenLimit` | Establece la atenuación máxima del ruido. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | Deslizador, 0.00–0.30 | 0.00 | `DfnrPostFilterBeta` | Aplica un postfiltro adicional para mayor supresión. El deslizador almacena valor*100 internamente. |

## Notas

- Los seis conmutadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de habilitación/deshabilitación del motor. Cuando se activa NR2, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.
- El diálogo utiliza `PersistentDialog`, que guarda y restaura automáticamente su geometría entre sesiones. La posición y el tamaño del diálogo se persisten mediante la clave de configuración `AetherDspDialogGeometry`.
- Todos los deslizadores de este diálogo utilizan el estilo de deslizador principal personalizable, adaptándose al tema de color actual.
- El último método de reducción de ruido del lado del cliente activo se recuerda entre sesiones mediante la configuración `LastClientNr`. Si DFNR fue el último activo pero DeepFilterNet no está disponible, la preferencia se borra automáticamente.

## Consejos

- NR2: OSMS funciona bien para ruido de fondo constante, como silbido atmosférico o ruido blanco. NSTAT es mejor para pisos de ruido que cambian rápidamente.
- NR2: Si cambiar el método NPE introduce más artefactos de ruido musical, active **AE Filter (eliminación de artefactos)**.
- NR2: Si la reducción de ruido suena demasiado agresiva o "deficiente", aumente ligeramente **Gain Floor:** (p. ej., 0.05–0.10) para conservar algo de ruido ambiente.
- NR4: La estimación de ruido adaptativa ayuda a seguir condiciones de ruido cambiantes. Desactívela si el piso de ruido es estable.
- RN2: Establezca el deslizador **Noise Floor** en 10–20% para mantener el receptor sonando vivo mientras aún suprime el ruido entre frases.
- DFNR: Post-Filter Beta añade supresión adicional, pero puede introducir artefactos en valores más altos.
- Haga clic en el botón Restablecer valores (↺) en cualquier pestaña para devolver todos los parámetros de esa pestaña a sus valores de fábrica.

## Solución de problemas

- **Cambiar parámetros no produce diferencia audible** — Confirme que el motor DSP está habilitado en el receptor. El diálogo de Configuración de AetherDSP ajusta parámetros pero no activa el motor por sí mismo; el motor debe activarse desde los controles del receptor.
- **La pestaña MNR está atenuada o no disponible** — MNR solo está disponible en macOS. Las compilaciones para Windows y Linux no incluyen el backend de MNR.
- **La pestaña BNR está atenuada** — El SDK de NVIDIA Broadcast no está instalado en este sistema.
- **La pestaña DFNR está atenuada** — DeepFilterNet no está disponible en esta compilación. Recompile AetherSDR con soporte de DeepFilterNet para habilitar DFNR.
- **El deslizador Gain Floor no aparece** — Está ejecutando una versión anterior a v26.7.4. Actualice a la última versión.
- **El deslizador Noise Floor no aparece en la pestaña RN2** — Está ejecutando una versión anterior a v26.8.4. Actualice a la última versión.

## Relacionado

- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción de NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
