# Seleccionar un ancho de filtro preestablecido para el modo actual

Los presets de ancho de filtro permiten cambiar la banda de paso de recepción a un ancho estándar con un solo clic. Los presets están agrupados por modo, por lo que los botones mostrados cambian al cambiar de modo. El ancho seleccionado se refleja de inmediato en el indicador de ancho de filtro y en el widget de banda de paso del filtro.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet RX Controls.
- Establezca el modo en el que desea operar usando el combo Mode, ya que los presets son específicos de cada modo.

## Pasos

1. Si el applet RX Controls no está visible, haga clic en el botón **RX** del panel lateral derecho para mostrarlo.
2. Confirme que el slice correcto está activo verificando la insignia de slice (A/B/C/D/E/F/G/H) en el encabezado del applet. Haga clic en la pestaña de slice correspondiente si no lo está.
3. Confirme que el modo correcto está configurado en el **combo Mode**. Los botones de preset no se muestran para los modos FM, NFM ni DFM.
4. Ubique los botones de preset de ancho de filtro debajo del combo Mode. Cada botón muestra un valor de ancho (por ejemplo, **1800**, **2700** o **3300** para USB/LSB).
5. Haga clic en el botón de preset para el ancho deseado. El indicador de ancho de filtro **2.7K** en el encabezado se actualiza para reflejar el nuevo ancho, y el widget de banda de paso del filtro se ajusta en consecuencia.
6. Para guardar el ancho de filtro actual como un preset personalizado, haga clic derecho en cualquier botón de preset y siga la indicación para almacenar el ancho actual en ese espacio. El valor se guarda en `FilterPresets`.

## Qué hace cada control

| Control | Descripción | Valores válidos | Clave persistida |
|---|---|---|---|
| Presets de ancho de filtro | Botones que aplican un ancho de banda de paso estándar para el modo actual. No se muestran para FM/NFM/DFM. | USB/LSB: 1800, 2100, 2400, 2700, 2900, 3300 Hz; AM/SAM: 5600, 6000, 8000, 10000, 12000, 14000 Hz; CW: 50, 100, 250, 400 Hz; DIGU/DIGL: 100, 300, 600, 1000, 1500, 2000 Hz; RTTY: 250, 300, 350, 400, 500, 1000 Hz | `FilterPresets` |
| Indicador de ancho de filtro | Etiqueta de solo lectura en el encabezado del applet que muestra el ancho de filtro actual (p. ej., **2.7K**). | Se actualiza al seleccionar un preset o al arrastrar manualmente la banda de paso. | — |
| Widget de banda de paso del filtro | Arrastre los bordes inferior/superior para establecer un ancho no cubierto por un preset. | Controladores de arrastre en los bordes inferior y superior del filtro. | — |

## Consejos

- Hacer clic derecho en un botón de preset permite sobrescribir ese espacio con el ancho de banda de paso actual, de modo que pueda personalizar los presets según sus hábitos operativos sin perder los demás espacios.
- Después de aplicar un preset, puede ajustar los bordes arrastrando el controlador inferior o superior en el widget de banda de paso del filtro. El indicador de ancho se actualiza en tiempo real.
- Los modos FM, NFM y DFM no muestran botones de preset. El radio gestiona la banda de paso automáticamente en esos modos.

## Temas relacionados

- [Cambiar de modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
