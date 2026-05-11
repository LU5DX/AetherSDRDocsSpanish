# Cambiar modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para una slice. Cambiar el modo reconfigura los preajustes de filtro y los tamaños de paso de sintonización para adaptarlos a la nueva modulación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de controles de RX requiere una conexión activa con la radio.
- Si tiene más de una slice, seleccione primero la slice correcta usando la fila de pestañas **A..H** en la parte superior del applet de controles de RX.

## Pasos

1. Si el applet de controles de RX no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de una slice activa, haga clic en la pestaña de slice correspondiente (**A** a la **H**) para vincular el applet a la slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. El modo actual se muestra (valor predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece solo en versiones con soporte RADE habilitado).
5. La slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los tamaños de paso de sintonización se actualizan automáticamente para adaptarse al nuevo modo.

## Qué hace cada control

| Control                      | Valor predeterminado | Valores válidos                                                                                                                         |
|------------------------------|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **Mode combo**               | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible)                                                        |
| **Preajustes de ancho de filtro** | Depende del modo    | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz      |
| **STEP**                     | 100 Hz (índice 2)   | Lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)         |
| **Widget de paso de banda del filtro** | —                   | Arrastre los bordes inferior/superior                                                                                                     |
| **SQL**                      | Desactivado          | Botón de alternancia para activar el squelch. Se desactiva automáticamente en modos RTTY, DIGU, DIGL, NT, CW y CWL. En modos RTTY y digitales, el squelch también se desactiva automáticamente para evitar el bloqueo de señales FSK (#2504). |
| **Nivel de squelch**         | 20                   | Deslizador (0-100) para establecer el umbral de squelch. Deshabilitado en modos RTTY, DIGU, DIGL, NT, CW y CWL.                         |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y desplazamiento de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado se vuelve relevante. Su estado se controla desde el applet CW, no desde controles de RX.
- Los controles de modo AGC están ocultos cuando un modo de la familia FM está activo.
- Los preajustes de filtro ahora se almacenan en formato `lo:hi` (ej. `300:3000`) además del formato anterior de ancho simple. Ambos formatos se leen correctamente. Si ha guardado preajustes personalizados de una versión anterior, siguen funcionando sin necesidad de realizar ninguna acción.
- El método `stepFilterWidth()` recorre la lista de preajustes por modo para que los atajos de teclado de ensanchar/estrechar produzcan una geometría de bordes correcta según el modo. Esto garantiza que al ensanchar o estrechar el filtro usando atajos de teclado, el filtro se mantenga dentro de los límites de preajuste apropiados para el modo actual.
- Al cambiar a RTTY o modos digitales (DIGU, DIGL), el squelch se desactiva y apaga automáticamente. Esto evita que el squelch elimine caracteres FSK e interrumpa la decodificación (#2504).

## Comportamiento de las pestañas de slice (v0.9.5.1)

Cuando la radio reporta un cambio en el número de slices disponibles, la fila de pestañas **A..H** ahora se reconstruye correctamente en lugar de omitirse. El comportamiento anterior mantenía los botones antiguos si ya estaban presentes; v0.9.5.1 elimina y recrea los botones cada vez que el número de slices cambia (`clearSliceButtons()`, #2254). Al desconectarse, la fila de pestañas se oculta y la **insignia de slice** estática se restaura automáticamente.

Las conexiones de señal para los clics de los botones de slice también están protegidas para que reconectarse a la radio no adjunte controladores duplicados.

## Formato del ancho de filtro (v0.9.8)

La lectura del ancho de filtro en el applet de controles de RX ahora utiliza lógica específica del modo para mostrar el ancho etiquetado correcto. Esta lectura se comparte con el panel VFO para un formato consistente (#2197). El método estático `formatFilterWidth()` aplica reglas según el modo para que los modos SSB y digitales muestren la etiqueta de ancho de banda esperada (ej., "2.7K" para 2700 Hz USB, "500" para 500 Hz CW).

## Solución de problemas

- **Mode combo falta o está atenuado** — El applet no está conectado a la radio. Verifique la conexión mediante `Settings > Connect to Radio...`
- **Los botones de preajuste de filtro desaparecieron después de cambiar de modo** — Esto es normal al cambiar a FM, NFM o DFM. Esos modos no utilizan preajustes de filtro.
- **Las pestañas de slice muestran un número incorrecto de botones después de reconectar** — Este era un problema conocido solucionado en v0.9.5.1 (#2254). Actualice a la versión actual si ve botones de pestaña obsoletos.

## Relacionados

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
