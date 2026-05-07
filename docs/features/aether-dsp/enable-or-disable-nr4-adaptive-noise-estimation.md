# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP permite ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo a los operadores afinar el equilibrio entre la supresión de ruido y la fidelidad del habla. Los seis módulos DSP se seleccionan mediante una fila de botones de alternancia en la parte superior; al hacer clic en un botón también se activa o desactiva ese motor.

## Antes de comenzar

- AetherSDR no necesita estar conectado a una radio para ajustar la configuración DSP.
- El motor NR seleccionado ya debe estar activo en su slice de recepción para que estos cambios tengan un efecto audible.
- Algunos motores DSP (MNR, BNR, RN2) dependen de la plataforma o son solo informativos. Para más detalles, consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md).

## Abrir la Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.

El diálogo aparece como una ventana sin marco con una barra de título personalizada. Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Haga clic y arrastre cualquier borde o esquina para redimensionar el diálogo.

La barra de título contiene tres controles de ventana:
- **— (Minimizar)**: Minimiza el diálogo.
- **□ (Maximizar)**: Maximiza o restaura el diálogo.
- **× (Cerrar)**: Cierra el diálogo.

## Seleccionar un motor DSP

En la parte superior del diálogo, seis pestañas de alternancia actúan tanto como selector como controles de activación/desactivación:

- **NR2** – Motor de reducción de ruido musical
- **NR4** – Supresión de ruido libspecbleach
- **MNR** – MMSE-Wiener de macOS (atenuado en compilaciones de Windows/Linux)
- **DFNR** – Supresión neuronal de ruido DeepFilterNet3
- **RN2** – RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** – NVIDIA Broadcast (atenuado en compilaciones sin el SDK de NVIDIA Broadcast)

Haga clic en un botón de alternancia para seleccionar su página de parámetros y activar o desactivar ese motor. Cuando NR2 está activado, AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

## Parámetros de NR2

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Gain Method** | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| **NPE Method** | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| **AE Filter (eliminación de artefactos)** | Activado (marcado) | Marcado / Sin marcar | `NR2AeFilter` |
| **Reduction:** | 1.50 | 0.50–2.00 | `NR2GainMax` |
| **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| **Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` |

Haga clic en **Reset Defaults (icono ↺)** para restaurar los valores predeterminados de NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20).

## Parámetros de NR4

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Noise Estimation:** | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| **Adaptive Noise Estimation** | Activado (marcado) | Marcado / Sin marcar | `NR4AdaptiveNoise` |
| **Reduction (dB):** | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Smoothing (%):** | 0 | 0–100 | `NR4SmoothingFactor` |
| **Whitening (%):** | 0 | 0–100 | `NR4WhiteningFactor` |
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

Haga clic en **Reset Defaults (icono ↺)** para restaurar los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50).

### Activar o desactivar la estimación de ruido adaptativa de NR4

Con la estimación de ruido adaptativa activada, NR4 rastrea los cambios en el entorno de ruido en tiempo real; desactivarla bloquea la estimación del piso de ruido a una instantánea estática, lo que puede ser adecuado para condiciones de ruido muy estables.

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation** para activar o desactivar la reestimación continua del piso de ruido.

El cambio surte efecto de inmediato y se guarda automáticamente en `NR4AdaptiveNoise`.

#### Consejos

- Si el piso de ruido en su banda es estable y consistente, desmarcar **Adaptive Noise Estimation** puede evitar que el estimador siga los cambios en el nivel de la señal y clasifique erróneamente el habla como ruido.
- Si el piso de ruido varía rápidamente (por ejemplo, durante aperturas de banda o con ruido impulsivo), deje **Adaptive Noise Estimation** marcado para que NR4 pueda rastrear las condiciones cambiantes.
- El selector **Noise Estimation Method** (MMSE, Brandt, Martin) determina cómo NR4 construye su modelo de ruido, independientemente de si el modo adaptativo está activado o desactivado. Cambiar el método puede afectar qué tan bien la estimación estática o adaptativa rastrea su piso de ruido.
- Haga clic en **Reset Defaults** en la pestaña NR4 para devolver todos los controles de NR4 a sus valores de fábrica (adaptativo activado, MMSE, 10 dB, 0, 0, 0.50, 0.50).

## Parámetros de MNR (solo macOS)

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Enable MNR (macOS only)** | Desactivado | Marcado / Sin marcar | `MnrEnabled` |
| **Strength** | 100 | 0–100 | `MnrStrength` |

El botón de alternancia de MNR está atenuado en compilaciones de Windows/Linux. La casilla de verificación **Enable MNR** activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.

## Parámetros de DFNR

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.

**Post-Filter Beta** aplica un post-filtro adicional para una supresión extra.

## Pestaña RN2

Seleccionar la pestaña RN2 muestra solo contenido informativo. No hay parámetros ajustables para RN2.

## Pestaña BNR

Seleccionar la pestaña BNR muestra los controles de reducción de ruido de NVIDIA Broadcast. El botón de alternancia de BNR está atenuado en compilaciones sin el SDK de NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto.

## Relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
