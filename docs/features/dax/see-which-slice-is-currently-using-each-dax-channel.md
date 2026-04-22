# Ver qué slice está usando cada canal DAX en un momento dado

El applet DAX Audio muestra un indicador de estado por canal junto a cada fila de canal DAX. Úselo para confirmar qué slice está enrutado actualmente a DAX 1–4 y qué slice tiene los privilegios de TX, sin necesidad de abrir diálogos adicionales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los indicadores se actualizan desde el estado en vivo del radio y muestran `—` cuando no hay conexión.
- El applet DAX debe estar visible. Está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **DAX** de la barra lateral derecha para abrir el applet DAX Audio.
2. Lea el indicador de estado a la derecha de cada etiqueta de canal:
   - **DAX 1:** a **DAX 4:** — cada uno muestra `—` (ningún slice asignado) o `Slice A` a `Slice H` (el slice actualmente enrutado a ese canal).
   - **TX:** — muestra `—` o la letra del slice que tiene actualmente los privilegios de TX.

No se requiere ninguna acción adicional. Los indicadores se actualizan automáticamente cada vez que cambian las asignaciones DAX de los slices o el slice de TX.

## Qué hace cada control

| Indicador | Ubicación | Valores posibles | Significado |
|---|---|---|---|
| Estado de asignación de slice (DAX 1) | A la derecha de la etiqueta "DAX 1:" | `—`, `Slice A`–`Slice H` | El slice enrutado al canal DAX 1, si existe. |
| Estado de asignación de slice (DAX 2) | A la derecha de la etiqueta "DAX 2:" | `—`, `Slice A`–`Slice H` | El slice enrutado al canal DAX 2, si existe. |
| Estado de asignación de slice (DAX 3) | A la derecha de la etiqueta "DAX 3:" | `—`, `Slice A`–`Slice H` | El slice enrutado al canal DAX 3, si existe. |
| Estado de asignación de slice (DAX 4) | A la derecha de la etiqueta "DAX 4:" | `—`, `Slice A`–`Slice H` | El slice enrutado al canal DAX 4, si existe. |
| Estado de asignación de TX | A la derecha de la etiqueta "TX:" | `—`, `Slice A`–`Slice H` | El slice que tiene actualmente los privilegios de TX (controla el flujo DAX TX). |

Ninguno de estos indicadores tiene una clave de configuración persistente. Son de solo lectura y reflejan el estado en vivo del radio.

## Consejos

- Si todos los indicadores muestran `—` y el radio está conectado, ningún slice tiene asignado un canal DAX. Asigne un canal DAX a un slice desde los controles de slice en la ventana principal.
- El indicador de TX y los indicadores de canales RX se actualizan de forma independiente. Un slice puede aparecer en ambos si es el slice de TX y también tiene asignado un canal DAX RX.

## Relacionado

- [Descripción general de DAX Audio](overview.md)
- [Activar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
