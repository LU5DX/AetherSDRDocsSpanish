# Diseño del Panadapter

Elija cuántos panadapters se muestran y cómo se organizan en el área del panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de diseño requiere una conexión activa con la radio.
- La configuración de su radio debe admitir la cantidad solicitada de panadapters. El diálogo limita los diseños disponibles a aquellos dentro del número de panadapters de la radio.

## Abrir el diálogo

Haga clic derecho en cualquier lugar del área del panadapter para abrir el diálogo **Panadapter Layout**.

## Diseños disponibles

El diálogo presenta mosaicos de vista previa para las siguientes disposiciones:

| Valor de diseño | Descripción visual |
|---|---|
| `1` | Un solo panadapter de ancho completo |
| `2v` | Dos panadapters apilados verticalmente |
| `2h` | Dos panadapters uno al lado del otro horizontalmente |
| `2h1` | Dos panadapters uno al lado del otro con un tercer panadapter más pequeño debajo |
| `12h` | Un panadapter grande con dos más pequeños uno al lado del otro debajo |
| `2x2` | Cuatro panadapters en una cuadrícula de 2×2 |
| `3h2` | Tres panadapters uno al lado del otro con dos debajo |
| `2x3` | Seis panadapters en una cuadrícula de 2×3 |
| `4h3` | Cuatro panadapters uno al lado del otro con tres debajo |
| `2x4` | Ocho panadapters en una cuadrícula de 2×4 |

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Botones de diseño | Mosaicos de vista previa que representan cada disposición disponible. Haga clic en un mosaico para aplicarlo y cerrar el diálogo. Los mosaicos que requieren más panadapters de los que la radio admite se muestran deshabilitados con un cursor prohibido. | `PanLayout` |
| Cancelar | Cierra el diálogo sin cambiar el diseño actual. | — |

## Consejos

- El mosaico de diseño actualmente activo se resalta con un borde distintivo en el diálogo, para que pueda ver su punto de partida antes de realizar un cambio.
- Si selecciona un diseño que requiere más panadapters de los que permite el límite de slices actual de la radio, aparece una advertencia en la barra de estado: *"La capacidad de slices está completa; no se puede agregar otro panadapter (<modelo> admite <N> slices)"* y el cambio de diseño se cancela.

## Solución de problemas

- **Un mosaico aparece atenuado y no se puede hacer clic** — La conexión de la radio no admite tantos panadapters a la vez. El diálogo limita los diseños disponibles a aquellos dentro del número de panadapters de la radio. Verifique la configuración actual de su radio Flex.
- **Se aplica un cambio de diseño, pero la barra de estado muestra una advertencia** — La radio ha alcanzado su capacidad de slices para la conexión actual. El cambio de diseño se cancela; intente con un diseño que tenga menos panadapters.
- **Hacer clic derecho en el área del panadapter no hace nada** — AetherSDR no está conectado a una radio. Establezca una conexión a través de `Settings > Connect to Radio...` primero.

## Relacionado

- [Descripción general del diseño del Panadapter](overview.md)
- [Dividir el área del panadapter lado a lado](split-panadapter-area-side-by-side.md)
- [Cambiar a un solo panadapter de ancho completo](switch-to-a-single-full-width-panadapter.md)
