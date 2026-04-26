# Compensar los cambios de nivel con Output

El control Output aplica una ganancia de compensación o ajuste posterior al modelo de tubo, permitiéndole corregir el cambio de nivel que introducen Drive y Bias sin alterar el carácter de la saturación.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo en cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe estar visible en el Panel de Applets.

## Pasos

1. Localice la fila de cinco controles en la parte inferior del subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX).
2. Encuentre el cuarto control, etiquetado como **Output**.
3. Gire el control Output hasta el valor de ganancia deseado. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `0.0 dB`).
   - Gire en sentido horario para aumentar el nivel de salida.
   - Gire en sentido antihorario para reducir el nivel de salida.
4. Suelte el control. El nuevo valor se guarda automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---------|---------------------|--------------|----------------------------|
| Output | 0.0 dB | −24.0 a 12.0 dB | `ClientTubeTxOutputGainDb` / `ClientTubeRxOutputGainDb` |

Output aplica una etapa de ganancia lineal después del modelo de tubo. No afecta a Drive, Bias ni Tone — solo el nivel final de la señal que sale de la etapa de tubo. El formato de la etiqueta es `X.X dB`.

## Consejos

- Si un Drive elevado o un Bias alto provocan que la salida sature en etapas posteriores, reduzca Output para compensar antes de disminuir Drive.
- El control Output del applet y el control Output del editor flotante ("Aetherial Tube — TX" / "— RX") comparten el mismo parámetro. Los cambios en uno se reflejan en el otro en aproximadamente 33 ms.
- Para restaurar el valor predeterminado de 0.0 dB, haga doble clic en el control Output.

## Temas relacionados

- [Ajustar Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplazar Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Mezclar en paralelo la saturación con Mix](parallel-blend-saturation-with-mix.md)
- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
