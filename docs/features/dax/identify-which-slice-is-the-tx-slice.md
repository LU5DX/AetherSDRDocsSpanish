# Identificar qué slice es el slice TX

El applet DAX muestra un indicador en vivo de asignación TX que le indica qué slice tiene actualmente los privilegios de transmisión. Úselo cuando necesite confirmar el slice de transmisión antes de operar modos digitales o verificar el enrutamiento de audio DAX TX.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El indicador de asignación TX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para abrir el applet DAX.
2. Observe la fila **TX:** en la parte inferior del applet.
3. Lea el indicador de estado a la derecha de la etiqueta **TX:**. Muestra `—` (ningún slice TX asignado) o `Slice A` hasta `Slice H` (el slice que tiene actualmente los privilegios de transmisión).

## Qué hace cada control

| Control | Descripción | Predeterminado | Estados válidos | Clave de configuración |
|---|---|---|---|---|
| Indicador de asignación TX | Muestra qué slice tiene actualmente los privilegios TX. Se actualiza automáticamente cuando el TX se transfiere entre slices. | `—` | `—` o `Slice A`–`Slice H` | none |

## Consejos

- El indicador TX se actualiza en tiempo real. Si transfiere el TX a otro slice en la radio, el indicador cambia de inmediato sin necesidad de actualización manual.
- Las filas RX sobre la fila TX muestran las asignaciones DAX por canal (`DAX 1:` hasta `DAX 4:`). Estas indican qué slice está enrutado a cada canal DAX RX y son independientes de la asignación TX.

## Relacionado

- [Ver qué slice está utilizando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Descripción general de audio DAX](overview.md)
