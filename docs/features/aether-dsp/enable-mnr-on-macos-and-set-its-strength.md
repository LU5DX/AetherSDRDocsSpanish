# Configuración de AetherDSP

La configuración de AetherDSP es un diálogo que le permite ajustar los motores de reducción de ruido del lado del cliente disponibles en AetherSDR: NR2, NR4, MNR, DFNR, RN2 y BNR. Cada motor tiene su propia pestaña. Abra el diálogo desde `Settings > AetherDSP Settings...`.

El diálogo admite modos de decoración de ventana sin marco (chrome personalizado) y nativa. Por defecto, el modo sin marco está habilitado, controlado por la configuración de aplicación `FramelessWindow` (`Settings > Preferences > General > Frameless Window`). Cuando el modo sin marco está activo, el diálogo utiliza una barra de título degradada personalizada, botones de control de ventana, redimensionamiento de 8 ejes y arrastre para mover. Cuando el modo sin marco está deshabilitado, el diálogo utiliza el chrome de ventana estándar del sistema operativo. El diálogo aloja un `AetherDspWidget` incrustado que contiene todos los controles. Las conexiones de señal existentes al diálogo continúan funcionando sin cambios.

---

## Pestaña NR2

NR2 es el motor de reducción de ruido musical de AetherSDR.

### Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Seleccione un botón de opción **Gain Method**.
4. Seleccione un botón de opción **NPE Method**.
5. Marque o desmarque **AE Filter (artifact elimination)** según sea necesario.
6. Arrastre **Reduction:**, **Smoothing:** y **Threshold:** a los valores deseados.
7. Haga clic en **Reset Defaults (icono ↺)** para devolver todos los controles de NR2 a sus valores de fábrica.

### Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Gain Method | Botón de opción | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` |
| NPE Method | Botón de opción | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | Casilla de verificación | Activado | On / Off | `NR2AeFilter` |
| Reduction: | Deslizador | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Deslizador | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Threshold: | Deslizador | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — |

`NR2GainMethod` se almacena como un entero 0–3 (Linear=0, Log=1, Gamma=2, Trained=3). `NR2NpeMethod` se almacena como un entero 0–2 (OSMS=0, MMSE=1, NSTAT=2). `NR2GainMax` se almacena internamente como valor × 100.

### Consejos

- El método de ganancia **Gamma** es adecuado para la mayoría del trabajo en SSB de voz. **Trained** puede mejorar los resultados en señales débiles.
- Aumente **Threshold:** si NR2 está suprimiendo el habla. Redúzcalo si el ruido se filtra durante las pausas.
- Haga clic en **Reset Defaults (icono ↺)** para restaurar: Gamma / OSMS / AE activado / 1.50 / 0.85 / 0.20.

---

## Pestaña NR4

NR4 utiliza el motor libspecbleach. En Windows, NR4 requiere LLVM (clang-cl) para compilarse. Si NR4 no está disponible en Windows, instale LLVM desde `llvm.org` y reconstruya AetherSDR.

### Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Seleccione un botón de opción **Noise Estimation:**.
4. Marque o desmarque **Adaptive Noise Estimation** según sea necesario.
5. Ajuste los deslizadores **Reduction (dB):**, **Smoothing (%)**:, **Whitening (%)**:, **Masking Depth:** y **Suppression:**.
6. Haga clic en **Reset Defaults (icono ↺)** para devolver todos los controles de NR4 a sus valores de fábrica.

### Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Noise Estimation: | Botón de opción | MMSE | MMSE / Brandt / Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla de verificación | Activado | On / Off | `NR4AdaptiveNoise` |
| Reduction (dB): | Deslizador | 10.0 | 0.0–40.0 | `NR4ReductionAmount` |
| Smoothing (%): | Deslizador | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Deslizador | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Deslizador | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Deslizador | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — |

`NR4NoiseEstimationMethod` se almacena como un entero 0–2 (MMSE=0, Brandt=1, Martin=2). `NR4ReductionAmount` se almacena internamente como valor × 10.

### Consejos

- Deje **Adaptive Noise Estimation** activado a menos que el nivel de ruido sea estable y desee bloquear la estimación.
- Aumente **Whitening (%)** para aplanar el ruido coloreado residual después de la reducción.
- Haga clic en **Reset Defaults (icono ↺)** para restaurar: MMSE / adaptativo activado / 10 dB / 0 / 0 / 0.50 / 0.50.
- Si la pestaña NR4 aparece atenuada en Windows, instale LLVM y reconstruya para habilitar el motor.

---

## Pestaña MNR

MNR es el motor de reducción de ruido MMSE-Wiener de AetherSDR, disponible solo en macOS. La activación de MNR está atenuada en las compilaciones de Windows y Linux.

### Antes de comenzar

- AetherSDR debe estar ejecutándose en macOS. La casilla de verificación **Enable MNR (macOS only)** solo está presente en las compilaciones de macOS.
- No se requiere conexión de radio para ajustar esta configuración.

### Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **MNR**.
3. Marque **Enable MNR (macOS only)** para activar el motor.
4. Arrastre el deslizador **Strength** para establecer la agresividad. 0 es la configuración más suave; 100 es la reducción máxima de ruido.

### Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla de verificación | *(leído del motor de audio al inicio)* | On / Off | `MnrEnabled` |
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

`MnrStrength` se conserva internamente como un valor normalizado entre 0.00 y 1.00.

### Consejos

- Comience con **Strength** en 100 y redúzcalo si nota artefactos en el habla o un sonido hueco. Los valores más bajos intercambian supresión de ruido por una reproducción de voz más natural.
- Debido a que el estado de activación inicial de MNR se lee en vivo del motor de audio al abrir el diálogo, la casilla de verificación refleja el estado actual del motor en lugar de un valor predeterminado guardado fijo.

### Solución de problemas

- **La pestaña MNR es visible pero "Enable MNR (macOS only)" no tiene efecto** — confirme que está ejecutando AetherSDR en macOS. La etiqueta de la casilla de verificación indica explícitamente la disponibilidad solo en macOS; en otras plataformas, el motor no está activo independientemente de esta configuración.

---

## Pestaña RN2

La pestaña **RN2** muestra información sobre el motor RNNoise. No hay parámetros ajustables en esta pestaña.

---

## Pestaña BNR

La pestaña **BNR** muestra información sobre el motor de reducción de ruido de NVIDIA. La intensidad se controla desde el menú superpuesto, no desde este diálogo. La activación de BNR está atenuada en las compilaciones sin el SDK de NVIDIA Broadcast.

---

## Pestaña DFNR

DFNR utiliza el motor DeepFilterNet3.

### Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Arrastre **Attenuation Limit** para establecer la atenuación máxima de ruido. Ajústelo a 0 para paso directo; ajústelo a 100 para atenuación máxima.
4. Arrastre **Post-Filter Beta** para aplicar supresión adicional del postfiltro. Déjelo en 0.00 si no se necesita supresión adicional.

### Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Attenuation Limit | Deslizador | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Deslizador | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

`DfnrPostFilterBeta` se almacena internamente como valor × 100.

### Consejos

- Reduzca **Attenuation Limit** si DeepFilterNet3 está suprimiendo en exceso y causando artefactos en los picos de voz.
- Deje **Post-Filter Beta** en 0.00 a menos que quede ruido residual después de ajustar **Attenuation Limit**.

---

## Controles de ventana

El diálogo de configuración de AetherDSP admite dos modos determinados por la configuración `FramelessWindow` (`Settings > Preferences > General > Frameless Window`). Cuando el modo sin marco está habilitado, se utiliza el chrome personalizado de v0.9.8. Cuando está deshabilitado, el diálogo utiliza las decoraciones de ventana estándar del sistema operativo.

### Controles del modo sin marco

Cuando el modo sin marco está activo:

### Barra de título

- 18 px de alto con un fondo degradado azul (`#5a7494` a `#1e2e3e`).
- Un glifo de asa (⋮⋮) a la izquierda y "AetherDSP Settings" en texto negro de 10 px en negrita.
- Tres botones de control de ventana a la derecha: **—** (Minimizar), **□** (Maximizar/Restaurar), **×** (Cerrar).

### Arrastrar para mover

- Haga clic y arrastre la barra de título para mover el diálogo.
- Haga doble clic en la barra de título para alternar entre los estados maximizado y restaurado.

### Redimensionamiento de 8 ejes

- Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento.
- La zona de selección para redimensionar se extiende 12 px desde los bordes del diálogo (el widget de contenido interno tiene un relleno de 6 px).

---

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de la configuración de AetherDSP](overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
