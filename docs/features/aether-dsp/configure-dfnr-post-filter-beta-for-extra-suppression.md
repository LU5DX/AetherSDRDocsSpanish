# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP proporciona control avanzado sobre los seis motores de reducción de ruido del lado del cliente en AetherSDR: NR2, NR4, DFNR, MNR, RN2 y BNR. Cada motor se selecciona mediante una fila de alternancia en la parte superior del diálogo; al hacer clic en una alternancia también se activa o desvía ese motor.

## Cómo abrir la Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.
2. El diálogo se abre con una barra de título sin marco basada en la configuración `FramelessWindow`. Si el modo sin marco está deshabilitado, el diálogo utiliza el marco nativo de la ventana.
3. El diálogo se puede abrir sin una conexión de radio, pero el efecto solo es audible durante la recepción en vivo.

## Diseño del diálogo y controles de ventana

El diálogo de Configuración de AetherDSP utiliza un marco personalizado que coincide con NetworkDiagnosticsDialog y AetherialAudioStrip:

| Control | Descripción |
|---------|-------------|
| **Barra de título** | Barra de título de 18 px con degradado azul, glifo de agarre (⋮⋮) a la izquierda y título del diálogo. Añadido en v0.9.8 (#2425 refit). Visible solo cuando el modo sin marco está habilitado (predeterminado). |
| **— (Minimizar)** | Minimiza el diálogo. Visible solo cuando el modo sin marco está habilitado. |
| **□ (Maximizar)** | Maximiza o restaura el diálogo. Haga doble clic en la barra de título para alternar entre maximizar/restaurar. Visible solo cuando el modo sin marco está habilitado. |
| **× (Cerrar)** | Cierra el diálogo. Visible solo cuando el modo sin marco está habilitado. |
| **Arrastrar para mover** | Haga clic y arrastre la barra de título para mover el diálogo. Solo funciona en modo sin marco. |
| **Redimensionar en 8 ejes** | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Zona de redimensionamiento de 6 px alrededor del widget de contenido interno. Solo activo en modo sin marco. |

### Alternancia de modo sin marco

- El diálogo lee la configuración `FramelessWindow` de `Settings > Appearance > Frameless Window` para determinar si debe usar marco sin marco o nativo.
- Predeterminado: Sin marco (True).
- Cuando el modo sin marco está desactivado, la barra de título con el glifo de agarre y los botones de control de ventana (Minimizar, Maximizar, Cerrar) están ocultos; el sistema operativo proporciona la barra de título y los controles de ventana.

## Seleccionar y activar motores de reducción de ruido

Las seis alternancias DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores de pestañas exclusivos y controles de activación/desactivación del motor. Haga clic en una alternancia para seleccionar su página de configuración; el mismo clic también activa o desvía ese motor.

Cuando NR2 está activado, AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

## Pestaña: NR2 — Reducción de ruido musical

El motor NR2 utiliza sustracción espectral con mapeo de curva de ganancia y estimación de potencia de ruido.

### Método de Ganancia

Selecciona el mapeo de curva de ganancia utilizado por NR2.

| Opción | Descripción |
|--------|-------------|
| Linear | Curva de ganancia lineal |
| Log | Curva de ganancia logarítmica |
| Gamma | Curva de ganancia basada en gamma (predeterminado) |
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

- Alterna el post-filtro anti-artefacto.
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
- Se muestra como un botón de icono plano con flecha en sentido antihorario (U+21BA).

## Pestaña: NR4 — Reducción de ruido Libspecbleach

El motor NR4 utiliza la biblioteca [libspecbleach](https://github.com/geraldmwangi/libspecbleach) para el enmascaramiento espectral de ruido.

**Nota:** En Windows, NR4 requiere LLVM (clang-cl) para compilar. Si LLVM no está instalado, la alternancia NR4 aparece atenuada con un tooltip: "NR4 requires LLVM (clang-cl) on Windows. Install LLVM from llvm.org and rebuild to enable NR4."

### Estimación de Ruido:

Selecciona el estimador de piso de ruido utilizado por NR4.

| Opción | Descripción |
|--------|-------------|
| MMSE | Error cuadrático medio mínimo (predeterminado) |
| Brandt | Estimador de ruido Brandt |
| Martin | Estimador de ruido Martin |

Almacenado en la configuración `NR4NoiseEstimationMethod` como entero 0-2.

### Estimación Adaptativa de Ruido

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

### Profundidad de Enmascaramiento:

- Controla la profundidad del enmascaramiento espectral.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Almacenado en la configuración `NR4MaskingDepth`.

### Supresión:

- Fuerza general de supresión de NR4.
- Predeterminado: 0.50
- Rango válido: 0.00–1.00
- Almacenado en la configuración `NR4SuppressionStrength`.

### Restablecer valores predeterminados (icono ↺)

- Restaura los valores predeterminados de NR4: MMSE, Adaptativo activado, 10 dB, 0, 0, 0.50, 0.50.
- Se muestra como un botón de icono plano con flecha en sentido antihorario (U+21BA).

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

La pestaña RN2 (RNNoise) es **puramente informativa** — no hay parámetros ajustables disponibles. La alternancia activa o desvía el motor RNNoise, pero la configuración se gestiona en otro lugar.

## Pestaña: BNR — NVIDIA Broadcast

La pestaña BNR (NVIDIA) muestra la intensidad controlada desde el menú superpuesto. **La alternancia BNR está atenuada en compilaciones sin el SDK de NVIDIA Broadcast.**

## Pestaña: DFNR — DeepFilterNet3

La pestaña DFNR proporciona controles para el motor de reducción de ruido DeepFilterNet3.

### Límite de Atenuación

- Establece la atenuación máxima de ruido aplicada por DeepFilterNet3.
- Predeterminado: 100
- Rango válido: 0–100 dB
- 0 = paso directo; 100 = máximo.
- Almacenado en la configuración `DfnrAttenLimit`.

### Beta del Post-Filtro

- Aplica un post-filtro adicional para una supresión extra más allá del límite de atenuación.
- Predeterminado: 0.00
- Rango válido: 0.00–0.30
- Almacenado en la configuración `DfnrPostFilterBeta` (valor * 100).

## Consejos

- Comience con **Beta del Post-Filtro** en o por debajo de 0.10. Los artefactos audibles tienden a aparecer antes de alcanzar 0.30, especialmente en señales de voz SSB.
- Si necesita una atenuación general más fuerte sin tocar el post-filtro, aumente primero el **Límite de Atenuación**, luego agregue **Beta del Post-Filtro** solo para el ruido residual que permanezca.
- Un valor de 0.00 desactiva el post-filtro por completo, dejando la salida de DeepFilterNet3 sin cambios.
- Para NR2, comience con los valores predeterminados y ajuste la Reducción hacia arriba gradualmente mientras verifica la presencia de artefactos musicales.

## Solución de problemas

- **La voz suena hueca o con fase** — **Beta del Post-Filtro** está configurado demasiado alto. Redúzcalo hacia 0.00 en incrementos pequeños hasta que regrese la naturalidad.
- **No hay cambio audible al mover el control deslizante** — El motor seleccionado puede no estar activo en el slice actual. Confirme que la alternancia del motor esté seleccionada y que los parámetros no estén al mínimo.
- **NR2 produce ruido musical** — Reduzca la **Reducción** o active el **Filtro AE** para suprimir artefactos.
- **Las pestañas MNR o BNR están atenuadas** — El backend requerido (macOS para MNR, SDK de NVIDIA Broadcast para BNR) no está disponible en su plataforma.
- **La pestaña NR4 está atenuada en Windows** — LLVM (clang-cl) no está instalado. Instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.
- **Falta la barra de título o los controles de ventana** — El modo sin marco está deshabilitado. Actívelo en `Settings > Appearance > Frameless Window` para restaurar el marco personalizado.

## Relacionados

- [Ajustar la profundidad de reducción de NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Configurar el beta del post-filtro DFNR para supresión extra](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
