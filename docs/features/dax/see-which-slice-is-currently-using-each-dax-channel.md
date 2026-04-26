# Ver qué slice está usando cada canal DAX

El applet DAX Audio muestra un indicador por canal junto a cada canal DAX y la fila TX, lo que permite confirmar de un vistazo qué slice está enrutado a qué canal sin necesidad de abrir ningún diálogo adicional.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los indicadores de asignación de slice no se muestran cuando no hay ningún radio conectado.
- El applet DAX debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón `DAX` de la bandeja en la barra lateral derecha para abrir el applet DAX Audio.
2. Observe la etiqueta a la derecha del nombre de cada canal (`DAX 1:` a `DAX 4:` y `TX:`).
3. Lea el indicador de cada canal:
   - `—` significa que no hay ningún slice asignado actualmente a ese canal.
   - `Slice A` a `Slice H` significa que ese slice está enrutado al canal.

No se requiere ninguna acción adicional. Los indicadores se actualizan automáticamente cada vez que cambia la asignación de canal DAX de un slice.

## Qué hace cada control

| Indicador | Ubicación | Valores posibles | Configuración persistida |
|---|---|---|---|
| Estado de asignación de slice | Junto a `DAX 1:` – `DAX 4:` | `—` o `Slice A`–`Slice H` | ninguna |
| Estado de asignación TX | Junto a `TX:` | `—` o `Slice A`–`Slice H` | ninguna |

Los indicadores RX reflejan qué slice ha sido asignado a cada canal DAX en el radio. El indicador TX refleja qué slice tiene actualmente los privilegios de TX; ese slice gestiona el flujo DAX TX.

## Consejos

- Un canal que muestre `—` no transportará audio aunque su control deslizante de ganancia esté por encima de cero. Si espera audio en un canal pero ve `—`, asigne el slice a ese canal DAX desde los controles del slice.
- El indicador TX cambia automáticamente cuando mueve el TX entre slices. No es necesario volver a abrir el applet.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
