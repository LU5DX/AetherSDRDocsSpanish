# Ajustar Bias para modificar el balance de armónicos pares e impares

El control Bias desplaza el punto de operación en la curva de transferencia del tubo, cambiando la proporción de armónicos pares respecto a los impares en la señal saturada. Úselo para moverse entre un carácter más cálido y suave, o uno más áspero y asimétrico.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- El applet es visible dentro del contenedor principal Aetherial Audio (TXDSP) — "Aetherial Mic-PreAmp" para TX, "Aetherial Dynamic Tube" para RX.
- Tener algo de Drive aplicado (Drive > 0.0 dB) hace que los cambios de armónicos provocados por Bias sean audibles. Consulte [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).

## Pasos

1. Localice el subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor flotante titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Encuentre el control **Bias** en la fila central del editor, a la derecha del selector Model.
3. Gire el control Bias. La etiqueta se actualiza en tiempo real y muestra el valor actual como porcentaje (por ejemplo, `50 %`).
4. Observe la curva de transferencia: a medida que Bias aumenta, la curva se desplaza asimétricamente, incrementando los armónicos pares respecto a los impares.
5. Detenga el ajuste en el valor que proporcione el balance de armónicos deseado. La configuración se guarda automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---|---|---|---|
| Bias (TX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeTxBias` |
| Bias (RX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeRxBias` |

Las instancias de TX y RX son completamente independientes. Ajustar Bias en un lado no afecta al otro.

## Monitoreo del nivel posterior a la saturación

El editor flotante ("Aetherial Tube — TX" / "Aetherial Tube — RX") incluye un **medidor de nivel de salida** etiquetado como **OUT** en el extremo derecho del editor. Muestra el nivel de pico posterior a la saturación con balística de ataque rápido y liberación lenta, y utiliza las siguientes bandas de color:

| Color | Rango |
|---|---|
| Verde | −60 dB a −12 dB |
| Lima | −12 dB a −6 dB |
| Ámbar | −6 dB a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor solo es visible en el editor flotante. No aparece en el tile del applet acoplado.

## Consejos

- La pantalla de la curva de transferencia y su indicador de entrada en vivo se actualizan al girar Bias, por lo que puede ver el desplazamiento del punto de operación sin necesidad de transmitir ni recibir señal.
- Los cambios realizados en el editor flotante y en el applet acoplado se mantienen sincronizados. Un temporizador de 30 Hz mantiene ambas vistas actualizadas, de modo que puede realizar ajustes desde cualquier ubicación.
- Con Bias en 0 %, el tubo opera simétricamente, favoreciendo los armónicos impares. Aumentar Bias introduce asimetría e incrementa los armónicos pares. El carácter audible cambia de forma más notable cuando Drive está varios dB por encima de su valor predeterminado.
- Use el medidor OUT en el editor flotante para confirmar que los ajustes de Bias no han elevado significativamente el nivel de salida posterior a la saturación. Si el medidor satura (rojo), reduzca el control Output según corresponda.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezclar la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
