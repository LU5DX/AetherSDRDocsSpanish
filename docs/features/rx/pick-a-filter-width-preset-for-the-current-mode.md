# Elija un ancho de filtro preestablecido para el modo actual

Utilice los botones de ancho de filtro preestablecido en el applet RX Controls para aplicar rápidamente un ancho de banda estándar para el modo activo. Los preestablecidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa a la radio.
- Seleccione la slice que desea ajustar utilizando las pestañas de slice (A..H) si hay más de una slice activa.
- Establezca primero el modo de la slice. Los valores preestablecidos varían según el modo, y los preestablecidos no se muestran para los modos FM, NFM o DFM.

## Pasos

1. Abra el applet RX Controls. Si no es visible, haga clic en el botón RX tray en la barra lateral derecha.
2. Si la fila de pestañas de slice es visible, haga clic en la pestaña (A a H) correspondiente a la slice que desea ajustar.
3. Confirme que el modo mostrado en el combo Mode es correcto. Los preestablecidos de filtro cambian cuando cambia el modo.
4. Haga clic en cualquiera de los botones de ancho de filtro preestablecido para aplicar ese ancho de banda inmediatamente. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el preestablecido aplicado.
5. Para guardar el ancho de banda actual del filtro como preestablecido, haga clic con el botón derecho en cualquier botón de ancho de filtro preestablecido y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control                | Comportamiento                                                                                                                                                                | Preestablecidos por defecto por modo |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| Preestablecidos de ancho de filtro   | Haga clic para aplicar un ancho de banda preestablecido a la slice actual. Haga clic con el botón derecho para guardar el ancho de filtro actual como preestablecido. Oculto en modos FM, NFM y DFM.                     | Vea la tabla siguiente         |
| Etiqueta de ancho de filtro     | Indicador de solo lectura que muestra el ancho de banda de filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un preestablecido o cuando se arrastran los bordes de la banda de paso. | —                       |
| Widget de banda de paso del filtro | Arrastre el borde inferior o superior para establecer una banda de paso personalizada. Utilice preestablecidos para anchos estándar.                                                                                                                    | —                       |
| Modo                   | Anchos preestablecidos (Hz)                                                                                                                                                      |                         |
| ---                    | ---                                                                                                                                                                     |                         |
| USB, LSB               | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                      |                         |
| AM, SAM                | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                                   |                         |
| CW                     | 50, 100, 250, 400                                                                                                                                                       |                         |
| DIGU, DIGL, NT         | 100, 300, 600, 1000, 1500, 2000                                                                                                                                         |                         |
| RTTY                   | 250, 300, 350, 400, 500, 1000                                                                                                                                           |                         |
| FM, NFM, DFM           | Sin preestablecidos (botones ocultos)                                                                                                                                             |                         |

## Colores de pestañas de slice y distintivos (v0.9.3)

A partir de v0.9.3, los botones de pestaña de slice y el distintivo de slice utilizan colores por slice gestionados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de pestaña y el fondo del distintivo reflejan todos el color asignado a esa slice. Los colores persisten entre sesiones y también se reflejan en widgets VFO y tiras de medidores. No se requiere ninguna acción; los colores se actualizan automáticamente cuando se conecta una slice.

## Consejos

- Si necesita un ancho que no coincida con ningún preestablecido, arrastre los bordes del widget de banda de paso del filtro para establecer un valor arbitrario, luego haga clic con el botón derecho en un botón preestablecido para guardar ese ancho para uso futuro.
- Los preestablecidos son por modo. Cambiar de modo remodela el filtro y muestra los botones preestablecidos para el nuevo modo.
- El modo NT utiliza los mismos preestablecidos de filtro y comportamiento de squelch que DIGU y DIGL. El squelch está deshabilitado en modo NT y se envía automáticamente squelch off a la radio si el squelch estaba habilitado anteriormente.

## Solución de problemas

- **Los botones preestablecidos no son visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen preestablecidos de filtro. Cambie el modo utilizando el combo Mode a un modo que admita preestablecidos (por ejemplo, USB o CW).
- **Hacer clic con el botón derecho en un botón preestablecido no hace nada visible** — Confirme que la slice está conectada a la radio. El applet RX requiere una conexión activa a la radio para guardar valores preestablecidos.
- **Los controles de squelch aparecen atenuados** — El modo activo es DIGU, DIGL, NT, CW o CWL. El squelch está deshabilitado en estos modos. En modos digitales (incluido NT) el squelch se desactiva automáticamente; en modos CW la radio gestiona el estado de squelch directamente.

## Relacionado

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices utilizando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
