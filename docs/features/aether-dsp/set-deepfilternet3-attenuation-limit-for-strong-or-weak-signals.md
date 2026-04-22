# Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles

El parámetro `DfnrAttenLimit` controla la agresividad con la que DeepFilterNet3 suprime el ruido. Reducirlo preserva más la señal original en estaciones fuertes; aumentarlo maximiza la eliminación de ruido en señales débiles.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar este parámetro.
- DeepFilterNet3 (DFNR) debe estar activo como motor de reducción de ruido seleccionado para que este parámetro tenga efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Arrastre el control deslizante **Attenuation Limit** hasta el valor deseado (0–100 dB).
4. Cierre el cuadro de diálogo. El valor se guarda inmediatamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de parámetro | Comportamiento |
|---|---|---|---|---|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación de ruido máxima aplicada por DeepFilterNet3. 0 = paso directo (sin atenuación); 100 = atenuación máxima. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro adicional posterior sobre DeepFilterNet3 para una supresión extra. |

## Consejos

- En señales fuertes donde el procesamiento excesivo sea perceptible, establezca **Attenuation Limit** en un valor más bajo (por ejemplo, 40–60 dB) para reducir artefactos sin dejar de eliminar el ruido de fondo.
- En señales débiles o enterradas en el ruido, deje **Attenuation Limit** en 100 para permitir la supresión máxima.
- Con **Attenuation Limit** en 0, el audio pasa a través de DeepFilterNet3 sin cambios, lo cual es útil para comparaciones A/B.

## Temas relacionados

- [Configurar el beta del filtro posterior de DFNR para supresión extra](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
