# Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained

El método de ganancia de NR2 controla cómo AetherSDR asigna las estimaciones de ruido a las curvas de reducción de ganancia. Elegir el método adecuado permite equilibrar la supresión de ruido y la fidelidad de la voz según las condiciones de la banda.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar esta configuración.
- NR2 debe estar activo en su slice de recepción para que el cambio tenga un efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En **Gain Method**, haga clic en uno de los cuatro botones de opción: **Linear**, **Log**, **Gamma** o **Trained**.
4. Cierre el cuadro de diálogo. La configuración surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona el mapeo de curva de ganancia utilizado por NR2. Se almacena como entero 0–3 en el orden indicado. |

**Descripción de los métodos de ganancia:**

- **Linear** — Utiliza una escala de amplitud de audio lineal para el cálculo de la ganancia.
- **Log** — Utiliza una escala de amplitud logarítmica que comprime el rango dinámico.
- **Gamma** — Modela la ganancia mediante una distribución Gamma que se ajusta a los patrones típicos de amplitud de voz. Es el valor predeterminado.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de voz y ruido.

## Consejos

- **Gamma** es adecuado para la mayoría de los contactos SSB. Comience aquí si no está seguro.
- **Trained** puede rendir mejor en bandas con mucho ruido y patrones de voz reconocibles, pero puede sonar excesivamente procesado en señales débiles.
- **Log** puede ayudar a reducir artefactos de ruido musical cuando **Linear** produce un residual irregular en el piso de ruido.
- Después de cambiar el método de ganancia, ajuste **Reduction Depth:** y **Voice Threshold:** en la misma pestaña para adaptarlos. Consulte [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md).
- Haga clic en **Reset Defaults** en la pestaña NR2 para volver a Gamma y a todos los demás valores predeterminados de NR2 a la vez.

## Solución de problemas

- **Cambiar el método no produce ningún efecto audible** — Confirme que NR2 esté habilitado en su slice de recepción. El cuadro de diálogo AetherDSP Settings solo configura parámetros; la habilitación de NR2 se realiza desde los controles del slice.
- **La voz suena distorsionada después de cambiar a Trained** — Reduzca **Reduction Depth:** desde su valor predeterminado de 1.50 hacia 1.00, o vuelva a **Gamma**.

## Relacionados

- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
