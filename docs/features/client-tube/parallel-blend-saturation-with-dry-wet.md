# Saturación combinada en paralelo con Control Seco/Húmedo (Dry/Wet)

Utilice el control Seco/Húmedo (Dry/Wet) para combinar la señal saturada del tubo con la señal original sin procesar. Al ajustar Dry/Wet por debajo del 100 %, puede añadir un sutil color armónico sin reemplazar completamente la señal limpia.

## Antes de empezar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Abra el editor flotante del lado correspondiente: haga doble clic en la etapa TUBE del widget CHAIN para abrir "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE del widget CHAIN en el lado TX o RX.
2. Localice el control **Dry/Wet** en la columna izquierda del editor (el control superior de esa columna).
3. Gire **Dry/Wet** hacia 0 % para incorporar más señal sin procesar, o hacia 100 % para una salida completamente saturada.
4. Observe la curva de transferencia y el medidor de nivel **OUT** en la parte derecha del editor mientras ajusta. Reducir Dry/Wet disminuye la contribución de la señal saturada; utilice **Output** para compensar si el nivel general cambia.

Alternativamente, ajuste **Mix** directamente desde el mosaico de la applet acoplada sin abrir el editor. El control **Mix** del mosaico es el mismo control Dry/Wet.

### Edición inline de valores

Para introducir un valor numérico preciso para Dry/Wet, haga clic en la visualización del valor debajo del control. Aparecerá un editor de texto transparente que muestra el valor actual. Escriba el valor deseado (por ejemplo, `67.5`) y presione Enter, o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido. Presione Escape para cancelar y volver al valor anterior.

El editor inline también está disponible en todos los demás controles del editor flotante (Drive, Tone, Bias, Output, Envelope, Attack, Release) y en los controles del mosaico acoplado.

## Función de cada control

| Control                                                   | Valor por defecto | Rango válido                                                   |
|-----------------------------------------------------------|-------------------|-----------------------------------------------------------------|
| **Dry/Wet** (editor) / **Mix** (mosaico acoplado)         | 100 %             | 0 % a 100 % (almacenado como 0.0 a 1.0)                         |
| RN2                                                       | Alternancia solo en TX (oculto en modo RX). Activa el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al compuerta/compresor/saturador. | Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva mediante AudioEngine. |

### Colores visuales de los controles

Los controles de la applet del tubo de AetherSDR utilizan colores adaptados al tema para todos los componentes de los controles. El anillo de fondo del control, el arco en primer plano, la manija, el texto de la etiqueta y el texto del valor leen cada uno de las claves de color del tema dedicadas. El contenedor de la applet del tubo (`applet/tube`) puede proporcionar anulaciones por applet — por ejemplo, el color del primer plano del control del tubo puede diferir de los colores de los controles de otras applets. El widget de la curva de transferencia también lee su fondo, marco, rejilla, ejes, curva, brillo de la bola y color del núcleo de la bola del tema activo, lo que garantiza una apariencia visual coherente en todos los temas.

## Consejos

- Un valor de Dry/Wet entre 20 % y 50 % es efectivo para añadir calidez en TX de SSB sin artefactos de distorsión audibles. La señal seca ancla la fundamental mientras que la señal húmeda contribuye con armónicos.
- Los cambios realizados en el editor flotante y en el mosaico acoplado se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene ambas vistas actualizadas automáticamente.
- Si aumenta **Drive** para obtener más densidad armónica, reducir **Dry/Wet** le permite recuperar una mezcla de sonido natural sin reducir el propio Drive.
- Utilice la edición inline de valores para restaurar exactamente un valor guardado previamente, o para establecer un porcentaje de mezcla preciso.

## Solución de problemas

- **Ajustar Dry/Wet no tiene efecto audible**: confirme que la etapa Tube está habilitada. Si la etapa está en modo bypass en el widget CHAIN, la señal pasa sin procesar independientemente de la configuración de Dry/Wet. Cuando la etapa está en bypass, todo el mosaico de la applet acoplada se atenúa aproximadamente al 55 % de opacidad como recordatorio visual de que la etapa está inactiva.
- **El nivel cambia al mover Dry/Wet**: esto es normal. Utilice el control **Output** (rango −24.0 a 12.0 dB, valor por defecto 0.00 dB) para ajustar el nivel posterior a la saturación. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).
- **La edición inline del valor se rechaza o se revierte**: verifique que su entrada sea un número dentro del rango válido (0 a 100). El análisis de valores según la configuración regional admite la coma como separador decimal. Los caracteres no numéricos se eliminan automáticamente.

## Relacionados

- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
