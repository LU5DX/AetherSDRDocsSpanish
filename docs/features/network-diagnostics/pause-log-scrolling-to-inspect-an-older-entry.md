# Pausar el desplazamiento del registro para inspeccionar una entrada anterior

La pestaña **Logs** en Network Diagnostics sigue el archivo de registro de AetherSDR en tiempo real. Esta página explica cómo pausar ese desplazamiento automático para leer una entrada anterior sin que la vista salte, y cómo reanudar el seguimiento en vivo cuando termine.

## Antes de comenzar

- Abra Network Diagnostics mediante `Settings > Network...`.
- Haga clic en la pestaña **Logs** para que el visor de registros sea visible.

## Pasos

1. Vaya a `Settings > Network...`.
2. Haga clic en la pestaña **Logs**.
3. Para pausar el desplazamiento, realice una de las siguientes acciones:
   - Desplácese hacia arriba en el visor de registros. El visor cambia automáticamente a **Paused**.
   - Haga clic en el botón de alternancia, que indica **Live**, para cambiarlo a **Paused**.
4. Lea la entrada que necesita. La pantalla permanece fija mientras el botón muestra **Paused**.
5. Cuando esté listo para volver al seguimiento en vivo, haga clic en el botón de alternancia, que ahora indica **Paused**, para cambiarlo de nuevo a **Live**. El visor salta inmediatamente a la salida más reciente y reanuda el desplazamiento automático.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Live / Paused** (botón de alternancia) | Live | Cuando está en **Live**, el visor se desplaza automáticamente hasta la salida de registro más reciente. Cuando está en **Paused**, el desplazamiento se detiene y la pantalla mantiene su posición actual. Desplazarse hacia arriba en el visor cambia el botón automáticamente a **Paused**. Hacer clic en el botón mientras indica **Paused** reanuda el desplazamiento automático y salta al final del registro. |

## Consejos

- Desplazarse hacia arriba es la forma más rápida de pausar: no es necesario alcanzar primero el botón de alternancia.
- La vista de registros tiene resaltado de sintaxis por nivel de registro y nombre de categoría, lo que facilita identificar la entrada que busca antes de que la pantalla se pausara.
- Las casillas de verificación de filtro de categorías (**Filter Categories**) y los botones **Select All** y **Deselect All** permanecen activos durante la pausa, de modo que puede reducir las entradas visibles sin reanudar el desplazamiento en vivo.

## Relacionados

- [Ver la salida de registro en vivo filtrada por categoría de diagnóstico](view-live-log-output-filtered-by-diagnostic-category.md)
- [Descripción general de Network Diagnostics](overview.md)
