# Haga clic en el espectro para activar un panadapter (modo multi-slice)

Cuando hay varios panadapters abiertos, solo uno está activo a la vez. Al hacer clic en el área de espectro de cualquier panadapter, este se convierte en el activo y recibe las acciones de sintonía, desplazamiento y entrada de teclado.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. La visualización del panadapter requiere una conexión de radio activa.
- Debe haber al menos un panadapter adicional presente. En el modo de un solo panadapter, los botones de la barra de título están ocultos y solo existe un panadapter.

## Pasos

1. Ubique el panadapter que desea activar. Cada panadapter muestra un indicador de "Slice title" (por ejemplo, "Slice A" o "Slice B") en su barra de título.
2. Haga clic en cualquier parte del área de espectro o waterfall de ese panadapter.

El clic activa el panadapter. La sintonía, el zoom con desplazamiento y la entrada de teclado se aplican ahora al slice vinculado a ese panadapter.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| Slice title | Indicador | Slice A | Slice A – Slice H | — | Muestra qué slice está vinculado a este panadapter. |
| Espectro / waterfall | Controlador de arrastre | — | — | — | El clic activa el panadapter. Arrastre para sintonizar. Desplácese para hacer zoom. |
| ⬈ / ↩ (separar/acoplar) | Botón | — | — | — | Separa el panadapter en una ventana flotante o lo acopla de nuevo. Oculto en modo de un solo panadapter. |
| □ (maximizar) | Botón | — | — | — | Maximiza este panadapter en un diseño multi-panadapter. Oculto en modo de un solo panadapter. |
| × (cerrar) | Botón | — | — | — | Cierra este panadapter. Oculto en modo de un solo panadapter. |

## Consejos

- En el modo de un solo panadapter, los botones ⬈, □ y × de la barra de título están ocultos. Aparecen únicamente cuando hay más de un panadapter presente.
- Si desea que un solo clic también resintonice el VFO en ese punto, active `View > Single-Click to Tune` antes de hacer clic.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Separar un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
