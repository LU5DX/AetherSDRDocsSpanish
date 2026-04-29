# Cambiar a un panadapter único de ancho completo

Esta página explica cómo cambiar el área de panadapter para mostrar un único panadapter de ancho completo. Use esta opción cuando desee concentrarse en un solo slice sin la confusión de la pantalla dividida.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo de disposición requiere una conexión de radio activa.

## Pasos

1. Haga clic derecho en cualquier parte del área de panadapter para abrir el diálogo **Panadapter Layout**.
2. Haga clic en el mosaico de vista previa etiquetado como **Single (1 pan)**.
3. El diálogo se cierra de inmediato y el área de panadapter cambia a una vista única de ancho completo.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Mosaico **Single (1 pan)** | Selecciona la disposición única de ancho completo (ID de disposición `1`). Al hacer clic se confirma la selección y se cierra el diálogo. | `PanLayout` |
| Mosaicos de disposición (otros) | Mosaicos de vista previa para todas las demás configuraciones. Aparecen atenuados si la cantidad de panadapters con licencia de la radio es insuficiente. | `PanLayout` |
| **Cancel** | Cierra el diálogo sin modificar la disposición actual. | — |

## Consejos

- El mosaico de la disposición activa actualmente aparece resaltado con un borde distintivo. Si el mosaico **Single (1 pan)** ya está resaltado, la disposición ya está configurada como única y no se requiere ningún cambio.
- Los mosaicos para disposiciones que requieren más panadapters de los que admite su radio están deshabilitados y muestran un cursor de prohibición. La disposición única siempre está disponible.

## Relacionado

- [Descripción general de Panadapter Layout](overview.md)
- [Dividir el área de panadapter en paralelo](split-panadapter-area-side-by-side.md)
- [Ver y seleccionar entre las 10 variantes de disposición](preview-and-pick-among-the-10-layout-variants.md)
