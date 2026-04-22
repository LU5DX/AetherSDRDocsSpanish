# Cambiar a un panadapter único de ancho completo

Esta página explica cómo configurar el área del panadapter para mostrar un único panadapter de ancho completo. Use esta opción cuando desee enfocarse en un solo slice sin la división de pantalla.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo de disposición requiere una conexión de radio activa.

## Pasos

1. Haga clic derecho en cualquier lugar del área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Haga clic en la celda de vista previa con la etiqueta **Single (1 pan)**.
3. El diálogo se cierra de inmediato y el área del panadapter cambia a la vista única de ancho completo.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Celda **Single (1 pan)** | Selecciona la disposición única de ancho completo (ID de disposición `1`). Al hacer clic se confirma la selección y se cierra el diálogo. | `PanLayout` |
| Celdas de disposición (otras) | Celdas de vista previa para todas las demás configuraciones. Aparecen desactivadas si el número de panadapters con licencia de la radio es insuficiente. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin modificar la disposición actual. | — |

## Consejos

- La celda de la disposición activa actualmente aparece resaltada con un borde distintivo. Si la celda **Single (1 pan)** ya está resaltada, la disposición ya está configurada como única y no se requiere ningún cambio.
- Las celdas de disposiciones que requieren más panadapters de los que admite su radio están desactivadas y muestran un cursor de acceso prohibido. La disposición única siempre está disponible.

## Temas relacionados

- [Descripción general de Panadapter Layout](overview.md)
- [Dividir el área del panadapter en dos paneles](split-panadapter-area-side-by-side.md)
- [Vista previa y selección entre las 10 variantes de disposición](preview-and-pick-among-the-10-layout-variants.md)
