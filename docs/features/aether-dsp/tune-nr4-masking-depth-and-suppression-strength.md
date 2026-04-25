# Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4

Use esta página para ajustar la profundidad de enmascaramiento espectral y la fuerza de supresión general de NR4, controlando con qué agresividad el motor NR4 atenúa el ruido en relación con el contenido similar a la voz.

## Antes de comenzar

- Abra AetherSDR.
- NR4 debe estar seleccionado como su motor de reducción de ruido activo. Consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md) si no está seguro.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Ajuste **Masking Depth:** para establecer con qué profundidad se aplica el enmascaramiento espectral. Los valores más bajos aplican menos enmascaramiento; los valores más altos aplican más.
4. Ajuste **Suppression:** para establecer la fuerza de supresión general de NR4. Los valores más bajos son más suaves; los valores más altos son más agresivos.
5. Cierre el diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

**Masking Depth:** controla la profundidad del enmascaramiento espectral aplicado por el motor NR4. En 0.00 el enmascaramiento no se aplica; en 1.00 se aplica a profundidad máxima.

**Suppression:** establece la fuerza de supresión general del motor NR4. En 0.00 la supresión es mínima; en 1.00 es máxima.

## Consejos

- Comience con ambos controles deslizantes en sus valores predeterminados (0.50) y realice ajustes incrementales pequeños. Aumentar demasiado **Suppression:** puede causar artefactos audibles en señales débiles.
- Si queda ruido residual después de aumentar **Suppression:**, aumente también **Masking Depth:** de forma gradual. Los dos controles interactúan: la profundidad de enmascaramiento define qué bins espectrales son el objetivo, mientras que la supresión determina cuánta reducción de ganancia se les aplica.
- Use **Reset Defaults** para devolver ambos controles deslizantes —junto con todos los demás parámetros de NR4— a sus valores de fábrica (SPP-MMSE, adaptativo activado, 10.0 dB, Smoothing 0, Whitening 0, Masking Depth 0.50, Suppression 0.50).

## Solución de problemas

- **La voz suena apagada después de aumentar Suppression:** — El nivel de supresión es demasiado alto. Reduzca **Suppression:** y, si es necesario, reduzca también **Masking Depth:** para restaurar la claridad de la voz.
- **El piso de ruido sigue siendo audible con Suppression: al máximo** — Verifique que **Reduction (dB):** esté configurado con un valor suficientemente alto y que **Adaptive Noise Estimation** esté habilitado. Consulte [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md) y [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md).

## Relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
