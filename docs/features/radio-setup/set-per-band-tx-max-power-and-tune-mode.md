# Establecer la potencia TX máxima por banda y el modo de sintonía

Use esta página para limitar la potencia de transmisión por banda y elegir el comportamiento de la función Tune. Estos ajustes se almacenan en el radio y se aplican independientemente del cliente que se conecte.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña TX no es accesible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y sintonía por banda.
4. En la tabla por banda, localice la banda que desea configurar.
5. Ajuste el límite de potencia para esa banda según sea necesario. El rango válido para **Max Power:** es 0–100 %.
6. Para cambiar el comportamiento de la sintonía, seleccione la opción deseada en el cuadro combinado **Tune Mode:**.
7. Cierre el diálogo cuando haya terminado. Los ajustes se aplican inmediatamente al radio.

## Qué hace cada control

| Control | Tipo | Rango válido / opciones | Comportamiento |
|---|---|---|---|
| **TX Band Settings** | Botón | — | Abre el diálogo dedicado de potencia y sintonía por banda. |
| **Max Power:** | Cuadro de número | 0–100 % | Establece el límite de potencia TX a nivel de radio para la banda seleccionada. |
| **Tune Mode:** | Cuadro combinado | Consulte las opciones del firmware del radio | Selecciona el comportamiento del botón Tune cuando se activa. |
| **Show TX in Waterfall:** | Botón de alternancia | Enabled / Disabled | Dibuja la señal TX en la visualización de waterfall durante la transmisión. |
| **TX Follows Active Slice / Active Slice Follows TX** | Par de botones | Mutuamente excluyentes | Controla si el slice TX sigue al slice activo o viceversa. |

## Consejos

- **TX Band Settings** también es accesible directamente desde `Settings > TX Band Settings...` sin necesidad de abrir Radio Setup primero.
- El cuadro de número **Max Power:** en la pestaña TX establece un límite a nivel de radio. Los límites por banda configurados dentro de **TX Band Settings** operan sobre este límite.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Cargar un nuevo firmware .ssdr en el radio](upload-a-new-firmware-ssdr-to-the-radio.md)
