# Configurar el beta del postfiltro de DFNR para una supresión adicional

La pestaña DFNR en AetherDSP Settings permite aplicar un postfiltro adicional sobre la reducción de ruido principal de DeepFilterNet3. Aumentar el valor de Post-Filter Beta incrementa la supresión más allá de lo que proporciona el límite de atenuación por sí solo, a costa de cierta fidelidad de la voz.

## Antes de comenzar

- AetherDSP Settings puede abrirse sin una conexión a un radio, pero el efecto solo es audible durante la recepción en vivo.
- Verifique que DeepFilterNet3 ya esté activo en su receptor de slice antes de ajustar estos parámetros. Consulte [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md) para saber cómo habilitarlo y configurar el límite de atenuación.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **DFNR**.
3. Localice el control deslizante **Post-Filter Beta**.
4. Arrastre el control hacia la derecha para aumentar la supresión del postfiltro. El rango válido es 0.00–0.30; el valor predeterminado es 0.00 (postfiltro inactivo).
5. Suelte el control deslizante. El valor se guarda inmediatamente en `DfnrPostFilterBeta`.
6. Supervise la calidad del audio. Si la voz suena hueca o distorsionada, reduzca el valor hacia 0.00.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Attenuation Limit** | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo. |
| **Post-Filter Beta** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un postfiltro adicional sobre DeepFilterNet3 para una supresión extra. Valores más altos suprimen más ruido residual. |

## Consejos

- Comience con **Post-Filter Beta** en 0.10 o por debajo. Los artefactos audibles tienden a aparecer antes de alcanzar 0.30, especialmente en señales de voz SSB.
- Si necesita una atenuación general más fuerte sin modificar el postfiltro, aumente primero **Attenuation Limit** y luego agregue **Post-Filter Beta** solo para el ruido residual que permanezca.
- Un valor de 0.00 desactiva el postfiltro por completo, dejando la salida de DeepFilterNet3 sin cambios.

## Solución de problemas

- **La voz suena hueca o con efecto de fase** — **Post-Filter Beta** está configurado demasiado alto. Redúzcalo hacia 0.00 en incrementos pequeños hasta que la naturalidad regrese.
- **No se percibe ningún cambio al mover el control deslizante** — Es posible que DeepFilterNet3 no esté activo en el slice actual. Confirme que el motor DFNR esté seleccionado y que **Attenuation Limit** sea mayor que 0.

## Temas relacionados

- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
