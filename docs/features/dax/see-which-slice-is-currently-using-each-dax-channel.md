# Ver qué slice está usando cada canal DAX

El applet DAX Audio muestra un indicador de asignación de slice junto a cada canal DAX para que pueda confirmar de un vistazo qué slice está enrutado a cada destino, sin abrir ningún menú ni cuadro de diálogo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los indicadores de asignación de slice reflejan el estado en vivo del radio y muestran `—` cuando no hay ningún radio conectado.
- El applet DAX debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón de bandeja **DAX** de la barra lateral derecha para abrir el applet DAX Audio.
2. Observe el indicador de estado a la derecha de cada etiqueta de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**).
3. Lea el valor del indicador:
   - `Slice A` hasta `Slice H` — ese slice está enrutado actualmente a este canal DAX.
   - `—` — ningún slice está asignado a este canal.
4. Para verificar qué slice está controlando actualmente el flujo DAX TX, lea el indicador de estado a la derecha de la etiqueta **TX:**.

## Qué hace cada control

| Etiqueta | Tipo | Valores posibles | Significado |
|---|---|---|---|
| Indicador de asignación de slice (DAX 1–4) | Indicador | `—` o `Slice A`–`Slice H` | El slice enrutado actualmente a ese canal RX. Se actualiza automáticamente cuando cambian las asignaciones DAX de los slices. Sin configuración persistida. |
| Indicador de asignación TX | Indicador | `—` o `Slice A`–`Slice H` | El slice que tiene actualmente los privilegios de TX. Se actualiza automáticamente cuando cambia el slice TX. Sin configuración persistida. |

## Consejos

- Los indicadores se actualizan en tiempo real. Si reasigna un slice a un canal DAX diferente en el radio, la etiqueta cambia de inmediato sin necesidad de actualización manual.
- Un canal que muestra `—` no transporta audio. Si espera audio en un canal y ve `—`, asigne un canal DAX al slice correspondiente desde el radio o desde los controles de slice en AetherSDR.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar cuál es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
