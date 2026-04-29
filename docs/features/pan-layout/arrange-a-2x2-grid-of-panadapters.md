# Organizar una cuadrícula de 2×2 panadapters

Use el diálogo Panadapter Layout para mostrar cuatro panadapters organizados en dos filas y dos columnas. Esta disposición es útil cuando desea monitorear cuatro slices o bandas independientes simultáneamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de disposición requiere una conexión de radio activa.
- La configuración de su radio debe admitir al menos cuatro panadapters. Las opciones de disposición que requieren más panadapters de los que su radio permite aparecen deshabilitadas en el diálogo.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Localice el mosaico de vista previa etiquetado como **A|B / C|D (4 pans)**.
3. Haga clic en ese mosaico. El diálogo se cierra inmediatamente y el área del panadapter cambia a la disposición en cuadrícula 2×2.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Layout buttons | Mosaicos de vista previa que representan cada disposición disponible. Haga clic en un mosaico para aplicarlo y cerrar el diálogo. Los mosaicos que requieren más panadapters de los que admite la radio se muestran deshabilitados. | `PanLayout` |
| Cancel | Cierra el diálogo sin modificar la disposición actual. | — |

La disposición 2×2 se almacena como valor `2x2` en `PanLayout`.

## Consejos

- El mosaico de disposición actualmente activo aparece resaltado con un borde distintivo en el diálogo, de modo que puede ver su punto de partida antes de realizar un cambio.
- Si el mosaico **A|B / C|D (4 pans)** aparece atenuado y no puede hacer clic en él, su radio no admite cuatro panadapters simultáneos. Verifique los límites de slices y panadapters de su radio.

## Solución de problemas

- **El mosaico 2×2 aparece en gris y no se puede hacer clic** — La conexión de radio no admite cuatro panadapters a la vez. El diálogo limita las disposiciones disponibles a las que se encuentran dentro del número de panadapters de la radio. Verifique la configuración actual de su radio Flex.
- **Hacer clic derecho en el área del panadapter no tiene efecto** — AetherSDR no está conectado a una radio. Establezca una conexión mediante `Settings > Connect to Radio...` primero.

## Relacionado

- [Descripción general de Panadapter Layout](overview.md)
- [Vista previa y selección entre las 10 variantes de disposición](preview-and-pick-among-the-10-layout-variants.md)
- [Dividir el área del panadapter en paralelo](split-panadapter-area-side-by-side.md)
- [Cambiar a un único panadapter de ancho completo](switch-to-a-single-full-width-panadapter.md)
