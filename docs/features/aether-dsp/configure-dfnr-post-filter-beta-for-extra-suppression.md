# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP proporciona control avanzado sobre los seis motores de reducción de ruido del lado del cliente en AetherSDR: NR2, NR4, DFNR, MNR, RN2 y BNR. Cada motor se selecciona mediante una fila de conmutadores en la parte superior del diálogo; al hacer clic en un conmutador también se activa o desactiva ese motor.

## Abrir la Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.
2. El diálogo se abre con una barra de título sin marco de forma predeterminada.
3. El diálogo se puede abrir sin una conexión de radio, pero el efecto solo se escucha durante la recepción en vivo.

## Disposición del diálogo y controles de ventana

El diálogo de Configuración de AetherDSP utiliza un marco personalizado que coincide con NetworkDiagnosticsDialog y AetherialAudioStrip:

| Control | Descripción |
|---------|-------------|
| **Barra de título** | Barra de título con degradado de 18 px con glifo de agarre (⋮⋮) a la izquierda y título del diálogo. Añadido en v0.9.8 (#2425 refit). |
| **— (Minimizar)** | Minimiza el diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. |
| **× (Cerrar)** | Cierra el diálogo. |
| **Arrastrar para mover** | Haga clic y arrastre la barra de título para mover el diálogo. |
| **Redimensionamiento en 8 ejes** | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Zona de redimensionamiento de 6 px alrededor del widget de contenido interno. |

El diálogo utiliza `PersistentDialog` con la geometría almacenada en la configuración `AetherDspDialogGeometry`. La posición y el tamaño se restauran automáticamente al reabrir el diálogo.

El fondo del diálogo, los colores de la barra de título y el estilo de los deslizadores utilizan tokens del tema activo. Los deslizadores ahora usan `applyPrimarySliderStyle()` en lugar de hojas de estilo en línea codificadas, lo que hace que respeten el esquema de color elegido por el usuario.

## Seleccionar y activar motores de reducción de ruido

Los seis conmutadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de pestaña exclusivos como controles de habilitación/deshabilitación del motor. Haga clic en un conmutador para seleccionar su página de configuración; el mismo clic también activa o desactiva ese motor.

Cuando se activa NR2, AudioEngine aplica exclusión en cascada, deshabilitando DFNR y otros módulos mutuamente excluyentes.

## Pestaña: NR2 — Reducción de ruido musical

El motor NR2 utiliza sustracción espectral con mapeo de curva de ganancia y estimación de potencia de ruido.

### Método de ganancia

Selecciona el mapeo de curva de ganancia utilizado por NR2.

| Opción | Descripción |
|--------|-------------|
| Linear | Curva de ganancia lineal |
| Log | Curva de ganancia logarítmica |
| Gamma | Curva de ganancia basada en gamma (predeterminada) |
| Trained | Curva de ganancia preentrenada |

Almacenado en la configuración `NR2GainMethod` como entero 0-3.

### Método NPE

Selecciona el estimador de potencia de ruido.

| Opción | Descripción |
|--------|-------------|
| OSMS | Suavizado óptimo y estadísticas mínimas (predeterminado) |
| MMSE | Error cuadrático medio mínimo |
| NSTAT | Estimación basada en estadísticas de ruido |

Almacenado en la configuración `NR2NpeMethod` como entero 0-2.

### Filtro AE (eliminación de artefactos)

- Activa/desactiva el postfiltro antiartefactos.
- Predeterminado: Activado (`True`).
- Almacenado en la configuración `NR2AeFilter`.

### Reducción:

- Establece la profundidad máxima de reducción de NR2.
- Predeterminado: 1.50
- Rango válido: 0.50–2.00
- Almacenado en la configuración `NR2GainMax` (valor * 100).

### Suavizado:

- Controla la suavidad con la que la estimación de ruido sigue los cambios.
- Predeterminado: 0.85
- Rango válido: 0.50–0.98
- Almacenado en la configuración `NR2GainSmooth`.

### Umbral:

- Establece el umbral de probabilidad de presencia de voz.
- Predeterminado: 0.20
- Rango válido: 0.05–0.50
- Almacenado en la configuración `NR2Qspp`.

### Restablecer valores predeterminados (icono ↺)

- Restaura los valores predeterminados de la pestaña NR2: Gamma, OSMS, AE activado, Reducción 1.50, Suavizado 0.85, Umbral 0.20.
- Se representa como un botón de icono plano con flecha en sentido antihorario (U+21BA).

## Pestaña: NR4 — Reducción de ruido Libspecbleach

El motor NR4 utiliza la biblioteca [libspecbleach](https://github.com/geraldmwangi/libspecbleach) para la compuerta de ruido espectral.

### Estimación de ruido:

Selecciona el estimador de piso de ruido utilizado por NR4.

| Opción | Descripción |
|--------|-------------|
| MMSE | Error cuadrático medio mínimo (predeterminado) |
| Brandt | Estimador de ruido Brandt |
| Martin | Estimador de ruido Martin |

Almacenado en la configuración `NR4NoiseEstimationMethod` como entero 0-2.

### Estimación de ruido adaptativa

- Habilita la reestimación continua del piso de ruido.
- Predeterminado: Activado (`True`).
- Almacenado en la configuración `NR4AdaptiveNoise`.

### Reducción (dB):

- Establece la reducción máxima de ruido de NR4 en dB.
- Predeterminado: 10.0
- Rango válido: 0.0–40.0
- Almacenado en la configuración `NR4ReductionAmount` (valor * 10).

### Suavizado (%):

- Suavizado en el dominio del tiempo de la estimación de ruido de NR4.
- Predeterminado: 0
- Rango válido: 0–100
- Almacenado en la configuración `NR4SmoothingFactor`.

### Blanqueamiento (%):

- Aplana la forma espectral del ruido residual.
- Predeterminado: 0
- Rango válido: 0–100
- Almacenado en la configuración `NR4WhiteningFactor`.

### Profundidad de enmascaramiento:

- Controla la profundidad del enmascaramiento espectral.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Almacenado en la configuración `NR4MaskingDepth`.

### Supresión:

- Fuerza de supresión general de NR4.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Almacenado en la configuración `NR4SuppressionStrength`.

### Restablecer valores predeterminados (icono ↺)

- Restaura los valores predeterminados de NR4: MMSE, Adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.
- Se representa como un botón de icono plano con flecha en sentido antihorario (U+21BA).

## Pestaña: MNR — Reducción de ruido MMSE-Wiener

El motor MNR proporciona reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. **Esta pestaña está atenuada en las compilaciones de Windows y Linux** — el motor no tiene backend en esas plataformas.

### Habilitar MNR (solo macOS)

- Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.
- El estado inicial se lee en vivo desde el motor de audio.
- Almacenado en la configuración `MnrEnabled`.

### Intensidad

- Ajusta la agresividad de MNR (0 suave, 100 máximo).
- Predeterminado: 100
- Rango válido: 0–100
- Almacenado en la configuración `MnrStrength` (normalizado como 0.00–1.00).

## Pestaña: RN2 — RNNoise

La pestaña RN2 (RNNoise) es **puramente informativa** — no hay parámetros ajustables disponibles. El conmutador activa o desactiva el motor RNNoise, pero la configuración se gestiona en otro lugar.

## Pestaña: BNR — NVIDIA Broadcast

La pestaña BNR (NVIDIA) muestra la intensidad controlada desde el menú superpuesto. **El conmutador BNR está atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.**

## Pestaña: DFNR — DeepFilterNet3

La pestaña DFNR proporciona controles para el motor de reducción de ruido DeepFilterNet3.

### Límite de atenuación

- Establece la atenuación máxima de ruido aplicada por DeepFilterNet3.
- Predeterminado: 100
- Rango válido: 0–100 dB
- 0 = paso directo; 100 = máximo.
- Almacenado en la configuración `DfnrAttenLimit`.

### Beta del postfiltro

- Aplica un postfiltro adicional para una supresión extra más allá del límite de atenuación.
- Predeterminado: 0.00
- Rango válido: 0.00–0.30
- Almacenado en la configuración `DfnrPostFilterBeta` (valor * 100).

## Consejos

- Comience con **Beta del postfiltro** en o por debajo de 0.10. Los artefactos audibles tienden a aparecer antes de alcanzar 0.30, especialmente en señales de voz SSB.
- Si necesita una atenuación general más fuerte sin tocar el postfiltro, aumente primero el **Límite de atenuación**, luego agregue **Beta del postfiltro** solo para el ruido residual que permanezca.
- Un valor de 0.00 desactiva el postfiltro por completo, dejando la salida de DeepFilterNet3 sin cambios.
- Para NR2, comience con los valores predeterminados y aumente la Reducción gradualmente mientras verifica la presencia de artefactos musicales.

## Solución de problemas

- **El sonido suena hueco o con cambio de fase** — **Beta del postfiltro** está demasiado alto. Redúzcalo hacia 0.00 en pequeños incrementos hasta que regrese la naturalidad.
- **No hay cambio audible al mover el deslizador** — Es posible que el motor seleccionado no esté activo en el segmento actual. Confirme que el conmutador del motor esté seleccionado y que los parámetros no estén en el mínimo.
- **NR2 produce ruido musical** — Reduzca la **Reducción** o active el **Filtro AE** para suprimir artefactos.
- **Las pestañas MNR o BNR están atenuadas** — El backend requerido (macOS para MNR, SDK de NVIDIA Broadcast para BNR) no está disponible en su plataforma.
- **Los colores no coinciden con el resto de AetherSDR** — El diálogo ahora utiliza estilo consciente del tema. Intente cambiar de tema en `Settings > Appearance` si los colores no son de su agrado.

## Relacionados

- [Ajustar la profundidad de reducción de NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Configurar beta del postfiltro DFNR para supresión extra](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
