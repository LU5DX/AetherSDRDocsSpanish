# Gire Drive hasta que la curva empiece a curvarse (calidez en TX o modelado de tono en RX)

Use el potenciómetro Drive para introducir más señal en la etapa de tubo hasta que la curva de transferencia se curve visiblemente, añadiendo riqueza armónica al audio de TX o modelando el tono del audio recibido.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Si todavía no está activa, habilítela desde el widget CHAIN. Consulte [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md).
- Abra el applet: el applet de tubo TX aparece en el subcontenedor "Aetherial Mic-PreAmp" dentro del contenedor principal Aetherial Audio (TXDSP); el applet de tubo RX aparece en el subcontenedor "Aetherial Dynamic Tube". Haga doble clic en la etapa TUBE del widget CHAIN para abrir el editor flotante correspondiente ("Aetherial Tube — TX" o "Aetherial Tube — RX") si prefiere una vista más amplia.

## Pasos

1. Localice el potenciómetro **Drive** en la fila de cinco controles (Drive, Tone, Bias, Output, Mix).
2. Observe la pantalla **Transfer curve** sobre la fila de potenciómetros. Con el valor predeterminado de 0.0 dB, la curva es casi recta.
3. Gire **Drive** en sentido horario. La etiqueta del potenciómetro se actualiza como `X.X dB`. Aumente Drive hasta que vea que la curva de transferencia empieza a curvarse en su parte superior e inferior — aquí es donde comienza la saturación.
4. Observe el **Live input ball** (el punto que se desplaza sobre la curva de transferencia). Al aumentar Drive, el punto se adentra más en la región curvada durante los picos de señal elevados, mostrando con qué intensidad se está llevando el tubo al límite.
5. Deje de aumentar Drive cuando el grado de curvatura se adapte al efecto deseado. Una curvatura moderada (aproximadamente 6–12 dB de Drive) produce una calidez sutil; valores más altos de Drive producen una saturación más evidente.
6. Si la señal procesada suena más fuerte o más suave que la señal sin procesar, gire el potenciómetro **Output** para compensar. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).
7. La configuración se guarda automáticamente. El valor del potenciómetro se almacena como `ClientTubeTxDriveDb` (TX) o `ClientTubeRxDriveDb` (RX).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave almacenada (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Drive | 0.0 dB | 0.0 a 24.0 dB | `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb` | Introduce más señal en la etapa de tubo; valores más altos curvan más la curva de transferencia. |
| Transfer curve | — | — | — | Muestra la curva de transferencia del tubo. Se curva visiblemente al modificar Drive, Bias o el modelo. |
| Live input ball | — | — | — | Punto que se desplaza a lo largo de la curva de transferencia según el nivel de entrada actual, mostrando el régimen de saturación activo. |

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente. La primera curvatura apreciable en la curva de transferencia suele ser el punto de operación con sonido más musical.
- Los potenciómetros del applet y los del editor flotante permanecen sincronizados. Los cambios realizados en una vista se reflejan en la otra en aproximadamente 33 ms.
- Si desea solo un toque de saturación en lugar de un procesamiento completo, ajuste **Mix** por debajo del 100 % para mezclar de nuevo la señal sin procesar. Consulte [Mezcla paralela de saturación con Mix](parallel-blend-saturation-with-mix.md).
- Tras ajustar Drive, use **Tone** para aclarar u oscurecer el resultado sin modificar la cantidad de saturación. Consulte [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md).
- Use **Bias** para desplazar el punto de operación en la curva y cambiar el carácter armónico de la saturación. Consulte [Ajustar Bias para modificar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md).

## Temas relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md)
- [Ajustar Bias para modificar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla paralela de saturación con Mix](parallel-blend-saturation-with-mix.md)
