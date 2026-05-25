# Cambiar modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para una slice. Cambiar el modo reajusta los preajustes de filtro y los pasos de sintonización para adaptarse a la nueva modulación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles RX requiere una conexión activa a la radio.
- Si tiene más de una slice, seleccione primero la slice correcta usando la fila de pestañas A..H en la parte superior del applet de Controles RX.

## Pasos

1. Si el applet de Controles RX no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de una slice activa, haga clic en la pestaña de slice adecuada (**A** a **H**) para vincular el applet a la slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. El modo actual se muestra (predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece solo en versiones con soporte de RADE habilitado.)
5. La slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los pasos de sintonización se actualizan automáticamente para adaptarse al nuevo modo.

## Función de cada control

| Control                        | Predeterminado   | Valores válidos                                                                                                                                                                                        |
|--------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Mode combo**                 | USB              | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible)                                                                                                                      |
| **Preajustes de ancho de filtro** | Dependiente del modo | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz                                                                   |
| **STEP**                       | 100 Hz (índice 2) | Lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)                                                                        |
| **Widget de banda pasante del filtro** | —                | Arrastre bordes lo/hi                                                                                                                                                                                   |
| **SQL**                        | Apagado          | Botón de conmutación para habilitar el squelch. Deshabilitado automáticamente en modos RTTY, DIGU, DIGL, NT, CW y CWL. En modos RTTY y digitales, el squelch también se apaga automáticamente para evitar el bloqueo de señales FSK (#2504). |
| **Nivel de squelch**           | 20               | Deslizador (0-100) para ajustar el umbral de squelch. Deshabilitado en modos RTTY, DIGU, DIGL, NT, CW y CWL.                                                                                            |
| **Antena RX**                  | ANT1             | Cuadro combinado que lista las antenas de recepción disponibles. Se completa desde `ant_list` de la radio o desde `rxAntennaList()` de la slice cuando esté disponible.                                   |
| **Antena TX**                  | ANT1             | Cuadro combinado que lista las antenas aptas para TX. Los puertos de solo RX (prefijo 'RX') se filtran. Usa `txAntennaOptions()` para la lista.                                                          |
| **🔊 / 🔇 (silencio)**        | 🔊 (sin silenciar) | Botón pulsador. Un solo clic silencia/reactiva el audio de esta slice. Doble clic silencia/reactiva el audio de todas las slices propias. El icono cambia cuando la radio confirma el cambio.          |
| **Ganancia AF**                | 70               | Deslizador (0-100) para la ganancia de salida de audio de la slice.                                                                                                                                    |
| **Paneo L / R**                | 50 (centro)      | Deslizador (0-100) para la posición estéreo. Doble clic restablece al centro.                                                                                                                           |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y offset de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Trabajar con un repetidor FM con tono CTCSS y offset +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado se vuelve relevante. Su estado se controla desde el applet de CW, no desde Controles RX.
- Los controles de modo AGC se ocultan cuando un modo de la familia FM está activo.
- Los preajustes de filtro ahora se almacenan en formato `lo:hi` (ej. `300:3000`) además del formato antiguo de ancho simple. Ambos formatos se leen correctamente. Si ha guardado preajustes personalizados de una versión anterior, siguen funcionando sin necesidad de realizar ninguna acción.
- El método `stepFilterWidth()` recorre la lista de preajustes por modo, por lo que los atajos de ensanchar/estrechar producen una geometría de bordes correcta para el modo. Esto asegura que cuando ensanche o estreche el filtro usando atajos de teclado, el filtro se mantenga dentro de los límites de preajuste apropiados para el modo actual.
- Al cambiar a modo RTTY o digital (DIGU, DIGL), el squelch se deshabilita y apaga automáticamente. Esto evita que el squelch elimine caracteres FSK y rompa la decodificación (#2504).
- El nivel de squelch manual se conserva entre sesiones. El último valor elegido por el usuario se almacena en la configuración `LastManualSquelchLevel` y se restaura al iniciar. Esto preserva la preferencia manual del operador a través de los ciclos de modo, ya que el modo automático podría sobrescribir el `squelchLevel` de la slice con valores sugeridos por el algoritmo (#2606).
- La insignia de slice ahora admite formato de texto enriquecido (HTML) para la letra de la slice (#2606).

## Comportamiento del botón de silencio (v26.5.3)

El botón de silencio (🔊 / 🔇) funciona como un botón pulsador, no como un botón de conmutación. El comportamiento sigue la **Política de configuración de autoridad de la radio (#2489)** — el estado de silencio NO se guarda ni restaura al reconectar; la radio es la fuente de verdad para el silencio de audio.

**Un solo clic:** Silencia o reactiva la slice actual. La acción se retrasa por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularla. El icono se actualiza solo cuando la radio confirma el cambio a través de `SliceModel::audioMuteChanged`.

**Doble clic:** Silencia o reactiva todas las slices propias. El manejador de doble clic se implementa en el método `eventFilter` y cancela el temporizador de un solo clic, evitando que la acción de un solo clic se ejecute.

Cuando ocurre una secuencia de doble clic, la segunda pulsación no emite una señal `clicked()` — eventFilter devuelve true en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. Esto asegura una discriminación limpia entre un solo clic y doble clic.

## Comportamiento de las pestañas de slice (v0.9.5.1)

Cuando la radio reporta un cambio en el número de slices disponibles, la fila de pestañas A..H ahora se reconstruye correctamente en lugar de omitirse. El comportamiento anterior mantenía los botones antiguos si ya existía alguno; v0.9.5.1 elimina y recrea los botones cada vez que el número de slices cambia (`clearSliceButtons()`, #2254). Al desconectarse, la fila de pestañas se oculta y la **insignia de slice** estática se restaura automáticamente.

Las conexiones de señal para los clics de los botones de slice también están protegidas para que la reconexión a la radio no adjunte manejadores duplicados.

## Formato del ancho de filtro (v0.9.8)

La lectura del ancho de filtro en el applet de Controles RX ahora usa lógica específica del modo para mostrar el ancho etiquetado correcto. Esta lectura se comparte con el panel VFO para un formato consistente (#2197). El método estático `formatFilterWidth()` aplica regbasadas en el modo para que los modos SSB y digitales muestren la etiqueta de ancho de banda esperada (ej., "2.7K" para 2700 Hz USB, "500" para 500 Hz CW).

## Comportamiento de selección de antena

Los cuadros combinados de antena RX y TX ahora usan `rxAntennaList()` y `txAntennaOptions()` respectivamente para completar sus menús. La `ant_list` de la radio se usa como respaldo cuando las listas de antenas específicas de la slice no están disponibles.

Los elementos del menú de antena ahora incluyen tooltips y status tips que muestran el identificador de antena sin procesar, y la etiqueta del menú se genera mediante `antennaMenuLabel()` para una visualización consistente. La antena seleccionada se envía a través de `setData()` en lugar de `text()` para asegurar que se use el identificador correcto.

El helper `likelyTxAntennaFallbackToken()` determina si un token de antena es adecuado para TX verificando si comienza con "ANT", "TX", o es igual a "XVTR". Los puertos de solo RX (prefijo "RX") se excluyen.

## Comportamiento de entrada de frecuencia (v26.5.3)

El editor de frecuencia ahora usa `FrequencyEntryParser::normalizedMhzText()` para limpiar el texto ingresado antes de convertirlo a un double. Esto asegura un manejo consistente de separadores de miles y punto decimal en todas las configuraciones regionales.

**Entrada con detección de XVTR:** El rango de frecuencia máximo ahora se determina por dos condiciones:
- Si la slice está en una antena XVTR (el nombre de la antena comienza con "XVT" o la frecuencia > 54.0 MHz)
- O si el usuario ingresa un valor explícito en MHz por encima de 54.0 MHz

Cuando se cumple cualquiera de las condiciones, el editor de frecuencia acepta hasta 50000.0 MHz. Esto permite la entrada directa de frecuencias VHF/UHF (ej., 144.6 MHz) incluso cuando no está actualmente en una antena XVTR.

La convención de banda de 3 dígitos (ej., "1446" → 144.6 MHz para 2m) se aplica solo a slices XVTR y se omite para entradas que ya parecen valores explícitos en MHz por encima de 54.0 MHz.

Cuando se confirma una frecuencia válida, el applet emite `directEntryCommitted(freqMhz, "rx-direct-entry")` en lugar de llamar directamente a `slice->tuneAndRecenter()`.

## Solución de problemas

- **El cuadro combinado de modo falta o está atenuado** — El applet no está conectado a la radio. Verifique la conexión a través de `Settings > Connect to Radio...`.
- **Los botones de preajuste de filtro desaparecieron después de cambiar de modo** — Esto es esperado al cambiar a FM, NFM o DFM. Esos modos no usan preajustes de filtro.
- **Las pestañas de slice muestran un número incorrecto de botones después de reconectar** — Este era un problema conocido solucionado en v0.9.5.1 (#2254). Actualice a la versión actual si ve botones de pestaña obsoletos.
- **El nivel de squelch se restablece inesperadamente** — El nivel de squelch manual ahora se conserva del lado del cliente entre sesiones (#2606). Si el squelch parece restablecerse, verifique si el modo automático está sobrescribiendo el nivel de squelch de la slice, ya que la radio podría no preservar el valor manual.
- **El botón de silencio no responde a un solo clic** — Esto puede ocurrir si el intervalo de doble clic de su plataforma es muy corto. La acción de un solo clic se retrasa por este intervalo; intente hacer clic con más deliberación. Verifique que la radio confirme el cambio de estado de silencio.
- **Entrada de frecuencia rechazada para frecuencias VHF/UHF** — Asegúrese de ingresar la frecuencia en MHz con un punto decimal (ej., "144.600"). Ingresar "144600" se interpretará como 144.600 MHz (división por 1000) porque supera los 54.0 MHz.

## Relacionados

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Trabajar con un repetidor FM con tono CTCSS y offset +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Entender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
