# Cambiar a un único panadapter de ancho completo

Esta página explica cómo cambiar el área de panadapter para mostrar un único panadapter de ancho completo. Utilice esta opción cuando desee concentrarse en una sola slice sin la distracción de la pantalla dividida.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El cuadro de diálogo de diseño requiere una conexión activa con la radio.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el cuadro de diálogo **Panadapter Layout**.
2. Haga clic en el mosaico de vista previa etiquetado como **Single (1 pan)**.
3. El cuadro de diálogo se cierra inmediatamente y el área del panadapter cambia a una vista única de ancho completo.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Mosaico **Single (1 pan)** | Selecciona el diseño único de ancho completo (ID de diseño `1`). Al hacer clic se confirma la selección y se cierra el cuadro de diálogo. | `PanLayout` |
| Mosaicos de diseño (otros) | Mosaicos de vista previa para todas las demás disposiciones. Se muestran atenuados si la cantidad de panadapters con licencia de la radio es insuficiente. Si el límite de slices de la radio ya está al máximo cuando se selecciona un diseño que requiere más panadapters, se muestra una advertencia en la barra de estado y se cancela el cambio de diseño. | `PanLayout` |
| **Cancel** | Cierra el cuadro de diálogo sin cambiar el diseño actual. | — |

## Consejos

- El mosaico del diseño activo actualmente se resalta con un borde distintivo. Si el mosaico **Single (1 pan)** ya está resaltado, el diseño ya está configurado como único y no es necesario realizar cambios.
- Los mosaicos para diseños que requieren más panadapters de los que su radio admite están deshabilitados y muestran un cursor prohibido. El diseño único siempre está disponible.
- Si intenta aplicar un diseño que requiere más panadapters de los que permite la capacidad de slices disponible de la radio, aparece un mensaje en la barra de estado: "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y se cancela el cambio de diseño.

## Relacionado

- [Panadapter Layout overview](overview.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
