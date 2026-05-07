# Vista previa y selección entre las 10 variantes de diseño

El cuadro de diálogo "Panadapter Layout" muestra vistas previas en miniatura de todas las disposiciones de panadaptadores disponibles, para que pueda compararlas de un vistazo y cambiar con un solo clic. Úselo siempre que desee modificar cuántos panadaptadores están visibles y cómo están organizados.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El cuadro de diálogo requiere una conexión activa con la radio.
- La cantidad de diseños seleccionables depende de cuántos panadaptadores admita su licencia de radio. Los diseños que requieren más panadaptadores de su máximo se muestran, pero no se pueden seleccionar.

## Pasos

1. Haga clic con el botón derecho en cualquier lugar del área de panadaptadores para abrir el menú contextual.
2. Seleccione la opción de diseño de panadaptadores del menú contextual. Se abre el cuadro de diálogo "Panadapter Layout".
3. Examine las miniaturas. Cada miniatura muestra una vista previa en miniatura de la disposición con celdas con letras (A, B, C, …) y una etiqueta como `A|B / C (3 pans)`. El diseño actualmente activo está resaltado con un borde azul.
4. Haga clic en la miniatura del diseño que desee. El cuadro de diálogo se cierra inmediatamente y se aplica el nuevo diseño. La selección se guarda en `PanLayout`.
5. Para dejar el diseño sin cambios, haga clic en "Cancel".

## Descripción de cada control

| Control | Descripción | Valores válidos | Clave persistida |
|---|---|---|---|
| Botones de diseño | Miniaturas, una por cada disposición. Haga clic en una miniatura para aplicar ese diseño y cerrar el cuadro de diálogo. Las miniaturas de diseños que exceden la cantidad de panadaptadores de su radio están deshabilitadas. | `1`, `2v`, `2h`, `2h1`, `12h`, `2x2`, `3h2`, `2x3`, `4h3`, `2x4` | `PanLayout` |
| Cancel | Cierra el cuadro de diálogo sin cambiar el diseño actual. | — | — |

Los 10 diseños y sus cantidades de panadaptadores son:

| ID de diseño | Etiqueta | Pan. |
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

- La miniatura del diseño actualmente activo tiene un resalte distintivo para que pueda confirmar su punto de partida antes de realizar un cambio.
- Las miniaturas deshabilitadas muestran una imagen atenuada y un cursor de prohibición. Para desbloquearlas, necesita una licencia de radio que admita una mayor cantidad de panadaptadores.

## Relacionados

- [Panadapter Layout overview](overview.md)
- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Arrange a 2x2 grid of panadapters](arrange-a-2x2-grid-of-panadapters.md)
