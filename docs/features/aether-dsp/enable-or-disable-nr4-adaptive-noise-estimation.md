# Configuración de AetherDSP

El cuadro de diálogo Configuración de AetherDSP ajusta los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), lo que permite a los operadores ajustar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o se ignora ese motor.

## Antes de comenzar

- AetherSDR no necesita estar conectado a una radio para ajustar la configuración de DSP.
- El motor de NR seleccionado ya debe estar activo en su slice de recepción para que estos cambios tengan un efecto audible.
- Algunos motores DSP (MNR, BNR, RN2, NR4) dependen de la plataforma o son solo informativos. Para obtener más detalles, consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md).

## Abrir Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.

El cuadro de diálogo aparece con una barra de título de degradado sin marco de 18 px que muestra un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. Haga clic y arrastre cualquier borde o esquina para redimensionar el diálogo. La zona de redimensionamiento de 6 px rodea el widget de contenido interno; el cursor cambia para indicar la dirección del redimensionamiento.

La barra de título contiene tres controles de ventana:
- **— (Minimizar)**: Minimiza el diálogo.
- **□ (Maximizar)**: Maximiza o restaura el diálogo.
- **× (Cerrar)**: Cierra el diálogo.

La geometría del diálogo se guarda automáticamente en el ajuste `AetherDspDialogGeometry` y se restaura en el próximo inicio.

El diálogo utiliza el tema de color definido por el tema actual de AetherSDR (clave de ajuste `theme/aetherDsp`). Los deslizadores se representan con el estilo `applyPrimarySliderStyle` aplicado por el administrador de temas.

## Seleccionar un motor DSP

En la parte superior del diálogo, seis pestañas de conmutación actúan tanto como selector como controles de activación/desactivación:

- **NR2** – Motor de reducción de ruido musical
- **NR4** – Supresión de ruido libspecbleach (atenuado en compilaciones de Windows sin LLVM/clang-cl)
- **MNR** – MMSE-Wiener para macOS (atenuado en compilaciones de Windows/Linux)
- **DFNR** – Supresión de ruido neuronal DeepFilterNet3
- **RN2** – RNNoise
- **BNR** – NVIDIA Broadcast (atenuado en compilaciones sin NVIDIA Broadcast SDK)

Haga clic en un conmutador para seleccionar su página de parámetros y activar o ignorar ese motor. Cuando NR2 está activado, AudioEngine procesa la exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

## Parámetros de NR2

| Control | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|
| **Gain Method** | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| **NPE Method** | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| **AE Filter (eliminación de artefactos)** | Habilitado (marcado) | Marcado / Desmarcado | `NR2AeFilter` |
| **Reduction:** | 1.50 | 0.50–2.00 | `NR2GainMax` |
| **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| **Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` |

- **Gain Method** selecciona la asignación de la curva de ganancia utilizada por NR2. Se almacena como entero 0-3 en el orden Linear, Log, Gamma, Trained.
- **NPE Method** selecciona el estimador de potencia de ruido. Se almacena como entero 0-2.
- **AE Filter (eliminación de artefactos)** activa el post-filtro anti-artefactos.
- **Reduction:** establece la profundidad máxima de reducción de NR2. El deslizador almacena valor*100 internamente.
- **Smoothing:** controla la suavidad con la que la estimación de ruido sigue los cambios.
- **Threshold:** establece el umbral de probabilidad de presencia de habla.

Haga clic en **Reset Defaults (icono ↺)** para restaurar los valores predeterminados de NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20).

## Parámetros de NR4

| Control | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|
| **Noise Estimation:** | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| **Adaptive Noise Estimation** | Habilitado (marcado) | Marcado / Desmarcado | `NR4AdaptiveNoise` |
| **Reduction (dB):** | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

- **Noise Estimation:** selecciona el estimador de piso de ruido utilizado por NR4. Se almacena como entero 0-2.
- **Adaptive Noise Estimation** habilita la re-estimación continua del piso de ruido.
- **Reduction (dB):** establece la reducción máxima de ruido de NR4 en dB. El deslizador almacena valor*10.
- **Smoothing (%):** aplica suavizado en el dominio del tiempo de la estimación de ruido de NR4.
- **Whitening (%):** aplana la forma espectral del ruido residual.
- **Masking Depth:** controla la profundidad del enmascaramiento espectral.
- **Suppression:** establece la fuerza general de supresión de NR4.

Haga clic en **Reset Defaults (icono ↺)** para restaurar los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50).

### Habilitar o deshabilitar la estimación de ruido adaptativa de NR4

Con la estimación de ruido adaptativa habilitada, NR4 sigue los cambios en el entorno de ruido en tiempo real; deshabilitarla bloquea la estimación del piso de ruido a una instantánea estática, lo que puede ser adecuado para condiciones de ruido muy estables.

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation** para habilitar o deshabilitar la re-estimación continua del piso de ruido.

El ajuste surte efecto de inmediato y se guarda automáticamente en `NR4AdaptiveNoise`.

#### Consejos

- Si el piso de ruido en su banda es estable y constante, desmarcar **Adaptive Noise Estimation** puede evitar que el estimador siga los cambios en el nivel de la señal y clasifique erróneamente el habla como ruido.
- Si el piso de ruido varía rápidamente (por ejemplo, durante aperturas de banda o con ruido impulsivo), deje **Adaptive Noise Estimation** marcado para que NR4 pueda seguir las condiciones cambiantes.
- El selector **Noise Estimation Method** (MMSE, Brandt, Martin) determina cómo NR4 construye su modelo de ruido independientemente de si el modo adaptativo está activado o desactivado. Cambiar el método puede afectar la precisión con la que la estimación estática o adaptativa sigue su piso de ruido.
- Haga clic en **Reset Defaults** en la pestaña NR4 para devolver todos los controles de NR4 a sus valores de fábrica (adaptativo activado, MMSE, 10 dB, 0, 0, 0.50, 0.50).

### Disponibilidad de NR4 en Windows

NR4 utiliza la biblioteca libspecbleach, que requiere el compilador clang-cl en Windows. Si la pestaña NR4 está atenuada, instale LLVM desde llvm.org y recompile AetherSDR para habilitar la compatibilidad con NR4.

## Parámetros de MNR (solo macOS)

| Control | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|
| **Enable MNR (macOS only)** | Off | Marcado / Desmarcado | `MnrEnabled` |
| **Strength** | 100 | 0–100 | `MnrStrength` |

El conmutador MNR está atenuado en las compilaciones de Windows/Linux. La casilla **Enable MNR** habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. **Strength** ajusta la agresividad de MNR (0 suave, 100 máxima) y se guarda como un valor normalizado de 0.00–1.00.

## Parámetros de DFNR

| Control | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.

**Post-Filter Beta** aplica un post-filtro adicional para una supresión extra. El deslizador almacena valor*100 internamente.

## Pestaña RN2

Al seleccionar la pestaña RN2 se muestra información del motor RNNoise y se aloja el deslizador ajustable de mezcla seca Noise Floor.

| Control | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|
| **Noise Floor (RN2 dry mix)** | 0 | 0–100 | Ninguna (guardado por `Rn2SettingsModel`) |

**Noise Floor (RN2 dry mix)** establece el porcentaje de la señal original que RN2 deja bajo el audio denoizado. Cero produce una supresión total (silencio entre frases); 10–20% mantiene un piso de ruido bajo constante para que el receptor siga sonando vivo.

El ajuste afecta solo al audio recibido; el denoizador de transmisión no cambia. Se expone a la cadena DSP mediante la señal `rn2DryMixChanged` de AetherDspWidget. No hay clave de ajuste: el valor se guarda mediante `Rn2SettingsModel`.

Haga clic en **Reset Defaults (icono ↺)** en la pestaña RN2 para devolver el deslizador Noise Floor a 0.

## Pestaña BNR

Al seleccionar la pestaña BNR se muestran los controles de reducción de ruido de NVIDIA Broadcast. El conmutador BNR está atenuado en las compilaciones sin NVIDIA Broadcast SDK. La intensidad se controla desde el menú superpuesto.

## Relacionado

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
