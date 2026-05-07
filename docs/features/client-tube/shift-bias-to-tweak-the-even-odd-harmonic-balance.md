# Ajuste de Bias para modificar el balance de armónicos pares/impares

El control Bias desplaza el punto de operación en la curva de transferencia del tubo, cambiando la proporción de armónicos pares e impares en la señal saturada. Úselo para alternar entre un carácter más cálido y redondo y otro más áspero y asimétrico.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- El applet es visible dentro del contenedor principal "Aetherial Audio (TXDSP)" — "Aetherial Mic-PreAmp" para TX, "Aetherial Dynamic Tube" para RX.
- Se necesita algo de Drive aplicado (Drive > 0.0 dB) para que los cambios armónicos de Bias sean audibles. Consulte [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).

## Pasos

1. Localice el subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) dentro del contenedor principal "Aetherial Audio (TXDSP)", o haga doble clic en la etapa TUBE del widget CHAIN para abrir el editor flotante titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Busque el control **Bias** en la fila central del editor, a la derecha del selector Model.
3. Gire el control Bias. La etiqueta se actualiza en tiempo real, mostrando el valor actual como porcentaje (por ejemplo, `50 %`).
4. Observe la curva de transferencia: a medida que Bias aumenta, la curva se desplaza asimétricamente, incrementando los armónicos pares en relación con los impares.
5. Deténgase en el valor que proporcione el balance armónico deseado. El ajuste se guarda automáticamente.

## Descripción de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste persistente |
|---|---|---|---|
| Bias (TX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeTxBias` |
| Bias (RX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeRxBias` |

Las instancias TX y RX son totalmente independientes. Ajustar Bias en un lado no afecta al otro.

## Monitoreo del nivel posterior a la saturación

El editor flotante ("Aetherial Tube — TX" / "Aetherial Tube — RX") incluye un **Medidor de nivel de salida** etiquetado **OUT** en el extremo derecho del editor. Muestra el nivel pico posterior a la saturación con una balística de ataque rápido / liberación lenta y utiliza las siguientes bandas de color:

| Color | Rango |
|---|---|
| Verde | −60 dB a −12 dB |
| Lima | −12 dB a −6 dB |
| Ámbar | −6 dB a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor solo es visible en el editor flotante. No aparece en el tile del applet acoplado.

## Consejos

- La visualización de la curva de transferencia y su bola de entrada en vivo se actualizan al girar Bias, por lo que puede ver el desplazamiento del punto de operación sin transmitir ni recibir señal.
- Los cambios realizados en el editor flotante y en el applet acoplado se mantienen sincronizados. Un temporizador de 30 Hz mantiene ambas vistas actualizadas, por lo que puede ajustar desde cualquier ubicación.
- Con Bias al 0 %, el tubo opera simétricamente, favoreciendo los armónicos impares. Aumentar Bias introduce asimetría y eleva los armónicos pares. El carácter audible cambia más notablemente cuando Drive está varios dB por encima de su valor predeterminado.
- Use el medidor OUT en el editor flotante para confirmar que los ajustes de Bias no han elevado significativamente el nivel de salida posterior a la saturación. Si el medidor recorta (rojo), reduzca el control Output en consecuencia.

## Relacionados

- [Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX) overview](overview.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Mix](parallel-blend-saturation-with-mix.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
