# Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles

La configuración `DfnrAttenLimit` establece el máximo de supresión de ruido que DeepFilterNet3 tiene permitido aplicar. Reducir el límite preserva más el carácter de la señal en señales fuertes y limpias; aumentarlo proporciona la máxima eliminación de ruido en señales débiles o ruidosas.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- DeepFilterNet3 (DFNR) debe estar ya seleccionado como motor de reducción de ruido activo. Consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md) si aún no lo ha hecho.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. En el cuadro de diálogo AetherDSP Settings, haga clic en la pestaña **DFNR**.
3. Arrastre el control deslizante **Attenuation Limit** hasta el valor deseado.
4. Cierre el cuadro de diálogo. El valor se guarda de inmediato.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación de ruido máxima que DeepFilterNet3 puede aplicar. 0 es modo de paso directo (sin atenuación); 100 es atenuación máxima. |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro adicional posterior sobre DFNR para una supresión extra. |

## Consejos

- Para señales fuertes en las que se desea preservar el carácter natural del audio, establezca **Attenuation Limit** en un valor más bajo, como 20–40 dB.
- Para señales débiles o con mucho ruido, deje **Attenuation Limit** en 100 para permitir la supresión completa.
- Establecer **Attenuation Limit** en 0 omite efectivamente DeepFilterNet3 sin deshabilitar el motor.

## Temas relacionados

- [Configurar el beta del filtro posterior de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
