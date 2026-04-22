# Ajustar la profundidad de reducción y el umbral de voz de NR2

Esta página explica cómo ajustar la profundidad máxima de reducción de ruido y el umbral de presencia de voz de NR2 en el diálogo AetherDSP Settings de AetherSDR. Estos dos controles deslizantes determinan con qué agresividad suprime el ruido NR2 y con qué sensibilidad protege la voz para que no sea tratada como ruido.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar estos ajustes.
- NR2 debe estar activo en el slice que desea afectar. Esta página cubre únicamente el ajuste de parámetros, no la activación de NR2.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Ajuste el control deslizante **Reduction Depth:** para establecer la profundidad máxima de supresión. El valor predeterminado es **1.50**; el rango válido es **0.50–2.00**. Los valores más altos suprimen más ruido, pero aumentan el riesgo de distorsión de la voz.
4. Ajuste el control deslizante **Voice Threshold:** para establecer el umbral de probabilidad de presencia de voz. El valor predeterminado es **0.20**; el rango válido es **0.05–0.50**. Los valores más bajos preservan la voz más débil, pero pueden dejar pasar más ruido.
5. Los ajustes se guardan automáticamente al mover un control deslizante. No se requiere ningún paso adicional de confirmación.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido | Comportamiento |
|---|---|---|---|---|
| **Reduction Depth:** | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción de NR2. Los valores más altos suprimen más ruido; los valores más bajos preservan más el carácter de la señal. |
| **Voice Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. Los valores más bajos detectan la voz más débil como voz, reduciendo la supresión de señales débiles. Los valores más altos exigen mayor presencia de voz antes de retener la reducción de ruido. |
| **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla con qué suavidad la estimación de ruido sigue los cambios. Los valores más altos producen una estimación más estable que reacciona con mayor lentitud a cambios rápidos de ruido. |
| **AE Filter (artifact elimination)** | Activado | Activado / Desactivado | `NR2AeFilter` | Activa o desactiva el posfiltro antiartefactos que reduce el timbre y el ruido musical. |
| **Gain Method** | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` | Selecciona el mapeo de curva de ganancia utilizado durante la supresión. |
| **NPE Method** | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. |
| **Reset Defaults** | — | — | — | Restaura todos los controles de NR2 a sus valores predeterminados: Gamma, OSMS, AE activado, 1.50, 0.85, 0.20. |

## Consejos

- Si la voz suena hueca o distorsionada, reduzca **Reduction Depth:** hacia 1.00 o active **AE Filter (artifact elimination)** si está desactivado.
- Si el ruido se filtra en señales débiles, intente reducir **Voice Threshold:** hacia 0.05 para que la voz débil se detecte con mayor facilidad y se retenga la supresión.
- Si NR2 reacciona con demasiada lentitud cuando las condiciones de ruido cambian rápidamente, reduzca **Smoothing:** hacia 0.50 para que la estimación de ruido siga los cambios con mayor rapidez.
- Use **Reset Defaults** para volver a una línea base conocida como correcta antes de realizar una nueva ronda de ajustes.

## Solución de problemas

- **La voz suena apagada o con procesamiento excesivo** — **Reduction Depth:** puede estar demasiado alto. Redúzcalo hacia 1.00. Verifique también que **AE Filter (artifact elimination)** esté marcado, ya que reduce los artefactos de ruido musical que pueden acompañar a una supresión intensa.
- **El ruido sigue siendo audible incluso con la profundidad máxima de Reduction Depth: (2.00)** — NR2 puede no ser el motor adecuado para este tipo de ruido. Consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md).
- **Los controles deslizantes vuelven a su posición o no conservan sus valores** — Esto puede indicar un problema de permisos en el archivo de ajustes. Confirme que AetherSDR tiene acceso de escritura a su directorio de configuración y reinicie la aplicación.

## Relacionados

- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
