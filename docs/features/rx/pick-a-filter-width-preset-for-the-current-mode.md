# Seleccionar un ajuste preestablecido de ancho de filtro para el modo actual

Use los botones de ajuste preestablecido de ancho de filtro en el applet RX Controls para aplicar rápidamente un ancho de paso estándar para el modo activo. Los ajustes preestablecidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet RX Controls requiere una conexión activa con el equipo.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Establezca primero el modo del slice. Los valores preestablecidos varían según el modo, y los ajustes preestablecidos no se muestran para los modos FM, NFM ni DFM.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón RX del panel lateral derecho.
2. Si la fila de pestañas de slice está visible, haga clic en la pestaña (A hasta H) correspondiente al slice que desea ajustar.
3. Confirme que el modo mostrado en el combo Mode sea el correcto. Los ajustes preestablecidos de filtro cambian cuando el modo cambia.
4. Haga clic en cualquiera de los botones de ajuste preestablecido de ancho de filtro para aplicar ese ancho de banda de inmediato. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el ajuste preestablecido aplicado.
5. Para guardar el paso de banda de filtro actual como ajuste preestablecido, haga clic derecho en cualquier botón de ajuste preestablecido de ancho de filtro y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control | Comportamiento | Ajustes preestablecidos predeterminados por modo | Clave persistente |
|---|---|---|---|
| Ajustes preestablecidos de ancho de filtro | Haga clic para aplicar un ancho de banda preestablecido al slice actual. Haga clic derecho para guardar el ancho de filtro actual como ajuste preestablecido. Oculto en los modos FM, NFM y DFM. | Vea la tabla a continuación | `FilterPresets` |
| Etiqueta de ancho de filtro | Indicador de solo lectura que muestra el ancho de banda de filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un ajuste preestablecido o cuando se arrastran los bordes del paso de banda. | — | — |
| Widget de paso de banda del filtro | Arrastre el borde inferior o superior para establecer un paso de banda personalizado. Use los ajustes preestablecidos para anchos estándar. | — | — |

**Valores preestablecidos predeterminados por modo:**

| Modo | Anchos preestablecidos (Hz) |
|---|---|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin ajustes preestablecidos (botones ocultos) |

## Consejos

- Si necesita un ancho que no coincida con ningún ajuste preestablecido, arrastre los bordes del widget de paso de banda del filtro para establecer un valor arbitrario y, luego, haga clic derecho en un botón de ajuste preestablecido para guardar ese ancho para uso futuro.
- Los ajustes preestablecidos son por modo. Al cambiar de modo, el filtro se reconfigura y se muestran los botones de ajuste preestablecido para el nuevo modo.

## Solución de problemas

- **Los botones de ajuste preestablecido no son visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen ajustes preestablecidos de filtro. Cambie el modo usando el combo Mode a un modo que admita ajustes preestablecidos (por ejemplo, USB o CW).
- **El clic derecho en un botón de ajuste preestablecido no produce ningún efecto visible** — Confirme que el slice está conectado al equipo. El applet RX requiere una conexión activa con el equipo para guardar los valores preestablecidos.

## Relacionados

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
