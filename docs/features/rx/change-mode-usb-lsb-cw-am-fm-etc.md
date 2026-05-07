# Cambiar modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para un slice. Cambiar el modo reconfigura los valores predefinidos del filtro y los pasos de sintonización para adaptarse a la nueva modulación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles RX requiere una conexión activa con la radio.
- Si tiene más de un slice, seleccione primero el slice correcto usando la fila de pestañas A..H en la parte superior del applet de Controles RX.

## Pasos

1. Si el applet de Controles RX no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de un slice activo, haga clic en la pestaña del slice correspondiente (**A** a **H**) para vincular el applet al slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. Se muestra el modo actual (valor predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece solo en versiones con soporte RADE habilitado).
5. El slice cambia al modo seleccionado. Los valores predefinidos del ancho de filtro y los pasos de sintonización se actualizan automáticamente para adaptarse al nuevo modo.

## Qué hace cada control

| Control                    | Valor predeterminado | Valores válidos                                                                                                                       |
|----------------------------|----------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Mode combo**             | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible)                                                     |
| **Filter width presets**   | Depende del modo     | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz   |
| **STEP**                   | 100 Hz (índice 2)    | Lista por modo (p. ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)    |
| **Filter passband widget** | —                    | Arrastre los bordes lo/hi                                                                                                             |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de valores predefinidos de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y desplazamiento de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado se vuelve relevante. Su estado se controla desde el applet CW, no desde Controles RX.
- Los controles de modo AGC están ocultos cuando un modo de la familia FM está activo.
- Los valores predefinidos de filtro ahora se almacenan en un formato `lo:hi` (p. ej. `300:3000`) además del formato anterior de solo ancho. Ambos formatos se leen correctamente. Si ha guardado valores predefinidos personalizados de una versión anterior, siguen funcionando sin necesidad de ninguna acción de su parte.
- El método `stepFilterWidth()` recorre la lista de valores predefinidos por modo, de modo que los atajos de teclado para ensanchar/estrechar producen una geometría de bordes correcta para el modo. Esto garantiza que al ensanchar o estrechar el filtro usando atajos de teclado, el filtro se mantenga dentro de los límites predefinidos adecuados para el modo actual.

## Comportamiento de las pestañas de slice (v0.9.5.1)

Cuando la radio informa un cambio en el número de slices disponibles, la fila de pestañas A..H se reconstruye correctamente en lugar de omitirse. El comportamiento anterior mantenía los botones antiguos si ya estaban presentes; la v0.9.5.1 elimina y vuelve a crear los botones cada vez que cambia el número de slices (`clearSliceButtons()`, #2254). Al desconectarse, la fila de pestañas se oculta y el **Slice badge** estático se restaura automáticamente.

Las conexiones de señal para los clics en los botones de slice también están protegidas para que la reconexión a la radio no agregue controladores duplicados.

## Formato del ancho de filtro (v0.9.8)

La lectura del ancho de filtro en el applet de Controles RX ahora usa lógica específica por modo para mostrar el ancho etiquetado correcto. Esta lectura se comparte con el panel VFO para un formato consistente (#2197). El método estático `formatFilterWidth()` aplica reglas sensibles al modo para que los modos SSB y digitales muestren la etiqueta de ancho de banda esperada (p. ej., "2.7K" para 2700 Hz USB, "500" para 500 Hz CW).

## Solución de problemas

- **Mode combo falta o está atenuado** — El applet no está conectado a la radio. Verifique la conexión en `Settings > Connect to Radio...`.
- **Los botones de valores predefinidos de filtro desaparecieron después de cambiar el modo** — Esto es esperado al cambiar a FM, NFM o DFM. Esos modos no usan valores predefinidos de filtro.
- **Las pestañas de slice muestran el número incorrecto de botones después de reconectar** — Este era un problema conocido solucionado en v0.9.5.1 (#2254). Actualice a la versión actual si ve botones de pestaña obsoletos.

## Relacionados

- [Seleccionar un valor predefinido de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
