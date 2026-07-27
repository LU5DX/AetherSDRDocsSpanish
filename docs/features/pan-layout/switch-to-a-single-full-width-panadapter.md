# Cambiar a un solo panadaptador de ancho completo

Esta página explica cómo cambiar el área de panadaptadores para mostrar un único panadaptador de ancho completo. Úsela cuando desee concentrarse en una sola franja sin la distracción de una pantalla dividida.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El cuadro de diálogo de diseño requiere una conexión de radio activa.

## Pasos

1. Haga clic derecho en cualquier lugar del área de panadaptadores para abrir el cuadro de diálogo **Panadapter Layout**.
2. Haga clic en la miniatura de vista previa etiquetada **Single (1 pan)**.
3. El cuadro de diálogo se cierra inmediatamente y el área de panadaptadores cambia a una vista única de ancho completo.

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Single (1 pan)** tile | Selecciona el diseño único de ancho completo (ID de diseño `1`). Al hacer clic, confirma la selección y cierra el cuadro de diálogo. | `PanLayout` |
| Layout tiles (other) | Miniaturas de vista previa para todas las demás disposiciones: **2v** (2 verticales), **2h** (2 horizontales), **2h1** (2 horizontales, 1 pequeño), **12h** (1 grande, 2 horizontales), **2x2** (cuadrícula 2x2), **3h2** (3 horizontales, 2 debajo), **2x3** (cuadrícula 2x3), **4h3** (4 horizontales, 3 debajo), **2x4** (cuadrícula 2x4). Las miniaturas que requieren más panadaptadores de los que admite el límite de franjas de la radio están deshabilitadas (cursor prohibido). Si el límite de franjas de la radio ya está al máximo cuando se selecciona un diseño que requiere más panadaptadores, se muestra una advertencia en la barra de estado y se cancela el cambio de diseño. | `PanLayout` |
| **Cancel** | Cierra el cuadro de diálogo sin cambiar el diseño actual. | — |

## Consejos

- La miniatura del diseño actualmente activo se resalta con un borde distintivo. Si la miniatura **Single (1 pan)** ya está resaltada, el diseño ya está configurado como único y no es necesario realizar cambios.
- Las miniaturas para diseños que requieren más panadaptadores de los que su radio admite están deshabilitadas y muestran un cursor prohibido. El diseño único siempre está disponible.
- Si intenta aplicar un diseño que requiere más panadaptadores de la capacidad de franjas disponible en la radio, aparece un mensaje en la barra de estado: "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y se cancela el cambio de diseño.
- El ancho del cuerpo del cuadro de diálogo es fijo para que la cuadrícula de miniaturas de 3 columnas permanezca centrada. El botón Cancelar siempre se encuentra debajo de la cuadrícula, en lugar de superponerse sobre la fila de miniaturas inferior.
- La ventana del cuadro de diálogo sigue el tema activo de AetherSDR. Los colores de los botones y el estilo del texto se adaptan al color de fondo y de acento del tema para una apariencia visual coherente.

## Relacionados

- [Panadapter Layout overview](overview.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
