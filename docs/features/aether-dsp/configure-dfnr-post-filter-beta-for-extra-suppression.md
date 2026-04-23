# Configurar el beta del postfiltro de DFNR para supresión adicional

El beta del postfiltro de DFNR aplica una etapa de supresión adicional después de la reducción de ruido principal de DeepFilterNet3. Úselo cuando la atenuación primaria deje ruido residual que desee reducir aún más.

## Antes de comenzar

- Abra AetherSDR.
- DFNR (DeepFilterNet3) debe estar habilitado en su receptor de slice (canal de recepción). El diálogo AetherDSP Settings no requiere una conexión de radio, pero el procesamiento DFNR debe estar activo para que los cambios tengan un efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Arrastre el control deslizante **Post-Filter Beta** hacia la derecha para aumentar la supresión del postfiltro. El valor predeterminado es `0.00`; el rango válido es de `0.00` a `0.30`.
4. Cierre el diálogo. El valor se guarda automáticamente en `DfnrPostFilterBeta`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Attenuation Limit** | `100` | `0`–`100` dB | `DfnrAttenLimit` | Establece la atenuación de ruido máxima aplicada por DeepFilterNet3. `0` deja pasar el audio sin atenuación; `100` permite la atenuación máxima. |
| **Post-Filter Beta** | `0.00` | `0.00`–`0.30` | `DfnrPostFilterBeta` | Aplica una etapa de postfiltro adicional sobre la salida principal de DeepFilterNet3 para una supresión de ruido extra. |

## Consejos

- Comience con **Post-Filter Beta** en `0.00` y auméntelo en incrementos pequeños. Dado que el postfiltro actúa después del modelo principal, valores altos pueden afectar la naturalidad de la voz incluso cuando la reducción primaria suena limpia.
- Si solo necesita una supresión moderada, ajuste primero **Attenuation Limit** antes de aumentar **Post-Filter Beta**. Consulte [Configurar el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md).

## Solución de problemas

- **El cambio de Post-Filter Beta no tiene efecto audible** — Es posible que el procesamiento DFNR no esté activo en el slice actual. Confirme que DFNR esté habilitado antes de ajustar este control.
- **La voz suena sobreprocesada o apagada** — Reduzca **Post-Filter Beta** hacia `0.00`. El postfiltro agrega supresión más allá de la salida propia del modelo neuronal, por lo que valores pequeños suelen ser suficientes.

## Relacionado

- [Configurar el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
