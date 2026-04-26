# Haga clic en el espectro para activar un panadapter (modo multi-slice)

En una disposición de múltiples panadapters, solo uno está activo a la vez. Hacer clic en el área de espectro de un panadapter inactivo lo lleva al foco, de modo que sus controles, slices y sintonización se aplican a él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters. En el modo de un solo panadapter, los botones de la barra de título (⬈, □, ×) están ocultos y no hay nada entre lo que alternar.

## Pasos

1. Localice el panadapter que desea activar. Su barra de título muestra el slice al que está vinculado (por ejemplo, "Slice B").
2. Haga clic en cualquier lugar del área Spectrum / waterfall de ese panadapter.
3. El panadapter ahora está activo. La sintonización, el desplazamiento para hacer zoom y todos los controles del slice se aplican a él.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Título del slice | Indicador | Slice A | Slice A – Slice H | — |
| Spectrum / waterfall | Área de clic / arrastre | — | — | — |
| ⬈ / ↩ (separar/anclar) | Botón | — | — | — |
| □ (maximizar) | Botón | — | — | — |
| × (cerrar) | Botón | — | — | — |
| Sens | Control deslizante | 30 | 0 – 100 | `CwDecoderSensitivity` |

Los botones ⬈ / ↩, □ y × están ocultos en el modo de un solo panadapter. Aparecen únicamente cuando hay más de un panadapter abierto.

## Consejos

- Arrastre sobre el área Spectrum / waterfall para sintonizar la frecuencia del slice. Desplace la rueda del ratón para ajustar el span.
- Para darle a un panadapter más espacio en pantalla sin cerrar los demás, haga clic en □ (maximize) en su barra de título. Consulte [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md).
- Para mover un panadapter a una ventana separada, haga clic en ⬈ (pop-out). Consulte [Separar un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md).

## Relacionados

- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Separar un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
