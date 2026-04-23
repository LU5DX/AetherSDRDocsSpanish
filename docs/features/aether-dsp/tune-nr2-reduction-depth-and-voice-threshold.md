# Ajustar la profundidad de reducción y el umbral de voz en NR2

Ajuste la agresividad con la que NR2 suprime el ruido y la sensibilidad con la que detecta la voz. Estos dos controles deslizantes regulan el equilibrio entre la eliminación de ruido y la fidelidad de la voz — útil cuando la configuración predeterminada suprime en exceso señales débiles o deja demasiado ruido.

## Antes de comenzar

- Abra AetherSDR.
- NR2 debe estar activo en el slice que está monitoreando. Estos controles afectan los parámetros del motor NR2 de forma global; no activan NR2 en un slice.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. Localice el control deslizante **Reduction Depth:**. Arrástrelo hacia la izquierda para reducir la agresividad de la supresión, o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del control.
4. Localice el control deslizante **Voice Threshold:**. Arrástrelo hacia la izquierda para hacer la detección de voz más sensible (preserva la voz más débil, pero puede dejar pasar más ruido) o hacia la derecha para elevar el umbral (detección de voz más estricta).
5. Cierre el diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| **Reduction Depth:** | 1.50 | 0.50–2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción de ruido. Valores más altos suprimen más ruido, pero aumentan el riesgo de distorsión de la voz. |
| **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios de señal. Valores más altos producen una estimación más estable, pero de adaptación más lenta. |
| **Voice Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. Valores más bajos preservan la voz débil; valores más altos aplican la reducción de forma más agresiva en señales dudosas. |
| **AE Filter (artifact elimination)** | Activado | On / Off | `NR2AeFilter` | Aplica un postfiltro anti-artefactos que reduce el timbre y el ruido musical. Déjelo activado salvo durante pruebas. |
| **Gain Method** | Gamma | Linear / Log / Gamma / Trained | `NR2GainMethod` | Selecciona la curva de ganancia utilizada por NR2. Consulte [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md). |
| **NPE Method** | OSMS | OSMS / MMSE / NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido. Consulte [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md). |
| **Reset Defaults** | — | — | — | Restaura todos los valores de la pestaña NR2 a sus valores predeterminados: Gamma, OSMS, AE activado, Reduction Depth 1.50, Smoothing 0.85, Voice Threshold 0.20. |

## Consejos

- Comience con **Reduction Depth:** en el valor predeterminado de 1.50. Auméntelo hacia 2.00 solo en bandas con ruido de banda ancha intenso; valores superiores a 1.80 pueden introducir artefactos audibles en la voz SSB.
- Si NR2 corta la primera sílaba de una transmisión, reduzca **Voice Threshold:** de 0.20 hacia 0.05. El motor clasificará entonces las señales marginales como voz y retendrá la reducción antes.
- Si el ruido residual aparece durante las pausas, aumente **Voice Threshold:** hacia 0.30–0.40. El motor aplicará la reducción con mayor facilidad cuando no haya voz.
- Reducir **Smoothing:** por debajo de 0.70 hace que la estimación de ruido reaccione más rápido ante cambios en el piso de ruido, pero puede causar bombeo en señales SSB.
- Haga clic en **Reset Defaults** para volver a la configuración de referencia antes de continuar experimentando.

## Resolución de problemas

- **La voz suena hueca o distorsionada** — **Reduction Depth:** está configurado demasiado alto. Redúzcalo hacia 1.00–1.50.
- **El ruido vuelve durante las pausas de voz pero se corta abruptamente cuando la estación transmite** — **Voice Threshold:** está configurado demasiado alto. Redúzcalo para que el motor detecte la presencia de voz antes.
- **NR2 reacciona demasiado lentamente ante un piso de ruido cambiante** — Reduzca **Smoothing:** para permitir una adaptación más rápida de la estimación de ruido.

## Temas relacionados

- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
