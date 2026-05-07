# Identificar qué segmento es el segmento TX

El Applet de DAX muestra un indicador de asignación TX en vivo que le indica qué segmento posee actualmente los privilegios de TX. Úselo cuando necesite confirmar el segmento de transmisión antes de operar modos digitales o verificar el enrutamiento de audio TX de DAX.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El indicador de asignación TX requiere una conexión activa con la radio.
- El Applet de DAX debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para abrir el Applet de DAX.
2. Observe la fila **TX:** en la parte inferior del applet.
3. Lea el indicador de estado a la derecha de la etiqueta **TX:**. Muestra `—` (ningún segmento TX asignado) o `Slice A` a `Slice H` (el segmento que posee actualmente los privilegios de TX).

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Estados válidos | Clave de configuración |
|---|---|---|---|---|
| Indicador de asignación TX | Muestra qué segmento tiene actualmente privilegios de TX. Se actualiza automáticamente cuando TX se mueve entre segmentos. | `—` | `—` o `Slice A`–`Slice H` | none |

## Consejos

- El indicador TX se actualiza en tiempo real. Si transfiere TX a otro segmento en la radio, el indicador cambia inmediatamente sin necesidad de actualización manual.
- Las filas RX sobre la fila TX muestran las asignaciones DAX por canal (`DAX 1:` a `DAX 4:`). Estas indican qué segmento está enrutado a cada canal RX de DAX y son independientes de la asignación TX.

## Relacionado

- [Ver qué segmento está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Activar DAX para enrutar audio de segmento a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Resumen de audio DAX](overview.md)
