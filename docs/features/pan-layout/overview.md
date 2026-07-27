# Resumen de la Disposición del Panadapter

La función Disposición del Panadapter controla cuántos panadapters se muestran y cómo se organizan en la pantalla. Úsela para adaptarse a su estilo de operación, desde una vista única de ancho completo hasta una cuadrícula de ocho panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. Los botones de disposición para configuraciones que requieren más panadapters de los que la radio soporta están deshabilitados.
- La radio tiene un límite de slices que determina el número máximo de panadapters. Si la radio ya está en su capacidad de slices cuando se solicita una disposición más grande, se muestra una advertencia en la barra de estado y el cambio de disposición se cancela.

## Cómo funciona

Haga clic derecho en el área del panadapter para abrir el cuadro de diálogo **Panadapter Layout**. El diálogo presenta una cuadrícula de vistas previas en miniatura, cada una mostrando una disposición etiquetada de celdas con letras (A, B, C, etc.). La disposición actualmente activa se resalta con un borde de acento verde azulado.

Haga clic en cualquier miniatura habilitada para aplicar esa disposición inmediatamente. El diálogo se cierra y AetherSDR reorganiza el área del panadapter. Haga clic en **Cancel** para cerrar el diálogo sin realizar cambios.

La disposición elegida se almacena como `PanLayout`.

Las miniaturas de configuraciones que exceden el número de panadapters que su radio soporta se muestran atenuadas y no se pueden seleccionar. Si el límite de slices de la radio ya está en su capacidad cuando se aplica una disposición más grande, se muestra un mensaje en la barra de estado: "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y el cambio de disposición se cancela.

El diálogo utiliza la paleta de colores del tema actual para el fondo, texto, acentos y estilos de botones. Si cambia el tema, el diálogo se actualiza automáticamente la próxima vez que se abra. El cuerpo del diálogo tiene un ancho fijo que mantiene la cuadrícula de miniaturas de tres columnas centrada; su altura está determinada por la disposición para que el botón **Cancel** siempre aparezca debajo de la cuadrícula.

## Lo que hace cada control

| Control | Descripción | Disposiciones disponibles | Configuración persistida |
|---|---|---|---|
| Botones de disposición | Azulejos de vista previa — haga clic en uno para aplicar esa disposición. | `1`, `2v`, `2h`, `2h1`, `12h`, `2x2`, `3h2`, `2x3`, `4h3`, `2x4` | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar la disposición actual. | — | — |

Las configuraciones disponibles son:

| ID de disposición | Etiqueta | Número de panadapters |
|---|---|---|
| `1` | Único | 1 |
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

- Cada etiqueta de miniatura muestra el número de panadapters, por ejemplo "A\|B / C (3 pans)", para que pueda confirmar el número antes de hacer clic.
- Las disposiciones que requieren más panadapters de los que la radio proporciona están deshabilitadas y muestran un cursor de prohibición al pasar el ratón. Conéctese a una radio que soporte el número deseado de panadapters para habilitarlas.
- Si intenta seleccionar una disposición que requiere más panadapters cuando el límite de slices de su radio ya está completo, revise la barra de estado para ver un mensaje de advertencia que explica la limitación.

## Relacionados

- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Arrange a 2x2 grid of panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
