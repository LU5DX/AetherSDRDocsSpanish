# Haga clic en el espectro para activar un panadapter (modo multi-slice)

Cuando hay varios panadapters abiertos, solo uno está activo a la vez. Al hacer clic en el área del espectro de un panadapter, este se convierte en el activo, dirigiendo la sintonización y el desplazamiento hacia ese panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. La visualización del panadapter requiere una conexión de radio activa.
- Deben estar abiertos al menos dos panadapters. En el modo de un solo panadapter, el clic de activación no tiene efecto visible y los botones de la barra de título descritos a continuación están ocultos.

## Pasos

1. Abra AetherSDR con varios panadapters visibles en la ventana principal.
2. Localice el panadapter que desea activar.
3. Haga clic en cualquier lugar del área Spectrum / waterfall de ese panadapter.

El panadapter ahora está activo. Los gestos de arrastre posteriores sintonizarán el VFO y los gestos de desplazamiento harán zoom en el espectro de ese panadapter.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Título del slice | Indicador | Slice A | Slice A–Slice H | — | Muestra qué slice está vinculado a este panadapter. |
| Spectrum / waterfall | Controlador de arrastre | — | — | — | El clic activa el panadapter; arrastre para sintonizar, desplace para hacer zoom. |
| ⬈ / ↩ (separar/acoplar) | Botón | — | — | — | Separa el panadapter en una ventana flotante o lo acopla de nuevo. Oculto en modo de un solo panadapter. |
| □ (maximizar) | Botón | — | — | — | Maximiza este panadapter en un diseño multi-panadapter. Oculto en modo de un solo panadapter. |
| × (cerrar) | Botón | — | — | — | Cierra este panadapter. Oculto en modo de un solo panadapter. |

## Consejos

- En los diseños multi-panadapter, los botones ⬈ / ↩, □ y × de la barra de título solo aparecen cuando hay más de un panadapter abierto. Si no los ve, está en modo de un solo panadapter.
- Para sintonizar haciendo un solo clic en el espectro en lugar de doble clic, habilite `View > Single-Click to Tune`.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Separar un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Comprensión de los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
