# Configurar la potencia TX máxima por banda y el modo de ajuste

Esta página explica cómo establecer un límite de potencia TX para toda la radio y cómo elegir un modo de ajuste en AetherSDR, así como la manera de abrir la configuración dedicada de potencia TX y ajuste por banda para el FLEX-8600.

## Antes de comenzar

- La radio debe estar conectada. `Settings > Radio Setup...` no está disponible sin una conexión de radio activa.
- Tenga en cuenta el nivel de potencia máximo que desea permitir, en porcentaje (0–100 %).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Para establecer un límite de potencia para toda la radio, ajuste **Max Power:** al valor deseado (0–100 %).
4. Para cambiar el comportamiento del botón de ajuste, seleccione la opción deseada en el menú desplegable **Tune Mode:**.
5. Para configurar la potencia y el modo de ajuste por banda, haga clic en **TX Band Settings**. Esto abre el diálogo dedicado de potencia TX y ajuste por banda.

   Como alternativa, abra el diálogo por banda directamente desde `Settings > TX Band Settings...`.

## Qué hace cada control

| Control | Tipo | Rango válido | Comportamiento |
|---|---|---|---|
| **Max Power:** | Spinbox | 0–100 % | Establece un límite de potencia TX a nivel de radio que se aplica a todas las bandas. |
| **Tune Mode:** | Menú desplegable | Modos listados en el desplegable | Selecciona el comportamiento del botón de ajuste cuando se activa. |
| **TX Band Settings** | Botón | — | Abre el diálogo por banda donde puede configurar la potencia TX, la potencia de ajuste, los parámetros de inhibición y el control de amplificador externo para cada banda individual. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Cuando está habilitado, muestra la señal TX en el display de waterfall durante la transmisión. |
| **TX Follows Active Slice / Active Slice Follows TX** | Botón | — | Modos mutuamente excluyentes que controlan si el TX sigue al slice activo o si el slice activo sigue al TX. |

## Consejos

- **Max Power:** se aplica a nivel de radio en todas las bandas. Use el diálogo por banda (abierto mediante **TX Band Settings**) para imponer límites más precisos en bandas individuales.
- El elemento de menú `Settings > TX Band Settings...` abre el diálogo por banda directamente, sin pasar por el diálogo Radio Setup.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Verificar el número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
