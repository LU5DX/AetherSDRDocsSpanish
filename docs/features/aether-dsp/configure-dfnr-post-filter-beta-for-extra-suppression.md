# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP proporciona control avanzado sobre los seis motores de reducción de ruido del lado del cliente en AetherSDR: NR2, NR4, DFNR, MNR, RN2 y BNR. Cada motor se selecciona mediante una fila de alternancia en la parte superior del diálogo; al hacer clic en una alternancia también se activa o se omite dicho motor.

## Abrir la Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.
2. El diálogo se abre con una barra de título sin marco de forma predeterminada.
3. El diálogo puede abrirse sin conexión de radio, pero el efecto solo es audible durante la recepción en vivo.

## Diseño del diálogo y controles de ventana

El diálogo de Configuración de AetherDSP utiliza un marco personalizado que coincide con NetworkDiagnosticsDialog y AetherialAudioStrip:

| Control                   | Descripción                                                                                                                                                                                                  | Notas                                                                                                                                                                      |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Barra de título**       | Barra de título degradada de 18 px con glifo de agarre (⋮⋮) a la izquierda y título del diálogo. Agregado en v0.9.8 (#2425 refit).                                                                           |                                                                                                                                                                            |
| **— (Minimizar)**         | Minimiza el diálogo.                                                                                                                                                                                         |                                                                                                                                                                            |
| **□ (Maximizar)**         | Maximiza o restaura el diálogo. Hacer doble clic en la barra de título también alterna maximizar/restaurar.                                                                                                  |                                                                                                                                                                            |
| **× (Cerrar)**            | Cierra el diálogo.                                                                                                                                                                                           |                                                                                                                                                                            |
| **Arrastrar para mover**  | Haga clic y arrastre la barra de título para mover el diálogo.                                                                                                                                               |                                                                                                                                                                            |
| **Redimensionar en 8 ejes** | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección del redimensionamiento. Zona de redimensionamiento de 6 px alrededor del widget de contenido interno. |                                                                                                                                                                            |
| Noise Floor (RN2 dry mix) | Establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce supresión total (silencio entre frases); 10-20% mantiene un piso silencioso estable para que el receptor siga sonando vivo. | Afecta solo al audio recibido; el denoizador de transmisión no cambia. Lo conserva Rn2SettingsModel y se expone a la cadena DSP mediante la señal `rn2DryMixChanged` de AetherDspWidget. |

El diálogo utiliza `PersistentDialog` con la geometría almacenada en la configuración `AetherDspDialogGeometry`. La posición y el tamaño se restauran automáticamente cuando se vuelve a abrir el diálogo.

El fondo del diálogo, los colores de la barra de título y el estilo de los controles deslizantes utilizan tokens de tema del tema activo. Los controles deslizantes ahora usan `applyPrimarySliderStyle()` en lugar de hojas de estilo en línea codificadas, lo que hace que respeten el esquema de color elegido por el usuario.

## Seleccionar y activar motores de reducción de ruido

Las seis alternancias DSP (NR2, NR4, MNR, DFNR, RN2, BNR) funcionan tanto como selectores de pestaña exclusivos como controles de habilitación/deshabilitación del motor. Haga clic en una alternancia para seleccionar su página de configuración; el mismo clic también activa u omite ese motor.

Cuando se activa NR2, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

Cada botón de alternancia tiene un nombre de objeto estable (`dspMethodBtnNR2`, `dspMethodBtnNR4`, etc.) y un nombre accesible para lectores de pantalla y herramientas de automatización.

## Pestaña: NR2 — Reducción de ruido musical

El motor NR2 utiliza sustracción espectral con mapeo de curva de ganancia y estimación de potencia de ruido.

### Método de ganancia (Gain Method)

Selecciona el mapeo de curva de ganancia utilizado por NR2.

| Opción  | Descripción                    |
|---------|--------------------------------|
| Linear  | Curva de ganancia lineal       |
| Log     | Curva de ganancia logarítmica  |
| Gamma   | Curva de ganancia basada en gamma (predeterminada) |
| Trained | Curva de ganancia preentrenada |

Se almacena en la configuración `NR2GainMethod` como entero 0-3.

### Método NPE

Selecciona el estimador de potencia de ruido.

| Opción | Descripción                                           |
|--------|-------------------------------------------------------|
| OSMS   | Suavizado óptimo y estadísticas mínimas (predeterminado) |
| MMSE   | Error cuadrático medio mínimo                         |
| NSTAT  | Estimación basada en estadísticas de ruido            |

Se almacena en la configuración `NR2NpeMethod` como entero 0-2.

### Filtro AE (eliminación de artefactos)

- Alterna el postfiltro antiartefactos.
- Predeterminado: Activado (`True`).
- Se almacena en la configuración `NR2AeFilter`.

### Reducción (Reduction):

- Establece la profundidad máxima de reducción de NR2.
- Predeterminado: 1.50
- Rango válido: 0.50–2.00
- Se almacena en la configuración `NR2GainMax` (valor * 100).

### Piso de ganancia (Gain Floor):

- Establece el piso mínimo de ganancia para NR2, evitando la supresión excesiva de señales débiles.
- Predeterminado: 0.10
- Rango válido: 0.00–0.50
- Se almacena en la configuración `NR2GainFloor`.

### Suavizado (Smoothing):

- Controla la suavidad con la que la estimación de ruido sigue los cambios.
- Predeterminado: 0.85
- Rango válido: 0.50–0.98
- Se almacena en la configuración `NR2GainSmooth`.

### Umbral (Threshold):

- Establece el umbral de probabilidad de presencia de voz.
- Predeterminado: 0.20
- Rango válido: 0.05–0.50
- Se almacena en la configuración `NR2Qspp`.

### Restablecer predeterminados (icono ↺)

- Restaura los valores predeterminados de la pestaña NR2: Gamma, OSMS, AE activado, Reducción 1.50, Piso de ganancia 0.10, Suavizado 0.85, Umbral 0.20.
- Se muestra como un botón de icono plano con flecha en sentido antihorario (U+21BA).

## Pestaña: NR4 — Reducción de ruido Libspecbleach

El motor NR4 utiliza la biblioteca [libspecbleach](https://github.com/geraldmwangi/libspecbleach) para el enmascaramiento espectral de ruido.

### Estimación de ruido (Noise Estimation):

Selecciona el estimador de piso de ruido utilizado por NR4.

| Opción | Descripción                                     |
|--------|-------------------------------------------------|
| MMSE   | Error cuadrático medio mínimo (predeterminado)  |
| Brandt | Estimador de ruido Brandt                       |
| Martin | Estimador de ruido Martin                       |

Se almacena en la configuración `NR4NoiseEstimationMethod` como entero 0-2.

### Estimación de ruido adaptativa (Adaptive Noise Estimation)

- Habilita la reestimación continua del piso de ruido.
- Predeterminado: Activado (`True`).
- Se almacena en la configuración `NR4AdaptiveNoise`.

### Reducción (dB):

- Establece la reducción máxima de ruido de NR4 en dB.
- Predeterminado: 10.0
- Rango válido: 0.0–40.0
- Se almacena en la configuración `NR4ReductionAmount` (valor * 10).

### Suavizado (%):

- Suavizado en el dominio del tiempo de la estimación de ruido de NR4.
- Predeterminado: 0
- Rango válido: 0–100
- Se almacena en la configuración `NR4SmoothingFactor`.

### Blanqueamiento (%):

- Aplana la forma espectral del ruido residual.
- Predeterminado: 0
- Rango válido: 0–100
- Se almacena en la configuración `NR4WhiteningFactor`.

### Profundidad de enmascaramiento (Masking Depth):

- Controla la profundidad del enmascaramiento espectral.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Se almacena en la configuración `NR4MaskingDepth`.

### Supresión:

- Fuerza general de supresión de NR4.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Se almacena en la configuración `NR4SuppressionStrength`.

### Restablecer predeterminados (icono ↺)

- Restaura los valores predeterminados de NR4: MMSE, Adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.
- Se muestra como un botón de icono plano con flecha en sentido antihorario (U+21BA).

## Pestaña: MNR — Reducción de ruido MMSE-Wiener

El motor MNR proporciona reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. **Esta pestaña está atenuada en las versiones de Windows y Linux**: el motor no tiene backend en esas plataformas.

### Fuerza (Strength)

- Ajusta la agresividad de MNR (0 suave, 100 máximo).
- Predeterminado: 100
- Rango válido: 0–100
- Se almacena en la configuración `MnrStrength` (normalizado como 0.00–1.00).

## Pestaña: RN2 — RNNoise

La pestaña RN2 (RNNoise) aloja el control deslizante de mezcla seca Noise Floor introducido en v26.8.4. La alternancia activa u omite el motor RNNoise.

### Noise Floor (RN2 dry mix)

- Establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado.
- Predeterminado: 0
- Rango válido: 0–100
- Cero produce supresión total (silencio entre frases); 10-20% mantiene un piso silencioso estable para que el receptor siga sonando vivo.
- Afecta solo al audio recibido; el denoizador de transmisión no cambia.
- Lo conserva Rn2SettingsModel y se expone a la cadena DSP mediante la señal `rn2DryMixChanged` de AetherDspWidget.

### Restablecer predeterminados (icono ↺)

- Restaura el control deslizante de Noise Floor a 0.
- Se muestra como un botón de icono plano con flecha en sentido antihorario (U+21BA).

## Pestaña: BNR — NVIDIA Broadcast

La pestaña BNR (NVIDIA) muestra la intensidad controlada desde el menú superpuesto. **La alternancia BNR está atenuada en las versiones sin el SDK de NVIDIA Broadcast.**

## Pestaña: DFNR — DeepFilterNet3

La pestaña DFNR proporciona controles para el motor de reducción de ruido DeepFilterNet3. **La alternancia DFNR está atenuada en las versiones sin el backend DeepFilterNet3.**

### Límite de atenuación (Attenuation Limit)

- Establece la atenuación máxima de ruido aplicada por DeepFilterNet3.
- Predeterminado: 100
- Rango válido: 0–100 dB
- 0 = paso directo; 100 = máximo.
- Se almacena en la configuración `DfnrAttenLimit`.

### Beta de postfiltro (Post-Filter Beta)

- Aplica un postfiltro adicional para una supresión extra más allá del límite de atenuación.
- Predeterminado: 0.00
- Rango válido: 0.00–0.30
- Se almacena en la configuración `DfnrPostFilterBeta` (valor * 100).

## Consejos

- Comience con **Post-Filter Beta** en 0.10 o menos. Los artefactos audibles tienden a aparecer antes de alcanzar 0.30, especialmente en señales de voz SSB.
- Si necesita una atenuación general más fuerte sin tocar el postfiltro, aumente primero **Attenuation Limit** y luego agregue **Post-Filter Beta** solo para el ruido residual que permanezca.
- Un valor de 0.00 deshabilita el postfiltro por completo, dejando la salida de DeepFilterNet3 sin cambios.
- Para NR2, comience con los valores predeterminados y aumente Reduction gradualmente mientras verifica la presencia de artefactos musicales.
- El control deslizante **Gain Floor** evita que NR2 silencie por completo las señales débiles. Auméntelo si las señales desaparecen durante las pausas, disminúyalo si el ruido de fondo es demasiado prominente.
- Para RN2, pruebe un Noise Floor de 10-20% si la supresión total deja un silencio incómodo entre frases.

## Solución de problemas

- **El habla suena hueca o con efecto de fase** — **Post-Filter Beta** está demasiado alto. Redúzcalo hacia 0.00 en pequeños incrementos hasta que regrese la naturalidad.
- **No hay cambio audible al mover el control deslizante** — Es posible que el motor seleccionado no esté activo en el slice actual. Confirme que la alternancia del motor esté seleccionada y que los parámetros no estén al mínimo.
- **NR2 produce ruido musical** — Reduzca **Reduction** o active **AE Filter** para suprimir artefactos.
- **NR2 hace desaparecer señales débiles** — Aumente **Gain Floor** para evitar la supresión excesiva.
- **El audio de RN2 suena muerto entre frases** — Establezca **Noise Floor** al 10-20% para que quede un piso silencioso bajo el audio denoizado.
- **Las pestañas MNR, BNR o DFNR están atenuadas** — El backend requerido (macOS para MNR, SDK de NVIDIA Broadcast para BNR, DeepFilterNet para DFNR) no está disponible en su plataforma.
- **La pestaña DFNR falta por completo** — AetherSDR se compiló sin soporte de DeepFilterNet. Recompile con el backend DFNR para usar este motor.
- **Los colores no coinciden con el resto de AetherSDR** — El diálogo ahora utiliza estilo consciente del tema. Pruebe cambiar de tema en `Settings > Appearance` si los colores no son de su agrado.

## Relacionados

- [Ajuste la profundidad de reducción de NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Configure el beta de postfiltro DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Establezca el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
