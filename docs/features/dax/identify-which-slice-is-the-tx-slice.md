# Identificar qué slice es el slice de TX

El Applet DAX muestra un indicador de asignación de TX en vivo que le indica qué slice tiene actualmente los privilegios de TX. Utilícelo cuando necesite confirmar el slice de transmisión antes de operar en modos digitales o verificar el enrutamiento de audio DAX TX.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El indicador de asignación de TX requiere una conexión activa con la radio.
- El Applet DAX debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para abrir el Applet DAX.
2. Observe la fila **TX:** en la parte inferior del applet.
3. Lea el indicador de estado a la derecha de la etiqueta **TX:**. Muestra `—` (ningún slice de TX asignado) o una letra de slice `A` a `H` (el slice que actualmente tiene los privilegios de TX). La letra del slice se muestra en un recuadro de color que coincide con el color del slice.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Estados válidos | Clave de configuración |
|---|---|---|---|---|
| DAX Enable | Botón de alternancia que inicia el puente de audio DAX. Interruptor maestro para todos los flujos DAX RX y TX. La etiqueta es "Enable". | off | on/off | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor y deslizador combinados para la ganancia de RX en el canal DAX 1. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Medidor y deslizador combinados para la ganancia de RX en el canal DAX 2. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Medidor y deslizador combinados para la ganancia de RX en el canal DAX 3. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Medidor y deslizador combinados para la ganancia de RX en el canal DAX 4. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor y deslizador combinados para el flujo DAX TX. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| DAX 1 assignment indicator | Muestra qué slice (si lo hay) está enrutado actualmente al canal DAX 1. | `—` | `—` o `Slice A`–`Slice H` | ninguno |
| DAX 2 assignment indicator | Muestra qué slice (si lo hay) está enrutado actualmente al canal DAX 2. | `—` | `—` o `Slice A`–`Slice H` | ninguno |
| DAX 3 assignment indicator | Muestra qué slice (si lo hay) está enrutado actualmente al canal DAX 3. | `—` | `—` o `Slice A`–`Slice H` | ninguno |
| DAX 4 assignment indicator | Muestra qué slice (si lo hay) está enrutado actualmente al canal DAX 4. | `—` | `—` o `Slice A`–`Slice H` | ninguno |
| TX assignment indicator | Muestra qué slice tiene actualmente los privilegios de TX. Se actualiza automáticamente cuando se mueve la TX entre slices. La letra del slice se muestra en un recuadro de color que coincide con el color del slice. | `—` | `—` o letra de slice coloreada `A`–`H` | ninguno |

## Consejos

- El indicador de TX se actualiza en tiempo real. Si transfiere la TX a otro slice en la radio, el indicador cambia inmediatamente sin necesidad de actualización manual.
- Las filas de RX sobre la fila de TX muestran las asignaciones de DAX por canal (`DAX 1:` a `DAX 4:`). Estas indican qué slice está enrutado a cada canal DAX RX y son independientes de la asignación de TX.
- La letra del slice en el indicador de TX se representa como texto enriquecido, lo que permite la visualización del recuadro de color cuando la radio está conectada.
- En Linux con PipeWire, una ruta de origen `pw_stream` nativa reemplaza al cliente PulseAudio anterior, reduciendo la latencia de DAX RX de aproximadamente 400 ms a aproximadamente 200 ms.
- Cada deslizador de ganancia y medidor tiene un nombre accesible para soporte de lectores de pantalla: `DAX RX 1 gain` a `DAX RX 4 gain` para los canales de recepción, y `DAX TX gain` para el canal de transmisión.

## Relacionado

- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Resumen de audio DAX](overview.md)
