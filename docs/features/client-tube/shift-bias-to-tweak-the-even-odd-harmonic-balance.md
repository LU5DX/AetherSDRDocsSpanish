# Ajustar el Bias para equilibrar los armónicos pares e impares

El mando Bias desplaza el punto de operación en la curva de transferencia del tubo, modificando la proporción entre armónicos pares e impares en la señal saturada. Úselo para moverse entre un carácter más cálido y redondeado o uno más áspero y asimétrico.

## Antes de empezar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo en cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- El applet es visible dentro del contenedor principal Aetherial Audio (TXDSP) — "Aetherial Mic-PreAmp" para TX, "Aetherial Dynamic Tube" para RX.
- Aplicar algo de Drive (Drive > 0.0 dB) hace que los cambios de armónicos producidos por Bias sean audibles. Consulte [Ajustar Drive hasta que la curva comience a curvarse (calidez TX o modelado de tono RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).

## Pasos

1. Localice el subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa TUBE del widget CHAIN para abrir el editor flotante titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice el mando **Bias** en la fila de cinco mandos (Drive, Tone, Bias, Output, Mix).
3. Gire el mando Bias. La etiqueta se actualiza en tiempo real y muestra el valor actual como porcentaje (por ejemplo, `50 %`).
4. Observe la curva de transferencia: al aumentar Bias, la curva se desplaza asimétricamente, incrementando los armónicos pares con respecto a los impares.
5. Detenga el ajuste en el valor que proporcione el equilibrio de armónicos deseado. La configuración se guarda automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---|---|---|---|
| Bias (TX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeTxBiasAmount` |
| Bias (RX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeRxBiasAmount` |

Las instancias de TX y RX son completamente independientes. Ajustar Bias en un lado no afecta al otro.

## Consejos

- La pantalla de la curva de transferencia y su punto de entrada en tiempo real se actualizan al girar Bias, de modo que puede ver el desplazamiento del punto de operación sin necesidad de transmitir ni recibir una señal.
- Los cambios realizados en el editor flotante y en el applet acoplado permanecen sincronizados. Un temporizador de 30 Hz mantiene ambas vistas actualizadas, por lo que puede ajustar desde cualquiera de las dos ubicaciones.
- Con Bias al 0 % el tubo opera simétricamente, favoreciendo los armónicos impares. Aumentar Bias introduce asimetría e incrementa los armónicos pares. El carácter audible cambia de forma más notable cuando Drive se encuentra varios dB por encima de su valor predeterminado.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez TX o modelado de tono RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla en paralelo de la saturación con Mix](parallel-blend-saturation-with-mix.md)
- [Omitir el tubo en cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
