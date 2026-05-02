# Saturación en mezcla paralela con Dry/Wet

Use el control Dry/Wet para mezclar la señal saturada de tubo con la señal original sin procesar. Ajustar Dry/Wet por debajo del 100 % permite añadir color armónico sutil sin reemplazar completamente la señal limpia.

## Antes de comenzar

- La etapa de tubo debe estar habilitada para el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- Abra el editor flotante del lado correspondiente: haga doble clic en la etapa TUBE del widget CHAIN para abrir "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE del widget CHAIN en el lado TX o RX.
2. Localice el mando **Dry/Wet** en la columna izquierda del editor (el mando superior de esa columna).
3. Gire **Dry/Wet** hacia 0 % para incorporar más señal sin procesar, o hacia 100 % para obtener una salida completamente saturada.
4. Observe la curva de transferencia y el medidor de nivel **OUT** a la derecha del editor mientras realiza el ajuste. Reducir Dry/Wet disminuye la contribución de la señal saturada; use **Output** para compensar si el nivel general cambia.

Como alternativa, ajuste **Mix** directamente desde el applet (ficha anclada) sin abrir el editor. El mando **Mix** de la ficha es el mismo control Dry/Wet.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---|---|---|---|
| **Dry/Wet** (editor) / **Mix** (ficha anclada) | 100 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientTubeTxDryWet` (TX), `ClientTubeRxDryWet` (RX) |

## Consejos

- Un valor de Dry/Wet entre 20 % y 50 % es efectivo para añadir calidez en TX SSB sin artefactos de distorsión audibles. La señal seca ancla la fundamental mientras que la señal húmeda aporta armónicos.
- Los cambios realizados en el editor flotante y en la ficha anclada se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene ambas vistas actualizadas automáticamente.
- Si aumenta **Drive** para mayor densidad armónica, reducir **Dry/Wet** permite recuperar una mezcla de sonido natural sin necesidad de reducir Drive.

## Solución de problemas

- **Ajustar Dry/Wet no produce ningún efecto audible** — confirme que la etapa de tubo está habilitada. Si la etapa está omitida en el widget CHAIN, la señal pasa sin procesar independientemente del valor de Dry/Wet.
- **El nivel cambia al mover Dry/Wet** — esto es normal. Use el mando **Output** (rango −24.0 a 12.0 dB, valor predeterminado 0.00 dB) para ajustar el nivel posterior a la saturación. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

## Relacionado

- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Monitorear el recorte de salida con el medidor de nivel en el editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
