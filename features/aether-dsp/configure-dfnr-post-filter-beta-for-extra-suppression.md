# Configurar Post-Filter Beta de DFNR para supresión adicional

El control Post-Filter Beta agrega una segunda etapa de supresión después de la reducción de ruido principal de DeepFilterNet3. Úselo cuando quede ruido residual tras ajustar el límite de atenuación.

## Antes de comenzar

- Abra AetherSDR.
- DFNR (DeepFilterNet3) debe estar activo en su receptor. Post-Filter Beta no tiene efecto si DFNR no está en ejecución.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Ajuste el control deslizante **Post-Filter Beta** al valor deseado.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación de ruido máxima aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo. |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica una etapa de postfiltro adicional para supresión extra más allá del límite de atenuación principal. |

## Consejos

- Comience con **Post-Filter Beta** en 0.00 y auméntelo en pasos pequeños. Los valores más altos suprimen más ruido residual, pero pueden afectar la fidelidad de la voz.
- Si la señal suena sobreprocesada con un determinado valor de **Post-Filter Beta**, reduzca primero **Attenuation Limit** y luego vuelva a subir **Post-Filter Beta** según su preferencia.
- Un valor de **Post-Filter Beta** de 0.00 deshabilita el postfiltro por completo, dejando activa únicamente la etapa principal de DeepFilterNet3.

## Temas relacionados

- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
