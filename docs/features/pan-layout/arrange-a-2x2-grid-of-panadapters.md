# Organizar una cuadrícula de 2×2 de panadaptadores

Utilice el diálogo "Panadapter Layout" para mostrar cuatro panadaptadores dispuestos en dos filas y dos columnas. Esta disposición es útil cuando desea monitorear cuatro slices o bandas simultáneamente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El diálogo de disposición requiere una conexión activa con el radio.
- La configuración de su radio debe admitir al menos cuatro panadaptadores. Las opciones de disposición que requieran más panadaptadores de los que su radio permite aparecen deshabilitadas en el diálogo.

## Pasos

1. Haga clic derecho en cualquier lugar del área de panadaptadores para abrir el diálogo **Panadapter Layout**.
2. Localice la miniatura de vista previa etiquetada como **A|B / C|D (4 pans)**.
3. Haga clic en esa miniatura. El diálogo se cierra inmediatamente y el área de panadaptadores cambia a la disposición de cuadrícula 2×2.

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Botones de disposición | Miniaturas de vista previa que representan cada disposición disponible. Haga clic en una miniatura para aplicarla y cerrar el diálogo. Las miniaturas que requieren más panadaptadores de los que el radio admite se muestran deshabilitadas. | `PanLayout` |
| Cancelar | Cierra el diálogo sin cambiar la disposición actual. | — |

La disposición 2×2 se almacena como valor `2x2` en `PanLayout`.

## Consejos

- La miniatura de la disposición activa actualmente se resalta con un borde distintivo en el diálogo, para que pueda ver su punto de partida antes de realizar un cambio.
- Si la miniatura **A|B / C|D (4 pans)** aparece atenuada y no se puede hacer clic, su radio no admite cuatro panadaptadores simultáneos. Verifique los límites de slices y panadaptadores de su radio.

## Solución de problemas

- **La miniatura 2×2 está atenuada y no se puede hacer clic** — La conexión del radio no admite cuatro panadaptadores a la vez. El diálogo limita las disposiciones disponibles a aquellas dentro del recuento de panadaptadores del radio. Verifique la configuración actual de su radio Flex.
- **Hacer clic derecho en el área de panadaptadores no hace nada** — AetherSDR no está conectado a un radio. Establezca una conexión mediante `Settings > Connect to Radio...` primero.

## Relacionados

- [Descripción general de la disposición de panadaptadores](overview.md)
- [Vista previa y selección entre las 10 variantes de disposición](preview-and-pick-among-the-10-layout-variants.md)
- [Dividir el área de panadaptadores lado a lado](split-panadapter-area-side-by-side.md)
- [Cambiar a un único panadaptador de ancho completo](switch-to-a-single-full-width-panadapter.md)
