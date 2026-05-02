# Cambiar el grosor de la línea marcadora del VFO

Use el botón de grosor del marcador para controlar qué tan prominente aparece la línea marcadora del VFO en la pantalla del espectro, o para ocultarla por completo. La configuración se guarda por slice (receptor individual).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto para el slice que desea ajustar. Si no está visible, haga clic en la bandera marcadora del VFO de ese slice en la pantalla del espectro.

## Pasos

1. Abra el panel VFO del slice deseado haciendo clic en su bandera marcadora del VFO en la pantalla del espectro.
2. Localice el botón **Marker thickness** en el panel VFO.
3. Haga clic en el botón para recorrer los valores disponibles: **Off**, **1 px** y **3 px**.
4. Deje de hacer clic cuando se muestre el grosor deseado. El marcador en la pantalla del espectro se actualiza de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Configuración persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |

Cada clic avanza al siguiente valor en el ciclo: **Off** → **1 px** → **3 px** → **Off**. La configuración se guarda por slice, por lo que el slice 1 y el slice 2 pueden tener grosores diferentes.

## Consejos

- Establecer el marcador en **Off** oculta la línea vertical por completo. El panel VFO y la bandera permanecen visibles y funcionales.
- Si ejecuta múltiples slices en el mismo panadapter, aumentar un marcador a **3 px** puede ayudar a distinguirlo de los slices adyacentes.

## Temas relacionados

- [Ocultar o mostrar las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Contraer el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)
