# Desprender un panadapter a su propia ventana

Esta página explica cómo desprender un panadapter de la ventana principal para que flote en su propia ventana. Esto es útil cuando se dispone de varios monitores y se desea colocar el visualizador de espectro de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El botón de desprendimiento solo está disponible cuando hay una conexión de radio activa.
- Debe estar en modo multi-slice. El botón ⬈ está oculto en el modo de panel único.

## Pasos

1. En la ventana principal, localice la barra de título delgada en la parte superior del panadapter que desea desprender. Muestra el nombre del slice (por ejemplo, "Slice A") y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** de la barra de título de ese panadapter. La información emergente indica "Pop out panadapter".
3. El panadapter se desprende y se abre en una ventana flotante independiente. El botón **⬈** cambia a **↩**.
4. Arrastre la ventana flotante por su barra de título para colocarla en cualquier monitor.
5. Para acoplar el panadapter de nuevo a la ventana principal, haga clic en el botón **↩** de la barra de título de la ventana flotante.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| ⬈ / ↩ (desprender/acoplar) | Botón | Desprende el panadapter a una ventana flotante cuando está acoplado; lo vuelve a acoplar cuando está flotando. Oculto en el modo de panel único. |
| □ (maximizar) | Botón | Maximiza este panadapter dentro de un diseño multi-panel. Oculto en el modo de panel único. |
| × (cerrar) | Botón | Cierra este panadapter. Oculto en el modo de panel único. |
| Título del slice | Indicador | Muestra qué slice está vinculado a este panadapter (Slice A hasta Slice H). |

## Consejos

- La ventana flotante conserva su barra de título completa con los botones ⬈ / ↩, □ y ×, por lo que puede acoplarlo, maximizarlo o cerrarlo desde la posición flotante.
- Arrastrar la barra de título de la ventana flotante mueve la ventana; esto no afecta la asignación de slice de la radio.

## Temas relacionados

- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Descripción general del panadapter](overview.md)
