# Ajustar la cantidad de reducción de NR4 en dB

El parámetro `NR4ReductionAmount` controla la agresividad con la que el motor NR4 (libspecbleach) atenúa el ruido. Aumentar el valor elimina más ruido; reducirlo preserva más el carácter original de la señal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar este parámetro.
- Abra la pestaña NR4 en AetherDSP Settings (consulte los pasos a continuación).

## Pasos

1. Vaya a `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4 (tab)**.
3. Localice el control deslizante **Reduction (dB):**.
4. Arrastre el control hacia la izquierda para reducir la supresión de ruido o hacia la derecha para aumentarla. El valor actual en dB se muestra a la derecha del control deslizante.
5. Cierre el cuadro de diálogo. El valor se guarda de inmediato al mover el control deslizante.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |

**Reduction (dB):** Establece la reducción de ruido máxima aplicada por el motor NR4, en decibeles. Con 0.0 dB, NR4 no aplica atenuación. Con 40.0 dB, aplica la supresión máxima. Los valores entre 10–20 dB funcionan bien para ruido moderado de banda sin artefactos audibles en la voz.

## Consejos

- Si el piso de ruido desaparece pero la voz suena hueca o acuosa, reduzca **Reduction (dB):** entre 5–10 dB.
- **Reduction (dB):** interactúa con **Suppression:** y **Masking Depth:** — consulte [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md) para orientación sobre cómo combinar estos controles.
- Para restablecer **Reduction (dB):** y todos los demás parámetros de NR4 a los valores de fábrica (10.0 dB), haga clic en **Reset Defaults** en la parte inferior de la pestaña NR4 — consulte [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md).
- Activar **Adaptive Noise Estimation** permite que NR4 reestime continuamente el piso de ruido, lo que puede hacer que la reducción se sienta más uniforme a medida que cambian las condiciones de banda — consulte [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md).

## Resolución de problemas

- **Mover el control deslizante no produce ningún efecto audible** — confirme que NR4 es el motor de reducción de ruido activo. Otros motores (NR2, DFNR, MNR) tienen controles independientes y no comparten este parámetro.
- **La voz suena distorsionada incluso con valores bajos** — verifique que **Suppression:** (`NR4SuppressionStrength`) no esté configurado cerca de 1.00, ya que ambos controles se amplifican mutuamente.

## Relacionado

- [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
