# Destacar un panadapter en su propia ventana

Destaque un panadapter para darle una ventana flotante independiente — útil cuando desea mover la pantalla de espectro a un segundo monitor o mantenerla visible mientras trabaja en otra aplicación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de destacado no están disponibles sin una conexión de radio activa.
- Debe estar en modo multi-slice. Los botones ⬈, □ y × de la barra de título están ocultos cuando solo hay un panadapter presente.

## Pasos

1. Localice la delgada barra de título en la parte superior del panadapter que desea destacar. Muestra el nombre del slice (por ejemplo, "Slice A") y el control de arrastre a la izquierda.
2. Haga clic en el botón **⬈** en el lado derecho de esa barra de título. El panadapter se desprende en una ventana flotante.
3. Arrastre o redimensione la ventana flotante según sea necesario usando los controles de ventana del sistema operativo.
4. Para acoplarlo de nuevo, haga clic en el botón **↩** que aparece ahora en la misma posición en la barra de título de la ventana flotante.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Notas |
|---|---|---|---|
| **⬈** (destacar) | Desprende el panadapter en una ventana flotante. | — | Visible solo en modo multi-slice. |
| **↩** (acoplar) | Devuelve el panadapter flotante a la ventana principal. | — | Reemplaza a ⬈ mientras el panadapter está flotando. |
| **□** (maximizar) | Maximiza este panadapter para ocupar el área principal. | — | Visible solo en modo multi-slice. |
| **×** (cerrar) | Cierra este panadapter. | — | Visible solo en modo multi-slice. |
| Título del slice | Indica qué slice está vinculado a este panadapter (Slice A hasta Slice H). | Slice A | Indicador de solo lectura. |

## Consejos

- El control de arrastre (⋮⋮) en el lado izquierdo de la barra de título no activa el destacado; use el botón **⬈** específicamente.
- Puede maximizar un panadapter diferente con **□** mientras otro ya está flotando.

## Relacionado

- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Entender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
