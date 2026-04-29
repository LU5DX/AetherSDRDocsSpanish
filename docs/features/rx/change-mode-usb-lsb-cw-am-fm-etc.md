# Cambiar el modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para un slice (receptor virtual). Cambiar el modo adapta automáticamente los preajustes de filtro y los tamaños de paso de sintonía al nuevo tipo de modulación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- Si tiene más de un slice activo, seleccione primero el slice correcto usando la fila de pestañas A..H en la parte superior del applet RX Controls.

## Pasos

1. Si el applet RX Controls no está visible, haga clic en el botón **RX** del panel lateral derecho para mostrarlo.
2. Si su radio tiene más de un slice activo, haga clic en la pestaña correspondiente (**A** a **H**) para vincular el applet al slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. Se muestra el modo actual (predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece únicamente en versiones con soporte RADE habilitado.)
5. El slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los tamaños de paso de sintonía se actualizan automáticamente para adaptarse al nuevo modo.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Notas |
|---|---|---|---|
| **Mode combo** | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible) | Cambiar el modo adapta los preajustes de filtro y los tamaños de paso. |
| **Preajustes de ancho de filtro** | Depende del modo | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz | Los botones se ocultan en los modos FM, NFM y DFM. Haga clic derecho en un botón de preajuste para guardar el ancho de filtro actual en ese espacio. Se conservan en `FilterPresets`. |
| **STEP** | 100 Hz (índice 2) | Lista por modo (p. ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz) | Use los botones **<** / **>** o la rueda de desplazamiento para recorrer los tamaños de paso disponibles. |
| **Widget de banda de paso del filtro** | — | Arrastre los bordes inferior/superior | Ajuste fino de la banda de paso de forma independiente a los preajustes. |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo en esos modos.
- Tras cambiar a FM o NFM, los controles de tono CTCSS y desplazamiento de repetidor (Tone mode, Offset, −, Simplex, +, REV) quedan visibles. Consulte [Trabajar con un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para más detalles.
- Tras cambiar a CW, el indicador **QSK** en el encabezado pasa a ser relevante. Su estado se controla desde el applet CW, no desde RX Controls.
- Los controles de modo AGC se ocultan cuando hay un modo de la familia FM activo.

## Solución de problemas

- **El menú Mode combo no aparece o está desactivado** — El applet no está conectado al radio. Verifique la conexión mediante `Settings > Connect to Radio...`.
- **Los botones de preajuste de filtro desaparecieron después de cambiar el modo** — Esto es lo esperado al cambiar a FM, NFM o DFM. Esos modos no usan preajustes de filtro.

## Relacionados

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Trabajar con un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Entender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
