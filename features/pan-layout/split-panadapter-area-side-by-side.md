# Dividir el área del panadapter en dos paneles uno al lado del otro

Use esta página para dividir el área del panadapter en dos paneles mostrados a la izquierda y a la derecha. La disposición en paralelo (A | B) asigna a cada panadapter el mismo espacio horizontal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo de disposición requiere una conexión de radio activa.
- Su licencia de radio debe admitir al menos 2 panadapters. Los botones de disposición para cantidades de panadapters que superan el máximo de su radio se desactivan automáticamente.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Haga clic en el mosaico de vista previa etiquetado como **A | B (2 pans)**. El mosaico muestra dos celdas iguales una al lado de la otra.
3. El diálogo se cierra de inmediato y el área del panadapter se divide en dos paneles en paralelo.

Para cancelar sin cambiar la disposición, haga clic en **Cancel**.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Botón de disposición **A | B (2 pans)** | Aplica la disposición de dos paneles en paralelo (`2h`). Al hacer clic se confirma la selección y se cierra el diálogo. | `PanLayout` |
| Otros botones de disposición | Aplican una disposición diferente. Los botones para disposiciones que requieren más panadapters de los que admite la radio están desactivados. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar la disposición actual. | — |

## Consejos

- El mosaico de disposición activo en ese momento aparece resaltado con un borde distintivo, de modo que puede ver qué disposición está en efecto antes de realizar un cambio.
- Si el mosaico **A | B (2 pans)** aparece atenuado y no se puede hacer clic en él, su conexión de radio no admite 2 panadapters. Verifique los límites de slice y panadapter de su radio.

## Relacionados

- [Descripción general de Panadapter Layout](overview.md)
- [Cambiar a un único panadapter de ancho completo](switch-to-a-single-full-width-panadapter.md)
- [Organizar una cuadrícula 2x2 de panadapters](arrange-a-2x2-grid-of-panadapters.md)
- [Previsualizar y elegir entre las 10 variantes de disposición](preview-and-pick-among-the-10-layout-variants.md)
