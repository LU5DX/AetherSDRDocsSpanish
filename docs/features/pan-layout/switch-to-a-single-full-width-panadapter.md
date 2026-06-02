# Cambiar a un único panadapter de ancho completo

Esta página explica cómo modificar el área de panadapters para mostrar un único panadapter de ancho completo. Utilice esta opción cuando desee concentrarse en una sola franja sin la distracción de la pantalla dividida.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El cuadro de diálogo de diseño requiere una conexión de radio activa.

## Pasos

1. Haga clic derecho en cualquier lugar del área de panadapters para abrir el cuadro de diálogo **Panadapter Layout**.
2. Haga clic en el mosaico de vista previa etiquetado como **Single (1 pan)**.
3. El cuadro de diálogo se cierra inmediatamente y el área de panadapters cambia a una vista única de ancho completo.

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Mosaico **Single (1 pan)** | Selecciona el diseño único de ancho completo (ID de diseño `1`). Al hacer clic, confirma la selección y cierra el cuadro de diálogo. | `PanLayout` |
| Mosaicos de diseño (otros) | Mosaicos de vista previa para todas las demás disposiciones: **2v** (2 verticales), **2h** (2 horizontales), **2h1** (2 horizontales, 1 pequeño), **12h** (1 grande, 2 horizontales), **2x2** (cuadrícula 2x2), **3h2** (3 horizontales, 2 abajo), **2x3** (cuadrícula 2x3), **4h3** (4 horizontales, 3 abajo), **2x4** (cuadrícula 2x4). Los mosaicos que requieren más panadapters de los que admite la cantidad de franjas de la radio se muestran deshabilitados (cursor prohibido). Si el límite de franjas de la radio ya está al máximo cuando se selecciona un diseño que requiere más panadapters, se muestra una advertencia en la barra de estado y se cancela el cambio de diseño. | `PanLayout` |
| **Cancel** | Cierra el cuadro de diálogo sin cambiar el diseño actual. | — |

## Consejos

- El mosaico del diseño activo actual se resalta con un borde distintivo. Si el mosaico **Single (1 pan)** ya está resaltado, el diseño ya está configurado como único y no es necesario realizar ningún cambio.
- Los mosaicos para diseños que requieren más panadapters de los que admite su radio están deshabilitados y muestran un cursor prohibido. El diseño único está siempre disponible.
- Si intenta aplicar un diseño que requiere más panadapters de la capacidad de franjas disponible de la radio, aparece un mensaje en la barra de estado: "Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)" y se cancela el cambio de diseño.
- La ventana del cuadro de diálogo ahora sigue el tema activo de AetherSDR. Los colores de los botones y el estilo del texto se adaptan al color de fondo y de acento del tema para una apariencia visual coherente.

## Relacionado

- [Panadapter Layout overview](overview.md)
- [Split panadapter area side-by-side](split-panadapter-area-side-by-side.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
