# Diseño del Panadapter

Elija cuántos panadapters se muestran y cómo se organizan en el área del panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El cuadro de diálogo de diseño requiere una conexión activa a la radio.
- Su configuración de radio debe ser compatible con la cantidad de panadapters solicitada. El cuadro de diálogo limita los diseños disponibles a aquellos que estén dentro del límite de panadapters de la radio.

## Abrir el cuadro de diálogo

Haga clic con el botón secundario en cualquier lugar del área del panadapter para abrir el cuadro de diálogo **Panadapter Layout**.

## Diseños disponibles

El cuadro de diálogo presenta mosaicos de vista previa para las siguientes disposiciones:

| Valor del diseño | Descripción visual |
|---|---|
| `1` | Un único panadapter de ancho completo |
| `2v` | Dos panadapters apilados verticalmente |
| `2h` | Dos panadapters lado a lado horizontalmente |
| `2h1` | Dos panadapters lado a lado con un tercer panadapter más pequeño debajo |
| `12h` | Un panadapter grande con dos más pequeños lado a lado debajo |
| `2x2` | Cuatro panadapters en una cuadrícula de 2×2 |
| `3h2` | Tres panadapters lado a lado con dos debajo |
| `2x3` | Seis panadapters en una cuadrícula de 2×3 |
| `4h3` | Cuatro panadapters lado a lado con tres debajo |
| `2x4` | Ocho panadapters en una cuadrícula de 2×4 |

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Botones de diseño | Mosaicos de vista previa que representan cada disposición disponible. Haga clic en un mosaico para aplicarlo y cerrar el cuadro de diálogo. Los mosaicos que requieren más panadapters de los que la radio admite se muestran deshabilitados con un cursor de prohibición. | `PanLayout` |
| Cancelar | Cierra el cuadro de diálogo sin cambiar el diseño actual. | — |

## Consejos

- El mosaico de diseño actualmente activo se resalta con un borde distintivo en el cuadro de diálogo, para que pueda ver su punto de partida antes de realizar un cambio.
- Si selecciona un diseño que requiere más panadapters de los que permite el límite de slices actual de la radio, aparece una advertencia en la barra de estado: *"La capacidad de slices está completa; no se puede agregar otro panadapter (<modelo> admite <N> slices)"* y el cambio de diseño se cancela.

## Solución de problemas

- **Un mosaico aparece atenuado y no se puede hacer clic en él** — La conexión a la radio no admite tantos panadapters a la vez. El cuadro de diálogo limita los diseños disponibles a aquellos que estén dentro del límite de panadapters de la radio. Verifique la configuración actual de su radio Flex.
- **Se aplica un cambio de diseño pero la barra de estado muestra una advertencia** — La radio ha alcanzado su capacidad de slices para la conexión actual. El cambio de diseño se cancela; intente usar un diseño con menos panadapters.
- **Hacer clic con el botón secundario en el área del panadapter no hace nada** — AetherSDR no está conectado a una radio. Primero establezca una conexión a través de `Settings > Connect to Radio...`.

## Temas relacionados

- [Panadapter Layout overview](overview.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
