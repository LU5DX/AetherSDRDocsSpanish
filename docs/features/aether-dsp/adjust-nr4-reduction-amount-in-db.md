# Ajustar la cantidad de reducción de NR4 en dB

La configuración `NR4ReductionAmount` controla cuántos decibeles de reducción de ruido aplica NR4 (libspecbleach). Aumentar este valor suprime más ruido; reducirlo preserva más el carácter original de la señal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar esta configuración.
- Decida con anticipación qué tan agresiva desea que sea la reducción de ruido. Un valor de 10.0 dB es adecuado para la mayoría de las condiciones SSB; valores más altos (20–40 dB) son apropiados para bandas muy ruidosas, pero pueden afectar la fidelidad de la voz.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña **NR4**.
3. Ubique el control deslizante **Reduction (dB):**.
4. Arrastre el control deslizante hacia la izquierda para reducir la cantidad o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del control deslizante.
5. Cierre el diálogo. El valor se guarda de inmediato; no se requiere un paso separado de Apply ni Save.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Control deslizante **Reduction (dB):** | 10.0 dB | 0.0–40.0 dB | `NR4ReductionAmount` |

Ajustar el control deslizante a 0.0 dB desactiva la reducción de NR4 sin apagar el motor NR4. Ajustarlo a 40.0 dB aplica la supresión máxima.

## Consejos

- Si escucha artefactos en la voz o una calidad hueca, reduzca el valor de **Reduction (dB):** en pasos pequeños en lugar de cambiar a un motor de reducción de ruido diferente.
- El control deslizante **Reduction (dB):** funciona junto con **Suppression:** y **Masking Depth:**. Si el resultado general sigue siendo demasiado agresivo después de reducir **Reduction (dB):**, consulte [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md).
- Para restablecer todos los parámetros de NR4 a sus valores predeterminados (incluido **Reduction (dB):** a 10.0 dB), haga clic en **Reset Defaults** en la parte inferior de la pestaña NR4.

## Solución de problemas

- **El control deslizante se mueve, pero el nivel de ruido no cambia** — Es posible que NR4 no sea el motor de reducción de ruido activo para el slice actual. Verifique que NR4 esté habilitado en la cadena de audio antes de ajustar sus parámetros.
- **El valor se restablece a 10.0 después de reiniciar AetherSDR** — La configuración no se guardó correctamente. Confirme que AetherSDR tenga acceso de escritura a su directorio de configuración y que no haya otra instancia en ejecución que pueda estar sobreescribiendo `NR4ReductionAmount`.

## Temas relacionados

- [Habilitar o deshabilitar la estimación de ruido adaptativa de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Ajustar la profundidad de enmascaramiento y la intensidad de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
