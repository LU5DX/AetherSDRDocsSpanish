# Pausar el desplazamiento del registro para inspeccionar una entrada antigua

La pestaña Logs en Diagnóstico de red sigue el archivo de registro de AetherSDR en tiempo real. Esta página explica cómo pausar ese desplazamiento automático para poder leer una entrada antigua sin que la vista se mueva, y cómo reanudar la visualización en vivo cuando haya terminado.

## Antes de comenzar

- Abra Diagnóstico de red mediante `Settings > Network...`.
- Haga clic en la pestaña **Logs** para que el visor de registros sea visible.

## Pasos

1. Vaya a `Settings > Network...`.
2. Haga clic en la pestaña **Logs**.
3. Para pausar el desplazamiento, realice una de las siguientes acciones:
   - Desplácese hacia arriba en el visor de registros. El visor cambia automáticamente a **Paused**.
   - Haga clic en el botón de alternancia, que muestra **Live**, para cambiarlo a **Paused**.
4. Lea la entrada que necesite. La pantalla permanece fija mientras el botón muestra **Paused**.
5. Cuando esté listo para volver a la visualización en vivo, haga clic en el botón de alternancia, que ahora muestra **Paused**, para cambiarlo de nuevo a **Live**. El visor salta inmediatamente a la salida más reciente y reanuda el desplazamiento automático.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Live / Paused** (botón de alternancia) | Live | Cuando está en **Live**, el visor se desplaza automáticamente a la salida de registro más reciente. Cuando está en **Paused**, el desplazamiento se detiene y la pantalla mantiene su posición actual. Desplazarse hacia arriba en el visor cambia automáticamente el botón a **Paused**. Al hacer clic en el botón mientras muestra **Paused** se reanuda el desplazamiento automático y salta al final del registro. |

## Consejos

- Desplazarse hacia arriba es la forma más rápida de pausar: no necesita alcanzar primero el botón de alternancia.
- La vista de registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría, lo que facilita localizar la entrada que busca antes de que se detenga la pantalla.
- Las casillas de verificación de filtro por categoría (**Filter Categories**) y los botones **Select All** y **Deselect All** permanecen activos mientras está en pausa, por lo que puede reducir las entradas visibles sin reanudar el desplazamiento en vivo.

## Relacionado

- [View live log output filtered by diagnostic category](view-live-log-output-filtered-by-diagnostic-category.md)
- [Network Diagnostics overview](overview.md)
