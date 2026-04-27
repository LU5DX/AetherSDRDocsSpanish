# Saturación de mezcla paralela con Mix

El control Mix mezcla la señal seca (sin procesar) con la salida de tubo completamente saturada. Reducir Mix desde el 100 % permite agregar color armónico mientras se preserva el carácter transitorio y la sensación dinámica de la señal original — una técnica llamada saturación paralela.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible dentro del contenedor principal Aetherial Audio (TXDSP).

## Pasos

1. Localice la fila de cinco controles en la parte inferior del applet — Drive, Tone, Bias, Output, Mix.
2. Encuentre el control más a la derecha, etiquetado como **Mix**.
3. Gire **Mix** para establecer el balance seco/húmedo. Al **100 %** solo pasa la señal saturada. Al **0 %** solo pasa la señal seca. Los valores intermedios mezclan ambas proporcionalmente.
4. Observe la curva de transferencia y escuche el resultado. Un valor alrededor de 30–60 % es típico para la saturación paralela.
5. Si el nivel mezclado es más alto o más bajo que la señal seca, ajústelo con el control **Output**. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---|---|---|---|
| Mix (TX) | 100 % | 0 % a 100 % (almacenado como 0.0–1.0) | `ClientTubeTxDryWet` |
| Mix (RX) | 100 % | 0 % a 100 % (almacenado como 0.0–1.0) | `ClientTubeRxDryWet` |

Mix funciona como una mezcla lineal seco/húmedo. La etiqueta del control muestra el valor como porcentaje (p. ej., `50 %`).

## Consejos

- Los ajustes de Mix realizados en el editor flotante Aetherial Tube se reflejan en el control del applet en aproximadamente 33 ms, y viceversa. No es necesario reabrir el editor después de cambiar Mix en el applet.
- Mix se aplica después de la etapa de tubo pero antes de ningún otro elemento en la cadena — ajuste primero Drive a su gusto, luego use Mix para reducir la intensidad sin perder la forma armónica que configuró.

## Relacionado

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez TX o modelado de tono RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md)
