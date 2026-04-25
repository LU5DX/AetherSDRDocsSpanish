# Configurar el beta del postfiltro DFNR para supresión adicional

Use esta página para ajustar el beta del postfiltro de DeepFilterNet3, que aplica una etapa de supresión adicional sobre la atenuación principal. Aumente este valor cuando el ruido residual siga siendo audible después de configurar el límite de atenuación.

## Antes de comenzar

- AetherDSP Settings se puede abrir sin una conexión de radio activa.
- DFNR (DeepFilterNet3) debe estar seleccionado como motor de reducción de ruido activo. Si no está seguro de qué motor utilizar, consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md).

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña **DFNR**.
3. Ajuste el control deslizante **Post-Filter Beta** al valor deseado (predeterminado: `0.00`, rango: `0.00`–`0.30`).
4. Cierre el diálogo. El valor se guarda inmediatamente al mover el control deslizante.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Attenuation Limit** | `100` | `0`–`100` dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. `0` es paso directo; `100` es el máximo. |
| **Post-Filter Beta** | `0.00` | `0.00`–`0.30` | `DfnrPostFilterBeta` | Aplica un postfiltro adicional para supresión extra sobre el límite de atenuación. |

## Consejos

- Comience con **Post-Filter Beta** en `0.00` y auméntelo en incrementos pequeños. Los valores más altos proporcionan mayor supresión, pero pueden afectar la naturalidad de la voz.
- Si el piso de ruido es aceptable pero ráfagas ocasionales lo superan, pruebe un valor moderado de **Post-Filter Beta**, como `0.05`–`0.10`, antes de aumentar más el **Attenuation Limit**.
- **Attenuation Limit** en `0` omite por completo la atenuación de DFNR, dejando **Post-Filter Beta** como la única etapa activa.

## Solución de problemas

- **Post-Filter Beta no produce efecto audible** — Confirme que DFNR es el motor de reducción de ruido activo en su cadena de recepción. Si **Attenuation Limit** está en `0`, la atenuación de DFNR queda desactivada; aumente primero **Attenuation Limit** para que DFNR procese el audio.
- **La voz suena distorsionada tras aumentar Post-Filter Beta** — Reduzca **Post-Filter Beta** hacia `0.00`. Los valores superiores a `0.15` pueden introducir artefactos audibles en señales débiles o con bajo SNR.

## Relacionados

- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
