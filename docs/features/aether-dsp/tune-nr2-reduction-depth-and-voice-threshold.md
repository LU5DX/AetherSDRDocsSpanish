# Ajustar la profundidad de reducción y el umbral de voz de NR2

Controle cuán agresivamente NR2 suprime el ruido y cuán sensiblemente detecta la voz. Estos dos controles — **Reduction Depth:** y **Voice Threshold:** — establecen el equilibrio fundamental entre la supresión de ruido y la preservación de la voz.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio para ajustar estos parámetros.
- NR2 debe estar habilitado en el slice que desea afectar. Estos controles ajustan los parámetros del motor; no activan NR2 por sí mismos.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Arrastre el control deslizante **Reduction Depth:** para establecer cuánto ruido puede eliminar NR2. Los valores más altos suprimen más ruido; los valores más bajos preservan un sonido más natural a costa de menor reducción.
4. Arrastre el control deslizante **Voice Threshold:** para establecer el umbral de probabilidad de presencia de voz. Los valores más bajos hacen que NR2 trate señales más débiles como voz y aplique menos reducción; los valores más altos requieren una señal más fuerte antes de que NR2 reduzca la supresión.
5. Los cambios surten efecto de inmediato. No se necesita ningún paso de confirmación.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Reduction Depth:** | 1.50 | 0.50 – 2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción de NR2. Los valores más bajos producen una reducción más suave; los valores más altos producen una supresión de ruido más profunda con mayor riesgo de distorsión de la voz. |
| **Voice Threshold:** | 0.20 | 0.05 – 0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. Los valores más bajos preservan la voz débil pero pueden dejar pasar más ruido; los valores más altos suprimen más ruido pero pueden recortar la voz de bajo nivel. |
| **Smoothing:** | 0.85 | 0.50 – 0.98 | `NR2GainSmooth` | Controla la rapidez con la que la estimación de ruido sigue los cambios. Los valores más altos producen una estimación más estable pero de reacción más lenta. |
| **AE Filter (artifact elimination)** | On | On / Off | `NR2AeFilter` | Activa o desactiva el postfiltro anti-artefactos que reduce el ruido musical típico de la reducción de ruido en el dominio de la frecuencia. |
| **Gain Method** | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` | Selecciona el mapeo de curva de ganancia utilizado por NR2. |
| **NPE Method** | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. |
| **Reset Defaults** | — | — | — | Restaura todos los valores de la pestaña NR2 a sus valores predeterminados: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20. |

## Consejos

- Comience con **Reduction Depth:** en el valor predeterminado de 1.50 y auméntelo solo si el ruido sigue siendo claramente audible después de habilitar NR2.
- Si la voz suena hueca o distorsionada tras aumentar **Reduction Depth:**, reduzca ligeramente **Voice Threshold:** para que NR2 identifique los segmentos de voz con mayor facilidad y reduzca la supresión.
- Si escucha artefactos de ruido musical (una calidad temblorosa o burbujeante en el ruido residual), verifique que **AE Filter (artifact elimination)** esté marcado.
- Haga clic en **Reset Defaults** para devolver la pestaña NR2 completa a sus valores de fábrica si los ajustes se vuelven difíciles de gestionar.

## Solución de problemas

- **El ruido apenas se reduce incluso con la profundidad de reducción máxima** — Es posible que **NPE Method** haya perdido el rastro del piso de ruido. Intente cambiar **NPE Method** a MMSE o NSTAT, o habilite un escenario de ruido de variación más lenta aumentando **Smoothing:**.
- **La voz suena recortada o sobreprocessada** — Es probable que **Reduction Depth:** sea demasiado alto o que **Voice Threshold:** sea demasiado alto, lo que provoca que los cuadros de voz sean tratados como ruido. Reduzca **Reduction Depth:** y disminuya **Voice Threshold:** hacia 0.05.
- **Los ajustes se revierten después de reiniciar** — Esto no debería ocurrir, ya que los valores se persisten de inmediato al cambiarlos. Si ocurre, verifique que AetherSDR tenga acceso de escritura a su ubicación de almacenamiento de configuración.

## Relacionados

- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
