# Cambiar modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para un slice. Cambiar el modo adapta automáticamente los preajustes de filtro y los tamaños de paso de sintonía al nuevo tipo de modulación.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión de radio activa.
- Si tiene más de un slice activo, seleccione el slice correcto primero usando la fila de pestañas A..H en la parte superior del applet RX Controls.

## Pasos

1. Si el applet RX Controls no está visible, haga clic en el botón **RX** de la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de un slice activo, haga clic en la pestaña de slice correspondiente (**A** a **H**) para vincular el applet al slice que desea cambiar.
3. Haga clic en la lista desplegable **Mode combo**. Se muestra el modo actual (predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**, **NT**
   - (RADE aparece solo en compilaciones con soporte RADE habilitado.)
5. El slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los tamaños de paso de sintonía se actualizan automáticamente para adaptarse al nuevo modo.

## Qué hace cada control

| Control                    | Predeterminado   | Valores válidos                                                                                                                                |
|----------------------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| **Mode combo**             | USB              | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY, NT (+ RADE si está disponible)                                                         |
| **Filter width presets**   | Depende del modo | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL/NT: 100–2000 Hz; RTTY: 250–1000 Hz          |
| **STEP**                   | 100 Hz (índice 2) | Lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)               |
| **Filter passband widget** | —                | Arrastre los bordes inferior/superior                                                                                                          |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y desplazamiento de repetidor (Tone mode, Offset, −, Simplex, +, REV) se hacen visibles. Vea [Trabajar en un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para obtener detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado se vuelve relevante. Su estado se controla desde el applet CW, no desde RX Controls.
- Los controles de modo AGC se ocultan cuando está activo un modo de la familia FM.
- El modo NT se comporta como un modo digital: usa los mismos preajustes de filtro que DIGU/DIGL, los controles de squelch están deshabilitados (el audio se enruta a través de DAX), y la etiqueta de ancho de filtro se calcula de la misma manera que para USB/DIGU.

## Solución de problemas

- **Mode combo falta o está deshabilitado** — El applet no está conectado a la radio. Verifique la conexión mediante `Settings > Connect to Radio...`.
- **Los botones de preajuste de filtro desaparecieron después de cambiar de modo** — Esto es esperado al cambiar a FM, NFM o DFM. Esos modos no utilizan preajustes de filtro.
- **El botón SQL está deshabilitado después de cambiar a NT** — Esto es esperado. NT se trata como un modo digital; el squelch está deshabilitado y el audio se enruta a través de DAX.

## Relacionado

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Trabajar en un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Entender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
