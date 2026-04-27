# Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles

`DfnrAttenLimit` controla la agresividad con la que DeepFilterNet3 suprime el ruido. Al reducirlo se conserva más la señal original en señales fuertes; al aumentarlo se maximiza la eliminación de ruido en señales débiles o ruidosas.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para ajustar los parámetros de DSP.
- DeepFilterNet3 (DFNR) debe estar seleccionado como motor de reducción de ruido activo.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Arrastre el control deslizante **Attenuation Limit** hasta el valor deseado (0–100 dB).
4. Cierre el cuadro de diálogo. El ajuste surte efecto de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación de ruido máxima aplicada por DeepFilterNet3. En 0 el motor pasa el audio sin modificaciones; en 100 aplica la atenuación completa. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro adicional posterior sobre el límite de atenuación para una supresión extra. |

## Consejos

- Para señales fuertes y limpias donde preservar la fidelidad es importante, reduzca **Attenuation Limit** hacia 0 para limitar cuánto puede alterar el audio el motor.
- Para señales débiles o con degradación severa por ruido, establezca **Attenuation Limit** en 100 y combínelo con un valor distinto de cero en **Post-Filter Beta** para obtener la supresión más agresiva.

## Solución de problemas

- **El audio no parece verse afectado después de mover el control deslizante** — Confirme que se encuentra en la pestaña **DFNR** y que DeepFilterNet3 es el motor de reducción de ruido activo. Otros motores (NR2, NR4, MNR) tienen controles independientes y no se ven afectados por `DfnrAttenLimit`.

## Relacionados

- [Configurar el post-filter beta de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
