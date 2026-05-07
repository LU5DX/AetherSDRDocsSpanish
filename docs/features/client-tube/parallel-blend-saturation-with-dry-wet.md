# Saturación combinada en paralelo con Dry/Wet

Use el control Dry/Wet para combinar la señal saturada del tubo con la señal original sin procesar. Al ajustar Dry/Wet por debajo del 100 %, puede añadir un color armónico sutil sin reemplazar completamente la señal limpia.

## Antes de empezar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Abra el editor flotante para el lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN para abrir "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX.
2. Localice el control **Dry/Wet** en la columna izquierda del editor (el control superior de esa columna).
3. Gire **Dry/Wet** hacia 0 % para mezclar más señal sin procesar, o hacia 100 % para obtener una salida completamente saturada.
4. Observe la curva de transferencia y el medidor de nivel **OUT** a la derecha del editor mientras ajusta. Reducir Dry/Wet disminuye la contribución de la señal saturada; use **Output** para compensar si cambia el nivel general.

Alternativamente, ajuste **Mix** directamente desde el mosaico de la applet acoplada sin abrir el editor. El control **Mix** en el mosaico es el mismo control Dry/Wet.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistente |
|---|---|---|---|
| **Dry/Wet** (editor) / **Mix** (mosaico acoplado) | 100 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientTubeTxDryWet` (TX), `ClientTubeRxDryWet` (RX) |

## Consejos

- Un valor de Dry/Wet entre 20 % y 50 % es eficaz para añadir calidez en TX de SSB sin artefactos de distorsión audibles. La señal seca ancla la fundamental mientras que la señal húmeda aporta armónicos.
- Los cambios realizados en el editor flotante y en el mosaico acoplado se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene ambas vistas actualizadas automáticamente.
- Si aumenta **Drive** para obtener más densidad armónica, reducir **Dry/Wet** le permite recuperar una mezcla de sonido natural sin reducir Drive en sí mismo.

## Solución de problemas

- **Ajustar Dry/Wet no tiene efecto audible** — confirme que la etapa Tube esté habilitada. Si la etapa está en bypass en el widget CHAIN, la señal pasa sin procesar independientemente del ajuste de Dry/Wet. Cuando la etapa está en bypass, todo el mosaico de la applet acoplada se atenúa aproximadamente al 55 % de opacidad como recordatorio visual de que la etapa está inactiva.
- **Cambios de nivel al mover Dry/Wet** — esto es normal. Use el control **Output** (rango −24.0 a 12.0 dB, valor predeterminado 0.00 dB) para ajustar el nivel posterior a la saturación. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).

## Relacionados

- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
