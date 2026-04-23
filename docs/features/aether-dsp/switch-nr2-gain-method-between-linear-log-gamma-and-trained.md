# Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained

El método de ganancia del motor NR2 controla cómo mapea el ruido estimado a una curva de supresión. Cambiarlo permite equilibrar entre una eliminación de ruido agresiva y una voz que suene natural.

## Antes de comenzar

- No se requiere conexión a radio. AetherDSP Settings puede abrirse en cualquier momento.
- NR2 debe estar activo en un slice receptor para que los cambios surtan efecto en el audio en vivo.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En el grupo **Gain Method**, haga clic en uno de los cuatro botones de opción: **Linear**, **Log**, **Gamma** o **Trained**.

El ajuste surte efecto de inmediato. AetherSDR guarda la selección en `NR2GainMethod`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|---|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` |

**Opciones de Gain Method:**

- **Linear** — Mapea la ganancia usando una escala de amplitud de audio lineal. Sin compresión del rango dinámico.
- **Log** — Usa una escala de amplitud logarítmica. Comprime el rango dinámico; tiende a reducir los artefactos de ruido musical a costa de cierta naturalidad en la voz.
- **Gamma** — Modela la amplitud de la voz usando una distribución Gamma. Predeterminado. Generalmente ofrece el mejor equilibrio entre supresión y fidelidad de la voz para trabajo en SSB y CW.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de voz y ruido. Puede rendir mejor en tipos de ruido específicos, pero puede sonar procesado en otros.

La selección se almacena como un entero: Linear = 0, Log = 1, Gamma = 2, Trained = 3.

## Consejos

- Comience con **Gamma** si no está seguro. Es el valor predeterminado y se adapta a la mayoría de las condiciones en HF.
- Si escucha ruido musical residual con Gamma, pruebe **Log**.
- Si el tipo de ruido es constante (por ejemplo, un ventilador estacionario o el zumbido de un sistema HVAC), **Trained** puede ofrecer resultados más limpios.
- Después de cambiar el método, use los controles deslizantes **Reduction Depth:** y **Voice Threshold:** para reoptimizar la supresión con la nueva curva. Consulte [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md).
- Para restaurar todos los parámetros de NR2 a sus valores predeterminados, haga clic en **Reset Defaults** en la pestaña NR2. Esto restablece el Gain Method a **Gamma**. Consulte [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md).

## Relacionados

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
