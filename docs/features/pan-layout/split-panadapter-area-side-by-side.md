# Dividir el área de panadaptadores en paneles lado a lado

Utilice esta página para dividir el área de panadaptadores en dos paneles mostrados a la izquierda y a la derecha. La disposición lado a lado (A | B) otorga a cada panadaptador el mismo espacio horizontal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de disposición requiere una conexión de radio activa.
- La licencia de su radio debe admitir al menos 2 panadaptadores. Los botones de disposición para cantidades de paneles que excedan el máximo de su radio se deshabilitan automáticamente.

## Pasos

1. Haga clic derecho en cualquier lugar del área de panadaptadores para abrir el diálogo **Panadapter Layout**.
2. Haga clic en la miniatura de vista previa etiquetada como **A | B (2 pans)**. La miniatura muestra dos celdas iguales lado a lado.
3. El diálogo se cierra inmediatamente y el área de panadaptadores se divide en dos paneles lado a lado.

Para cancelar sin cambiar la disposición, haga clic en **Cancel**.

## Funciones de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Botones de disposición** | Haga clic en la miniatura de vista previa que coincida con la disposición deseada. Confirmar cierra el diálogo. Las disposiciones que requieran más panadaptadores de los que admite el límite de slices de la radio se muestran deshabilitadas con un cursor de prohibición. Si el límite de slices ya está completo cuando se aplica una disposición más grande, se muestra en la barra de estado el mensaje "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y se cancela el cambio de disposición. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar la disposición actual. | — |

## Consejos

- La miniatura de la disposición actualmente activa se resalta con un borde distintivo para que pueda ver qué disposición está activa antes de realizar un cambio.
- Si la miniatura **A | B (2 pans)** aparece atenuada y no se puede hacer clic, su conexión de radio no admite 2 panadaptadores. Verifique los límites de slices y panadaptadores de su radio.

## Relacionados

- [Panadapter Layout overview](overview.md)
- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
- [Arrange a 2x2 grid of panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
