# Ajustar la cantidad de reducción de NR4 en dB

La configuración `NR4ReductionAmount` controla cuántos decibeles de supresión de ruido aplica NR4 (libspecbleach). Aumentarla elimina más ruido; disminuirla preserva más el carácter original de la señal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- Decida aproximadamente cuánta supresión necesita. El valor predeterminado de 10.0 dB es adecuado para la mayoría de las condiciones SSB.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Localice el control deslizante **Reduction (dB):**.
4. Arrastre el control deslizante hacia la izquierda para disminuir la supresión o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del control deslizante.
5. Cierre el cuadro de diálogo. El valor se guarda automáticamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |

**Reduction (dB):** establece la reducción de ruido máxima que NR4 aplicará en decibeles. A 0.0 dB, NR4 no aplica atenuación alguna. A 40.0 dB, aplica la supresión máxima disponible.

## Consejos

- Comience cerca del valor predeterminado de 10.0 dB y auméntelo en pasos pequeños mientras monitorea la calidad del audio. Los valores altos (por encima de 25–30 dB) pueden introducir artefactos de procesamiento en señales débiles.
- **Smoothing (%):** (`NR4SmoothingFactor`) y **Suppression:** (`NR4SuppressionStrength`) interactúan con la cantidad de reducción. Si al aumentar `NR4ReductionAmount` aparece ruido musical, intente primero incrementar el suavizado.
- Si el piso de ruido varía rápidamente, habilite **Adaptive Noise Estimation** (`NR4AdaptiveNoise`) para que NR4 reestime el piso de manera continua en lugar de depender de una medición estática.

## Solución de problemas

- **El control deslizante no tiene efecto audible** — confirme que NR4 es el motor de reducción de ruido activo para su slice. Habilitar NR2 u otro motor de forma simultánea puede enmascarar la contribución de NR4.
- **La voz suena hueca o distorsionada con valores de reducción altos** — disminuya **Reduction (dB):** y verifique que **Adaptive Noise Estimation** esté habilitado para que la estimación del piso de ruido se mantenga precisa.

## Relacionados

- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
