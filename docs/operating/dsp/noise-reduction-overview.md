# Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR ofrece cuatro motores de reducción de ruido del lado del cliente. Esta página explica qué hace cada uno y cómo decidir cuál usar, para que pueda abrir la pestaña correcta en AetherDSP Settings y comenzar a ajustar.

## Antes de comenzar

- Abra `Settings > AetherDSP Settings...` para acceder al diálogo AetherDSP Settings.
- No se requiere una conexión de radio para configurar estos parámetros.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña del motor que desea usar: **NR2**, **NR4**, **DFNR** o **MNR**.
3. Ajuste los controles de esa pestaña. Los ajustes se guardan inmediatamente; no hay botón Apply.
4. Si desea restaurar una pestaña a sus valores predeterminados de fábrica, haga clic en **Reset Defaults** en la parte inferior de la pestaña NR2 o NR4.

## Qué hace cada control

### Pestaña NR2 — reducción de ruido musical

NR2 es un motor en el dominio de la frecuencia enfocado en suprimir los artefactos tonales de "ruido musical" que son comunes en SSB y en trabajo con señales débiles. Úselo cuando escuche una calidad temblorosa o fluctuante en el ruido, en lugar de un silbido plano.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Gain Method | Botones de opción | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| NPE Method | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| AE Filter (eliminación de artefactos) | Casilla | Habilitado | — | `NR2AeFilter` |
| Reduction Depth: | Control deslizante | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | Control deslizante | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | Control deslizante | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Reset Defaults | Botón | — | — | — |

**Gain Method** selecciona la curva utilizada para calcular cuánta ganancia aplicar a cada bin espectral. Gamma es el valor predeterminado y es adecuado para la mayoría del trabajo de voz. Trained usa un modelo construido a partir de muestras reales de voz y ruido, y puede rendir mejor en señales débiles de DX. Linear y Log ofrecen asignaciones más simples si desea un comportamiento predecible y auditable.

**NPE Method** controla cómo NR2 estima el piso de ruido. OSMS rastrea el piso mediante un mínimo continuo y es robusto con ruido estable. MMSE minimiza el error cuadrático medio de estimación. NSTAT se adapta a ruido que cambia rápidamente con el tiempo.

**AE Filter (eliminación de artefactos)** aplica un postfiltro para reducir el repique y los residuos de ruido musical. Déjelo habilitado a menos que esté comparando deliberadamente la salida bruta de NR2.

**Reduction Depth:** establece con qué agresividad NR2 atenúa el ruido. Valores más altos suprimen más ruido, pero pueden distorsionar la voz.

**Smoothing:** controla la rapidez con que la estimación de ruido sigue los cambios. Valores más altos producen una estimación más estable, pero reaccionan más lentamente ante ráfagas repentinas de ruido.

**Voice Threshold:** es el umbral de probabilidad de presencia de voz por debajo del cual NR2 trata un bin como ruido. Valores más bajos protegen la voz más débil, pero dejan pasar más ruido.

---

### Pestaña NR4 — reducción de banda ancha con libspecbleach

NR4 está construido sobre libspecbleach y es adecuado para ruido de banda ancha: interferencia de red eléctrica, ruido de banda y ruido atmosférico bajo señales SSB. Ofrece reducción calibrada explícitamente en dB y una etapa de blanqueo espectral.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Noise Estimation Method | Botones de opción | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | Casilla | Habilitado | — | `NR4AdaptiveNoise` |
| Reduction (dB): | Control deslizante | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Reset Defaults | Botón | — | — | — |

**Noise Estimation Method** establece el estimador del piso de ruido. SPP-MMSE equilibra la estimación de ruido con la preservación de la voz. Brandt usa suavizado recursivo en bandas de frecuencia críticas y maneja bien el ruido no estacionario. Martin usa mínimos espectrales continuos y es robusto cuando el piso de ruido cambia lentamente.

**Adaptive Noise Estimation** habilita la reestimación continua del piso de ruido. Desactívelo solo si desea fijar la estimación a una instantánea.

**Reduction (dB):** es el control principal de profundidad. Comience con el valor predeterminado de 10.0 dB y auméntelo solo según sea necesario; valores altos en anchos de banda amplios pueden degradar la calidad de voz.

**Smoothing (%):** aplica suavizado en el dominio temporal a la estimación de ruido. Auméntelo para estabilizar la estimación ante ruido en ráfagas.

**Whitening (%):** aplana la forma espectral del ruido residual después de la reducción, cambiando un piso de ruido con color por un silbido más plano.

**Masking Depth:** controla cuán profundamente se aplica la supresión por enmascaramiento espectral.

**Suppression:** establece la intensidad general de supresión de NR4.

---

### Pestaña DFNR — DeepFilterNet3

DFNR ejecuta DeepFilterNet3, un filtro de red neuronal. Opera sobre la cadena de audio y no requiere estimación del piso de ruido. Es la opción más eficaz para la inteligibilidad en bandas congestionadas, pero tiene el mayor costo de CPU de los cuatro motores.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Attenuation Limit | Control deslizante | 100 dB | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | Control deslizante | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** limita la atenuación máxima que DeepFilterNet3 puede aplicar. En 0, deja pasar la señal sin cambios; en 100, aplica la atenuación máxima. Redúzcalo en señales fuertes para evitar la supresión excesiva.

**Post-Filter Beta** aplica un postfiltro adicional sobre la salida de DeepFilterNet3 para una supresión extra. El valor predeterminado de 0.00 lo deshabilita. Auméntelo con precaución; valores altos pueden degradar la calidad de la voz.

---

### Pestaña MNR — reducción MMSE-Wiener para macOS

MNR es un filtro MMSE-Wiener con suavizado de ganancia asimétrico. Solo está disponible en macOS.

| Control | Tipo | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla | Leído desde el motor de audio | — | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** activa el motor. El estado inicial refleja lo que informa el motor de audio, no un valor predeterminado almacenado.

**Strength** establece la agresividad. 0 es leve; 100 es la supresión máxima.

---

### Cómo elegir entre los motores

| Situación | Motor sugerido |
|---|---|
| Artefactos de ruido musical, fluctuación en el ruido SSB | NR2 |
| Ruido atmosférico de banda ancha o interferencia de red eléctrica | NR4 |
| Máxima inteligibilidad, CPU disponible | DFNR |
| Ruta de audio del sistema macOS, procesamiento ligero | MNR |

No está limitado a un solo motor a la vez; los botones de bandeja de cada motor los activan de forma independiente. Comience con uno y agregue un segundo solo si el primero es insuficiente.

## Consejos

- En la pestaña NR2, haga clic en **Reset Defaults** para volver a Gamma / OSMS / AE Filter activado / 1.50 / 0.85 / 0.20 en cualquier momento.
- En la pestaña NR4, haga clic en **Reset Defaults** para volver a SPP-MMSE / adaptativo activado / 10.0 dB / 0 / 0 / 0.50 / 0.50.
- La pestaña MNR está presente en todas las plataformas, pero **Enable MNR (macOS only)** no tiene efecto en Linux ni en Windows.
- Establecer el **Attenuation Limit** de DFNR en 0 deshabilita la supresión de DeepFilterNet3 sin cerrar el diálogo, lo que es útil para comparaciones A/B.

## Relacionados

- [Descripción general de AetherDSP Settings](../../features/aether-dsp/overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](../../features/aether-dsp/adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación adaptativa de ruido de NR4](../../features/aether-dsp/enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](../../features/aether-dsp/tune-nr4-masking-depth-and-
