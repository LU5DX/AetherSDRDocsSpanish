# Compensar cambios de nivel con Output

El mando **Output** aplica un ajuste de ganancia post-tubo a la señal procesada. Úselo para compensar el aumento o la disminución de nivel que introducen Drive y Bias, de modo que la etapa de tubo no eleve ni reduzca involuntariamente los niveles en el resto de la cadena.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- Abra el applet acoplado ("Aetherial Mic-PreAmp" para TX, "Aetherial Dynamic Tube" para RX) o el editor flotante (haga doble clic en la etapa TUBE en el widget CHAIN).

## Pasos

1. Localice el mando **Output** en la fila de cinco mandos (el cuarto desde la izquierda: Drive, Tone, Bias, **Output**, Mix).
2. Gire **Output** en el sentido de las agujas del reloj para aumentar el nivel post-tubo, o en sentido contrario para reducirlo.
3. Suelte el mando cuando el nivel de salida coincida con su objetivo. La etiqueta debajo del mando se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `0.0 dB`).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste persistente |
|---|---|---|---|
| Output (TX) | 0.0 dB | −24.0 to 12.0 dB | `ClientTubeTxOutputGainDb` |
| Output (RX) | 0.0 dB | −24.0 to 12.0 dB | `ClientTubeRxOutputGainDb` |

Output es una ganancia de compensación o recorte post-tubo. Actúa después de las etapas Drive, Bias y Tone, por lo que ajusta el nivel final sin afectar el carácter de saturación.

## Consejos

- Si al aumentar Drive el volumen sube más de lo deseado, reduzca Output en una cantidad equivalente para mantener el nivel neto constante.
- Los cambios realizados en el editor flotante y en el applet acoplado se mantienen sincronizados. Un temporizador de sondeo a 30 Hz mantiene ambas vistas actualizadas, por lo que un ajuste de Output en una ubicación se refleja inmediatamente en la otra.

## Temas relacionados

- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Mezclar saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
