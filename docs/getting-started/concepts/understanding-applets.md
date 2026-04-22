# Descripción del panel de applets de AetherSDR

El panel de applets es una región acoplable de la ventana de AetherSDR que agrupa los controles que más se utilizan durante una sesión de operación. Esta página explica qué es el panel de applets, cómo está organizado y cómo mostrarlo, ocultarlo o reposicionarlo.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución.
- No se requiere conexión a un radio para explorar el diseño del panel, pero la mayoría de los controles se activan únicamente cuando hay conexión a un FLEX-8600.

## Qué es el panel de applets

El panel de applets se encuentra en el lado derecho de la ventana principal. Contiene un conjunto de applets individuales — pequeños widgets de control para funciones como recepción, transmisión, TCI, entre otras. Cada applet está representado por un botón en la bandeja (por ejemplo, RX, TX, TCI) que alterna la vista expandida del applet.

El panel puede acoplarse dentro de la ventana principal o flotar como una ventana independiente. Los applets pueden reordenarse arrastrándolos, y el orden puede restaurarse en cualquier momento.

## Pasos

### Mostrar u ocultar el panel de applets

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Applet Panel` para alternar el panel entre visible y oculto. Una marca de verificación indica que el panel está visible.

### Hacer flotar el panel de applets en su propia ventana

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Pop Out Applet Panel` o presione `Ctrl+Shift+S`. El panel se desprende de la ventana principal.
3. Para acoplarlo nuevamente, repita la misma acción.

### Restablecer el orden de los applets al predeterminado

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Reset Applet Order`. Los applets regresan a su secuencia predeterminada.

## Qué hace cada control

| Control | Ubicación | Qué hace |
|---|---|---|
| `Applet Panel` | `View > Applet Panel` | Alterna la visibilidad del panel de applets. |
| `Pop Out Applet Panel` | `View > Pop Out Applet Panel` | Hace flotar el panel en una ventana independiente o lo vuelve a acoplar. Atajo: `Ctrl+Shift+S`. |
| `Reset Applet Order` | `View > Reset Applet Order` | Restaura los applets a su orden predeterminado. |
| Botones de bandeja (RX, TX, TCI, etc.) | Panel de applets | Cada botón expande o contrae su applet correspondiente. |

## Consejos

- Si el panel de applets desaparece después de cambiar el tamaño de la ventana, verifique que `View > Applet Panel` tenga una marca de verificación junto a la opción.
- Hacer flotar el panel con `Pop Out Applet Panel` es útil en configuraciones de varios monitores donde se desea mover los controles a una segunda pantalla mientras se mantiene el panadapter (visualizador panorámico) en la pantalla principal.
- Si ha reordenado los applets y desea volver a un estado conocido, `View > Reset Applet Order` restaura el diseño predeterminado sin afectar ninguna otra configuración.

## Relacionado

- [Activar el panel de applets](../../reference/menu-actions/enable-applet-panel.md)
- [Activar la extracción del panel de applets](../../reference/menu-actions/enable-pop-out-applet-panel.md)
- [Restablecer el orden de los applets](../../reference/menu-actions/reset-applet-order.md)
- [Activar el modo mínimo](../../reference/menu-actions/enable-minimal-mode.md)
