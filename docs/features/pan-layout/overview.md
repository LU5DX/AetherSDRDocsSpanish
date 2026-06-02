# Descripción general de la disposición del panadapter

La función de disposición del panadapter controla cuántos panadapters se muestran y cómo se organizan en la pantalla. Úsela para adaptarse a su estilo de operación, desde una vista individual de ancho completo hasta una cuadrícula de ocho panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. Los botones de disposición para configuraciones que requieren más panadapters de los que la radio soporta están deshabilitados.
- La radio tiene un límite de slices que determina el número máximo de panadapters. Si la radio ya está en su capacidad máxima de slices cuando se solicita una disposición más grande, se muestra una advertencia en la barra de estado y el cambio de disposición se cancela.

## Cómo funciona

Haga clic derecho en el área del panadapter para abrir el diálogo **Panadapter Layout**. El diálogo presenta una cuadrícula de vistas previas en miniatura, cada una mostrando una disposición etiquetada de celdas con letras (A, B, C, etc.). La disposición activa actual se resalta con un borde de acento en color verde azulado.

Haga clic en cualquier miniatura habilitada para aplicar esa disposición de inmediato. El diálogo se cierra y AetherSDR reorganiza el área del panadapter. Haga clic en **Cancel** para cerrar el diálogo sin realizar cambios.

La disposición elegida se guarda como `PanLayout`.

Las miniaturas de configuraciones que exceden el número de panadapters que su radio soporta se muestran atenuadas y no se pueden seleccionar. Si el límite de slices de la radio ya está al máximo cuando se aplica una disposición más grande, se muestra un mensaje en la barra de estado "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y el cambio de disposición se cancela.

El diálogo utiliza la paleta de colores del tema actual para su fondo, texto, acento y estilos de botones. Si cambia el tema, el diálogo se actualiza automáticamente la próxima vez que se abra.

## Qué hace cada control

| Control | Descripción | Disposiciones disponibles | Configuración persistente |
|---|---|---|---|
| Botones de disposición | Baldosas de vista previa: haga clic en una para aplicar esa configuración. | `1`, `2v`, `2h`, `2h1`, `12h`, `2x2`, `3h2`, `2x3`, `4h3`, `2x4` | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar la disposición actual. | — | — |

Las configuraciones disponibles son:

| ID de disposición | Etiqueta | Cantidad de panadapters |
|---|---|---|
| `1` | Individual | 1 |
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
- Las disposiciones que requieren más panadapters de los que la radio proporciona están deshabilitadas y muestran un cursor de prohibido al pasar el ratón. Conéctese a una radio que soporte la cantidad deseada de panadapters para habilitarlas.
- Si intenta seleccionar una disposición que requiere más panadapters cuando el límite de slices de su radio ya está completo, revise la barra de estado para ver un mensaje de advertencia que explica la limitación.

## Relacionados

- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Arrange a 2x2 grid of panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
