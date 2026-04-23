# Vista previa y selección entre las 10 variantes de diseño

El diálogo Panadapter Layout muestra miniaturas de todas las disposiciones de panadapter disponibles para que pueda compararlas de un vistazo y cambiar con un solo clic. Úselo cuando desee cambiar cuántos panadapters son visibles y cómo están organizados.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo requiere una conexión de radio activa.
- La cantidad de diseños seleccionables depende de cuántos panadapters admite la licencia de su radio. Los diseños que requieren más panadapters que su máximo permitido se muestran, pero no pueden seleccionarse.

## Pasos

1. Haga clic derecho en cualquier parte del área del panadapter para abrir el menú contextual.
2. Seleccione la opción de diseño de panadapter en el menú contextual. Se abre el diálogo "Panadapter Layout".
3. Examine las miniaturas. Cada miniatura muestra una vista previa reducida de la disposición con celdas identificadas con letras (A, B, C, …) y una etiqueta como `A|B / C (3 pans)`. El diseño activo actualmente aparece resaltado con un borde azul.
4. Haga clic en la miniatura del diseño que desea. El diálogo se cierra de inmediato y el nuevo diseño se aplica. La selección se guarda en `PanLayout`.
5. Para dejar el diseño sin cambios, haga clic en "Cancel".

## Qué hace cada control

| Control | Descripción | Valores válidos | Clave persistente |
|---|---|---|---|
| Layout buttons | Miniaturas, una por disposición. Haga clic en una miniatura para aplicar ese diseño y cerrar el diálogo. Las miniaturas de diseños que superan la cantidad de panadapters de su radio están deshabilitadas. | `1`, `2v`, `2h`, `2h1`, `12h`, `2x2`, `3h2`, `2x3`, `4h3`, `2x4` | `PanLayout` |
| Cancel | Cierra el diálogo sin cambiar el diseño actual. | — | — |

Los 10 diseños y su cantidad de panadapters son:

| ID de diseño | Etiqueta | Panadapters |
|---|---|---|
| `1` | Single | 1 |
| `2v` | A / B | 2 |
| `2h` | A \| B | 2 |
| `2h1` | A\|B / C | 3 |
| `12h` | A / B\|C | 3 |
| `2x2` | A\|B / C\|D | 4 |
| `3h2` | A\|B\|C / D\|E | 5 |
| `2x3` | A\|B / C\|D / E\|F | 6 |
| `4h3` | A\|B\|C\|D / E\|F\|G | 7 |
| `2x4` | A\|B / C\|D / E\|F / G\|H | 8 |

## Consejos

- La miniatura del diseño activo actualmente tiene un resaltado distintivo para que pueda confirmar su punto de partida antes de realizar un cambio.
- Las miniaturas deshabilitadas muestran una imagen atenuada y un cursor de acceso prohibido. Para habilitarlas, necesita una licencia de radio que admita una mayor cantidad de panadapters.

## Relacionado

- [Descripción general de Panadapter Layout](overview.md)
- [Cambiar a un único panadapter de ancho completo](switch-to-a-single-full-width-panadapter.md)
- [Dividir el área del panadapter en vista lateral](split-panadapter-area-side-by-side.md)
- [Organizar una cuadrícula 2x2 de panadapters](arrange-a-2x2-grid-of-panadapters.md)
