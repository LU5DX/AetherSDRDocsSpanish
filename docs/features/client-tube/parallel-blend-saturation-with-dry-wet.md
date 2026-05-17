# Saturación combinada en paralelo con control de mezcla (Dry/Wet)

Use el control Dry/Wet para mezclar la señal saturada del tubo con la señal original sin procesar. Al ajustar Dry/Wet por debajo del 100 %, puede agregar un color armónico sutil sin reemplazar completamente la señal limpia.

## Antes de comenzar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Abra el editor flotante para el lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN para abrir "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX.
2. Localice el control **Dry/Wet** en la columna izquierda del editor (el control superior de esa columna).
3. Gire **Dry/Wet** hacia el 0 % para mezclar más señal sin procesar, o hacia el 100 % para obtener una salida completamente saturada.
4. Observe la curva de transferencia y el medidor de nivel **OUT** a la derecha del editor mientras ajusta. Reducir Dry/Wet disminuye la contribución de la señal saturada; use **Output** para compensar si cambia el nivel general.

Alternativamente, ajuste **Mix** directamente desde el mosaico de la applet acoplada sin abrir el editor. El control **Mix** en el mosaico es el mismo control Dry/Wet.

### Edición de valores en línea

Para ingresar un valor numérico preciso para Dry/Wet, haga clic en la pantalla de valor debajo del control. Aparecerá un editor de texto transparente que muestra el valor actual. Escriba el valor deseado (por ejemplo, `67.5`) y presione Enter, o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido. Presione Escape para cancelar y volver al valor anterior.

El editor en línea también está disponible en todos los demás controles del editor flotante (Drive, Tone, Bias, Output, Envelope, Attack, Release) y en los controles del mosaico acoplado.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---|---|---|---|
| **Dry/Wet** (editor) / **Mix** (mosaico acoplado) | 100 % | 0 % a 100 % (almacenado como 0,0 a 1,0) | `ClientTubeTxDryWet` (TX), `ClientTubeRxDryWet` (RX) |

## Consejos

- Un valor de Dry/Wet entre el 20 % y el 50 % es efectivo para agregar calidez en TX de SSB sin artefactos de distorsión audibles. La señal seca ancla la fundamental mientras que la señal húmeda contribuye con armónicos.
- Los cambios realizados en el editor flotante y en el mosaico acoplado se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene ambas vistas actualizadas automáticamente.
- Si aumenta **Drive** para obtener más densidad armónica, reducir **Dry/Wet** le permite recuperar una mezcla de sonido natural sin reducir Drive.
- Use la edición de valores en línea para restaurar exactamente un valor guardado previamente o para establecer un porcentaje de mezcla preciso.

## Solución de problemas

- **Ajustar Dry/Wet no tiene efecto audible** — confirme que la etapa Tube esté habilitada. Si la etapa está en bypass en el widget CHAIN, la señal pasa sin procesar independientemente de la configuración de Dry/Wet. Cuando la etapa está en bypass, todo el mosaico de la applet acoplada se atenúa aproximadamente al 55 % de opacidad como recordatorio visual de que la etapa está inactiva.
- **El nivel cambia al mover Dry/Wet** — esto es normal. Use el control **Output** (rango de −24,0 a 12,0 dB, valor predeterminado 0,00 dB) para ajustar el nivel posterior a la saturación. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).
- **La edición de valores en línea se rechaza o revierte** — verifique que su entrada sea un número dentro del rango válido (0 a 100). El análisis con reconocimiento de configuración regional admite la coma como separador decimal. Los caracteres no numéricos se eliminan automáticamente.

## Relacionados

- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
