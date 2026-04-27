# Ajustar la profundidad de reducción y el umbral de voz de NR2

Esta página explica cómo ajustar la profundidad máxima de reducción de ruido y el umbral de presencia de voz de NR2 en AetherSDR. Modificar estos dos controles deslizantes permite equilibrar la agresividad con la que NR2 suprime el ruido frente a la fidelidad con la que preserva la voz.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar estos ajustes.
- NR2 debe estar activo en un slice de receptor para que los cambios surtan efecto de forma audible de inmediato.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. En el diálogo AetherDSP Settings, haga clic en la pestaña **NR2**.
3. Localice el control deslizante **Reduction Depth:**. Arrástrelo hacia la izquierda para reducir la supresión o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del control (valor predeterminado: `1.50`).
4. Localice el control deslizante **Voice Threshold:**. Arrástrelo hacia la izquierda para hacer la detección de voz más sensible (preserva la voz débil) o hacia la derecha para elevar el umbral (deja pasar menos ruido durante las pausas). El valor actual se muestra a la derecha del control (valor predeterminado: `0.20`).
5. Los cambios surten efecto de inmediato y se guardan automáticamente.

Para restaurar ambos controles a sus valores predeterminados junto con todos los demás parámetros de NR2, haga clic en **Reset Defaults** en la parte inferior derecha de la pestaña **NR2**.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave almacenada | Comportamiento |
|---|---|---|---|---|
| **Reduction Depth:** | `1.50` | `0.50`–`2.00` | `NR2GainMax` | Establece la profundidad máxima de reducción de ruido de NR2. Valores más altos suprimen más ruido; valores superiores a `1.50` pueden distorsionar la voz. |
| **Voice Threshold:** | `0.20` | `0.05`–`0.50` | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. Valores más bajos tratan más señal como voz y la preservan; valores más altos tratan más señal como ruido y la suprimen. |
| **Smoothing:** | `0.85` | `0.50`–`0.98` | `NR2GainSmooth` | Controla la rapidez con la que la estimación de ruido sigue los cambios. Valores más altos proporcionan una estimación más estable, pero con una adaptación más lenta a los cambios de ruido. |
| **AE Filter (artifact elimination)** | Activado | Activado / Desactivado | `NR2AeFilter` | Activa o desactiva el postfiltro anti-artefactos que reduce el ruido musical y el retimbre. |
| **Gain Method** | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` | Selecciona el mapeo de curva de ganancia utilizado al calcular la supresión. |
| **NPE Method** | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. |
| **Reset Defaults** | — | — | — | Restaura todos los parámetros de la pestaña NR2 a sus valores predeterminados: Gamma, OSMS, AE activado, `1.50`, `0.85`, `0.20`. |

## Consejos

- Para operación de voz en SSB, comience con **Reduction Depth:** en `1.50` y **Voice Threshold:** en `0.20`. Si la voz suena cortada o hueca, reduzca **Reduction Depth:** hacia `1.00`.
- Reducir **Voice Threshold:** por debajo de `0.15` puede provocar que el ruido residual se cuele durante las pausas en la voz, ya que más señal se clasifica como voz. Auméntelo si nota este efecto.
- Si la estimación de ruido reacciona demasiado lentamente ante el ruido impulsivo, reduzca **Smoothing:** hacia `0.60`. Si la puerta de ruido suena entrecortada, auméntelo hacia `0.95`.
- Se recomienda mantener **AE Filter (artifact elimination)** activado en la mayoría de las condiciones; desactívelo solo si nota que el propio postfiltro introduce artefactos.

## Solución de problemas

- **La voz suena hueca o con exceso de procesamiento** — **Reduction Depth:** es demasiado alto o **Voice Threshold:** es demasiado alto. Reduzca **Reduction Depth:** y/o **Voice Threshold:** para que se preserven más componentes de la voz.
- **El ruido sigue siendo audible durante las pausas en la voz** — **Voice Threshold:** es demasiado bajo, lo que hace que las pausas se clasifiquen como voz. Aumente **Voice Threshold:** hacia `0.30`–`0.40`.
- **La estimación de ruido reacciona con lentitud o el piso de ruido suena inestable** — Ajuste **Smoothing:** (consulte los Consejos anteriores). Verifique también que el **NPE Method** seleccionado sea adecuado para su tipo de ruido; NSTAT se adapta mejor al ruido no estacionario.

## Relacionados

- [Restaurar los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
