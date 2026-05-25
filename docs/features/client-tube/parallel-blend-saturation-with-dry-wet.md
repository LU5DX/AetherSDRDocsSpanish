# Saturación en paralelo con control Dry/Wet

Use el control Dry/Wet para mezclar la señal saturada del tubo con la señal original sin procesar. Ajustar Dry/Wet por debajo del 100 % le permite marcar un color armónico sutil sin reemplazar completamente la señal limpia.

## Antes de comenzar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Abra el editor flotante para el lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN para abrir "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX.
2. Localice la perilla **Dry/Wet** en la columna izquierda del editor (la perilla superior de esa columna).
3. Gire **Dry/Wet** hacia 0 % para incorporar más señal sin procesar, o hacia 100 % para obtener una salida completamente saturada.
4. Observe la curva de transferencia y el medidor de nivel **OUT** a la derecha del editor mientras ajusta. Reducir Dry/Wet disminuye la contribución de la señal saturada; use **Output** para compensar si el nivel general cambia.

Alternativamente, ajuste **Mix** directamente desde el mosaico de la applet acoplada sin abrir el editor. La perilla **Mix** en el mosaico es el mismo control Dry/Wet.

### Edición inline de valores

Para ingresar un valor numérico preciso para Dry/Wet, haga clic en la visualización del valor debajo de la perilla. Aparece un editor de texto transparente que muestra el valor actual. Escriba el valor deseado (por ejemplo, `67.5`) y presione Enter, o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido. Presione Escape para cancelar y revertir al valor anterior.

El editor inline también está disponible en todas las demás perillas del editor flotante (Drive, Tone, Bias, Output, Envelope, Attack, Release) y en las perillas del mosaico acoplado.

## Función de cada control

| Control                                      | Predeterminado                                                                                                                                                                     | Rango válido                                                                                                                                                                                               |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Dry/Wet** (editor) / **Mix** (mosaico acoplado) | 100 %                                                                                                                                                                               | 0 % a 100 % (almacenado como 0.0 a 1.0)                                                                                                                                                                       |
| RN2                                          | Alternancia solo TX (oculto en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada de micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al compuerta/compresor/saturador. | Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo lado TX. Solo modos de voz — los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva mediante AudioEngine. |
## Consejos

- Un valor de Dry/Wet entre 20 % y 50 % es efectivo para agregar calidez en TX de SSB sin artefactos de distorsión audibles. La señal seca ancla la fundamental mientras que la señal húmeda contribuye con armónicos.
- Los cambios realizados en el editor flotante y en el mosaico acoplado se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene ambas vistas actualizadas automáticamente.
- Si aumenta **Drive** para obtener más densidad armónica, reducir **Dry/Wet** le permite recuperar una mezcla de sonido natural sin reducir Drive por sí mismo.
- Use la edición inline de valores para restaurar exactamente un valor guardado previamente, o para establecer un porcentaje de mezcla preciso.

## Solución de problemas

- **Ajustar Dry/Wet no tiene efecto audible** — confirme que la etapa Tube esté habilitada. Si la etapa está omitida en el widget CHAIN, la señal pasa sin procesar independientemente del ajuste de Dry/Wet. Cuando la etapa está omitida, todo el mosaico de la applet acoplada se atenúa aproximadamente al 55 % de opacidad como recordatorio visual de que la etapa está inactiva.
- **El nivel cambia al mover Dry/Wet** — esto es esperado. Use la perilla **Output** (rango −24.0 a 12.0 dB, predeterminado 0.00 dB) para ajustar el nivel posterior a la saturación. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).
- **La edición inline de valores es rechazada o se revierte** — verifique que su entrada sea un número en el rango válido (0 a 100). El análisis con reconocimiento de configuración regional admite la coma como separador decimal. Los caracteres no numéricos se eliminan automáticamente.

## Relacionados

- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
