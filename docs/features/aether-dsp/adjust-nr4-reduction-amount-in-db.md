# Ajustar la cantidad de reducción de NR4 en dB

La configuración `NR4ReductionAmount` controla cuántos decibeles de ruido puede eliminar el motor NR4 (libspecbleach) como máximo. Aumentar este valor suprime más ruido; disminuirlo preserva más el carácter original de la señal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar esta configuración.
- Abra el motor NR4 en su receptor slice antes de hacer ajustes para escuchar el efecto en tiempo real.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Localice el control deslizante **Reduction (dB):**.
4. Arrastre el control hacia la izquierda para reducir la supresión o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del control.
5. Cierre el diálogo. El valor se guarda automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Control deslizante **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |
| Control deslizante **Smoothing (%):** | 0 | 0–100 % | `NR4SmoothingFactor` |
| Control deslizante **Whitening (%):** | 0 | 0–100 % | `NR4WhiteningFactor` |
| Control deslizante **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| Control deslizante **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| Botones de opción **Noise Estimation Method** | SPP-MMSE | SPP-MMSE / Brandt / Martin | `NR4NoiseEstimationMethod` |
| Casilla de verificación **Adaptive Noise Estimation** | Habilitado | On / Off | `NR4AdaptiveNoise` |
| Botón **Reset Defaults** | — | — | — |

**Reduction (dB):** establece el límite máximo de atenuación de ruido que aplica NR4. A 0 dB, la supresión está efectivamente desactivada. A 40 dB, el motor aplica la atenuación máxima para silenciar los pisos de ruido.

## Consejos

- Comience con el valor predeterminado de 10.0 dB y auméntelo en pasos pequeños mientras escucha una señal. Los valores altos (por encima de 25–30 dB) pueden introducir artefactos audibles en señales débiles o que se desvanecen rápidamente.
- Si el piso de ruido reaparece entre transmisiones, habilite **Adaptive Noise Estimation** para que NR4 actualice continuamente su modelo de ruido. Consulte [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md).
- Para restablecer todos los parámetros de NR4 a los valores de fábrica (incluyendo Reduction de vuelta a 10.0 dB), haga clic en **Reset Defaults** en la pestaña NR4. Consulte [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md).

## Solución de problemas

- **El control deslizante no tiene efecto audible** — confirme que NR4 es el motor de reducción de ruido activo en su receptor slice. Los motores NR del lado del cliente de AetherSDR requieren cada uno su propio paso de activación en los controles del receptor.
- **El ruido reaparece inmediatamente después de silenciarse** — es posible que el piso de ruido cambie más rápido de lo que una estimación fija puede seguir. Habilite **Adaptive Noise Estimation** y pruebe el método de estimación de ruido SPP-MMSE.
- **La voz suena hueca o con efecto de fase a valores de reducción altos** — disminuya **Reduction (dB):** hacia 10–15 dB y aumente ligeramente **Masking Depth:**. Consulte [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md).

## Relacionados

- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
