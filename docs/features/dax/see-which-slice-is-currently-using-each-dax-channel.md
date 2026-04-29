# Ver qué slice utiliza actualmente cada canal DAX

El applet DAX Audio muestra un indicador de asignación de slice junto a cada canal DAX, de modo que puede confirmar de un vistazo qué slice está enrutado a qué canal sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los indicadores de asignación de slice requieren una conexión activa con el radio.
- Al menos un slice debe tener asignado un canal DAX. Si no hay slices asignados, todos los indicadores muestran `—`.

## Pasos

1. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para abrir el applet DAX Audio.
2. Observe la etiqueta de estado a la derecha de cada etiqueta de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**).
3. Lea el indicador de cada canal. Muestra `—` (ningún slice asignado) o `Slice A` hasta `Slice H` (la letra del slice actualmente enrutado a ese canal).
4. Para ver qué slice está controlando el flujo DAX TX, lea la etiqueta de estado en la fila **TX:**. Sigue el mismo formato: `—` o `Slice A` hasta `Slice H`.

## Qué hace cada control

| Indicador | Ubicación | Valores posibles | Configuración persistente |
|---|---|---|---|
| Estado de asignación de slice (por canal) | A la derecha de las etiquetas **DAX 1:** – **DAX 4:** | `—` o `Slice A`–`Slice H` | Ninguna |
| Estado de asignación TX | A la derecha de la etiqueta **TX:** | `—` o `Slice A`–`Slice H` | Ninguna |

Estos indicadores son de solo lectura. Se actualizan automáticamente cuando cambia la asignación de canal DAX de un slice. La asignación de slice a canal se configura en el propio slice, no en este applet.

## Consejos

- Los indicadores se actualizan en tiempo real. Si cambia la asignación de canal DAX de un slice en el radio o en otra parte de la interfaz, el applet refleja el cambio de inmediato sin necesidad de una actualización manual.
- Un canal que muestra `—` significa que no hay ningún slice asignado actualmente a él; el audio no fluirá por ese canal.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar cuál es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
