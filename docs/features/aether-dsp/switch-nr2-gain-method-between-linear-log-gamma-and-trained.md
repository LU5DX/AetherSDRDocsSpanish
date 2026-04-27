# Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained

El método de ganancia de NR2 controla cómo el motor transforma su estimación de ruido en una curva de reducción efectiva. Cambiar entre Linear, Log, Gamma y Trained permite equilibrar entre una supresión de ruido agresiva y una voz con sonido natural.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar este ajuste.
- NR2 debe estar activo en el slice que desea afectar. Este diálogo configura los parámetros del motor NR2; la activación de NR2 en un slice se realiza desde la interfaz principal.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En el grupo **Gain Method**, haga clic en uno de los cuatro botones de opción: **Linear**, **Log**, **Gamma** o **Trained**.

La selección surte efecto de inmediato y se guarda en `NR2GainMethod`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona el mapeo de curva de ganancia utilizado por NR2. Se almacena como entero 0–3 en el orden mostrado. |

### Descripción de los métodos de ganancia

- **Linear** — Utiliza una escala de amplitud de audio lineal para el cálculo de ganancia.
- **Log** — Utiliza una escala de amplitud logarítmica, que comprime el rango dinámico.
- **Gamma** — Modela la ganancia sobre una distribución gamma que se ajusta a los patrones típicos de amplitud de voz. Este es el valor predeterminado.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de voz y ruido.

## Consejos

- **Gamma** es el valor predeterminado y funciona bien para la mayoría de los contactos de voz en SSB. Comience aquí si no está seguro.
- **Trained** puede producir una voz con sonido más natural en las señales para las que fue entrenado, pero los resultados varían según el tipo de señal.
- **Log** reduce el rango dinámico de la curva de ganancia, lo que puede ser útil con pisos de ruido muy irregulares.
- Después de cambiar el método de ganancia, ajuste **Reduction Depth:** (predeterminado 1.50, rango 0.50–2.00) y **Voice Threshold:** (predeterminado 0.20, rango 0.05–0.50) para adaptarlos a las características de la nueva curva. Consulte [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md).
- Haga clic en **Reset Defaults** en la pestaña NR2 para restablecer el método de ganancia a Gamma junto con el resto de los parámetros de NR2 a sus valores predeterminados.

## Relacionados

- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
