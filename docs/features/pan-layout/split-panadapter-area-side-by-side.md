# Dividir el área del panadapter en dos paneles lado a lado

Use esta página para dividir el área del panadapter en dos paneles que se muestran a la izquierda y a la derecha. El diseño lado a lado (A | B) otorga a cada panadapter el mismo espacio horizontal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El cuadro de diálogo de diseño requiere una conexión de radio activa.
- Su licencia de radio debe admitir al menos 2 panadapters. Los botones de diseño para cantidades de pan que excedan el máximo de su radio se deshabilitan automáticamente.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el cuadro de diálogo **Panadapter Layout**.
2. Haga clic en la miniatura de vista previa etiquetada **A | B (2 pans)**. La miniatura muestra dos celdas iguales lado a lado.
3. El cuadro de diálogo se cierra inmediatamente y el área del panadapter se divide en dos paneles lado a lado.

Para cancelar sin cambiar el diseño, haga clic en **Cancel**.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Layout buttons** | Haga clic en la miniatura de vista previa que coincida con la disposición deseada. Confirmar cierra el cuadro de diálogo. Los diseños que requieren más panadapters de los que admite el límite de slices de la radio aparecen deshabilitados con un cursor de prohibición. Si el límite de slices ya está completo al aplicar un diseño más grande, se muestra un mensaje en la barra de estado "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y se cancela el cambio de diseño. | `PanLayout` |
| **Cancel** | Cierra el cuadro de diálogo sin cambiar el diseño actual. | — |

## Consejos

- La miniatura del diseño actualmente activo se resalta con un borde distintivo para que pueda ver qué disposición está vigente antes de realizar un cambio.
- Si la miniatura **A | B (2 pans)** aparece atenuada y no se puede hacer clic, su conexión de radio no admite 2 panadapters. Verifique los límites de slices y panadapters de su radio.
- El cuerpo del cuadro de diálogo tiene un ancho fijo para mantener centrada la cuadrícula de miniaturas de 3 columnas. Su altura se ajusta automáticamente para que el botón **Cancel** siempre aparezca debajo de la cuadrícula, nunca superpuesto sobre la fila inferior de miniaturas.

## Relacionado

- [Panadapter Layout overview](overview.md)
- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
- [Arrange a 2x2 grid of panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
