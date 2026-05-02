# Compensar cambios de nivel con Output

El control **Output** aplica un ajuste de ganancia post-tubo a la señal procesada. Úselo para compensar el aumento o la disminución de nivel que introducen Drive y Bias, de modo que la etapa de tubo no eleve ni reduzca involuntariamente los niveles en el resto de la cadena.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- Abra el applet acoplado ("Aetherial Mic-PreAmp" para TX, "Aetherial Dynamic Tube" para RX) o el editor flotante (haga doble clic en la etapa TUBE en el widget CHAIN).

## Pasos

1. Localice el control **Output** en la fila de cinco mandos (el cuarto desde la izquierda: Drive, Tone, Bias, **Output**, Mix).
2. Gire **Output** en sentido horario para aumentar el nivel post-tubo, o en sentido antihorario para reducirlo.
3. Suelte el control cuando el nivel de salida coincida con su objetivo. La etiqueta debajo del mando se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `0.0 dB`).
4. Opcionalmente, observe el medidor de nivel **OUT** en el extremo derecho del editor flotante para confirmar el nivel de pico post-saturación. El medidor solo es visible en el editor flotante, no en el panel del applet acoplado.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste persistente |
|---|---|---|---|
| Output (TX) | 0.0 dB | −24.0 to 12.0 dB | `ClientTubeTxOutputDb` |
| Output (RX) | 0.0 dB | −24.0 to 12.0 dB | `ClientTubeRxOutputDb` |

Output es una ganancia de compensación o recorte post-tubo. Actúa después de las etapas Drive, Bias y Tone, por lo que ajusta el nivel final sin afectar el carácter de saturación.

## Medidor de nivel de salida

El editor flotante incluye un medidor de nivel pico **OUT** (el widget `ClientLevelMeter`) ubicado en el extremo derecho del panel del editor. Muestra el nivel de pico post-saturación con balística de ataque rápido y liberación lenta, y utiliza las siguientes bandas de color:

| Color | Rango de nivel |
|---|---|
| Verde | −60 to −12 dB |
| Lima | −12 to −6 dB |
| Ámbar | −6 to −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el panel del applet acoplado. Se actualiza de forma continua junto con los controles mientras el editor flotante está abierto.

## Consejos

- Si al aumentar Drive el volumen sube más de lo deseado, reduzca Output en una cantidad equivalente para mantener el nivel neto constante.
- Use el medidor **OUT** en el editor flotante para verificar que la señal post-tubo se mantenga por debajo de −3 dB (rojo) en condiciones normales de operación.
- Los cambios realizados en el editor flotante y en el applet acoplado permanecen sincronizados. Un temporizador de muestreo a 30 Hz mantiene ambas vistas actualizadas, por lo que ajustar Output en una ubicación se refleja de inmediato en la otra.

## Temas relacionados

- [Ajustar Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Mezclar saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
