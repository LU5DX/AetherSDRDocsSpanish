# Cambiar modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para un slice. Cambiar el modo reconfigura los preajustes de filtro y los tamaños de paso de sintonización para adaptarse a la nueva modulación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles RX requiere una conexión activa a la radio.
- Si tiene más de un slice, seleccione primero el slice correcto usando la fila de pestañas A..H en la parte superior del applet de Controles RX.

## Pasos

1. Si el applet de Controles RX no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de un slice activo, haga clic en la pestaña del slice correspondiente (**A** a **H**) para vincular el applet al slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. El modo actual se muestra (predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece solo en versiones con soporte RADE habilitado.)
5. El slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los tamaños de paso de sintonización se actualizan automáticamente para adaptarse al nuevo modo.

## Qué hace cada control

| Control                       | Predeterminado  | Valores válidos                                                                                                                                                                                                   |
|-------------------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Mode combo**                | USB             | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible)                                                                                                                                |
| **Preajustes de ancho de filtro** | Depende del modo | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz                                                                            |
| **STEP**                      | 100 Hz (índice 2) | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)                                                                            |
| **Widget de banda pasante del filtro** | —               | Arrastre los bordes inferior/superior                                                                                                                                                                             |
| **SQL**                       | Off             | Botón de alternancia para habilitar el squelch. Se desactiva automáticamente en modos RTTY, DIGU, DIGL, NT, CW y CWL. En modos RTTY y digitales, el squelch también se apaga automáticamente para evitar bloquear señales FSK (#2504). |
| **Nivel de squelch**          | 20              | Deslizador (0-100) para ajustar el umbral de squelch. Deshabilitado en modos RTTY, DIGU, DIGL, NT, CW y CWL.                                                                                                     |
| **Antena RX**                 | ANT1            | Cuadro combinado que lista las antenas de recepción disponibles. Se completa desde `ant_list` de la radio o desde `rxAntennaList()` del slice cuando está disponible.                                            |
| **Antena TX**                 | ANT1            | Cuadro combinado que lista las antenas capaces de transmitir. Los puertos de solo RX (prefijo 'RX') se filtran. Usa `txAntennaOptions()` para la lista.                                                           |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y desplazamiento de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado cobra relevancia. Su estado se controla desde el applet CW, no desde Controles RX.
- Los controles de modo AGC están ocultos cuando un modo de la familia FM está activo.
- Los preajustes de filtro ahora se almacenan en formato `lo:hi` (p. ej., `300:3000`) además del formato anterior de ancho simple. Ambos formatos se leen correctamente. Si ha guardado preajustes personalizados de una versión anterior, seguirán funcionando sin necesidad de ninguna acción de su parte.
- El método `stepFilterWidth()` recorre la lista de preajustes por modo, por lo que los atajos de teclado para ensanchar/estrechar producen una geometría de borde correcta para el modo. Esto asegura que al ensanchar o estrechar el filtro usando atajos de teclado, el filtro se mantenga dentro de los límites de preajuste apropiados para el modo actual.
- Al cambiar a RTTY o modos digitales (DIGU, DIGL), el squelch se deshabilita y apaga automáticamente. Esto evita que el squelch elimine caracteres FSK e interrumpa la decodificación (#2504).
- El nivel de squelch manual se conserva entre sesiones. El último valor elegido por el usuario se almacena en la configuración `LastManualSquelchLevel` y se restaura al iniciar. Esto preserva la preferencia manual del operador entre ciclos de modo, ya que el modo automático podría sobrescribir el `squelchLevel` del slice con valores sugeridos por el algoritmo (#2606).
- La insignia del slice ahora admite formato de texto enriquecido (HTML) para la letra del slice (#2606).

## Comportamiento de la pestaña de slice (v0.9.5.1)

Cuando la radio informa un cambio en el número de slices disponibles, la fila de pestañas A..H ahora se reconstruye correctamente en lugar de omitirse. El comportamiento anterior mantenía los botones antiguos si ya había alguno presente; la v0.9.5.1 destruye y recrea los botones cada vez que el número de slices cambia (`clearSliceButtons()`, #2254). Al desconectarse, la fila de pestañas se oculta y la **Insignia de slice** estática se restaura automáticamente.

Las conexiones de señal para los clics en los botones de slice también están protegidas para que la reconexión a la radio no añada manejadores duplicados.

## Formato del ancho de filtro (v0.9.8)

La indicación del ancho de filtro en el applet de Controles RX ahora usa lógica específica del modo para mostrar la etiqueta de ancho correcta. Esta indicación se comparte con el panel VFO para un formato consistente (#2197). El método estático `formatFilterWidth()` aplica reglas según el modo para que los modos SSB y digitales muestren la etiqueta de ancho de banda esperada (p. ej., "2.7K" para 2700 Hz USB, "500" para 500 Hz CW).

## Comportamiento de selección de antena

Los cuadros combinados de antena RX y TX ahora usan `rxAntennaList()` y `txAntennaOptions()` respectivamente para completar sus menús. El `ant_list` de la radio se usa como alternativa cuando las listas de antenas específicas del slice no están disponibles.

Los elementos del menú de antena ahora incluyen información sobre herramientas y consejos de estado que muestran el identificador de antena sin procesar, y la etiqueta del menú se genera con `antennaMenuLabel()` para una visualización consistente. La antena seleccionada se envía mediante `setData()` en lugar de `text()` para asegurar que se use el identificador correcto.

El ayudante `likelyTxAntennaFallbackToken()` determina si un token de antena es adecuado para TX verificando si comienza con "ANT", "TX" o es igual a "XVTR". Los puertos de solo RX (prefijo "RX") se excluyen.

## Solución de problemas

- **El Mode combo falta o está atenuado** — El applet no está conectado a la radio. Verifique la conexión a través de `Settings > Connect to Radio...`.
- **Los botones de preajuste de filtro desaparecieron después de cambiar de modo** — Esto es esperado al cambiar a FM, NFM o DFM. Esos modos no usan preajustes de filtro.
- **Las pestañas de slice muestran un número incorrecto de botones después de reconectar** — Este era un problema conocido solucionado en v0.9.5.1 (#2254). Actualice a la versión actual si ve botones de pestaña obsoletos.
- **El nivel de squelch se restablece inesperadamente** — El nivel de squelch manual ahora se conserva en el lado del cliente entre sesiones (#2606). Si el squelch parece restablecerse, verifique si el modo automático está sobrescribiendo el nivel de squelch del slice, ya que la radio podría no preservar el valor manual.

## Relacionados

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en la indicación)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Entender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
