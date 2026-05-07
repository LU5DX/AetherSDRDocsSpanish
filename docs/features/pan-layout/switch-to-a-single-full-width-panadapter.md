# Cambiar a un único panadapter de ancho completo

Esta página explica cómo cambiar el área de panadapters para mostrar un único panadapter de ancho completo. Utilice esta opción cuando desee centrarse en una sola porción de banda sin la distracción de la pantalla dividida.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de diseño requiere una conexión activa con la radio.

## Pasos

1. Haga clic derecho en cualquier lugar del área de panadapters para abrir el diálogo **Panadapter Layout**.
2. Haga clic en la miniatura de vista previa etiquetada **Single (1 pan)**.
3. El diálogo se cierra inmediatamente y el área de panadapters cambia a una vista de ancho completo único.

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Miniatura **Single (1 pan)** | Selecciona el diseño de ancho completo único (ID de diseño `1`). Al hacer clic confirma la selección y cierra el diálogo. | `PanLayout` |
| Miniaturas de diseño (otras) | Miniaturas de vista previa para todas las demás disposiciones. Aparecen atenuadas si la cantidad de panadapters con licencia de la radio es insuficiente. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin cambiar el diseño actual. | — |

## Consejos

- La miniatura del diseño actualmente activo está resaltada con un borde distintivo. Si la miniatura **Single (1 pan)** ya está resaltada, el diseño ya está configurado como único y no es necesario realizar cambios.
- Las miniaturas de diseños que requieren más panadapters de los que su radio soporta están deshabilitadas y muestran un cursor de prohibición. El diseño único siempre está disponible.

## Relacionado

- [Descripción general de Panadapter Layout](overview.md)
- [Dividir el área de panadapters lado a lado](split-panadapter-area-side-by-side.md)
- [Previsualizar y elegir entre las 10 variantes de diseño](preview-and-pick-among-the-10-layout-variants.md)
