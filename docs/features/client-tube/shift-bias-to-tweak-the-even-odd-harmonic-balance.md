# Ajustar el balance de armónicos pares e impares con Bias

El control Bias desplaza el punto de operación en la curva de transferencia del tubo, modificando la proporción de armónicos pares e impares en la señal saturada. Úselo para pasar de un carácter simétrico con predominio de armónicos impares hacia uno más cálido con armónicos pares, o a cualquier punto intermedio.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md) si la etapa está actualmente bypaseada.
- El applet debe estar visible. Si no lo está, abra el contenedor principal Aetherial Audio (TXDSP) y localice el subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX).

## Pasos

1. Localice la fila de cinco controles en la parte inferior del applet: Drive, Tone, Bias, Output, Mix.
2. Encuentre el control denominado **Bias** — el tercero en la fila.
3. Gire el control **Bias** hasta el valor deseado. La etiqueta debajo del control muestra el valor actual como porcentaje (por ejemplo, `50 %`).
4. Observe la curva de transferencia ubicada sobre la fila de controles. El punto de operación de la curva se desplaza al girar el control, visualizando el cambio en el balance de armónicos.
5. La bola de entrada en tiempo real sobre la curva de transferencia se mueve de manera continua, indicando dónde se encuentra el nivel de entrada actual en la nueva curva.

Para abrir el editor flotante ampliado y obtener un control más fino, haga doble clic en la etapa TUBE del widget CHAIN en el lado correspondiente. El editor se titula "Aetherial Tube — TX" o "Aetherial Tube — RX". El control Bias también está disponible allí, y tanto el applet como el editor permanecen sincronizados.

## Función de cada control

| Control | Valor por defecto | Rango válido | Ajuste persistente |
|---|---|---|---|
| Bias (TX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeTxBiasAmount` |
| Bias (RX) | 0 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeRxBiasAmount` |

En 0 % el punto de operación está centrado, produciendo un carácter con predominio de armónicos impares. Al aumentar Bias, el punto de operación se desplaza fuera del centro, introduciendo armónicos pares. La curva de transferencia en el applet refleja visualmente este desplazamiento.

## Consejos

- Bias interactúa con Drive. Valores más altos de Drive introducen más señal en la curva, por lo que el efecto de un ajuste determinado de Bias se vuelve más pronunciado. Ajuste Drive primero y luego afine Bias.
- Los controles del applet y los del editor flotante comparten el mismo estado y se sincronizan en aproximadamente 33 ms tras cualquier cambio realizado en cualquiera de las dos ubicaciones.
- Los cambios se guardan inmediatamente en `ClientTubeTxBiasAmount` o `ClientTubeRxBiasAmount` después de cada movimiento del control.

## Temas relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezclar la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
