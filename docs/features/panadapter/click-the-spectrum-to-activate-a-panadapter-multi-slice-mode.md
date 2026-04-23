# Haga clic en el espectro para activar un panadapter (modo multi-slice)

Cuando tiene más de un panadapter abierto, solo uno está activo a la vez. Haga clic en su espectro para convertirlo en el panadapter activo antes de sintonizar, ajustar configuraciones o usar atajos de teclado.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters (modo multi-slice). En el modo single-pan, el panadapter siempre está activo y no se requiere ningún clic.

## Pasos

1. Localice el panadapter con el que desea trabajar. Cada panadapter tiene una barra de título que muestra una etiqueta de slice (por ejemplo, "Slice A" o "Slice B").
2. Haga clic en cualquier parte del área de espectro o waterfall de ese panadapter.

El panadapter está ahora activo. La sintonización, el zoom y los atajos de teclado se aplican a este panadapter hasta que haga clic en otro.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Espectro / waterfall | Haga clic para activar este panadapter; arrastre para sintonizar; desplace para hacer zoom. | — | — | — |
| Título del slice | Indicador que muestra qué slice está vinculado a este panadapter. | Slice A | Slice A–Slice H | — |
| ⬈ / ↩ (flotante/acoplado) | Extrae el panadapter a una ventana flotante o lo vuelve a acoplar. Oculto en modo single-pan. | — | — | — |
| □ (maximizar) | Maximiza este panadapter en un diseño multi-pan. Oculto en modo single-pan. | — | — | — |
| × (cerrar) | Cierra este panadapter. Oculto en modo single-pan. | — | — | — |

## Consejos

- En el modo single-pan, ⬈ / ↩, □ y × están todos ocultos. Estos controles aparecen únicamente cuando hay más de un panadapter abierto.
- Si desea que un solo clic en el espectro vuelva a sintonizar en lugar de simplemente activar, habilite `View > Single-Click to Tune`.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Maximizar un panadapter para que ocupe el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
