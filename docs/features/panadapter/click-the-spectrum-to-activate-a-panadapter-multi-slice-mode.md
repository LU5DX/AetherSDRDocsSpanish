# Haga clic en el espectro para activar un panadapter (modo multi-slice)

Cuando hay varios panadapters abiertos, solo uno está activo a la vez. Al hacer clic en el espectro de un panadapter inactivo, este se convierte en el activo, dirigiendo los controles de sintonía y de slice a ese panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters. En el modo de panadapter único no hay nada que activar; los botones de la barra de título ⬈, □ y × están ocultos.

## Pasos

1. Localice el panadapter que desea activar. Su barra de título muestra el slice al que está vinculado (por ejemplo, "Slice A" o "Slice B").
2. Haga clic en cualquier parte del área de espectro o waterfall de ese panadapter.

El panadapter queda activo. La sintonía, el zoom con desplazamiento y los controles de slice se aplican al slice que aparece en su barra de título.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Espectro / waterfall | Clic / arrastre | — | — | — |
| Título del slice | Indicador | Slice A | Slice A – Slice H | — |
| ⬈ / ↩ (separar/acoplar) | Botón | — | — | — |
| □ (maximizar) | Botón | — | — | — |
| × (cerrar) | Botón | — | — | — |
| Sens | Control deslizante | 30 | 0 – 100 | `CwDecoderSensitivity` |

Los botones ⬈, □ y × están ocultos en el modo de panadapter único y se vuelven visibles una vez que se abre un segundo panadapter.

## Consejos

- Arrastre sobre el espectro para desplazar la visualización de frecuencia; desplace la rueda para hacer zoom. Ambos gestos funcionan únicamente en el panadapter activo, por lo que, si es necesario, haga clic primero para activarlo.
- El título del slice en la barra de título ("Slice A", "Slice B", etc.) confirma qué slice responderá a sus controles después de hacer clic.

## Temas relacionados

- [Descripción general del panadapter](overview.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
- [Maximizar un panadapter para que ocupe el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Separar un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
