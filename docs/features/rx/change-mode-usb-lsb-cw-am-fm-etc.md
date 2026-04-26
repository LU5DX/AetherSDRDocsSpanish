# Cambiar el modo (USB, LSB, CW, AM, FM, etc.)

Use esta página para cambiar el modo de demodulación de un slice de recepción. Al cambiar el modo, los preajustes de filtro y los tamaños de paso de sintonía se adaptan automáticamente al nuevo modo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls solo está activo cuando hay una conexión de radio presente.
- El applet RX Controls debe estar visible en el panel de applets. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña correspondiente (A hasta H) en la parte superior del applet RX Controls para seleccionar el slice que desea cambiar.
2. Localice el **Mode combo** en el applet RX Controls. Su valor predeterminado es USB.
3. Haga clic en el **Mode combo** para abrir la lista de modos.
4. Seleccione el modo deseado: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY.
5. El slice cambia al modo seleccionado de inmediato. Los botones de preajuste de filtro y los tamaños de paso de sintonía se actualizan para coincidir con el nuevo modo.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Notas |
|---|---|---|---|
| Mode combo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY | Al seleccionar un modo, se reconfiguran los preajustes de filtro y paso. |
| Preajustes de ancho de filtro | depende del modo | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz | Se almacenan como `FilterPresets`. No se muestran en los modos FM, NFM y DFM. Haga clic derecho en un botón de preajuste para guardar el ancho de filtro actual en ese preajuste. |
| STEP | 100 Hz (índice 2) | Lista por modo; p. ej., SSB: 1/10/50/100/500/1000/2000/3000 Hz; CW: 1/5/10/50/100/200/400 Hz; FM: 50/250/500/2500/3000/5000/10000/12500 Hz | Haga clic en `<` o `>`, o use la rueda del ratón, para recorrer los tamaños de paso. |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de filtro. El ancho de filtro es fijo en esos modos.
- Después de cambiar a CW, el indicador QSK en la fila de encabezado se ilumina en ámbar cuando el CW break-in está activo. Ese estado se controla desde el applet CW, no desde aquí.
- Hacer clic derecho en un botón de preajuste de filtro guarda el ancho de pasabanda actual en ese slot de preajuste, almacenado como `FilterPresets`.

## Relacionados

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Trabajar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de RX Controls](overview.md)
