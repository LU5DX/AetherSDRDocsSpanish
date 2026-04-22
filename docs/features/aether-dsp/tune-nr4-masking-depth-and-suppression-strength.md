# Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4

Los controles deslizantes **Masking Depth:** y **Suppression:** de la pestaña NR4 determinan con qué agresividad el motor libspecbleach de AetherSDR atenúa el ruido por debajo del piso de ruido estimado. Ajustar estos dos parámetros permite encontrar un equilibrio entre una reducción de ruido de sonido más limpio y una mejor preservación del detalle de voz débil o de bajo nivel.

## Antes de comenzar

- Abra AetherSDR. No se requiere una conexión de radio para ajustar los parámetros de DSP.
- Confirme que NR4 es el motor de reducción de ruido activo para su receptor. Si no está seguro de qué motor utilizar, consulte [Elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md).

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4 (tab)**.
3. Localice el control deslizante **Masking Depth:**. Arrástrelo hacia la izquierda para reducir el enmascaramiento espectral o hacia la derecha para aumentarlo. El rango válido es 0.00–1.00; el valor predeterminado es 0.50. El valor se almacena como `NR4MaskingDepth`.
4. Localice el control deslizante **Suppression:**. Arrástrelo hacia la izquierda para una supresión más ligera o hacia la derecha para una supresión más fuerte. El rango válido es 0.00–1.00; el valor predeterminado es 0.50. El valor se almacena como `NR4SuppressionStrength`.
5. Escuche el audio recibido y ajuste ambos controles deslizantes hasta que el equilibrio entre la reducción de ruido y la claridad de voz sea satisfactorio.
6. Cierre el diálogo. La configuración se guarda de inmediato al mover cada control deslizante.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral aplicado durante la reducción de ruido. Valores más altos aplican un enmascaramiento más profundo por debajo del piso de ruido estimado. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Establece la fuerza de supresión general de NR4. Valores más altos eliminan más ruido; valores más bajos preservan más el carácter original de la señal. |

## Consejos

- Estos dos controles deslizantes interactúan entre sí. Un valor alto de **Suppression:** combinado con un valor bajo de **Masking Depth:** produce una atenuación amplia pero superficial. Un valor alto de **Masking Depth:** combinado con un valor alto de **Suppression:** produce la eliminación de ruido más agresiva y conlleva el mayor riesgo de distorsionar la voz débil.
- Si el piso de ruido cambia rápidamente (QSB, ruido de banda), active **Adaptive Noise Estimation** para mantener actualizada la estimación de ruido antes de aumentar **Masking Depth:** y **Suppression:**. Consulte [Activar o desactivar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md).
- Para restablecer ambos controles deslizantes a sus valores predeterminados (0.50) junto con todos los demás parámetros de NR4, haga clic en **Reset Defaults** en la pestaña NR4. Consulte [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md).

## Solución de problemas

- **La voz suena hueca o distorsionada al aumentar los controles deslizantes** — Reduzca primero **Masking Depth:**. La profundidad de enmascaramiento tiene un efecto más fuerte sobre la coloración de la voz que **Suppression:**. Bájelo hacia 0.20–0.30 y vuelva a evaluar.
- **La reducción de ruido no tiene efecto audible incluso con los valores máximos** — Verifique que NR4 sea realmente el motor activo en el receptor. Compruebe también que **Reduction (dB):** esté por encima de 0.0 dB, ya que ese control deslizante determina el margen de trabajo disponible para NR4. Consulte [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md).

## Relacionado

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
