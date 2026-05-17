# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP proporciona control avanzado sobre los seis motores de reducción de ruido del lado del cliente en AetherSDR: NR2, NR4, DFNR, MNR, RN2 y BNR. Cada motor se selecciona mediante una fila de botones de alternancia en la parte superior del diálogo; al hacer clic en un botón también se activa o desactiva ese motor.

## Abrir la Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.
2. El diálogo se abre con una barra de título sin marco de forma predeterminada.
3. El diálogo se puede abrir sin una conexión de radio, pero el efecto solo es audible durante la recepción en vivo.

## Diseño del diálogo y controles de ventana

El diálogo de Configuración de AetherDSP utiliza un borde personalizado que coincide con el NetworkDiagnosticsDialog y AetherialAudioStrip:

| Control | Descripción |
|---------|-------------|
| **Barra de título** | Barra de título de 18 píxeles con degradado azul, con el glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. Añadido en v0.9.8 (#2425 refit). |
| **— (Minimizar)** | Minimiza el diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. |
| **× (Cerrar)** | Cierra el diálogo. |
| **Arrastrar para mover** | Haga clic y arrastre la barra de título para mover el diálogo. |
| **Redimensionamiento de 8 ejes** | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Zona de impacto de redimensionamiento de 6 píxeles alrededor del widget de contenido interno. |

El diálogo utiliza `PersistentDialog` con la geometría almacenada en la configuración `AetherDspDialogGeometry`. La posición y el tamaño se restauran automáticamente al volver a abrir el diálogo.

## Seleccionar y activar motores de reducción de ruido

Los seis botones de alternancia de DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de pestaña exclusivos como controles de activación/desactivación del motor. Haga clic en un botón para seleccionar su página de configuración; el mismo clic también activa o desactiva ese motor.

Cuando NR2 está activado, AudioEngine aplica la exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

## Pestaña: NR2 — Reducción de ruido musical

El motor NR2 utiliza sustracción espectral con mapeo de curva de ganancia y estimación de potencia de ruido.

### Método de Ganancia

Selecciona el mapeo de la curva de ganancia utilizado por NR2.

| Opción | Descripción |
|--------|-------------|
| Linear | Curva de ganancia lineal |
| Log | Curva de ganancia logarítmica |
| Gamma | Curva de ganancia basada en gamma (predeterminado) |
| Trained | Curva de ganancia preentrenada |

Se almacena en la configuración `NR2GainMethod` como un entero de 0 a 3.

### Método NPE

Selecciona el estimador de potencia de ruido.

| Opción | Descripción |
|--------|-------------|
| OSMS | Suavizado óptimo y estadísticas mínimas (predeterminado) |
| MMSE | Error cuadrático medio mínimo |
| NSTAT | Estimación basada en estadísticas de ruido |

Se almacena en la configuración `NR2NpeMethod` como un entero de 0 a 2.

### Filtro AE (eliminación de artefactos)

- Alterna el filtro posterior antiartefacto.
- Predeterminado: Activado (`True`).
- Se almacena en la configuración `NR2AeFilter`.

### Reducción:

- Establece la profundidad máxima de reducción de NR2.
- Predeterminado: 1.50
- Rango válido: 0.50–2.00
- Se almacena en la configuración `NR2GainMax` (valor * 100).

### Suavizado:

- Controla con qué suavidad la estimación de ruido sigue los cambios.
- Predeterminado: 0.85
- Rango válido: 0.50–0.98
- Se almacena en la configuración `NR2GainSmooth`.

### Umbral:

- Establece el umbral de probabilidad de presencia de voz.
- Predeterminado: 0.20
- Rango válido: 0.05–0.50
- Se almacena en la configuración `NR2Qspp`.

### Restablecer Valores Predeterminados (icono ↺)

- Restaura los valores predeterminados de la pestaña NR2: Gamma, OSMS, AE activado, Reducción 1.50, Suavizado 0.85, Umbral 0.20.
- Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).

## Pestaña: NR4 — Reducción de ruido Libspecbleach

El motor NR4 utiliza la biblioteca [libspecbleach](https://github.com/geraldmwangi/libspecbleach) para la compuerta de ruido espectral.

### Estimación de Ruido:

Selecciona el estimador de piso de ruido utilizado por NR4.

| Opción | Descripción |
|--------|-------------|
| MMSE | Error cuadrático medio mínimo (predeterminado) |
| Brandt | Estimador de ruido Brandt |
| Martin | Estimador de ruido Martin |

Se almacena en la configuración `NR4NoiseEstimationMethod` como un entero de 0 a 2.

### Estimación de Ruido Adaptativa

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

### Profundidad de Enmascaramiento:

- Controla la profundidad del enmascaramiento espectral.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Se almacena en la configuración `NR4MaskingDepth`.

### Supresión:

- Fuerza de supresión general de NR4.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Se almacena en la configuración `NR4SuppressionStrength`.

### Restablecer Valores Predeterminados (icono ↺)

- Restaura los valores predeterminados de NR4: MMSE, Adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.
- Se muestra como un botón de icono plano con una flecha en sentido antihorario (U+21BA).

## Pestaña: MNR — Reducción de ruido MMSE-Wiener

El motor MNR proporciona reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. **Esta pestaña está atenuada en las compilaciones de Windows y Linux** — el motor no tiene backend en esas plataformas.

### Habilitar MNR (solo macOS)

- Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.
- El estado inicial se lee en vivo del motor de audio.
- Se almacena en la configuración `MnrEnabled`.

### Intensidad

- Ajusta la agresividad de MNR (0 suave, 100 máximo).
- Predeterminado: 100
- Rango válido: 0–100
- Se almacena en la configuración `MnrStrength` (normalizado como 0.00–1.00).

## Pestaña: RN2 — RNNoise

La pestaña RN2 (RNNoise) es **puramente informativa** — no hay parámetros ajustables disponibles. El botón de alternancia activa o desactiva el motor RNNoise, pero la configuración se gestiona en otro lugar.

## Pestaña: BNR — NVIDIA Broadcast

La pestaña BNR (NVIDIA) muestra la intensidad controlada desde el menú superpuesto. **El botón de alternancia BNR está atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.**

## Pestaña: DFNR — DeepFilterNet3

La pestaña DFNR proporciona controles para el motor de reducción de ruido DeepFilterNet3.

### Límite de Atenuación

- Establece la atenuación máxima de ruido aplicada por DeepFilterNet3.
- Predeterminado: 100
- Rango válido: 0–100 dB
- 0 = paso directo; 100 = máximo.
- Se almacena en la configuración `DfnrAttenLimit`.

### Beta del Filtro Posterior

- Aplica un filtro posterior adicional para una supresión extra más allá del límite de atenuación.
- Predeterminado: 0.00
- Rango válido: 0.00–0.30
- Se almacena en la configuración `DfnrPostFilterBeta` (valor * 100).

## Consejos

- Comience con **Beta del Filtro Posterior** en 0.10 o menos. Los artefactos audibles tienden a aparecer antes de alcanzar 0.30, especialmente en señales de voz SSB.
- Si necesita una atenuación general más fuerte sin tocar el filtro posterior, aumente primero el **Límite de Atenuación**, luego añada **Beta del Filtro Posterior** solo para el ruido residual que persista.
- Un valor de 0.00 desactiva completamente el filtro posterior, dejando la salida de DeepFilterNet3 sin cambios.
- Para NR2, comience con los valores predeterminados y aumente la Reducción gradualmente mientras verifica la presencia de artefactos musicales.

## Solución de problemas

- **La voz suena hueca o con fases** — **Beta del Filtro Posterior** está demasiado alto. Redúzcalo hacia 0.00 en pequeños incrementos hasta que vuelva la naturalidad.
- **No hay un cambio audible al mover el control deslizante** — Es posible que el motor seleccionado no esté activo en el segmento actual. Confirme que el botón de alternancia del motor esté seleccionado y que los parámetros no estén en el mínimo.
- **NR2 produce ruido musical** — Reduzca la **Reducción** o active el **Filtro AE** para suprimir artefactos.
- **Las pestañas MNR o BNR están atenuadas** — El backend requerido (macOS para MNR, SDK de NVIDIA Broadcast para BNR) no está disponible en su plataforma.

## Relacionado

- [Ajustar la profundidad de reducción de NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Configurar el beta del filtro posterior de DFNR para supresión extra](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
