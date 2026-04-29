# Configurar el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles

`DfnrAttenLimit` controla la agresividad con la que DeepFilterNet3 suprime el ruido. Reducirlo preserva más la señal original en señales fuertes; aumentarlo maximiza la eliminación de ruido en señales débiles o ruidosas.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ajustar la configuración DSP.
- DeepFilterNet3 (DFNR) debe estar seleccionado como el motor de reducción de ruido activo.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Arrastre el control deslizante **Attenuation Limit** hasta el valor deseado (0–100 dB).
4. Cierre el diálogo. La configuración entra en vigor de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación de ruido máxima aplicada por DeepFilterNet3. En 0, el motor pasa el audio sin modificaciones; en 100, aplica la atenuación completa. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro adicional posterior sobre el límite de atenuación para una supresión extra. |

## Consejos

- Para señales fuertes y limpias donde la fidelidad es importante, reduzca **Attenuation Limit** hacia 0 para limitar cuánto puede alterar el audio el motor.
- Para señales débiles o con ruido intenso, establezca **Attenuation Limit** en 100 y combínelo con un valor de **Post-Filter Beta** distinto de cero para lograr la supresión más agresiva.

## Solución de problemas

- **El audio suena sin cambios después de mover el control deslizante** — Confirme que está en la pestaña **DFNR** y que DeepFilterNet3 es el motor de reducción de ruido activo. Otros motores (NR2, NR4, MNR) tienen controles independientes y no se ven afectados por `DfnrAttenLimit`.

## Relacionado

- [Configurar el post-filter beta de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
