# Identificar qué slice es el slice TX

El applet DAX Audio muestra un indicador en vivo de asignación TX para que pueda ver de un vistazo qué slice (canal de receptor virtual) tiene actualmente los privilegios de transmisión. Esto es útil cuando se operan múltiples slices o software de modos digitales, donde es necesario confirmar que el slice correcto está controlando el flujo DAX TX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El indicador de asignación TX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Si no lo está, haga clic en el botón DAX de la barra lateral derecha para abrirlo.

## Pasos

1. Haga clic en el botón DAX de la barra lateral derecha para abrir el applet DAX Audio.
2. Observe la fila TX en la parte inferior del applet. La etiqueta inmediatamente a la derecha de "TX:" muestra el slice TX actual.
3. Lea el indicador de asignación TX. Muestra `—` (ningún slice TX asignado) o `Slice A` hasta `Slice H` (la letra del slice que actualmente tiene los privilegios TX).

## Qué hace cada control

| Control | Descripción | Estados |
|---|---|---|
| Indicador de asignación TX | Muestra qué slice tiene actualmente los privilegios TX y controla el flujo DAX TX. Se actualiza automáticamente cuando se transfiere el TX entre slices. Sin configuración persistente. | `—` o `Slice A`–`Slice H` |

## Consejos

- El indicador TX se actualiza en tiempo real. Si transfiere el TX a un slice diferente (por ejemplo, haciendo clic en el botón TX de un slice en el panadapter), el indicador cambia inmediatamente sin necesidad de ninguna acción en el applet DAX.
- Las filas de canales RX ubicadas sobre la fila TX tienen cada una su propio indicador de asignación de slice, que muestra `—` o `Slice A`–`Slice H`. Esas filas indican qué slice está enrutado a cada canal DAX RX, lo cual es independiente de la asignación TX. Consulte [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md).

## Relacionados

- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software de modos digitales](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Descripción general de DAX Audio](overview.md)
