# Configuración de AetherDSP

El cuadro de diálogo de Configuración de AetherDSP ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo al operador ajustar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o desvía ese motor.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El motor DSP debe estar activo en un receptor para que los cambios surtan efecto audible de inmediato.

## Abrir el cuadro de diálogo

1. Haga clic en `Settings > AetherDSP Settings...`.

El cuadro de diálogo aparece como una ventana sin bordes con una barra de título degradada. Recuerda su tamaño y posición entre sesiones.

## Resumen de controles del cuadro de diálogo

| Control | Descripción |
|---------|-------------|
| Barra de título | Barra de título degradada de 18 px sin bordes con un glifo de agarre (⋮⋮) a la izquierda y el título del cuadro de diálogo. |
| — (Minimizar) | Minimiza el cuadro de diálogo. |
| □ (Maximizar) | Maximiza o restaura el cuadro de diálogo. |
| × (Cerrar) | Cierra el cuadro de diálogo. |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic para alternar entre maximizar y restaurar. |
| Redimensionamiento de 8 ejes | Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. Zona de impacto de redimensionamiento de 6 px alrededor del widget de contenido interno. |

## Pestaña NR2

La pestaña NR2 controla el motor de reducción de ruido musical.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **NR2 (pestaña)** | Pestaña | — | — | Selecciona la página NR2. Al hacer clic en el botón de conmutación NR2 también se activa o desvía el motor NR2. |
| **Gain Method** | Botón de opción (Linear, Log, Gamma, Trained) | Gamma | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0-3. |
| **NPE Method** | Botón de opción (OSMS, MMSE, NSTAT) | OSMS | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2. |
| **AE Filter (artifact elimination)** | Casilla de verificación | Verdadero | `NR2AeFilter` | Activa o desactiva el post-filtro anti-artefactos. |
| **Reduction:** | Deslizador, 0.50–2.00 | 1.50 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. El deslizador almacena el valor*100 internamente. |
| **Gain Floor:** | Deslizador, 0.00–1.00 | 0.00 | `NR2GainFloor` | Establece el piso de ganancia mínimo aplicado por NR2. Los valores más altos preservan más ruido ambiental. Añadido en v26.7.4. |
| **Smoothing:** | Deslizador, 0.50–0.98 | 0.85 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. |
| **Threshold:** | Deslizador, 0.05–0.50 | 0.20 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |
| **Use Original Geometry** | Casilla de verificación | Falso | `NR2UseOriginalGeometry` | Cuando está habilitado, NR2 utiliza la geometría espectral original (anterior a v26.7.4) para la estimación de ruido. Deshabilitado utiliza la geometría revisada para una mejor supresión de ruido musical. |
| Restablecer valores predeterminados (icono ↺) | Botón pulsador | — | — | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activado, 1.50/0.00/0.85/0.20, Use Original Geometry desactivado). |

### Cambiar el método NPE

1. Haga clic en la pestaña **NR2**.
2. En el grupo **NPE Method**, seleccione uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR2NpeMethod`.

### Ajustar el piso de ganancia (Gain Floor)

El deslizador **Gain Floor** (0.00–1.00, valor predeterminado 0.00) establece la ganancia mínima aplicada por el motor NR2. Un valor de 0.00 permite que el motor atenúe completamente el ruido cuando la probabilidad de presencia de voz es baja. Los valores más altos preservan más ruido ambiental, lo que puede reducir el sonido "falto" o "subacuático" que algunos operadores experimentan con una reducción de ruido agresiva.

1. Haga clic en la pestaña **NR2**.
2. Arrastre el deslizador **Gain Floor:** al nivel deseado.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR2GainFloor`.

### Usar la geometría espectral original

La casilla de verificación **Use Original Geometry** (valor predeterminado: desactivado) controla si NR2 utiliza la geometría espectral revisada introducida en v26.7.4 (desactivado) o la geometría original anterior a v26.7.4 (activado). La geometría revisada mejora la supresión de artefactos de ruido musical. Si prefiere el comportamiento anterior, habilite esta opción.

1. Haga clic en la pestaña **NR2**.
2. Marque o desmarque **Use Original Geometry**.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR2UseOriginalGeometry`.

## Pestaña NR4

La pestaña NR4 controla el motor de reducción de ruido libspecbleach.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **NR4 (pestaña)** | Pestaña | — | — | Selecciona la página NR4. |
| **Noise Estimation:** | Botón de opción (MMSE, Brandt, Martin) | MMSE | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido. Se almacena como entero 0-2. |
| **Adaptive Noise Estimation** | Casilla de verificación | Verdadero | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| **Reduction (dB):** | Deslizador, 0.0–40.0 | 10.0 | `NR4ReductionAmount` | Establece la reducción máxima en dB. El deslizador almacena el valor*10. |
| **Smoothing (%):** | Deslizador, 0–100 | 0 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido. |
| **Whitening (%):** | Deslizador, 0–100 | 0 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| **Masking Depth:** | Deslizador, 0.00–1.00 | 0.50 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| **Suppression:** | Deslizador, 0.00–1.00 | 0.50 | `NR4SuppressionStrength` | Fuerza de supresión general. |
| Restablecer valores predeterminados (icono ↺) | Botón pulsador | — | — | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50). |

## Pestaña MNR (solo macOS)

La pestaña MNR controla el motor de reducción de ruido MMSE-Wiener de macOS. El conmutador MNR aparece atenuado en las compilaciones de Windows/Linux: el motor no tiene backend en esas plataformas.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **MNR (pestaña)** | Pestaña | — | — | Selecciona la página MNR. |
| **Enable MNR (macOS only)** | Casilla de verificación | Leer en vivo de AudioEngine | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. |
| **Strength** | Deslizador, 0–100 | 100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se conserva como valor normalizado 0.00-1.00. |

## Pestaña RN2 (informativa)

La pestaña RN2 muestra la página de RNNoise. Es puramente informativa y no tiene parámetros ajustables. El motor RN2 se habilita mediante el botón de conmutación en la parte superior del cuadro de diálogo.

## Pestaña BNR (NVIDIA)

La pestaña BNR controla el motor de reducción de ruido NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto. El conmutador BNR aparece atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.

## Pestaña DFNR

La pestaña DFNR controla el motor de reducción de ruido DeepFilterNet3. El conmutador DFNR aparece atenuado en las compilaciones sin soporte para DeepFilterNet.

### Controles

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|------|---------|-------------|----------|
| **DFNR (pestaña)** | Pestaña | — | — | Selecciona la página de DeepFilterNet3. |
| **Attenuation Limit** | Deslizador, 0–100 dB | 100 | `DfnrAttenLimit` | Establece la atenuación máxima de ruido. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | Deslizador, 0.00–0.30 | 0.00 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para una supresión extra. El deslizador almacena el valor*100 internamente. |

## Notas

- Los seis conmutadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de activación/desactivación del motor. Cuando se activa NR2, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.
- El cuadro de diálogo utiliza `PersistentDialog`, que guarda y restaura automáticamente su geometría entre sesiones. La posición y el tamaño del cuadro de diálogo se conservan mediante la clave de configuración `AetherDspDialogGeometry`.
- Todos los deslizadores de este cuadro de diálogo utilizan el estilo de deslizador principal personalizable, adaptándose al tema de color actual.
- El último método de reducción de ruido del lado del cliente activo se recuerda entre sesiones mediante la configuración `LastClientNr`. Si DFNR fue el último activo pero DeepFilterNet no está disponible, la preferencia se borra automáticamente.

## Consejos

- NR2: OSMS funciona bien para ruido de fondo constante como silbido atmosférico o ruido blanco. NSTAT es mejor para pisos de ruido que cambian rápidamente.
- NR2: Si cambiar el método NPE introduce más artefactos de ruido musical, habilite **AE Filter (artifact elimination)**.
- NR2: Si la reducción de ruido suena demasiado agresiva o "falta", aumente ligeramente **Gain Floor:** (p. ej., 0.05–0.10) para retener algo de ruido ambiental.
- NR2: Desactive **Use Original Geometry** (el valor predeterminado) a menos que necesite específicamente el comportamiento anterior a v26.7.4.
- NR4: La estimación de ruido adaptativa ayuda a rastrear las condiciones cambiantes de ruido. Desactívela si el piso de ruido es estable.
- DFNR: Post-Filter Beta añade supresión extra pero puede introducir artefactos con valores más altos.
- Haga clic en el botón Restablecer valores predeterminados (↺) en cualquier pestaña para devolver todos los parámetros de esa pestaña a sus valores predeterminados de fábrica.

## Solución de problemas

- **Cambiar parámetros no produce diferencia audible** — Confirme que el motor DSP está habilitado en el receptor. El cuadro de diálogo de Configuración de AetherDSP ajusta los parámetros pero no activa el motor por sí mismo; el motor debe activarse desde los controles del receptor.
- **La pestaña MNR está atenuada o no disponible** — MNR solo está disponible en macOS. Las compilaciones de Windows y Linux no incluyen el backend de MNR.
- **La pestaña BNR está atenuada** — El SDK de NVIDIA Broadcast no está instalado en este sistema.
- **La pestaña DFNR está atenuada** — DeepFilterNet no está disponible en esta compilación. Recompile AetherSDR con soporte para DeepFilterNet para habilitar DFNR.
- **El deslizador Gain Floor no aparece** — Está ejecutando una versión anterior a v26.7.4. Actualice a la última versión.

## Relacionados

- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
