# Configurar la potencia TX máxima por banda y el modo de sintonía

Esta página explica cómo establecer la potencia de transmisión máxima y el modo de sintonía para cada banda de radioaficionado en su FLEX-8600. Use estos ajustes para proteger amplificadores, cumplir los límites de potencia específicos de cada banda o configurar el comportamiento de la función Tune.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos controles no están disponibles sin una conexión activa al radio.
- Identifique las bandas que desea configurar antes de abrir el cuadro de diálogo.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Para establecer un límite de potencia a nivel de radio que se aplique a todas las bandas, ajuste **Max Power:** a un valor entre 0 y 100 %.
4. Para seleccionar el comportamiento del botón Tune, elija una opción en el menú desplegable **Tune Mode:**.
5. Para abrir los ajustes de potencia y sintonía por banda, haga clic en **TX Band Settings**. Esto abre el cuadro de diálogo dedicado por banda, donde puede ajustar la potencia TX, la potencia de sintonía, los ajustes de inhibición y el control de amplificador externo para cada banda de forma individual.
6. Alternativamente, abra el cuadro de diálogo por banda directamente desde `Settings > TX Band Settings...` sin pasar por Radio Setup.
7. Cierre el cuadro de diálogo cuando termine. Los ajustes se aplican inmediatamente al radio.

## Qué hace cada control

| Control | Tipo | Rango válido | Comportamiento |
|---|---|---|---|
| **Max Power:** | Spinbox | 0–100 % | Establece un límite de potencia TX a nivel de radio que restringe la salida en todas las bandas. |
| **Tune Mode:** | Menú desplegable | Las opciones dependen del firmware del radio | Selecciona el comportamiento del botón Tune al activarse. |
| **TX Band Settings** | Botón | — | Abre el cuadro de diálogo de potencia TX, potencia de sintonía, inhibición y control de amplificador por banda. |
| **Show TX in Waterfall:** | Interruptor | On / Off | Dibuja la señal TX en la visualización del waterfall durante la transmisión. |
| **TX Follows Active Slice / Active Slice Follows TX** | Botón | Mutuamente excluyentes | Controla si la TX sigue al slice activo o si el slice activo sigue a la TX. |

## Consejos

- El spinbox **Max Power:** en la pestaña TX es un límite global. Los límites por banda establecidos en el cuadro de diálogo TX Band Settings operan dentro de ese techo.
- Puede acceder al mismo cuadro de diálogo TX Band Settings desde `Settings > TX Band Settings...` sin necesidad de abrir Radio Setup primero.
- Use **Inhibit during TUNE** (disponible en el menú `Settings`) para suprimir salidas TX específicas —ACC TX, TX1, TX2 o TX3— durante la sintonía.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
