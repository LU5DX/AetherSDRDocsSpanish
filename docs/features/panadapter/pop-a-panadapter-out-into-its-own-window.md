# Extraer un panadapter a su propia ventana

Extraer un panadapter a una ventana flotante permite moverlo a un segundo monitor o redimensionarlo de forma independiente del diseño principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El botón de extracción no está disponible sin una conexión de radio.
- Debe tener más de un panadapter abierto. El botón ⬈ / ↩ está oculto en el modo de un solo panadapter.

## Pasos

1. Localice la barra de título en la parte superior del panadapter que desea extraer. Muestra el nombre del slice (por ejemplo, "Slice A") y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** de esa barra de título. El panadapter se desacopla y se abre en una ventana flotante independiente.
3. Redimensione o mueva la ventana flotante usando los controles de ventana estándar del sistema operativo.
4. Para acoplar el panadapter de nuevo en la ventana principal, haga clic en el botón **↩** de la barra de título de la ventana flotante.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---|---|---|---|
| **⬈ / ↩** (extraer/acoplar) | Extrae el panadapter a una ventana flotante (⬈), o lo acopla de nuevo al diseño principal (↩). | — | Oculto cuando solo hay un panadapter abierto. |
| **□** (maximizar) | Maximiza este panadapter para ocupar el área principal en un diseño de múltiples panadapters. | — | Oculto cuando solo hay un panadapter abierto. |
| **×** (cerrar) | Cierra este panadapter. | — | Oculto cuando solo hay un panadapter abierto. |
| Título del slice | Indica qué slice está vinculado a este panadapter (Slice A hasta Slice H). | Slice A | Indicador de solo lectura. |

## Consejos

- Los botones ⬈ y ↩ comparten la misma posición en la barra de título; el ícono cambia según si el panadapter está actualmente acoplado o flotante.
- Si desea que un panadapter ocupe toda el área de la ventana principal sin extraerlo, use **□** (maximizar) en su lugar.

## Relacionado

- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](overview.md)
