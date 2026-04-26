# Aclarar u oscurecer la señal saturada con Tone

El control Tone define el carácter tonal de la salida saturada. Úselo para añadir aire y presencia (valores positivos) o para suavizar la aspereza y calentar el sonido (valores negativos) después de que la etapa de tubo ya ha coloreado la señal.

## Antes de comenzar

- La etapa de tubo debe estar habilitada para el lado correspondiente (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible en el Panel de Applets. Si no está visible, habilite la etapa de tubo mediante el widget CHAIN en el lado correspondiente, o haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor flotante.

## Pasos

1. Localice la fila de cinco controles en la parte inferior del applet Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX). Los controles son, de izquierda a derecha: Drive, Tone, Bias, Output, Mix.
2. Gire el control **Tone** hacia la derecha (positivo) para aclarar la señal saturada, o hacia la izquierda (negativo) para oscurecerla.
3. Lea el valor actual en la etiqueta ubicada debajo del control. La etiqueta se muestra en el formato `X.XX` (por ejemplo, `0.50` o `-0.75`).
4. Suelte el control. La configuración se guarda automáticamente.

Como alternativa, haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor flotante titulado **Aetherial Tube — TX** o **Aetherial Tube — RX**, donde el mismo control Tone está disponible en un tamaño mayor.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---------|---------------------|--------------|-----------------------------------|
| Tone (TX) | `0.00` | −1.0 a 1.0 | `ClientTubeTxTone` |
| Tone (RX) | `0.00` | −1.0 a 1.0 | `ClientTubeRxTone` |

Los valores negativos oscurecen la señal saturada; los valores positivos la aclaran. El mapeo es lineal en todo el rango. Un valor de `0.00` no aplica ninguna corrección tonal.

## Consejos

- Tone actúa sobre la señal después de que la etapa de tubo la colorea con Drive y Bias. Configure Drive y Bias primero, luego use Tone para ajustar el resultado, en lugar de trabajar en el orden inverso.
- La visualización de la curva de transferencia se actualiza en tiempo real mientras ajusta Tone, lo que proporciona una referencia visual junto con el cambio audible.
- Las instancias TX y RX son completamente independientes. Ajustar Tone en el lado TX no tiene ningún efecto en el lado RX y viceversa.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplazar Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
