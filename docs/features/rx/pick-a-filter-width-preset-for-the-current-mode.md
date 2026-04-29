# Seleccionar un ancho de filtro predefinido para el modo actual

Use los botones de ancho de filtro predefinido en el applet RX Controls para aplicar rápidamente un ancho de banda de paso estándar para el modo activo. Los valores predefinidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Configure primero el modo del slice. Los valores predefinidos varían según el modo, y los predefinidos no se muestran para los modos FM, NFM ni DFM.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón RX tray en la barra lateral derecha.
2. Si la fila de pestañas de slice está visible, haga clic en la pestaña (A hasta H) correspondiente al slice que desea ajustar.
3. Confirme que el modo mostrado en el combo Mode sea el correcto. Los predefinidos de filtro cambian cuando cambia el modo.
4. Haga clic en cualquiera de los botones de ancho de filtro predefinido para aplicar ese ancho de banda de inmediato. El ancho de filtro actual que se muestra en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el predefinido aplicado.
5. Para guardar el paso de banda de filtro actual como un predefinido, haga clic derecho en cualquier botón de ancho de filtro predefinido y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control | Comportamiento | Predefinidos predeterminados por modo | Clave persistente |
|---|---|---|---|
| Botones de ancho de filtro predefinido | Haga clic para aplicar un ancho de banda predefinido al slice actual. Haga clic derecho para guardar el ancho de filtro actual como predefinido. Ocultos en los modos FM, NFM y DFM. | Vea la tabla a continuación | `FilterPresets` |
| Etiqueta de ancho de filtro | Indicador de solo lectura que muestra el ancho de banda de filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un predefinido o cuando se arrastran los bordes del paso de banda. | — | — |
| Widget de paso de banda de filtro | Arrastre el borde inferior o superior para establecer un paso de banda personalizado. Use los predefinidos para anchos estándar. | — | — |

**Valores predefinidos predeterminados por modo:**

| Modo | Anchos predefinidos (Hz) |
|---|---|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin predefinidos (botones ocultos) |

## Consejos

- Si necesita un ancho que no coincida con ningún predefinido, arrastre los bordes del widget de paso de banda de filtro para establecer un valor arbitrario y, a continuación, haga clic derecho en un botón predefinido para guardar ese ancho para uso futuro.
- Los predefinidos son por modo. Al cambiar de modo, el filtro se reajusta y se muestran los botones predefinidos correspondientes al nuevo modo.

## Solución de problemas

- **Los botones predefinidos no están visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen predefinidos de filtro. Cambie el modo usando el combo Mode a un modo que admita predefinidos (por ejemplo, USB o CW).
- **Hacer clic derecho en un botón predefinido no produce ningún efecto visible** — Confirme que el slice esté conectado al radio. El applet RX requiere una conexión activa con el radio para guardar valores predefinidos.

## Temas relacionados

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
