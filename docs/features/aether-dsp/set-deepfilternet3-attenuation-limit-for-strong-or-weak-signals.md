# Configurar el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles

La configuración `DfnrAttenLimit` controla con qué agresividad DeepFilterNet3 suprime el ruido. Reducirla preserva más la señal original en señales fuertes y limpias; aumentarla maximiza la supresión en señales enterradas en ruido.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a la radio para ajustar esta configuración.
- DeepFilterNet3 (DFNR) debe estar activo en su cadena de recepción para que esta configuración tenga algún efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña `DFNR`.
3. Arrastre el control deslizante `Attenuation Limit` hasta el valor deseado.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| `Attenuation Limit` | 100 | 0–100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido que DeepFilterNet3 puede aplicar. 0 deja pasar la señal sin procesar; 100 permite la atenuación máxima. |
| `Post-Filter Beta` | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` | Aplica un filtro adicional posterior sobre el límite de atenuación para una supresión extra. |

## Consejos

- Para señales fuertes con un piso de ruido limpio, reduzca `Attenuation Limit` (por ejemplo, 20–40) para disminuir los artefactos de procesamiento y preservar la naturalidad del audio.
- Para señales débiles en ruido intenso, ajuste `Attenuation Limit` a 100 para permitir que DeepFilterNet3 aplique su capacidad de supresión máxima.
- Si persiste ruido residual al llegar a 100, combínelo con un valor distinto de cero en `Post-Filter Beta`. Consulte [Configurar el post-filter beta de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md).

## Solución de problemas

- **Cambiar el control deslizante no produce ningún efecto audible** — Es posible que DFNR no sea el motor de reducción de ruido activo en su slice de recepción. Confirme que DeepFilterNet3 esté habilitado en su cadena de recepción.
- **El audio suena sobreprocesado o distorsionado con valores altos** — Reduzca `Attenuation Limit`. Los valores superiores a 60–70 pueden introducir artefactos en algunos tipos de señal.

## Relacionados

- [Configurar el post-filter beta de DFNR para supresión adicional](configure-dfnr-post-filter-beta-for-extra-suppression.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
