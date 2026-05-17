# Vea qué slice utiliza cada canal DAX

El applet de audio DAX muestra un indicador de asignación de slice junto a cada canal DAX, para que pueda confirmar de un vistazo qué slice está enrutado a cada lugar sin salir de la ventana principal.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. Los indicadores de asignación de slice requieren una conexión activa con la radio.
- Al menos un slice debe tener asignado un canal DAX. Si no hay slices asignados, todos los indicadores muestran `—`.
- A partir de AetherSDR v26.5.2.1, las letras de los slices se muestran con formato de texto enriquecido para mejorar la visibilidad.

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet de audio DAX.
2. Observe la etiqueta de estado a la derecha de cada nombre de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**).
3. Lea el indicador de cada canal. Muestra `—` (ningún slice asignado) o `Slice A` hasta `Slice H` (la letra del slice enrutado actualmente a ese canal). En v26.5.2.1, la letra del slice puede mostrarse con formato de texto enriquecido para mejorar la legibilidad.
4. Para ver qué slice maneja el flujo DAX de TX, lea la etiqueta de estado en la fila **TX:**. Sigue el mismo formato: `—` o `Slice A` hasta `Slice H`.

## Qué hace cada control

| Indicador | Ubicación | Valores posibles | Ajuste persistente |
|---|---|---|---|
| Estado de asignación de slice (por canal) | A la derecha de las etiquetas **DAX 1:** – **DAX 4:** | `—` o `Slice A`–`Slice H` | Ninguno |
| Estado de asignación de TX | A la derecha de la etiqueta **TX:** | `—` o `Slice A`–`Slice H` | Ninguno |

Estos indicadores son de solo lectura. Se actualizan automáticamente cuando cambia la asignación del canal DAX de un slice. La asignación de slice a canal se configura en el propio slice, no en este applet.

## Consejos

- Los indicadores se actualizan en tiempo real. Si cambia la asignación del canal DAX de un slice en la radio o en otra parte de la interfaz, el applet refleja el cambio inmediatamente sin necesidad de actualización manual.
- Un canal que muestra `—` significa que ningún slice está asignado actualmente; el audio no fluirá por ese canal.
- A partir de v26.5.2.1, las letras de slice en los indicadores de estado pueden usar formato de texto enriquecido. Se trata de un cambio interno; no necesita ajustar ninguna configuración para ver los indicadores correctamente.

## Relacionado

- [Descripción general de DAX Audio](overview.md)
- [Active DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identifique qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Ajuste la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
