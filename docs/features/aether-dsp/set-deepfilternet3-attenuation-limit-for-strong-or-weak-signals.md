# Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles

Ajuste la agresividad con la que DeepFilterNet3 (DFNR) suprime el ruido. Un límite más bajo preserva más el carácter de la señal en señales ya fuertes; los 100 dB completos son apropiados cuando se necesita la máxima eliminación de ruido.

## Antes de comenzar

- AetherDSP Settings puede abrirse sin una conexión de radio.
- DFNR debe estar activo en un slice receptor para que los cambios tengan efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Arrastre el control deslizante **Attenuation Limit** hasta el valor deseado.

El nuevo valor surte efecto de inmediato; no se requiere confirmación. El ajuste se guarda automáticamente como `DfnrAttenLimit`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| Attenuation Limit | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación de ruido máxima aplicada por DeepFilterNet3. 0 dB es paso total sin filtro; 100 dB es supresión máxima. |
| Post-Filter Beta | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro posterior adicional sobre DFNR para mayor supresión. |

## Consejos

- Establezca **Attenuation Limit** en un valor más bajo (por ejemplo, 20–40 dB) cuando la señal entrante ya sea fuerte y desee evitar el procesamiento excesivo que puede hacer que la voz suene antinatural.
- Establezca **Attenuation Limit** en un valor más alto (por ejemplo, 80–100 dB) cuando el piso de ruido sea alto y la señal sea débil.
- Combine un **Attenuation Limit** moderado con un **Post-Filter Beta** distinto de cero si persiste ruido residual después de aumentar el límite. Consulte [Configurar el post-filter beta de DFNR para mayor supresión](configure-dfnr-post-filter-beta-for-extra-suppression.md).

## Relacionados

- [Configurar el post-filter beta de DFNR para mayor supresión](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
