# Activar o desactivar la estimación de ruido adaptativa de NR4

La estimación de ruido adaptativa de NR4 reestima continuamente el piso de ruido a medida que cambian las condiciones de la banda. Desactivarla fija la estimación en su último valor calculado, lo que puede ser útil en entornos de ruido muy estables, pero provocará supresión insuficiente o excesiva cuando el ruido cambie.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio para ajustar los parámetros de DSP.
- NR4 debe ser el motor de reducción de ruido activo en su cadena de recepción. Si está usando NR2, MNR o DFNR, este ajuste no tiene efecto.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation**.
   - Marcado (predeterminado): NR4 reestima continuamente el piso de ruido.
   - Desmarcado: NR4 mantiene la estimación de ruido fija.

El cambio surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Adaptive Noise Estimation** | Casilla de verificación | Marcado | On / Off | `NR4AdaptiveNoise` |
| **Noise Estimation Method** | Botones de opción | SPP-MMSE | SPP-MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| **Reduction (dB):** | Control deslizante | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Smoothing (%):** | Control deslizante | 0 | 0–100 | `NR4SmoothingFactor` |
| **Whitening (%):** | Control deslizante | 0 | 0–100 | `NR4WhiteningFactor` |
| **Masking Depth:** | Control deslizante | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | Control deslizante | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |
| **Reset Defaults** | Botón | — | — | — |

## Consejos

- Si el piso de ruido en la banda es estable (por ejemplo, un entorno local silencioso a altas horas de la noche), desactivar **Adaptive Noise Estimation** puede evitar que el estimador derive hacia los picos de señal y suprima inadvertidamente estaciones débiles.
- Si desactiva la estimación adaptativa y luego nota que la reducción de ruido ya no sigue correctamente tras un cambio en las condiciones de la banda, vuelva a activarla y espere unos segundos para que el estimador converja antes de ajustar otros controles deslizantes.
- La selección de **Noise Estimation Method** determina qué algoritmo alimenta al estimador adaptativo. SPP-MMSE es el predeterminado y se adapta a la mayoría de las condiciones; cambie a Brandt o Martin si trabaja con pisos de ruido que varían rápidamente o lentamente, respectivamente.
- Haga clic en **Reset Defaults** para restaurar `NR4AdaptiveNoise` al estado marcado junto con todos los demás parámetros de NR4.

## Resolución de problemas

- **La supresión de ruido deja de seguir el seguimiento tras un desvanecimiento QSB** — Es probable que la estimación de ruido adaptativa esté desactivada. Abra `Settings > AetherDSP Settings...`, seleccione la pestaña **NR4** y marque **Adaptive Noise Estimation**.
- **NR4 suprime los picos de señal junto con el ruido** — Es posible que el estimador esté adaptándose de forma demasiado agresiva. Desactive **Adaptive Noise Estimation** temporalmente, o reduzca **Reduction (dB):** y **Suppression:** a valores más bajos.

## Temas relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
