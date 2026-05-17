# Dividir el área del panadapter en dos paneles lado a lado

Use esta página para dividir el área del panadapter en dos paneles que se muestran a la izquierda y a la derecha. La disposición lado a lado (A | B) le da a cada panadapter un espacio horizontal igual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de disposición requiere una conexión activa con la radio.
- Su licencia de radio debe admitir al menos 2 panadapters. Los botones de disposición para cantidades de paneles que excedan el máximo de su radio se deshabilitan automáticamente.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Haga clic en el mosaico de vista previa etiquetado **A | B (2 pans)**. El mosaico muestra dos celdas iguales lado a lado.
3. El diálogo se cierra inmediatamente y el área del panadapter se divide en dos paneles lado a lado.

Para cancelar sin cambiar la disposición, haga clic en **Cancel**.

## Función de cada control

| Control | Descripción | Setting key |
|---|---|---|
| Botón de disposición **A | B (2 pans)** | Aplica la disposición lado a lado de dos paneles (`2h`). Al hacer clic confirma la selección y cierra el diálogo. | `PanLayout` |
| Otros botones de disposición | Aplican una disposición diferente. Las disposiciones que requieren más panadapters de los que admite el límite de slices de la radio se muestran deshabilitadas con un cursor prohibido. Si el límite de slices ya está completo cuando se aplica una disposición más grande, se muestra un mensaje en la barra de estado: "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y se cancela el cambio de disposición. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar la disposición actual. | — |

## Consejos

- El mosaico de disposición activo actualmente se resalta con un borde distintivo para que pueda ver qué disposición está activa antes de realizar un cambio.
- Si el mosaico **A | B (2 pans)** aparece atenuado y no se puede hacer clic, su conexión de radio no admite 2 panadapters. Verifique los límites de slices y panadapters de su radio.

## Relacionados

- [Panadapter Layout overview](overview.md)
- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
- [Arrange a 2x2 grid of panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
