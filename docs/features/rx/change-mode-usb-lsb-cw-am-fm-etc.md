# Cambiar el modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para un slice (receptor independiente dentro del ancho de banda). Cambiar el modo ajusta automáticamente los preajustes de filtro y los tamaños de paso de sintonía para adaptarse a la nueva modulación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa con la radio.
- Si tiene más de un slice activo, seleccione primero el slice correcto usando la fila de pestañas A..H en la parte superior del applet RX Controls.

## Pasos

1. Si el applet RX Controls no está visible, haga clic en el botón **RX** del panel lateral derecho para mostrarlo.
2. Si su radio tiene más de un slice activo, haga clic en la pestaña correspondiente (**A** a **H**) para vincular el applet al slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. Se muestra el modo actual (predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece únicamente en versiones compiladas con soporte RADE habilitado.)
5. El slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los tamaños de paso de sintonía se actualizan automáticamente para adaptarse al nuevo modo.

## Qué hace cada control

| Control                          | Predeterminado      | Valores válidos                                                                                                                         |
|----------------------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **Mode combo**                   | USB                 | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible)                                                     |
| **Preajustes de ancho de filtro** | Según el modo       | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz    |
| **STEP**                         | 100 Hz (índice 2)   | Lista por modo (p. ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)    |
| **Widget de banda de paso del filtro** | —            | Arrastre los bordes inferior/superior                                                                                                   |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo para estos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y desplazamiento de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Operar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado cobra relevancia. Su estado se controla desde el applet CW, no desde RX Controls.
- Los controles de modo AGC se ocultan cuando está activo un modo de la familia FM.
- Los preajustes de filtro ahora se almacenan en formato `lo:hi` (p. ej. `300:3000`), además del formato de ancho simple anterior. Ambos formatos se leen correctamente. Si guardó preajustes personalizados en una versión anterior, seguirán funcionando sin ninguna acción de su parte.

## Comportamiento de las pestañas de slice (v0.9.5.1)

Cuando la radio informa un cambio en el número de slices disponibles, la fila de pestañas A..H ahora se reconstruye correctamente en lugar de omitirse. El comportamiento anterior mantenía los botones antiguos si ya existían; la v0.9.5.1 elimina y recrea los botones cada vez que cambia el número de slices (`clearSliceButtons()`, #2254). Al desconectarse, la fila de pestañas se oculta y el **Slice badge** estático se restaura automáticamente.

Las conexiones de señal para los clics en los botones de slice también están protegidas para que al reconectarse a la radio no se añadan manejadores duplicados.

## Solución de problemas

- **El menú Mode combo no aparece o está desactivado** — El applet no está conectado a la radio. Verifique la conexión mediante `Settings > Connect to Radio...`.
- **Los botones de preajuste de filtro desaparecieron al cambiar de modo** — Esto es normal al cambiar a FM, NFM o DFM. Estos modos no utilizan preajustes de filtro.
- **Las pestañas de slice muestran un número incorrecto de botones tras reconectarse** — Este era un problema conocido corregido en la v0.9.5.1 (#2254). Actualice a la versión actual si observa botones de pestaña obsoletos.

## Relacionado

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Operar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
