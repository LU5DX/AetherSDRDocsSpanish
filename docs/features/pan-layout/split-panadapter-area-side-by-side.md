# Dividir el área del panadapter en paneles lado a lado

Use esta página para dividir el área del panadapter en dos paneles mostrados a la izquierda y a la derecha. La disposición lado a lado (A | B) asigna a cada panadapter el mismo espacio horizontal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de diseño requiere una conexión de radio activa.
- La licencia de su radio debe admitir al menos 2 panadapters. Los botones de diseño para cantidades de pan que excedan el máximo de su radio se deshabilitan automáticamente.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Haga clic en la miniatura de vista previa etiquetada **A | B (2 pans)**. La miniatura muestra dos celdas iguales lado a lado.
3. El diálogo se cierra inmediatamente y el área del panadapter se divide en dos paneles lado a lado.

Para cancelar sin cambiar el diseño, haga clic en **Cancel**.

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Botón de diseño **A | B (2 pans)** | Aplica la disposición lado a lado de dos paneles (`2h`). Al hacer clic en él se confirma la selección y se cierra el diálogo. | `PanLayout` |
| Otros botones de diseño | Aplican una disposición diferente. Los botones para diseños que requieren más panadapters de los que admite la radio se deshabilitan. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar el diseño actual. | — |

## Consejos

- La miniatura de diseño activa actualmente se resalta con un borde distintivo para que pueda ver qué disposición está en efecto antes de realizar un cambio.
- Si la miniatura **A | B (2 pans)** aparece atenuada y no se puede hacer clic en ella, su conexión de radio no admite 2 panadapters. Verifique los límites de slice y panadapter de su radio.

## Relacionados

- [Resumen del diseño de Panadapter](overview.md)
- [Cambiar a un panadapter único de ancho completo](switch-to-a-single-full-width-panadapter.md)
- [Organizar una cuadrícula 2x2 de panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Vista previa y selección entre las 10 variantes de diseño](preview-and-pick-among-the-10-layout-variants.md)
