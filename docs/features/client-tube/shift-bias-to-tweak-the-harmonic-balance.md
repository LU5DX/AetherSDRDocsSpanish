# Ajuste de Bias para modificar el equilibrio armónico

El mando Bias desplaza el punto de operación en la curva de transferencia del tubo, cambiando el equilibrio entre armónicos pares e impares que genera el saturator. Úselo para ajustar finamente el carácter de la saturación después de haber configurado Drive.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Drive ya debe estar configurado lo suficientemente alto como para que la curva de transferencia se vea visiblemente curvada. Consulte [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).
- Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. El editor se titula "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Localice el mando Bias en la fila central del editor, a la derecha del selector de modelo A / B / C.
2. Gire Bias desde su valor predeterminado de 0 % hacia valores más altos (hasta 100 %) para desplazar el punto de operación y aumentar la saturación asimétrica.
3. Observe la curva de transferencia: la curva desplaza su punto de curvatura a medida que gira el mando. La bola de entrada en vivo rastrea la nueva región de operación en tiempo real.
4. Deténgase cuando el equilibrio armónico suene correcto para su caso de uso.
5. Si el nivel general cambia notablemente, ajuste el mando Output para compensarlo. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---------|---------------------|--------------|-----------------------------------|
| Bias (TX) | 0 % | 0 % a 100 % (interno 0.0 a 1.0) | `ClientTubeTxBias` |
| Bias (RX) | 0 % | 0 % a 100 % (interno 0.0 a 1.0) | `ClientTubeRxBias` |

El mando Bias utiliza un mapeo lineal. El valor mostrado es un porcentaje. Internamente, la configuración se almacena como un valor de 0.0 a 1.0 en `ClientTubeTxBias` (lado TX) o `ClientTubeRxBias` (lado RX).

## Consejos

- Bias interactúa con el carácter de tubo seleccionado. Pruebe cada uno de A, B y C para escuchar cómo el mismo valor de Bias produce diferentes resultados armónicos con distintos modelos.
- El mando Bias también está presente en el mosaico acoplado de applet (la fila compacta de cinco mandos debajo de la curva de transferencia), por lo que puede hacer ajustes rápidos sin abrir el editor completo.
- Los cambios realizados en el mosaico acoplado y en el editor flotante se mantienen sincronizados; un temporizador de 30 Hz mantiene actualizadas ambas vistas.

## Atenuación cuando está en bypass

Cuando la etapa Tube está en bypass, todo el mosaico acoplado de applet se renderiza con opacidad reducida (aproximadamente el 55 % del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa.

## Solución de problemas

- **El mando Bias no tiene efecto audible** — Es posible que Drive esté en o cerca de 0.00 dB. Bias solo desplaza el punto de operación de manera significativa cuando la curva ya está curvada. Aumente Drive primero.
- **Cambios de nivel al ajustar Bias** — Esto es esperado. La asimetría introducida por Bias puede aumentar o disminuir la salida aparente. Ajuste el mando Output para compensar.
- **El mosaico acoplado aparece atenuado** — La etapa Tube está en bypass. Vuelva a habilitarla en el lado TX o RX. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Select a tube character (Model A, B, or C) to change harmonic flavour](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
