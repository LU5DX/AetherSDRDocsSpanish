# Elección de la reducción de ruido adecuada: NR2, NR4, DFNR, MNR

AetherSDR proporciona cuatro motores de reducción de ruido del lado del cliente. Esta página explica qué hace cada motor, cuándo utilizarlo y dónde encontrar sus controles.

## Antes de comenzar

- Abra AetherDSP Settings mediante `Settings > AetherDSP Settings...`.
- Los motores de reducción de ruido se seleccionan y activan de forma independiente desde este diálogo — el diálogo solo configura sus parámetros. Consulte los controles de su receptor slice (receptor de segmento) para habilitar un motor NR específico.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña del motor que desea configurar: `NR2 (tab)`, `NR4 (tab)`, `MNR (tab)` o `DFNR (tab)`.
3. Ajuste los parámetros según se describe a continuación.
4. Los cambios surten efecto de inmediato. No se requiere ningún botón Apply ni OK.
5. Para restaurar un motor a su estado de fábrica, haga clic en `Reset Defaults` en su pestaña.

## Qué hace cada control

### NR2

Reducción de ruido musical en dominio espectral. Use NR2 para voz SSB en pisos de ruido moderados a elevados cuando sea importante preservar la naturalidad del habla. Su control `Voice Threshold:` permite proteger el habla suave para que no sea suprimida.

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Gain Method | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` |
| NPE Method | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` |
| AE Filter (artifact elimination) | True (on) | on / off | `NR2AeFilter` |
| Reduction Depth: | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Smoothing: | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Voice Threshold: | 0.20 | 0.05–0.50 | `NR2Qspp` |

**Gain Method** selecciona cómo se calcula la curva de ganancia. Gamma se ajusta a los patrones típicos de amplitud del habla y es el punto de partida recomendado. Trained utiliza un modelo entrenado con muestras reales de voz y ruido. Linear y Log son mapeos más simples.

**NPE Method** selecciona el estimador de potencia de ruido. OSMS rastrea el piso de ruido mediante una estimación de mínimo continuo. MMSE minimiza el error de estimación esperado. NSTAT se adapta al ruido que cambia con el tiempo.

**AE Filter (artifact elimination)** aplica un postfiltro que reduce el repique y los artefactos musicales comunes en la reducción de ruido en dominio frecuencial. Déjelo activado a menos que necesite comparar la salida NR sin procesar.

**Reduction Depth:** establece la profundidad máxima de supresión. Valores más altos eliminan más ruido, pero pueden distorsionar el habla.

**Smoothing:** controla la rapidez con que se adapta la estimación de ruido. Valores más altos producen una estimación más estable, pero con respuesta más lenta ante cambios en el ruido.

**Voice Threshold:** establece el umbral de probabilidad de presencia de voz. Valores más bajos preservan el habla suave, pero pueden dejar pasar más ruido.

---

### NR4

Reducción basada en libspecbleach. Use NR4 cuando desee un control explícito calibrado en dB sobre la cantidad de ruido eliminado, o cuando el piso de ruido sea relativamente estacionario y quiera ajustar el blanqueo del ruido residual.

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Noise Estimation Method | SPP-MMSE | SPP-MMSE / Brandt / Martin | `NR4NoiseEstimationMethod` |
| Adaptive Noise Estimation | True (on) | on / off | `NR4AdaptiveNoise` |
| Reduction (dB): | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| Smoothing (%): | 0 | 0–100 | `NR4SmoothingFactor` |
| Whitening (%): | 0 | 0–100 | `NR4WhiteningFactor` |
| Masking Depth: | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Suppression: | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

**Noise Estimation Method** selecciona el estimador del piso de ruido. SPP-MMSE equilibra la estimación de ruido con la preservación del habla. Brandt utiliza suavizado recursivo sobre bandas críticas y es adecuado para ruido no estacionario. Martin utiliza mínimos espectrales continuos y es robusto para pisos de ruido que varían lentamente.

**Adaptive Noise Estimation** habilita la re-estimación continua del piso de ruido. Desactívelo si desea fijar la estimación tomada al inicio (útil con un piso de ruido muy estable).

**Reduction (dB):** establece la profundidad máxima de reducción en dB. 10 dB es un punto de partida conservador; valores superiores a 20 dB pueden introducir artefactos en la voz.

**Smoothing (%):** aplica suavizado en el dominio temporal a la estimación de ruido. 0 significa que no hay suavizado adicional más allá del comportamiento propio del estimador.

**Whitening (%):** aplana la forma espectral del ruido residual. Aumente este valor si escucha ruido residual coloreado (tonal) después de la reducción.

**Masking Depth:** controla la agresividad con que se aplica el enmascaramiento espectral.

**Suppression:** establece la intensidad general de supresión. Redúzcalo si NR4 suena excesivamente procesado.

---

### MNR

Reducción MMSE-Wiener con suavizado de ganancia asimétrico. MNR solo está activo en macOS.

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Enable MNR (macOS only) | (leído del motor de audio) | on / off | `MnrEnabled` |
| Strength | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** activa el motor. El estado inicial refleja el estado actual del motor de audio.

**Strength** establece la agresividad. 0 es leve; 100 es la supresión máxima.

---

### DFNR

Reducción de ruido por aprendizaje profundo con DeepFilterNet3. Use DFNR para obtener la mayor calidad de supresión en modos de voz, especialmente cuando otros motores dejan ruido residual o artefactos. DFNR requiere más CPU que NR2 o NR4.

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Attenuation Limit** limita la atenuación máxima de ruido. 0 es paso directo (sin reducción); 100 es el máximo. Redúzcalo si DFNR suprime demasiado agresivamente las señales débiles.

**Post-Filter Beta** aplica un postfiltro adicional sobre la salida de DeepFilterNet3 para una supresión extra. El valor predeterminado 0.00 lo desactiva. Auméntelo con precaución — valores altos pueden degradar la calidad del habla.

---

### RN2 y BNR

Las pestañas `RN2 (tab)` (RNNoise) y `BNR (tab)` (NVIDIA) no tienen parámetros ajustables en este diálogo. RN2 no tiene controles. La intensidad de BNR se controla desde el menú de superposición (overlay).

## Consejos

- Comience con NR2 en sus valores predeterminados (Gamma, OSMS, AE activado, Reduction Depth 1.50) antes de recurrir a DFNR. NR2 consume menos CPU y funciona bien con el ruido típico de SSB.
- Si NR2 deja un tono musical residual, intente cambiar `NPE Method` de OSMS a NSTAT, o habilite NR4 con un valor bajo de `Whitening (%)`.
- En macOS, MNR y DFNR pueden ejecutarse simultáneamente entre sí o junto con NR2/NR4; verifique la carga de CPU antes de apilar múltiples motores.
- `Attenuation Limit` de DFNR en 100 puede sonar artificial en CW o modos digitales. Configúrelo en 0 (paso directo) en esos modos.
- Haga clic en `Reset Defaults` en cualquier pestaña para devolver todos los parámetros de ese motor a los valores de fábrica sin afectar a otros motores.

## Resolución de problemas

- **La voz suena apagada o robótica después de habilitar NR2** — `Reduction Depth:` está configurado demasiado alto. Redúzcalo por debajo de 1.50, o disminuya `Voice Threshold:` para proteger mejor el habla.
- **NR4 parece no tener efecto** — Verifique que `Reduction (dB):` esté por encima de 0.0 y `Suppression:` por encima de 0.00. Ambos tienen valores predeterminados que producen una reducción audible, pero pueden haber sido modificados.
- **Los controles de la pestaña MNR aparecen atenuados o no están disponibles** — MNR solo está disponible en macOS. En Linux y Windows la pestaña está presente, pero el motor está inactivo.
- **DFNR no produce salida** — `Attenuation Limit` configurado en 0 es paso directo. Auméntelo por encima de 0.

## Relacionados

- [Descripción general de AetherDSP Settings](../../features/aether-dsp/overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](../../features/aether-dsp/tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](../../features/aether-dsp/switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](../../features/aether-dsp/change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](../../features/aether-dsp/adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación adaptativa de ruido de NR4](../../features/aether-dsp/enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](../../features/aether-dsp/tune-nr4-masking-depth-and-suppression
