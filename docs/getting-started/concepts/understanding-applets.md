# Descripción del panel de applets de AetherSDR

El panel de applets es un área acoplable en el lado derecho de la ventana de AetherSDR que agrupa controles relacionados en applets independientes. Esta página explica qué es el panel de applets, cómo está organizado y cómo mostrarlo, ocultarlo y reposicionarlo.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución.
- No es necesario estar conectado a una radio para explorar la disposición del panel de applets.

## Qué es el panel de applets

El panel de applets es una franja vertical de controles acoplada al borde derecho de la ventana principal. Cada applet dentro del panel cubre una función específica — por ejemplo, controles de slice (canal de recepción), cancelación de ruido o condiciones de propagación. El panel puede ocultarse cuando se desea maximizar el área del panadapter, o dejarse flotante en una ventana independiente si se trabaja con varios monitores.

El panel contiene botones de bandeja a lo largo de su borde superior. Estos son botones de alternancia compactos etiquetados con su función (por ejemplo, RX, TX, TCI). Al hacer clic en un botón de bandeja se muestra u oculta el applet correspondiente dentro del panel.

## Pasos

### Mostrar u ocultar el panel de applets

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Applet Panel`. Una marca de verificación indica que el panel está visible. Al hacer clic de nuevo, se oculta.

### Dejar el panel de applets flotante en su propia ventana

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Pop Out Applet Panel`, o presione `Ctrl+Shift+S`. El panel se desacopla de la ventana principal y se convierte en una ventana flotante independiente.
3. Para acoplarlo de nuevo, haga clic en `View > Pop Out Applet Panel` otra vez, o presione `Ctrl+Shift+S`.

### Restablecer el orden de los applets

Si reorganizó los applets y desea volver a la disposición predeterminada:

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Reset Applet Order`. Los applets regresan a sus posiciones predeterminadas dentro del panel.

## Qué hace cada control

| Control | Ubicación | Qué hace |
|---|---|---|
| `Applet Panel` | Menú `View` | Alterna la visibilidad del panel de applets. Activable. |
| `Pop Out Applet Panel` | Menú `View` | Deja el panel de applets flotante en una ventana independiente o lo vuelve a acoplar. Atajo: `Ctrl+Shift+S`. Activable. |
| `Reset Applet Order` | Menú `View` | Restaura el panel de applets a su orden predeterminado de applets. |
| Botones de bandeja | Parte superior del panel de applets | Cada botón muestra u oculta un applet dentro del panel (por ejemplo, RX, TX, TCI). |

## Consejos

- Si ejecuta AetherSDR en una pantalla pequeña, use `View > Minimal Mode` (`Ctrl+M`) junto con la opción de ocultar el panel de applets para maximizar el espacio del panadapter.
- Cuando el panel de applets está flotante, puede moverlo a un segundo monitor de forma independiente de la ventana principal.
- Si los botones de bandeja o los applets aparecen en un orden inesperado después de una actualización, use `View > Reset Applet Order` para restaurar los valores predeterminados.

## Temas relacionados

- [Activar el panel de applets](../../reference/menu-actions/enable-applet-panel.md)
- [Activar el panel de applets flotante](../../reference/menu-actions/enable-pop-out-applet-panel.md)
- [Restablecer el orden de los applets](../../reference/menu-actions/reset-applet-order.md)
- [Activar el modo mínimo](../../reference/menu-actions/enable-minimal-mode.md)
- [Descripción de los slices y los VFO](understanding-slices.md)
