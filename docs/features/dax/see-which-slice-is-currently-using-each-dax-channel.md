# Vea qué segmento está usando cada canal DAX

El applet de audio DAX muestra un indicador de asignación de segmento junto a cada canal DAX, para que pueda confirmar de un vistazo qué segmento está enrutado a dónde sin salir de la ventana principal.

## Antes de empezar

- AetherSDR debe estar conectado al radio. Los indicadores de asignación de segmento requieren una conexión activa al radio.
- Al menos un segmento debe tener asignado un canal DAX. Si no hay segmentos asignados, todos los indicadores muestran `—`.

## Pasos

1. Haga clic en el botón **DAX** de la barra lateral derecha para abrir el applet de audio DAX.
2. Observe la etiqueta de estado a la derecha de cada etiqueta de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**).
3. Lea el indicador de cada canal. Muestra `—` (ningún segmento asignado) o `Slice A` hasta `Slice H` (la letra del segmento enrutado actualmente a ese canal).
4. Para ver qué segmento está enviando la transmisión DAX, lea la etiqueta de estado en la fila **TX:**. Sigue el mismo formato: `—` o `Slice A` hasta `Slice H`.

## Función de cada control

| Indicador | Ubicación | Valores posibles | Configuración persistente |
|---|---|---|---|
| Estado de asignación de segmento (por canal) | Derecha de las etiquetas **DAX 1:** – **DAX 4:** | `—` o `Slice A`–`Slice H` | Ninguna |
| Estado de asignación de TX | Derecha de la etiqueta **TX:** | `—` o `Slice A`–`Slice H` | Ninguna |

Estos indicadores son de solo lectura. Se actualizan automáticamente cuando cambia la asignación de canal DAX de un segmento. La asignación segmento-a-canal se configura en el propio segmento, no en este applet.

## Consejos

- Los indicadores se actualizan en tiempo real. Si cambia la asignación de canal DAX de un segmento en el radio o en otra parte de la interfaz, el applet refleja el cambio de inmediato sin necesidad de una actualización manual.
- Un canal que muestra `—` significa que ningún segmento está asignado actualmente; el audio no fluirá por ese canal.

## Relacionados

- [Resumen de audio DAX](overview.md)
- [Active DAX para enrutar audio de segmento a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identifique qué segmento es el segmento de TX](identify-which-slice-is-the-tx-slice.md)
- [Configure la ganancia de RX DAX por canal](set-dax-rx-gain-per-channel.md)
