# Compensar los cambios de nivel con Output

La perilla Output aplica un ajuste de ganancia posterior al tubo sobre la señal procesada. Úsela para compensar el aumento o la disminución de nivel que introducen Drive y Bias, de modo que la etapa de tubo no altere involuntariamente los niveles en el resto de la cadena.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Abra el applet acoplado ("Aetherial Mic-PreAmp" para TX, "Aetherial Dynamic Tube" para RX) o el editor flotante (haga doble clic en la etapa TUBE en el widget CHAIN).

## Pasos

1. Localice la perilla **Output** en la fila de cinco perillas (cuarta desde la izquierda: Drive, Tone, Bias, **Output**, Mix).
2. Gire **Output** en sentido horario para aumentar el nivel posterior al tubo, o en sentido antihorario para reducirlo.
3. Suelte la perilla cuando el nivel de salida coincida con su objetivo. La etiqueta debajo de la perilla se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `0.0 dB`).
4. Opcionalmente, observe el medidor de nivel **OUT** en el extremo derecho del editor flotante para confirmar el nivel pico posterior a la saturación. El medidor solo es visible en el editor flotante, no en el mosaico del applet acoplado.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste persistente |
|---|---|---|---|
| Output (TX) | 0.0 dB | −24.0 a 12.0 dB | `ClientTubeTxOutputDb` |
| Output (RX) | 0.0 dB | −24.0 a 12.0 dB | `ClientTubeRxOutputDb` |

Output es una ganancia de maquillaje o ajuste posterior al tubo. Actúa después de las etapas Drive, Bias y Tone, por lo que ajusta el nivel final sin afectar el carácter de saturación.

## Medidor de nivel de salida

El editor flotante incluye un medidor de nivel pico **OUT** (el widget `ClientLevelMeter`) ubicado en el extremo derecho del panel del editor. Muestra el nivel pico posterior a la saturación con balística de ataque rápido y liberación lenta y utiliza las siguientes bandas de color:

| Color | Rango de nivel |
|---|---|
| Verde | −60 a −12 dB |
| Lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el mosaico del applet acoplado. Se actualiza continuamente junto con los controles de perilla siempre que el editor flotante esté abierto.

## Atenuación en bypass

Cuando la etapa de tubo está en bypass, todo el mosaico del applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % de lo normal). Esto coincide con el efecto de atenuación utilizado en el mosaico de la curva EQ y proporciona una indicación visual clara de que la etapa no está procesando audio. El mosaico vuelve a la opacidad total tan pronto como se vuelve a habilitar la etapa.

## Consejos

- Si aumentar Drive incrementa el volumen más de lo deseado, reduzca Output en una cantidad equivalente para mantener el nivel neto consistente.
- Use el medidor **OUT** en el editor flotante para verificar que la señal posterior al tubo se mantenga por debajo de −3 dB (rojo) en condiciones normales de operación.
- Los cambios realizados en el editor flotante y en el applet acoplado se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene ambas vistas actualizadas, por lo que ajustar Output en un lugar se refleja inmediatamente en el otro.
- Cuando el mosaico del applet aparece atenuado, la etapa de tubo está en bypass. Vuelva a habilitarla antes de realizar ajustes en Output; de lo contrario, el ajuste no tendrá efecto en la señal en vivo.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Parallel-blend saturation with Mix](parallel-blend-saturation-with-mix.md)
- [Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX) overview](overview.md)
