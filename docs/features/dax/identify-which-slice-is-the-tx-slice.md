# Identificar qué slice es el slice de TX

El applet DAX muestra un indicador de asignación de TX en tiempo real que le indica qué slice (canal de recepción/transmisión) tiene actualmente los privilegios de TX. Úselo cuando necesite confirmar el slice de transmisión antes de operar modos digitales o verificar el enrutamiento de audio DAX TX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El indicador de asignación de TX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para abrir el applet DAX.
2. Observe la fila **TX:** en la parte inferior del applet.
3. Lea el indicador de estado a la derecha de la etiqueta **TX:**. Muestra `—` (ningún slice de TX asignado) o `Slice A` a `Slice H` (el slice que actualmente tiene los privilegios de TX).

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Estados válidos | Clave de configuración |
|---|---|---|---|---|
| Indicador de asignación de TX | Muestra qué slice tiene actualmente los privilegios de TX. Se actualiza automáticamente cuando el TX se transfiere entre slices. | `—` | `—` o `Slice A`–`Slice H` | ninguna |

## Consejos

- El indicador de TX se actualiza en tiempo real. Si transfiere el TX a otro slice en el radio, el indicador cambia de inmediato sin necesidad de actualización manual.
- Las filas RX sobre la fila TX muestran las asignaciones DAX por canal (`DAX 1:` a `DAX 4:`). Estas indican qué slice está enrutado a cada canal DAX RX y son independientes de la asignación de TX.

## Relacionado

- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Descripción general de audio DAX](overview.md)
