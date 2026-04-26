# Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4

La pestaña NR4 en AetherDSP Settings expone dos controles que determinan con qué agresividad NR4 (libspecbleach) moldea el piso de ruido residual tras su etapa principal de reducción: `NR4MaskingDepth` y `NR4SuppressionStrength`. Ajústelos cuando desee un control más fino sobre el equilibrio entre la supresión de ruido y la naturalidad del audio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un radio para cambiar estos ajustes.
- Abra `Settings > AetherDSP Settings...` para acceder al cuadro de diálogo.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Mueva el control deslizante **Masking Depth:** al valor deseado entre 0.00 y 1.00. El valor predeterminado es 0.50.
4. Mueva el control deslizante **Suppression:** al valor deseado entre 0.00 y 1.00. El valor predeterminado es 0.50.
5. Cierre el cuadro de diálogo. Los ajustes se guardan de inmediato al mover cada control deslizante.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. Valores más altos aplican un enmascaramiento más profundo a los componentes de ruido por debajo del piso de ruido estimado. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Establece la fuerza de supresión general de NR4. Valores más altos reducen más ruido; valores más bajos preservan más el carácter original de la señal. |

## Consejos

- Para restablecer ambos controles a sus valores predeterminados (0.50 y 0.50), haga clic en **Reset Defaults** en la parte inferior derecha de la pestaña NR4. Esto también restablece todos los demás parámetros de NR4 a sus valores predeterminados (SPP-MMSE, adaptativo activado, reducción de 10.0 dB, 0% de suavizado, 0% de blanqueamiento).
- Si la señal suena sobreprocesada o delgada, reduzca primero **Suppression:** y luego **Masking Depth:** si es necesario.
- Estos controles actúan sobre la salida de la etapa de reducción principal. Establezca **Reduction (dB):** en un valor razonable antes de ajustar con precisión el enmascaramiento y la supresión. Consulte [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md).

## Solución de problemas

- **Los controles deslizantes no tienen efecto audible** — confirme que NR4 es el motor de reducción de ruido activo para el receptor. Los motores de AetherDSP se seleccionan por receptor desde la superposición del panadapter, no desde este cuadro de diálogo.
- **Reset Defaults cambia más que solo estos dos controles deslizantes** — esto es lo esperado. **Reset Defaults** en la pestaña NR4 restaura todos los parámetros de NR4 de forma simultánea.

## Relacionado

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
