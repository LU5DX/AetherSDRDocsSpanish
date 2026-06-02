# Identificar qué slice es el slice de TX

El DAX Applet muestra un indicador de asignación de TX en vivo que le indica qué slice tiene actualmente los privilegios de transmisión. Úselo cuando necesite confirmar el slice de transmisión antes de operar en modos digitales o verificar el enrutamiento de audio DAX TX.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El indicador de asignación de TX requiere una conexión de radio activa.
- El DAX Applet debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para abrir el DAX Applet.
2. Observe la fila **TX:** en la parte inferior del applet.
3. Lea el indicador de estado a la derecha de la etiqueta **TX:**. Muestra `—` (ningún slice de TX asignado) o una letra de slice `A` a `H` (el slice que actualmente tiene los privilegios de TX). La letra del slice se muestra en un cuadro de color que coincide con el color del slice.

## Qué hace cada control

| Control | Descripción | Predeterminado | Estados válidos | Clave de configuración |
|---|---|---|---|---|
| Indicador de asignación de TX | Muestra qué slice tiene actualmente los privilegios de TX. Se actualiza automáticamente cuando la TX se mueve entre slices. La letra del slice se muestra en un cuadro de color que coincide con el color del slice. | `—` | `—` o letra de slice de color `A`–`H` | ninguna |

## Consejos

- El indicador de TX se actualiza en tiempo real. Si transfiere la TX a otro slice en la radio, el indicador cambia inmediatamente sin necesidad de actualización manual.
- Las filas de RX sobre la fila de TX muestran las asignaciones de DAX por canal (`DAX 1:` a `DAX 4:`). Estas indican qué slice está enrutado a cada canal de RX de DAX y son independientes de la asignación de TX.
- La letra del slice en el indicador de TX se representa como texto enriquecido, lo que permite la visualización del cuadro de color cuando la radio está conectada.
- En Linux con PipeWire, una ruta de fuente `pw_stream` nativa reemplaza el cliente PulseAudio anterior, reduciendo la latencia de RX de DAX de aproximadamente 400 ms a aproximadamente 200 ms.

## Relacionado

- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Descripción general del audio DAX](overview.md)
