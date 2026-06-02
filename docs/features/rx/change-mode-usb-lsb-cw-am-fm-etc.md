# Cambio de modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para un slice. Cambiar el modo reajusta los preselecciones de filtro y los tamaños de paso de sintonización para adaptarse a la nueva modulación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet de RX Controls requiere una conexión activa al radio.
- Si tiene más de un slice, seleccione primero el slice correcto usando la fila de pestañas A..H en la parte superior del applet de RX Controls.

## Pasos

1. Si el applet de RX Controls no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de un slice activo, haga clic en la pestaña del slice correspondiente (**A** a **H**) para vincular el applet al slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. Se muestra el modo actual (valor predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece solo en versiones con soporte para RADE habilitado.)
5. El slice cambia al modo seleccionado. Las preselecciones de ancho de filtro y los tamaños de paso de sintonización se actualizan automáticamente para adaptarse al nuevo modo.

## Qué hace cada control

| Control                        | Valor predeterminado | Valores válidos                                                                                                                                                                                              |
|--------------------------------|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pestañas de slice (A..H)**   | —                    | 1–8 botones (limitado por el máximo de slices del hardware). Fila oculta si maxSlices ≤ 1.                                                                                                                   |
| **Insignia de slice**          | A                    | A/B/C/D/E/F/G/H, coloreada según la identidad del slice.                                                                                                                                                    |
| **🔓 / 🔒**                    | 🔓 (desbloqueado)    | Botón de alternancia. Activa/desactiva el bloqueo de sintonía en el slice; el slice bloqueado ignora los cambios de frecuencia.                                                                               |
| **Mode combo**                 | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible)                                                                                                                            |
| **Etiqueta de frecuencia**     | 0.000.000            | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para editar.                                                                                                                          |
| **Editor de frecuencia**       | —                    | Ingrese MHz (0.001–54.000 MHz, hasta 450.000 MHz en XVTR). Escape cancela y restaura la frecuencia anterior.                                                                                                 |
| **STEP**                       | 100 Hz (índice 2)    | Lista por modo (ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)                                                                            |
| **Preselecciones de ancho de filtro** | Dependiente del modo | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz. Oculto para FM/NFM/DFM.                                                |
| **Widget de banda pasante del filtro** | —                    | Arrastre los bordes de paso bajo/alto para ajustar la banda pasante del filtro.                                                                                                                            |
| **Modo de tono (FM)**          | Off                  | Off, CTCSS TX. Visible solo en modos de la familia FM.                                                                                                                                                      |
| **Valor de tono CTCSS**        | —                    | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Habilitado solo cuando el modo de tono es CTCSS TX.                                                                                                    |
| **Offset (FM)**                | 0.0 MHz              | Spinbox (0.0–100.0 MHz, paso 0.1). Establece la frecuencia de offset del repetidor de FM.                                                                                                                   |
| **− (offset abajo)**           | —                    | Botón de alternancia. Establece la dirección del offset del repetidor hacia abajo (TX por debajo de RX).                                                                                                   |
| **Simplex**                    | marcado              | Botón de alternancia. Establece el offset del repetidor a simplex (TX = RX).                                                                                                                               |
| **+ (offset arriba)**          | —                    | Botón de alternancia. Establece la dirección del offset del repetidor hacia arriba (TX por encima de RX).                                                                                                  |
| **REV**                        | —                    | Botón de alternancia. Invierte el signo del offset de TX para pares de repetidor invertidos.                                                                                                               |
| **🔊 / 🔇 (silencio)**         | 🔊 (sin silencio)    | Botón pulsador. Un solo clic silencia/activa el sonido de este slice. Doble clic silencia/activa el sonido de todos los slices propios. El icono cambia cuando el radio lo confirma.                       |
| **Ganancia AF**                | 70                   | Deslizador (0-100) para la ganancia de salida de audio del slice.                                                                                                                                            |
| **Panorámico L / R**           | 50 (centro)          | Deslizador (0-100) para la posición panorámica estéreo. Doble clic restablece al centro. El relleno del deslizador ahora se pinta desde el centro hacia afuera para una mejor retroalimentación visual (v26.6.1). |
| **SQL**                        | Off                  | Botón de alternancia para habilitar el squelch. Se desactiva automáticamente en modos RTTY, DIGU, DIGL, NT, CW y CWL. En modos RTTY y digitales, el squelch también se apaga automáticamente para evitar el bloqueo de señales FSK (#2504). |
| **Nivel de squelch**           | 20                   | Deslizador (0-100) para establecer el umbral de squelch. Deshabilitado en modos RTTY, DIGU, DIGL, NT, CW y CWL.                                                                                            |
| **Modo AGC**                   | Med                  | Off, Slow, Med, Fast. Oculto en modos de la familia FM.                                                                                                                                                     |
| **Umbral AGC**                 | 65                   | Deslizador (0-100). Establece el umbral AGC (o el nivel de apagado AGC cuando el modo AGC es Off).                                                                                                         |
| **Antena RX**                  | ANT1                 | Cuadro combinado que lista las antenas de recepción disponibles. Se completa desde `ant_list` del radio o desde `rxAntennaList()` del slice cuando esté disponible. Etiqueta de color azul.                |
| **Antena TX**                  | ANT1                 | Cuadro combinado que lista las antenas con capacidad de TX. Los puertos solo RX (prefijo 'RX') se filtran. Etiqueta de color rojo.                                                                         |
| **TX (insignia)**              | —                    | Botón de alternancia. Haga clic para establecer este slice como el slice de TX.                                                                                                                              |
| **RIT**                        | —                    | Botón de alternancia. Activa/desactiva la sintonización incremental de recepción.                                                                                                                         |
| **RIT 0**                      | —                    | Botón pulsador. Pone a cero el offset de RIT.                                                                                                                                                            |
| **Offset RIT**                 | +0 Hz                | Spinbox (paso 10 Hz). Ajusta el offset de RIT.                                                                                                                                                            |
| **XIT**                        | —                    | Botón de alternancia. Activa/desactiva la sintonización incremental de transmisión.                                                                                                                        |
| **XIT 0**                      | —                    | Botón pulsador. Pone a cero el offset de XIT.                                                                                                                                                            |
| **Offset XIT**                 | +0 Hz                | Spinbox (paso 10 Hz). Ajusta el offset de XIT.                                                                                                                                                            |
| **QSK**                        | —                    | Indicador. Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado a través del applet CW.                                                                                 |
| **Etiqueta de ancho de filtro**| 2.7K                 | Indicador. Muestra el ancho de banda actual del filtro (ej., '2.7K', '3.3K', '500', '6.0K').                                                                                                              |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preselección de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y offset de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Trabajar con un repetidor de FM con tono CTCSS y offset +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para obtener más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado se vuelve relevante. Su estado se controla desde el applet CW, no desde RX Controls.
- Los controles del modo AGC se ocultan cuando un modo de la familia FM está activo.
- Las preselecciones de filtro ahora se almacenan en un formato `lo:hi` (ej. `300:3000`) además del formato antiguo de ancho simple. Ambos formatos se leen correctamente. Si ha guardado preselecciones personalizadas de una versión anterior, siguen funcionando sin ninguna acción de su parte.
- El método `stepFilterWidth()` recorre la lista de preselecciones por modo para que los atajos de teclado para ensanchar/estrechar produzcan una geometría de borde correcta según el modo. Esto garantiza que cuando ensanche o estreche el filtro usando atajos de teclado, el filtro se mantenga dentro de los límites de preselección adecuados para el modo actual.
- Al cambiar a modos RTTY o digitales (DIGU, DIGL), el squelch se desactiva y apaga automáticamente. Esto evita que el squelch recorte los caracteres FSK y rompa la decodificación (#2504).
- El nivel de squelch manual se conserva entre sesiones. El último valor elegido por el usuario se almacena en la configuración `LastManualSquelchLevel` y se restaura al iniciar. Esto preserva la preferencia manual del operador a través de ciclos de modo, ya que el modo automático podría sobrescribir el `squelchLevel` del slice con valores sugeridos por algoritmos (#2606).
- La insignia de slice ahora admite formato de texto enriquecido (HTML) para la letra del slice (#2606).

## Comportamiento del botón de silencio (v26.5.3)

El botón de silencio (🔊 / 🔇) funciona como un botón pulsador, no como un botón de alternancia. El comportamiento sigue la **Política de Configuración de Autoridad del Radio (#2489)** — el estado de silencio NO se guarda ni restablece al reconectar; el radio es la fuente de verdad para el silencio de audio.

**Un solo clic:** Silencia o activa el sonido del slice actual. La acción se aplaza por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularla. El icono se actualiza solo cuando el radio confirma el cambio a través de `SliceModel::audioMuteChanged`.

**Doble clic:** Silencia o activa el sonido de todos los slices propios. El controlador de doble clic se implementa en el método `eventFilter` y cancela el temporizador de un solo clic, evitando que la acción de un solo clic se ejecute.

Cuando ocurre una secuencia de doble clic, la segunda pulsación no emite una señal `clicked()` — eventFilter devuelve true en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. Esto garantiza una discriminación limpia entre clic simple y doble clic.

## Relleno del deslizador panorámico L/R (v26.6.1)

El deslizador panorámico L/R ahora usa un **relleno anclado al centro** en lugar del relleno predeterminado de Qt de izquierda a derecha. Esto significa que la parte coloreada de la ranura del deslizador se extiende desde la marca central hacia afuera hasta la posición del mango, dando una indicación visual clara del sesgo panorámico. Este es solo un cambio visual; el comportamiento del control no cambia.

El punto de marca central (pequeño círculo azul-gris en el punto medio) permanece para mostrar la posición neutral de un vistazo. El doble clic restablece el deslizador al centro.

## Comportamiento de la pestaña de slice (v0.9.5.1)

Cuando el radio reporta un cambio en el número de slices disponibles, la fila de pestañas A..H ahora se reconstruye correctamente en lugar de omitirse. El comportamiento anterior mantenía los botones antiguos si ya estaban presentes; v0.9.5.1 derriba y recrea los botones cada vez que cambia el recuento de slices (`clearSliceButtons()`, #2254). Al desconectar, la fila de pestañas se oculta y la **Insignia de slice** estática se restaura automáticamente.

Las conexiones de señal para los clics de los botones de slice también están protegidas para que la reconexión al radio no adjunte controladores duplicados.

## Formato del ancho de filtro (v0.9.8)

La lectura del ancho de filtro en el applet de RX Controls ahora usa lógica específica del modo para mostrar el ancho etiquetado correcto. Esta lectura se comparte con el panel VFO para un formato consistente (#2197). El método estático `formatFilterWidth()` aplica reglas conscientes del modo para que los modos SSB y digitales muestren la etiqueta de ancho de banda esperada (ej., "2.7K" para 2700 Hz USB, "500" para 500 Hz CW).

## Comportamiento de selección de antena

Los cuadros combinados de antena RX y TX ahora usan `rxAntennaList()` y `txAntennaOptions()` respectivamente para llenar sus menús. El `ant_list` del radio se usa como respaldo cuando las listas de antenas específicas del slice no están disponibles.

Los elementos del menú de antena ahora incluyen tooltips y sugerencias de estado que muestran el identificador de antena sin procesar, y la etiqueta del menú se genera mediante `antennaMenuLabel()` para una visualización consistente. La antena seleccionada se envía a través de `setData()` en lugar de `text()` para garantizar que se use el identificador correcto.

El ayudante `likelyTxAntennaFallbackToken()` determina si un token de antena es adecuado para TX verificando si comienza con "ANT", "TX" o es igual a "XVTR". Los puertos solo RX (prefijo "RX") se excluyen.

## Comportamiento de ingreso de frecuencia (v26.5.3)

El editor de frecuencia ahora usa `FrequencyEntryParser::normalizedMhzText()` para limpiar el texto ingresado antes de la conversión a un doble. Esto garantiza un manejo consistente de los separadores de miles y puntos decimales en todas las configuraciones regionales.

**Ingreso con reconocimiento de XVTR:** El rango máximo de frecuencia ahora está determinado por dos condiciones:
- Si el slice está en una antena XVTR (el nombre de la antena comienza con "XVT" o la frecuencia > 54.0 MHz)
- O si el usuario ingresa un valor explícito en MHz por encima de 54.0 MHz

Cuando alguna de las condiciones es verdadera, el editor de frecuencia acepta hasta 50000.0 MHz. Esto permite el ingreso directo de frecuencias VHF/UHF (como las que se usan con adaptadores de downconversion).
