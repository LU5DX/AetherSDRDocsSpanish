# Sacar un panadapter a su propia ventana

Cuando tiene más de un panadapter abierto, puede desprender cualquiera de ellos en una ventana flotante independiente. Esto resulta útil para colocar el panadapter en un segundo monitor o para cambiarle el tamaño de forma independiente del diseño principal de AetherSDR.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El botón de extracción solo está disponible cuando hay una conexión de radio activa.
- Abra al menos un panadapter adicional. En el modo de un solo panadapter, el botón de extracción está oculto.

## Pasos

1. Localice la barra de título en la parte superior del panadapter que desea desprender. Muestra la etiqueta del slice (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** de esa barra de título.

   El panadapter se desprende en una ventana flotante sin marco.

3. Para mover la ventana flotante, haga clic y arrastre la barra de título en la parte superior de dicha ventana.
4. Para cambiar el tamaño de la ventana flotante, arrastre el control de tamaño en su esquina inferior derecha.
5. Para anclar la ventana de vuelta al diseño principal, haga clic en el botón **↩** de la barra de título de la ventana flotante.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Notas |
|---|---|---|---|
| **⬈** (extraer) | Desprende el panadapter en una ventana flotante. | — | Oculto en el modo de un solo panadapter. |
| **↩** (anclar) | Devuelve el panadapter flotante al diseño principal. | — | Aparece en lugar de ⬈ mientras la ventana está flotando. |
| **□** (maximizar) | Expande este panadapter para ocupar el área principal. | — | Oculto en el modo de un solo panadapter. |
| **×** (cerrar) | Cierra este panadapter. | — | Oculto en el modo de un solo panadapter. |
| Título del slice | Indicador que muestra qué slice está vinculado a este panadapter (Slice A a Slice H). | Slice A | Solo lectura. |

## Consejos

- La ventana flotante no tiene marco del sistema operativo. Use la barra de título integrada en la aplicación para arrastrarla y el control de tamaño en la esquina inferior derecha para cambiar su tamaño.
- Las etiquetas de los botones ⬈ y ↩ cambian para reflejar el estado actual: ⬈ cuando está anclado, ↩ cuando está flotando.

## Solución de problemas

- **El botón ⬈ no es visible** — Solo tiene un panadapter abierto. Los botones de extracción, maximizar y cerrar están todos ocultos en el modo de un solo panadapter. Abra un panadapter adicional para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la barra de título dentro de la ventana flotante, no el área del espectro. El área del espectro se utiliza para sintonizar.

## Relacionado

- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](overview.md)
