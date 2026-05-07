# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP proporciona control avanzado sobre los seis motores de reducción de ruido del lado del cliente en AetherSDR: NR2, NR4, DFNR, MNR, RN2 y BNR. Cada motor se selecciona mediante una fila de botones de alternancia en la parte superior del diálogo; al hacer clic en un botón también se activa o se desvía ese motor.

## Abrir la Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.
2. El diálogo se abre como una ventana sin marco con una barra de título personalizada de 18 píxeles.
3. El diálogo se puede abrir sin conexión de radio, pero el efecto solo se escucha durante la recepción en vivo.

## Disposición del diálogo y controles de ventana

El diálogo de Configuración de AetherDSP utiliza un marco personalizado que coincide con el NetworkDiagnosticsDialog y el AetherialAudioStrip:

| Control | Descripción |
|---------|-------------|
| **Barra de título** | Barra de título con degradado azul de 18 px con un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. Añadido en v0.9.8 (#2425 refit). |
| **— (Minimizar)** | Minimiza el diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el diálogo. Hacer doble clic en la barra de título también alterna entre maximizar/restaurar. |
| **× (Cerrar)** | Cierra el diálogo. |
| **Arrastrar para mover** | Haga clic y arrastre la barra de título para mover el diálogo. |
| **Redimensionamiento de 8 ejes** | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección del redimensionamiento. Zona de ajuste de redimensionamiento de 12 px (6 px interior, 6 px exterior). |

## Selección y activación de motores de reducción de ruido

Los seis botones de alternancia de DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan tanto como selectores de pestaña exclusivos como controles de activación/desactivación del motor. Haga clic en un botón de alternancia para seleccionar su página de configuración; el mismo clic también activa o desvía ese motor.

Cuando se activa NR2, AudioEngine aplica una exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

## Pestaña: NR2 — Reducción de ruido musical

El motor NR2 utiliza sustracción espectral con mapeo de curva de ganancia y estimación de potencia de ruido.

### Método de ganancia

Selecciona el mapeo de curva de ganancia utilizado por NR2.

| Opción | Descripción |
|--------|-------------|
| Linear | Curva de ganancia lineal |
| Log | Curva de ganancia logarítmica |
| Gamma | Curva de ganancia basada en gamma (predeterminado) |
| Trained | Curva de ganancia preentrenada |

Se almacena en la configuración `NR2GainMethod` como entero 0-3.

### Método NPE

Selecciona el estimador de potencia de ruido.

| Opción | Descripción |
|--------|-------------|
| OSMS | Suavizado óptimo y estadísticas mínimas (predeterminado) |
| MMSE | Error cuadrático medio mínimo |
| NSTAT | Estimación basada en estadísticas de ruido |

Se almacena en la configuración `NR2NpeMethod` como entero 0-2.

### Filtro AE (eliminación de artefactos)

- Alterna el post-filtro antiartefactos.
- Predeterminado: Activado (`True`).
- Se almacena en la configuración `NR2AeFilter`.

### Reducción:

- Establece la profundidad máxima de reducción de NR2.
- Predeterminado: 1.50
- Rango válido: 0.50–2.00
- Se almacena en la configuración `NR2GainMax` (valor * 100).

### Suavizado:

- Controla la suavidad con la que la estimación de ruido sigue los cambios.
- Predeterminado: 0.85
- Rango válido: 0.50–0.98
- Se almacena en la configuración `NR2GainSmooth`.

### Umbral:

- Establece el umbral de probabilidad de presencia de voz.
- Predeterminado: 0.20
- Rango válido: 0.05–0.50
- Se almacena en la configuración `NR2Qspp`.

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

Se almacena en la configuración `NR4NoiseEstimationMethod` como entero 0-2.

### Estimación de ruido adaptativa

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

### Profundidad de enmascaramiento:

- Controla la profundidad del enmascaramiento espectral.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Se almacena en la configuración `NR4MaskingDepth`.

### Supresión:

- Fuerza general de supresión de NR4.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Se almacena en la configuración `NR4SuppressionStrength`.

### Restablecer valores predeterminados (icono ↺)

- Restaura los valores predeterminados de NR4: MMSE, Adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.
- Se representa como un botón de icono plano con flecha en sentido antihorario (U+21BA).

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

La pestaña RN2 (RNNoise) es **puramente informativa** — no hay parámetros ajustables disponibles. El botón de alternancia activa o desvía el motor RNNoise, pero la configuración se gestiona en otro lugar.

## Pestaña: BNR — NVIDIA Broadcast

La pestaña BNR (NVIDIA) muestra la intensidad controlada desde el menú superpuesto. **El botón de alternancia de BNR está atenuado en las compilaciones sin el SDK de NVIDIA Broadcast.**

## Pestaña: DFNR — DeepFilterNet3

La pestaña DFNR proporciona controles para el motor de reducción de ruido DeepFilterNet3.

### Límite de atenuación

- Establece la atenuación máxima de ruido aplicada por DeepFilterNet3.
- Predeterminado: 100
- Rango válido: 0–100 dB
- 0 = paso directo; 100 = máximo.
- Se almacena en la configuración `DfnrAttenLimit`.

### Beta del post-filtro

- Aplica un post-filtro adicional para una supresión extra más allá del límite de atenuación.
- Predeterminado: 0.00
- Rango válido: 0.00–0.30
- Se almacena en la configuración `DfnrPostFilterBeta` (valor * 100).

## Consejos

- Comience con **Beta del post-filtro** en o por debajo de 0.10. Los artefactos audibles tienden a aparecer antes de alcanzar 0.30, especialmente en señales de voz SSB.
- Si necesita una atenuación general más fuerte sin tocar el post-filtro, aumente primero el **Límite de atenuación**, luego agregue **Beta del post-filtro** solo para el ruido residual que permanezca.
- Un valor de 0.00 desactiva el post-filtro por completo, dejando la salida de DeepFilterNet3 sin cambios.
- Para NR2, comience con los valores predeterminados y ajuste la Reducción hacia arriba gradualmente mientras verifica la aparición de artefactos musicales.

## Solución de problemas

- **El habla suena hueca o con cambio de fase** — **Beta del post-filtro** está demasiado alto. Redúzcalo hacia 0.00 en pequeños incrementos hasta que regrese la naturalidad.
- **No hay cambio audible al mover el control deslizante** — El motor seleccionado puede no estar activo en el segmento actual. Confirme que el botón de alternancia del motor esté seleccionado y que los parámetros no estén en el mínimo.
- **NR2 produce ruido musical** — Reduzca **Reducción** o active **Filtro AE** para suprimir artefactos.
- **Las pestañas MNR o BNR están atenuadas** — El backend requerido (macOS para MNR, SDK de NVIDIA Broadcast para BNR) no está disponible en su plataforma.

## Relacionado

- [Ajustar la profundidad de reducción de NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Configurar la beta del post-filtro de DFNR para supresión extra](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
