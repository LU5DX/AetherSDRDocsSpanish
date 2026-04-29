# Dividir el área del panadapter en dos paneles lado a lado

Use esta página para dividir el área del panadapter en dos paneles mostrados a la izquierda y a la derecha. El diseño lado a lado (A | B) asigna a cada panadapter el mismo espacio horizontal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de diseño requiere una conexión de radio activa.
- Su licencia de radio debe admitir al menos 2 panadapters. Los botones de diseño para cantidades de panadapters que superan el máximo de su radio se deshabilitan automáticamente.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Haga clic en el mosaico de vista previa etiquetado como **A | B (2 pans)**. El mosaico muestra dos celdas iguales lado a lado.
3. El diálogo se cierra de inmediato y el área del panadapter se divide en dos paneles lado a lado.

Para cancelar sin cambiar el diseño, haga clic en **Cancel**.

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Botón de diseño **A | B (2 pans)** | Aplica la disposición de dos paneles lado a lado (`2h`). Al hacer clic se confirma la selección y se cierra el diálogo. | `PanLayout` |
| Otros botones de diseño | Aplican una disposición diferente. Los botones para diseños que requieren más panadapters de los que admite la radio están deshabilitados. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar el diseño actual. | — |

## Consejos

- El mosaico de diseño activo actualmente aparece resaltado con un borde distintivo, de modo que puede ver qué disposición está en uso antes de realizar un cambio.
- Si el mosaico **A | B (2 pans)** aparece atenuado y no puede hacer clic en él, su conexión de radio no admite 2 panadapters. Verifique los límites de slice y panadapter de su radio.

## Relacionado

- [Descripción general de Panadapter Layout](overview.md)
- [Cambiar a un único panadapter de ancho completo](switch-to-a-single-full-width-panadapter.md)
- [Organizar una cuadrícula 2x2 de panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Vista previa y selección entre las 10 variantes de diseño](preview-and-pick-among-the-10-layout-variants.md)
