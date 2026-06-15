# Cambiar modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para un slice. Cambiar el modo ajusta los preajustes de filtro y los pasos de sintonización para adaptarse a la nueva modulación.

## Antes de empezar

- AetherSDR debe estar conectado al radio. El applet de Controles de RX requiere una conexión activa al radio.
- Si tiene más de un slice, seleccione primero el slice correcto usando la fila de pestañas A..H en la parte superior del applet de Controles de RX.

## Pasos

1. Si el applet de Controles de RX no está visible, haga clic en el botón de bandeja **RX** de la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de un slice activo, haga clic en la pestaña de slice correspondiente (**A** a **H**) para vincular el applet al slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. Se muestra el modo actual (por defecto: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece solo en compilaciones con soporte RADE habilitado.)
5. El slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los pasos de sintonización se actualizan automáticamente para adaptarse al nuevo modo.
6. Si desea usar el demodulador de software WFM, haga clic en el botón **WFM** (consulte más abajo para más detalles).

## WFM (Demodulador de FM por software)

El botón **WFM** proporciona un modo de demodulación de FM de banda ancha basado en software. Este no es un modo de radio: usa el flujo DAX IQ del slice y dirige el audio demodulado a través del cable Hi-Fi del sistema o un dispositivo de audio virtual similar.

**Cuando WFM está activo:**
- El botón **WFM** se ilumina en verde.
- El selector de modo muestra el último modo de radio seleccionado (p. ej., USB), pero el demodulador WFM anula la ruta de audio del radio.
- El audio del slice se demodula en software, lo que permite la recepción de FM de radiodifusión (88–108 MHz) y otras señales FM de banda ancha.

**Cuando cambia de modo:**
- Seleccionar cualquier modo de radio real (USB, LSB, CW, etc.) desactiva automáticamente el demodulador WFM.
- El estado del botón **WFM** se actualiza para reflejar que WFM ya no está activo en este slice.

**Al salir de WFM:**
- Haga clic en el botón **WFM** nuevamente para desactivarlo. El slice vuelve al audio normal del modo de radio.

**Limitaciones:**
- WFM requiere un canal DAX IQ activo en el slice.
- El cable Hi-Fi o el dispositivo de audio virtual equivalente debe estar configurado como la salida DAX.
- WFM no es un modo de radio – no afecta el modo del radio ni la configuración del filtro.

## Qué hace cada control

| Control                      | Valor predeterminado | Valores válidos                                                                                                                                                                                              |
|------------------------------|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pestañas de slice (A..H)** | —                    | 1–8 botones (limitado por el máximo de slices del hardware). La fila se oculta si maxSlices ≤ 1.                                                                                                             |
| **Insignia de slice**        | A                    | A/B/C/D/E/F/G/H, coloreado por la identidad del slice.                                                                                                                                                       |
| **🔓 / 🔒**                  | 🔓 (desbloqueado)    | Botón de alternancia. Activa/desactiva el bloqueo de sintonía en el slice; un slice bloqueado ignora los cambios de frecuencia.                                                                               |
| **Selector de modo (combo)** | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible)                                                                                                                            |
| **WFM**                      | Desactivado          | Botón de alternancia. Activa la demodulación de FM por software a través de DAX IQ. Anula la ruta de audio del radio.                                                                                        |
| **Etiqueta de frecuencia**   | 0.000.000            | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para editar.                                                                                                                            |
| **Editor de frecuencia**     | —                    | Introduzca MHz (0.001–54.000 MHz, hasta 450.000 MHz en XVTR). Escape cancela y restaura la frecuencia anterior.                                                                                             |
| **STEP**                     | 100 Hz (índice 2)    | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz)                                                                          |
| **Preajustes de ancho de filtro** | Depende del modo    | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz. Oculto para FM/NFM/DFM.                                                   |
| **Widget de banda pasante del filtro** | —                    | Arrastre los bordes inferior/superior para ajustar la banda pasante del filtro.                                                                                                                              |
| **Modo de tono (FM)**        | Desactivado          | Desactivado, CTCSS TX. Visible solo en modos de la familia FM.                                                                                                                                               |
| **Valor de tono CTCSS**      | —                    | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Habilitado solo cuando el modo de tono = CTCSS TX.                                                                                                       |
| **Desplazamiento (FM)**      | 0.0 MHz              | Cuadro giratorio (0.0–100.0 MHz, paso 0.1). Establece la frecuencia de desplazamiento del repetidor de FM.                                                                                                   |
| **− (desplazamiento hacia abajo)** | —               | Botón de alternancia. Establece la dirección de desplazamiento del repetidor hacia abajo (TX por debajo de RX).                                                                                                |
| **Simplex**                  | Marcado              | Botón de alternancia. Establece el desplazamiento del repetidor en simplex (TX = RX).                                                                                                                         |
| **+ (desplazamiento hacia arriba)** | —              | Botón de alternancia. Establece la dirección de desplazamiento del repetidor hacia arriba (TX por encima de RX).                                                                                               |
| **REV**                      | —                    | Botón de alternancia. Invierte el signo del desplazamiento de TX para pares de repetidores invertidos.                                                                                                       |
| **🔊 / 🔇 (silencio)**        | 🔊 (sin silenciar)   | Botón pulsador. Un clic silencia/restablece el sonido de este slice. Doble clic silencia/restablece el sonido de todos los slices propios. El icono cambia cuando el radio lo confirma.                        |
| **Ganancia de AF**           | 70                   | Control deslizante (0-100) para la ganancia de salida de audio del slice.                                                                                                                                    |
| **Panorámico L / R**         | 50 (centro)          | Control deslizante (0-100) para la posición estéreo panorámica. Doble clic restablece al centro. El relleno del control deslizante ahora se pinta desde el centro hacia afuera para una mejor retroalimentación visual (v26.6.1). |
| **SQL**                      | Desactivado          | Botón de alternancia para activar el squelch. Se desactiva automáticamente en modos RTTY, DIGU, DIGL, NT, CW y CWL. En modos RTTY y digitales, el squelch también se desactiva automáticamente para evitar el bloqueo de señales FSK (#2504). |
| **Nivel de squelch**         | 20                   | Control deslizante (0-100) para establecer el umbral de squelch. Deshabilitado en modos RTTY, DIGU, DIGL, NT, CW y CWL.                                                                                       |
| **Modo AGC**                 | Medio                | Desactivado, Lento, Medio, Rápido. Oculto en modos de la familia FM.                                                                                                                                         |
| **Umbral de AGC**            | 65                   | Control deslizante (0-100). Establece el umbral de AGC (o el nivel de desconexión de AGC cuando el modo AGC está en Desactivado). Haga clic derecho para calibrar contra el piso de ruido (consulte más abajo). |
| **Antena de RX**             | ANT1                 | Cuadro combinado que enumera las antenas de recepción disponibles. Se completa desde `ant_list` del radio o desde `rxAntennaList()` del slice cuando está disponible. Etiqueta de color azul.                 |
| **Antena de TX**             | ANT1                 | Cuadro combinado que enumera las antenas con capacidad de TX. Los puertos de antena solo de RX (prefijo 'RX') se filtran. Etiqueta de color rojo.                                                              |
| **TX (insignia)**            | —                    | Botón de alternancia. Haga clic para establecer este slice como el slice de TX.                                                                                                                              |
| **RIT**                      | —                    | Botón de alternancia. Activa/desactiva la sintonía incremental de recepción.                                                                                                                                 |
| **RIT 0**                    | —                    | Botón pulsador. Pone a cero el desplazamiento de RIT.                                                                                                                                                        |
| **Desplazamiento de RIT**    | +0 Hz                | Cuadro giratorio (paso 10 Hz). Ajusta el desplazamiento de RIT.                                                                                                                                              |
| **XIT**                      | —                    | Botón de alternancia. Activa/desactiva la sintonía incremental de transmisión.                                                                                                                               |
| **XIT 0**                    | —                    | Botón pulsador. Pone a cero el desplazamiento de XIT.                                                                                                                                                        |
| **Desplazamiento de XIT**    | +0 Hz                | Cuadro giratorio (paso 10 Hz). Ajusta el desplazamiento de XIT.                                                                                                                                              |
| **QSK**                      | —                    | Indicador. Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado a través del applet de CW.                                                                                |
| **Etiqueta de ancho de filtro** | 2.7K              | Indicador. Muestra el ancho de banda actual del filtro (p. ej., '2.7K', '3.3K', '500', '6.0K').                                                                                                              |

## Calibración de ruido AGC-T

El control deslizante de umbral de AGC ahora admite una función de calibración del piso de ruido. Esto le ayuda a establecer un umbral de AGC óptimo basado en el piso de ruido actual.

**Para calibrar:**
1. Haga clic derecho en el control deslizante **AGC threshold**.
2. Seleccione **Calibrate AGC-T against noise floor…** en el menú contextual.
3. El proceso de calibración muestrea el piso de ruido y ajusta el control deslizante de umbral de AGC a un nivel apropiado.

El menú contextual de clic derecho está disponible independientemente de la configuración del modo AGC. La información sobre herramientas del control deslizante ahora incluye un recordatorio: "Right-click to calibrate against the noise floor".

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y desplazamiento de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Work an FM repeater with CTCSS tone and +/- offset](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado es relevante. Su estado se controla desde el applet de CW, no desde Controles de RX.
- Los controles del modo AGC están ocultos cuando un modo de la familia FM está activo.
- Los preajustes de filtro ahora se almacenan en un formato `lo:hi` (p. ej., `300:3000`) además del formato de ancho simple anterior. Ambos formatos se leen correctamente. Si ha guardado preajustes personalizados de una versión anterior, continúan funcionando sin necesidad de ninguna acción de su parte.
- El método `stepFilterWidth()` recorre la lista de preajustes por modo, por lo que los atajos de teclado para ensanchar/estrechar producen una geometría de borde correcta para el modo. Esto garantiza que cuando ensanche o estreche el filtro usando atajos de teclado, el filtro se mantenga dentro de los límites de preajuste apropiados para el modo actual.
- Al cambiar a RTTY o modos digitales (DIGU, DIGL), el squelch se desactiva y apaga automáticamente. Esto evita que el squelch elimine los caracteres FSK e interrumpa la decodificación (#2504).
- El nivel de squelch manual se conserva entre sesiones. El último valor elegido por el usuario se almacena en la configuración `LastManualSquelchLevel` y se restaura al iniciar. Esto preserva la preferencia manual del operador a través de los ciclos de modo, ya que el modo automático podría sobrescribir el `squelchLevel` del slice con valores sugeridos por el algoritmo (#2606).
- La insignia de slice ahora admite formato de texto enriquecido (HTML) para la letra del slice (#2606).

## Comportamiento del botón de silencio (v26.5.3)

El botón de silencio (🔊 / 🔇) funciona como un botón pulsador, no como un botón de alternancia. El comportamiento sigue la **Política de Configuración Autoritativa del Radio (#2489)** — el estado de silencio NO se guarda ni se restaura al reconectar; el radio es la fuente de verdad para el silencio de audio.

**Un clic:** Silencia o restablece el sonido del slice actual. La acción se difiere por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularlo. El icono se actualiza solo cuando el radio confirma el cambio a través de `SliceModel::audioMuteChanged`.

**Doble clic:** Silencia o restablece el sonido de todos los slices propios. El controlador de doble clic se implementa en el método `eventFilter` y cancela el temporizador de un solo clic, evitando que la acción de un solo clic se ejecute.

Cuando ocurre una secuencia de doble clic, la segunda pulsación no emite una señal `clicked()` — eventFilter devuelve verdadero en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. Esto garantiza una discriminación limpia entre un solo clic y un doble clic.

## Relleno del control deslizante L/R Pan (v26.6.1)

El control deslizante de panorámico L/R ahora usa un **relleno anclado al centro** en lugar del relleno predeterminado de Qt de izquierda a derecha. Esto significa que la parte coloreada de la ranura del control deslizante se extiende desde la marca central hacia afuera hasta la posición del control deslizante, lo que proporciona una indicación visual clara del sesgo panorámico. Este es solo un cambio visual; el comportamiento del control no ha cambiado.

El punto de marca central (círculo azul grisáceo pequeño en el punto medio) permanece para mostrar la posición neutral de un vistazo. El doble clic restablece el control deslizante al centro.

## Comportamiento de la pestaña de slice (v0.9.5.1)

Cuando el radio inform
