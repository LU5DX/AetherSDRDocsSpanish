# Configurar el beta del post-filtro DFNR para supresión adicional

Use esta página para ajustar el valor beta del post-filtro de DeepFilterNet3, que aplica una etapa de supresión adicional sobre la reducción de ruido DFNR principal. Aumentar el beta incrementa la eliminación de ruido residual a costa de cierta naturalidad del audio.

## Antes de comenzar

- Abra AetherSDR y confirme que DFNR está activo en el receptor que desea ajustar.
- Tenga en cuenta que `DfnrPostFilterBeta` es independiente de `DfnrAttenLimit`; ambos controles afectan la salida DFNR pero operan en etapas diferentes.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña **DFNR**.
3. Arrastre el control deslizante **Post-Filter Beta** hasta el valor deseado. El valor predeterminado es `0.00` (post-filtro desactivado); el máximo es `0.30`.
4. Suelte el control deslizante. El ajuste se guarda inmediatamente en `DfnrPostFilterBeta`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| **Post-Filter Beta** | 0.00 | 0.00 – 0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para supresión extra después de la etapa principal de DeepFilterNet3. Valores más altos aumentan la supresión. 0.00 desactiva el post-filtro por completo. |
| **Attenuation Limit** | 100 | 0 – 100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3 antes de la etapa del post-filtro. 0 deja pasar el audio sin procesar; 100 aplica la atenuación máxima. |

## Consejos

- Comience con incrementos pequeños de beta (pasos de 0.05) y escuche si hay pérdida de claridad vocal antes de seguir aumentando.
- Si el ruido residual sigue siendo audible después de elevar **Post-Filter Beta** a 0.30, considere también aumentar **Attenuation Limit** en lugar de llevar el beta más allá de su rango.
- Establecer **Post-Filter Beta** en `0.00` deja la salida de DFNR sin cambios por el post-filtro, lo cual es apropiado cuando la etapa de atenuación principal por sí sola ofrece resultados limpios.

## Solución de problemas

- **El audio suena apagado o con exceso de procesamiento** — Reduzca **Post-Filter Beta** hacia `0.00`. Los valores altos de beta suprimen componentes de voz de bajo nivel junto con el ruido.
- **No se percibe ningún cambio al mover el control deslizante** — Confirme que el motor DFNR está habilitado en el receptor activo. El post-filtro no tiene efecto si DFNR no está en funcionamiento.

## Temas relacionados

- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
