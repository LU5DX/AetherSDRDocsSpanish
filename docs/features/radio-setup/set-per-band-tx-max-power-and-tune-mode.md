# Configurar la potencia TX máxima por banda y el modo de sintonía

Esta página explica cómo configurar el límite de potencia de transmisión y el comportamiento de sintonía para cada banda de radioaficionado en el FLEX-8600. Use estos ajustes para proteger amplificadores o cumplir con los límites de potencia específicos de cada banda sin tener que ajustar el control de potencia principal cada vez que cambie de banda.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Estos controles no están disponibles cuando no hay una conexión de radio activa.
- Identifique las bandas que desea restringir y el límite de potencia (como porcentaje de la salida total) que desea aplicar a cada una.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Para establecer un límite de potencia a nivel de radio que se aplique independientemente de la banda, ajuste **Max Power:** al valor deseado (0–100 %).
4. Para configurar la potencia y la sintonía por banda, haga clic en **TX Band Settings**. Esto abre el diálogo dedicado de potencia y sintonía por banda.
5. En el diálogo TX Band Settings, localice la fila correspondiente a la banda que desea configurar.
6. Establezca la potencia TX máxima para esa banda usando el campo de potencia en esa fila.
7. Establezca el comportamiento de sintonía para esa banda usando el campo de modo de sintonía en esa fila.
8. Repita los pasos 5–7 para cada banda que desee configurar.
9. Para establecer el comportamiento de sintonía a nivel de radio (fuera de los ajustes por banda), regrese a la pestaña **TX** y seleccione la opción deseada en **Tune Mode:**.
10. Cierre el diálogo cuando haya terminado. Los ajustes se aplican al equipo de inmediato.

## Qué hace cada control

| Control | Ubicación | Comportamiento | Rango válido | Valor predeterminado |
|---|---|---|---|---|
| **Max Power:** | Pestaña TX | Establece un límite de potencia TX a nivel de radio. Todas las transmisiones se restringen a este valor, independientemente de los ajustes de slice o modo. | 0–100 % | — |
| **Tune Mode:** | Pestaña TX | Selecciona cómo se comporta la función de sintonía cuando se activa. | Opciones del cuadro combinado (definidas por el firmware del equipo) | — |
| **TX Band Settings** | Pestaña TX | Abre el diálogo de potencia y sintonía por banda, donde cada banda de radioaficionado puede configurarse de forma independiente. | — | — |
| **Show TX in Waterfall:** | Pestaña TX | Cuando está habilitado, la señal transmitida se dibuja en el waterfall. | Activado / Desactivado | — |
| **TX Follows Active Slice / Active Slice Follows TX** | Pestaña TX | Modos mutuamente excluyentes que controlan si la frecuencia TX sigue al slice activo o viceversa. | Dos opciones | — |

## Consejos

- El cuadro numérico **Max Power:** en la pestaña TX es un límite global. Los límites por banda establecidos en el diálogo TX Band Settings operan dentro de este límite global. Si establece **Max Power:** en 50 %, un ajuste por banda del 100 % seguirá estando limitado al 50 % de la salida total del equipo.
- También puede acceder al diálogo TX Band Settings directamente mediante `Settings > TX Band Settings...` sin necesidad de abrir Radio Setup primero.

## Relacionado

- [Descripción general](overview.md)
