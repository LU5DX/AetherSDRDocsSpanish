# Cambiar el Grosor de la Línea del Marcador VFO

Use el botón de grosor del marcador para controlar cuán prominente aparece la línea del marcador VFO en la pantalla del espectro, o para ocultarla por completo. La configuración se guarda por slice.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto para el slice que desea ajustar. Si no es visible, haga clic en el indicador del marcador VFO de ese slice en la pantalla del espectro.

## Pasos

1. Abra el panel VFO para el slice deseado haciendo clic en su indicador de marcador VFO en la pantalla del espectro.
2. Localice el **botón de grosor del marcador** (Marker thickness button) en el panel VFO.
3. Haga clic en el botón para recorrer los valores disponibles: **Off** (Apagado), **1 px** y **3 px**.
4. Deje de hacer clic cuando se muestre el grosor deseado. El marcador en la pantalla del espectro se actualiza inmediatamente.

## Función de cada control

| Control                    | Valor predeterminado | Valores válidos |
|----------------------------|----------------------|-----------------|
| Botón de grosor del marcador | 1 px                 | Off (Apagado), 1 px, 3 px |

Cada clic avanza al siguiente valor en el ciclo: **Off** → **1 px** → **3 px** → **Off**. La configuración se conserva por slice, por lo que el slice 1 y el slice 2 pueden tener grosores diferentes.

## Consejos

- Configurar el marcador en **Off** oculta la línea vertical por completo. El panel VFO y el indicador permanecen visibles y funcionales.
- Si ejecuta varios slices en el mismo panadapter, aumentar un marcador a **3 px** puede ayudar a distinguirlo de los slices adyacentes.

## Relacionado

- [Ocultar o mostrar líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Colapsar el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)
