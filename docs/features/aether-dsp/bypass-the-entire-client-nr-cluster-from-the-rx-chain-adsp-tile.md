# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP proporciona la configuración avanzada para todos los motores de reducción de ruido del lado del cliente en AetherSDR. Incluye seis módulos DSP: NR2, NR4, MNR, DFNR, RN2 y BNR.

## Abrir el diálogo

- Desde la tira RX Chain, haga doble clic en el mosaico **ADSP**.
- Desde la cuadrícula DSP del VFO, haga clic en el botón **ADSP**.

## Ventana del diálogo

El diálogo tiene una barra de título sin marco con un glifo de agarre (⋮⋮) a la izquierda. La barra de título incluye tres botones:

- — (Minimizar) — Minimiza el diálogo.
- □ (Maximizar) — Maximiza o restaura el diálogo.
- × (Cerrar) — Cierra el diálogo.

Arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. Arrastre cualquier borde o esquina para redimensionar (zona de redimensionamiento de 6 px).

La posición y el tamaño del diálogo se guardan automáticamente entre sesiones mediante la clave de ajuste `AetherDspDialogGeometry`.

El diálogo utiliza estilos basados en el tema aplicados a través del `ThemeManager`. Los colores se derivan del tema de color activo en lugar de valores fijos.

## Fila de conmutadores

La parte superior del diálogo contiene seis botones de conmutación que funcionan tanto como selectores de pestaña como controles de habilitación/deshabilitación del motor:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Reducción de ruido espectral libspecbleach
- **MNR** — Reducción de ruido MMSE-Wiener de macOS (atenuado en Windows/Linux)
- **DFNR** — Reducción de ruido neuronal DeepFilterNet3
- **RN2** — Reducción de ruido neuronal RNNoise
- **BNR** — Reducción de ruido neuronal NVIDIA Broadcast (atenuado sin el SDK de NVIDIA Broadcast)

Al hacer clic en un conmutador se activa ese motor y se selecciona su pestaña. Al hacer clic nuevamente se desactiva el motor. Solo un motor puede estar activo a la vez: NR2, NR4 y DFNR son mutuamente excluyentes. MNR y BNR pueden superponerse en algunas compilaciones.

Cada botón de conmutación tiene un nombre accesible que incluye su etiqueta (por ejemplo, "método de reducción de ruido NR2") para tecnologías de asistencia y soporte del puente de automatización.

El último motor NR del cliente activo se guarda en el ajuste `LastClientNr`. Si DFNR no está disponible y estaba activo previamente, la preferencia se borra automáticamente.

## Pestaña NR2

Controles para el motor de reducción de ruido musical.

| Control                          | Tipo         | Predeterminado | Rango                | Clave de ajuste       | Comportamiento                                                        |
|----------------------------------|--------------|----------------|----------------------|-------------------|-----------------------------------------------------------------|
| Gain Method                      | Botón de opción | Gamma   | Linear, Log, Gamma, Trained | `NR2GainMethod`   | Selecciona la asignación de la curva de ganancia usada por NR2. Se almacena como entero 0-3.  |
| NPE Method                       | Botón de opción | OSMS    | OSMS, MMSE, NSTAT    | `NR2NpeMethod`    | Selecciona el estimador de potencia de ruido. Se almacena como entero 0-2.           |
| AE Filter (eliminación de artefactos) | Casilla de verificación     | True    | —                    | `NR2AeFilter`     | Activa el post-filtro anti-artefactos.                          |
| Reduction:                       | Deslizador       | 1.50    | 0.50-2.00            | `NR2GainMax`      | Establece la profundidad máxima de reducción NR2. El deslizador almacena el valor*100.      |
| Smoothing:                       | Deslizador       | 0.85    | 0.50-0.98            | `NR2GainSmooth`   | Controla la suavidad con la que la estimación de ruido sigue los cambios.        |
| Threshold:                       | Deslizador       | 0.20    | 0.05-0.50            | `NR2Qspp`         | Establece el umbral de probabilidad de presencia de voz.                     |
| Reset Defaults (icono ↺)          | Botón pulsador  | —       | —                    | —                 | Restaura los valores predeterminados de la pestaña NR2 (Gamma/OSMS/AE activados, 1.50/0.85/0.20).    |

Los deslizadores de esta pestaña utilizan estilos basados en el tema mediante `applyPrimarySliderStyle()`.

## Pestaña NR4

Controles para el motor de reducción de ruido espectral libspecbleach.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-------------|----------|
| Noise Estimation: | Botón de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador de piso de ruido (se almacena como entero 0-2). |
| Adaptive Noise Estimation | Casilla de verificación | True | — | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| Reduction (dB): | Deslizador | 10.0 | 0.0-40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. |
| Smoothing (%): | Deslizador | 0 | 0-100 | `NR4SmoothingFactor` | Suavizado en el dominio del tiempo de la estimación de ruido NR4. |
| Whitening (%): | Deslizador | 0 | 0-100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| Masking Depth: | Deslizador | 0.50 | 0.00-1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| Suppression: | Deslizador | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` | Fuerza general de supresión NR4. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activados, 10 dB, 0, 0, 0.50, 0.50). |

Los deslizadores de esta pestaña utilizan estilos basados en el tema mediante `applyPrimarySliderStyle()`.

**Nota:** NR4 requiere LLVM (clang-cl) en Windows. El conmutador está atenuado si LLVM no está instalado. Instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

## Pestaña MNR

Controles para el motor de reducción de ruido MMSE-Wiener de macOS. Esta pestaña y sus controles solo están disponibles en compilaciones de macOS.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-------------|----------|
| Enable MNR (solo macOS) | Casilla de verificación | — | — | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee en vivo desde AudioEngine. |
| Strength | Deslizador | 100 | 0-100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). Se guarda como valor normalizado 0.00-1.00. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de MNR (Strength 100). |

## Pestaña DFNR

Controles para el motor de reducción de ruido neuronal DeepFilterNet3.

**Nota:** DeepFilterNet3 es un sistema avanzado de reducción de ruido basado en redes neuronales que utiliza aprendizaje profundo para suprimir el ruido preservando la calidad de la voz. Puede requerir recursos significativos de CPU. DFNR requiere que DeepFilterNet esté configurado y que AetherSDR sea reconstruido. Si no está disponible, el conmutador DFNR muestra una información sobre herramientas explicando esto.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-------------|----------|
| Attenuation Limit | Deslizador | 100 | 0-100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = supresión máxima. |
| Post-Filter Beta | Deslizador | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para mayor supresión. El deslizador almacena el valor*100 internamente. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de DFNR (Attenuation 100, Beta 0.00). |

## Pestaña RN2

Controles para el motor de reducción de ruido neuronal RNNoise.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|----------------|-------|-------------|----------|
| Noise Floor (mezcla seca RN2) | Deslizador | 0 | 0-100 | — | Establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce supresión completa (silencio entre frases); 10-20% mantiene un piso de silencio constante para que el receptor siga sonando vivo. Afecta solo al audio recibido; el denoizador de transmisión no cambia. Se guarda mediante `Rn2SettingsModel` y se expone a la cadena DSP a través de la señal `rn2DryMixChanged` de `AetherDspWidget`. |
| Reset Defaults (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de RN2 (Noise Floor 0). |

## Pestaña BNR

Selecciona la página de denoizado neuronal NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto. El conmutador está atenuado en compilaciones sin el SDK de NVIDIA Broadcast. El botón Reset Defaults no tiene efecto en esta pestaña.

## Omitir todos los motores NR del cliente

Para deshabilitar rápidamente toda la reducción de ruido del lado del cliente sin abrir el diálogo de Configuración de AetherDSP:

1. Localice el mosaico **ADSP** en la tira RX Chain.
2. Haga doble clic en el mosaico **ADSP** para abrir la Configuración de AetherDSP.
3. En la fila de conmutadores en la parte superior, haga clic en cada conmutador de reducción de ruido activo (iluminado) para desactivarlo.
4. Continúe hasta que todos los conmutadores estén atenuados.

El mosaico ADSP se actualiza para reflejar el estado omitido. Ahora ningún motor NR del cliente está activo, devolviendo el audio al flujo de audio crudo segmentado de la radio.

## Consejos

- Los seis conmutadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) funcionan tanto como selectores de pestaña como controles de habilitación/deshabilitación del motor.
- NR2, NR4 y DFNR son mutuamente excluyentes: solo uno puede estar activo a la vez.
- MNR y BNR pueden superponerse con otros motores en algunas compilaciones.
- El botón Reset Defaults (icono ↺) en cada pestaña restaura los parámetros de ese motor a sus valores predeterminados.
- Los ajustes se guardan entre sesiones.
- El diálogo utiliza estilos basados en el tema. Los colores se toman del tema de color activo en lugar de valores fijos.
- El último motor NR del cliente activo se guarda; si DFNR deja de estar disponible, la preferencia almacenada se borra automáticamente.
- La pestaña NR2 incluye un deslizador "Reduction:" (no "Reduction Depth:") y un deslizador "Threshold:" (no "Voice Threshold:").
