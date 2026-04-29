# Descripción general del diseño del panadapter

La función de diseño del panadapter (Panadapter Layout) controla cuántos panadapters se muestran y cómo se organizan en pantalla. Úsela para adaptarse a su estilo de operación, desde una vista única de ancho completo hasta una cuadrícula de ocho panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. Los botones de diseño para configuraciones que requieren más panadapters de los que la radio admite están desactivados.

## Cómo funciona

Haga clic derecho en el área del panadapter para abrir el diálogo **Panadapter Layout**. El diálogo presenta una cuadrícula de vistas previas en miniatura, cada una con una disposición etiquetada de celdas con letras (A, B, C, etc.). El diseño activo actualmente aparece resaltado con un borde de color verde azulado.

Haga clic en cualquier miniatura habilitada para aplicar ese diseño de inmediato. El diálogo se cierra y AetherSDR reorganiza el área del panadapter. Haga clic en **Cancel** para cerrar el diálogo sin realizar cambios.

El diseño elegido se guarda como `PanLayout`.

Las miniaturas para configuraciones que superan el número de panadapters que admite su radio se muestran atenuadas y no pueden seleccionarse.

## Qué hace cada control

| Control | Descripción | Diseños disponibles | Configuración guardada |
|---|---|---|---|
| Botones de diseño | Miniaturas de vista previa — haga clic en una para aplicar esa configuración. | `1`, `2v`, `2h`, `2h1`, `12h`, `3v`, `2x2`, `4v`, `3h2`, `2x3`, `4h3`, `2x4` | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar el diseño actual. | — | — |

Las configuraciones disponibles son:

| ID de diseño | Etiqueta | Cantidad de panadapters |
|---|---|---|
| `1` | Single | 1 |
| `2v` | A / B | 2 |
| `2h` | A \| B | 2 |
| `2h1` | A\|B / C | 3 |
| `12h` | A / B\|C | 3 |
| `3v` | A / B / C | 3 |
| `2x2` | A\|B / C\|D | 4 |
| `4v` | A/B/C/D | 4 |
| `3h2` | A\|B\|C / D\|E | 5 |
| `2x3` | A\|B / C\|D / E\|F | 6 |
| `4h3` | A\|B\|C\|D / E\|F\|G | 7 |
| `2x4` | A\|B / C\|D / E\|F / G\|H | 8 |

## Consejos

- Cada etiqueta de miniatura muestra la cantidad de panadapters, por ejemplo "A\|B / C (3 pans)", para que pueda confirmar el número antes de hacer clic.
- Los diseños que requieren más panadapters de los que la radio ofrece están desactivados y muestran un cursor de prohibición al pasar el puntero sobre ellos. Conéctese a una radio que admita el número deseado de panadapters para habilitarlos.

## Relacionados

- [Cambiar a un panadapter único de ancho completo](switch-to-a-single-full-width-panadapter.md)
- [Dividir el área del panadapter en paralelo](split-panadapter-area-side-by-side.md)
- [Organizar una cuadrícula 2x2 de panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Previsualizar y elegir entre las 10 variantes de diseño](preview-and-pick-among-the-10-layout-variants.md)
