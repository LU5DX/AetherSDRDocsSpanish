# Descripción General del Diseño de Panadapters

La función de Diseño de Panadapters controla cuántos panadapters se muestran y cómo se organizan en la pantalla. Úsela para adaptarse a su estilo de operación, desde una única vista de ancho completo hasta una cuadrícula de ocho panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. Los botones de diseño para configuraciones que requieren más panadapters de los que la radio soporta están deshabilitados.
- La radio tiene un límite de slices que determina el número máximo de panadapters. Si la radio ya está al límite de su capacidad de slices cuando se solicita un diseño más grande, se muestra una advertencia en la barra de estado y el cambio de diseño se cancela.

## Cómo funciona

Haga clic derecho en el área del panadapter para abrir el cuadro de diálogo **Panadapter Layout**. El cuadro de diálogo presenta una cuadrícula de vistas previas en miniatura, cada una mostrando una disposición etiquetada de celdas con letras (A, B, C, etc.). El diseño actualmente activo se resalta con un borde color verde azulado.

Haga clic en cualquier miniatura habilitada para aplicar ese diseño inmediatamente. El cuadro de diálogo se cierra y AetherSDR reorganiza el área del panadapter. Haga clic en **Cancel** para cerrar el cuadro de diálogo sin realizar cambios.

El diseño elegido se guarda como `PanLayout`.

Las miniaturas de configuraciones que exceden el número de panadapters que su radio soporta se muestran atenuadas y no se pueden seleccionar. Si el límite de slices de la radio ya está al máximo cuando se aplica un diseño más grande, se muestra un mensaje en la barra de estado: "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y el cambio de diseño se cancela.

## Función de cada control

| Control | Descripción | Diseños disponibles | Configuración persistente |
|---|---|---|---|
| Botones de diseño | Iconos de vista previa: haga clic en uno para aplicar esa disposición. | `1`, `2v`, `2h`, `2h1`, `12h`, `2x2`, `3h2`, `2x3`, `4h3`, `2x4` | `PanLayout` |
| **Cancel** | Cierra el cuadro de diálogo sin cambiar el diseño actual. | — | — |

Las disposiciones disponibles son:

| ID de diseño | Etiqueta | Cantidad de panadapters |
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

- Cada etiqueta de miniatura muestra la cantidad de panadapters, por ejemplo "A\|B / C (3 pans)", para que pueda confirmar la cantidad antes de hacer clic.
- Los diseños que requieren más panadapters de los que la radio proporciona están deshabilitados y muestran un cursor de prohibición al pasar el ratón. Conéctese a una radio que soporte la cantidad deseada de panadapters para habilitarlos.
- Si intenta seleccionar un diseño que requiere más panadapters cuando el límite de slices de su radio ya está al máximo, revise la barra de estado para ver un mensaje de advertencia que explica la limitación.

## Relacionados

- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Arrange a 2x2 grid of panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
