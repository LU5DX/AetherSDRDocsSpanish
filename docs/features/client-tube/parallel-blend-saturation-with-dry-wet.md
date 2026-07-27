# Mezcla de saturación en paralelo con Dry/Wet

Use el control Dry/Wet para mezclar la señal saturada del tubo con la señal original sin procesar. Al ajustar Dry/Wet por debajo del 100 %, puede añadir un color armónico sutil sin reemplazar completamente la señal limpia.

## Antes de comenzar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Abra el editor flotante para el lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN para abrir "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE del widget CHAIN en el lado TX o RX.
2. Localice el control **Dry/Wet** en la columna izquierda del editor (el control superior de esa columna).
3. Gire **Dry/Wet** hacia 0 % para incorporar más señal sin procesar, o hacia 100 % para una salida completamente saturada.
4. Observe la curva de transferencia y el indicador de nivel **OUT** en la parte derecha del editor mientras ajusta. Reducir Dry/Wet disminuye la contribución de la señal saturada; use **Output** para compensar si cambia el nivel general.

Alternativamente, ajuste **Mix** directamente desde el mosaico de la applet acoplada sin abrir el editor. El control **Mix** en el mosaico es el mismo control Dry/Wet.

### Edición de valor en línea

Para ingresar un valor numérico preciso para Dry/Wet, haga clic en la visualización del valor debajo del control. Aparece un editor de texto transparente que muestra el valor actual. Escriba el valor deseado (por ejemplo, `67.5`) y presione Enter, o haga clic en otro lugar para confirmar. El valor se limita al rango válido. Presione Escape para cancelar y revertir al valor anterior.

El editor en línea también está disponible en todos los demás controles del editor flotante (Drive, Tone, Bias, Output, Envelope, Attack, Release) y en los controles del mosaico acoplado.

## Qué hace cada control

| Control                                      | Por defecto                                                                                                                                                                         | Rango válido                                                                                                                                                                                               |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Dry/Wet** (editor) / **Mix** (mosaico acoplado) | 100 %                                                                                                                                                                               | 0 % a 100 % (almacenado como 0.0 a 1.0)                                                                                                                                                                       |
| **Drive**                                    | 0.00 dB                                                                                                                                                                             | 0.0 a 24.0 dB                                                                                                                                                                                            |
| **Tone**                                     | 0.00                                                                                                                                                                                | -1.0 a 1.0                                                                                                                                                                                               |
| **Bias**                                     | 0 %                                                                                                                                                                                 | 0 % a 100 % (almacenado como 0.0 a 1.0)                                                                                                                                                                       |
| **Output**                                   | 0.00 dB                                                                                                                                                                             | -24.0 a 12.0 dB                                                                                                                                                                                          |
| **Envelope**                                 | 0 %                                                                                                                                                                                 | -100 % a 100 % (almacenado como -1.0 a 1.0)                                                                                                                                                                   |
| **Attack**                                   | 5.00 ms                                                                                                                                                                             | 0.1 a 30.0 ms                                                                                                                                                                                            |
| **Release**                                  | 35.00 ms                                                                                                                                                                            | 10.0 a 500.0 ms                                                                                                                                                                                          |
| **RN2**                                      | Alternancia solo TX (oculto en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al compuerta/compresor/saturador. | Ubicado en el panel flotante StripTubePanel debajo del indicador de nivel de salida, solo lado TX. Modos de voz únicamente: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. Configuración persistente a través de AudioEngine. |

### Modelos de carácter del tubo

Use los botones de alternancia **A**, **B** y **C** en la fila central del editor para seleccionar el modelo de carácter del tubo. Solo un modelo puede estar activo a la vez.

| Control | Por defecto | Comportamiento                                                                 |
|---------|-------------|---------------------------------------------------------------------------------|
| **A**   | marcado     | Selecciona el modelo de tubo A. Ámbar cuando está marcado. Excluyente con B y C. |
| **B**   | sin marcar  | Selecciona el modelo de tubo B. Ámbar cuando está marcado. Excluyente con A y C. |
| **C**   | sin marcar  | Selecciona el modelo de tubo C. Ámbar cuando está marcado. Excluyente con A y B. |

### Colores visuales de los controles

Los controles de la applet de tubo de AetherSDR usan colores adaptados al tema para todos los componentes. El anillo de fondo del control, el arco de primer plano, la manija, el texto de la etiqueta y el texto del valor leen cada uno de claves de color de tema dedicadas. El contenedor de la applet de tubo (`applet/tube`) puede proporcionar anulaciones por applet (por ejemplo, el color de primer plano del control de la applet de tubo puede diferir del de otras applets). El widget de curva de transferencia también lee su fondo, marco, cuadrícula, ejes, curva, resplandor de la bola y color del núcleo de la bola del tema activo, lo que garantiza una apariencia visual coherente en todos los temas.

## Consejos

- Un valor de Dry/Wet entre el 20 % y el 50 % es efectivo para añadir calidez en TX de SSB sin artefactos de distorsión audibles. La señal seca ancla la fundamental mientras que la señal húmeda contribuye con armónicos.
- Los cambios realizados en el editor flotante y en el mosaico acoplado se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene ambas vistas actualizadas automáticamente.
- Si aumenta **Drive** para obtener más densidad armónica, reducir **Dry/Wet** le permite recuperar una mezcla de sonido natural sin reducir el Drive en sí.
- Use la edición de valor en línea para restaurar exactamente un valor guardado previamente o para establecer un porcentaje de mezcla preciso.

## Solución de problemas

- **Ajustar Dry/Wet no tiene efecto audible**: confirme que la etapa Tube está habilitada. Si la etapa está omitida en el widget CHAIN, la señal pasa sin procesar independientemente de la configuración de Dry/Wet. Cuando la etapa está omitida, todo el mosaico de la applet acoplada se oscurece aproximadamente al 55 % de opacidad como recordatorio visual de que la etapa está inactiva.
- **Cambios de nivel al mover Dry/Wet**: esto es normal. Use el control **Output** (rango −24.0 a 12.0 dB, predeterminado 0.00 dB) para ajustar el nivel posterior a la saturación. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).
- **La edición de valor en línea es rechazada o se revierte**: verifique que su entrada sea un número dentro del rango válido (0 a 100). El análisis sensible a la configuración regional admite la coma como separador decimal. Los caracteres no numéricos se eliminan automáticamente.

## Relacionados

- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
