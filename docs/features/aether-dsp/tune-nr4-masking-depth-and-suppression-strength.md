# Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4

La pestaña **NR4** en AetherDSP Settings expone dos controles — `NR4MaskingDepth` y `NR4SuppressionStrength` — que en conjunto determinan con qué agresividad NR4 (libspecbleach) atenúa el ruido entre las sílabas del habla. Ajustar estos controles permite equilibrar el ruido residual frente a la naturalidad de la voz.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a la radio para cambiar estos ajustes.
- NR4 debe ser el motor de reducción de ruido activo en el slice que está escuchando. Si aún no ha habilitado NR4, los controles deslizantes tendrán efecto en cuanto lo haga.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Localice el control deslizante **Masking Depth:**. Arrástrelo hacia la izquierda o la derecha para establecer la profundidad de enmascaramiento espectral (rango 0.00–1.00, valor predeterminado 0.50). El valor actual se muestra a la derecha del control.
4. Localice el control deslizante **Suppression:**. Arrástrelo hacia la izquierda o la derecha para establecer la intensidad de supresión general (rango 0.00–1.00, valor predeterminado 0.50). El valor actual se muestra a la derecha del control.
5. Monitoree el audio en tiempo real. Ajuste hasta que el ruido residual sea aceptablemente bajo sin que se perciba degradación de la voz.
6. Cierre el diálogo. Los valores se guardan inmediatamente cuando se mueve cada control deslizante; no se requiere ninguna acción de guardado separada.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla con qué profundidad el enmascaramiento espectral suprime los bins estimados como ruido. Valores más altos aumentan el enmascaramiento con el riesgo de atenuar señales débiles. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Establece la intensidad de supresión general de NR4. Valores más altos eliminan más ruido; valores muy altos pueden introducir artefactos de procesamiento. |

## Consejos

- Estos dos controles interactúan entre sí: un valor alto de **Suppression:** combinado con un valor bajo de **Masking Depth:** tiende a producir un residual más seco y plano, mientras que ajustar ambos en niveles moderados (alrededor de 0.50) generalmente preserva el carácter más natural de la voz.
- Si desea volver a una línea base conocida como correcta, haga clic en **Reset Defaults** en la pestaña NR4. Esto restaura **Masking Depth:** a 0.50 y **Suppression:** a 0.50, junto con todos los demás parámetros de NR4.
- Los cambios surten efecto de inmediato sin necesidad de reiniciar AetherSDR ni de reconectarse a la radio.

## Solución de problemas

- **Al aumentar Suppression: las voces suenan huecas o con efecto de fase** — reduzca **Suppression:** hacia 0.30–0.40 y verifique que **Adaptive Noise Estimation** esté habilitado para que la estimación del piso de ruido se mantenga actualizada. Consulte [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md).
- **Los controles deslizantes no producen ningún efecto audible** — es posible que NR4 no sea el motor de reducción de ruido activo en el slice actual, o que la cantidad general de **Reduction (dB):** esté establecida en 0.0. Consulte [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md).

## Relacionado

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
