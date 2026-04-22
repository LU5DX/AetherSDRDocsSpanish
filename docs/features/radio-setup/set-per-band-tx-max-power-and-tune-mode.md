# Configurar la potencia TX máxima por banda y el modo de ajuste

Esta página explica cómo establecer un límite global de potencia TX y elegir el modo de ajuste para su FLEX-8600, y luego abrir la tabla de potencia y modo de ajuste por banda para configurar cada banda individualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos controles no están disponibles mientras está desconectado.
- Identifique qué bandas desea limitar y qué nivel máximo de potencia (como porcentaje) necesita.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Para establecer un límite de potencia global del radio, ajuste **Max Power:** al valor deseado (0–100 %).
4. Para cambiar el comportamiento del botón de ajuste, seleccione el modo deseado en el menú desplegable **Tune Mode:**.
5. Para configurar los ajustes de potencia y modo de ajuste por banda, haga clic en **TX Band Settings**. Esto abre el diálogo dedicado de potencia y modo de ajuste por banda.
6. En el diálogo por banda, establezca los parámetros de potencia y modo de ajuste para cada banda según sea necesario.
7. Cierre el diálogo cuando haya terminado. Los ajustes se aplican al radio de inmediato.

También puede abrir el diálogo por banda directamente desde el menú sin pasar por Radio Setup: use `Settings > TX Band Settings...`.

## Qué hace cada control

| Control | Tipo | Rango válido | Comportamiento |
|---|---|---|---|
| **Max Power:** | Cuadro de número | 0–100 % | Establece un límite de potencia TX a nivel del radio que se aplica a todos los slices. |
| **Tune Mode:** | Lista desplegable | Ver opciones del radio | Selecciona el comportamiento del botón de ajuste cuando se activa. |
| **TX Band Settings** | Botón | — | Abre el diálogo de potencia y modo de ajuste por banda, donde puede establecer la potencia TX, la potencia de ajuste, los ajustes de inhibición y el control de amplificador externo para cada banda individualmente. |
| **Show TX in Waterfall:** | Botón de alternancia | On / Off | Dibuja la señal TX en la pantalla de waterfall mientras se transmite. |
| **TX Follows Active Slice / Active Slice Follows TX** | Botón | Mutuamente excluyente | Controla si la TX sigue al slice activo o si el slice activo sigue a la TX. |

## Consejos

- **Max Power:** es un límite a nivel del radio. No reemplaza los límites por banda establecidos en el diálogo TX Band Settings; ambos se aplican.
- Si solo necesita ajustar una única banda rápidamente, use `Settings > TX Band Settings...` para omitir el diálogo Radio Setup por completo.

## Temas relacionados

- [Descripción general de Radio Setup](overview.md)
- [Verificar número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
