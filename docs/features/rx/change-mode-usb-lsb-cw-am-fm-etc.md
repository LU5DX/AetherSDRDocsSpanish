# Cambiar el modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo seleccionar un modo de recepción para una slice. Cambiar el modo ajusta los preajustes de filtro y los tamaños de paso de sintonización para adaptarse a la nueva modulación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles RX requiere una conexión de radio activa.
- Si tiene más de una slice, seleccione primero la slice correcta usando la fila de pestañas A..H en la parte superior del applet de Controles RX.

## Pasos

1. Si el applet de Controles RX no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha para mostrarlo.
2. Si su radio tiene más de una slice activa, haga clic en la pestaña de slice correspondiente (**A** a **H**) para vincular el applet a la slice que desea cambiar.
3. Haga clic en el menú desplegable **Mode combo**. Se muestra el modo actual (predeterminado: **USB**).
4. Seleccione el modo deseado de la lista:
   - **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL**, **RTTY**
   - (RADE aparece solo en versiones con soporte RADE habilitado).
5. La slice cambia al modo seleccionado. Los preajustes de ancho de filtro y los tamaños de paso de sintonización se actualizan automáticamente para adaptarse al nuevo modo.
6. Si desea usar el demodulador WFM por software, haga clic en el botón **WFM** (consulte los detalles a continuación).

## WFM (Demodulador FM por software)

El botón **WFM** proporciona un modo de demodulación FM de banda ancha basado en software. No es un modo de radio: utiliza el flujo DAX IQ de la slice y enruta el audio demodulado a través del cable Hi-Fi del sistema o un dispositivo de audio virtual similar.

**Cuando WFM está activo:**
- El botón **WFM** se ilumina en verde.
- El combo de modo muestra el último modo de radio seleccionado (p. ej., USB), pero el demodulador WFM anula la ruta de audio de la radio.
- El audio de la slice se demodula en software, lo que permite la recepción de FM de radiodifusión (88–108 MHz) y otras señales FM de banda ancha.

**Cuando cambia de modo:**
- Seleccionar cualquier modo de radio real (USB, LSB, CW, etc.) desactiva automáticamente el demodulador WFM.
- El estado del botón **WFM** se actualiza para reflejar que WFM ya no está activo en esta slice.

**Al salir de WFM:**
- Haga clic en el botón **WFM** nuevamente para desactivarlo. La slice vuelve al audio normal del modo de radio.

**Limitaciones:**
- WFM requiere un canal DAX IQ activo en la slice.
- El cable Hi-Fi o el dispositivo de audio virtual equivalente debe estar configurado como salida DAX.
- WFM no es un modo de radio: no afecta el modo de la radio ni la configuración del filtro.

## Qué hace cada control

| Control                    | Predeterminado  | Valores válidos                                                                                                                                                                                      |
|----------------------------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pestañas de slice (A..H)** | —               | 1–8 botones (limitado por el máximo de slices del hardware). Fila oculta si maxSlices ≤ 1.                                                                                                           |
| **Insignia de slice**      | A               | A/B/C/D/E/F/G/H, coloreada por identidad de slice.                                                                                                                                                   |
| **🔓 / 🔒**                  | 🔓 (desbloqueado) | Botón de alternancia. Activa/desactiva el bloqueo de sintonía en la slice; una slice bloqueada ignora los cambios de frecuencia.                                                                     |
| **Mode combo**             | USB             | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si está disponible).                                                                                                                   |
| **WFM**                    | Apagado         | Botón de alternancia. Habilita la demodulación FM por software a través de DAX IQ. Anula la ruta de audio de la radio.                                                                               |
| **Etiqueta de frecuencia** | 0.000.000       | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para editar.                                                                                                                    |
| **Edición de frecuencia**  | —               | Ingrese MHz (0.001–54.000 MHz, hasta 450.000 MHz en XVTR). Escape cancela y restaura la frecuencia anterior.                                                                                         |
| **STEP**                   | 100 Hz (índice 2) | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz; CW: 1, 5, 10, 50, 100, 200, 400 Hz; familia FM: 50–12500 Hz).                                                                 |
| **Preajustes de ancho de filtro** | Dependiente del modo | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400/500/600 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz. Oculto para FM/NFM/DFM.                                       |
| **Widget de banda pasante del filtro** | —             | Arrastre los bordes lo/hi para ajustar la banda pasante del filtro.                                                                                                                                  |
| **Modo de tono (FM)**      | Apagado         | Apagado, CTCSS TX. Visible solo en modos de la familia FM.                                                                                                                                           |
| **Valor de tono CTCSS**    | —               | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Habilitado solo cuando el modo de tono = CTCSS TX.                                                                                               |
| **Offset (FM)**            | 0.0 MHz         | Spinbox (0.0–100.0 MHz, paso 0.1). Establece la frecuencia de offset del repetidor FM.                                                                                                              |
| **− (offset hacia abajo)** | —               | Botón de alternancia. Establece la dirección del offset del repetidor hacia abajo (TX por debajo de RX).                                                                                             |
| **Símplex**                | Marcado         | Botón de alternancia. Establece el offset del repetidor en símplex (TX = RX).                                                                                                                        |
| **+ (offset hacia arriba)**| —               | Botón de alternancia. Establece la dirección del offset del repetidor hacia arriba (TX por encima de RX).                                                                                            |
| **REV**                    | —               | Botón de alternancia. Invierte el signo del offset de TX para pares de repetidores invertidos.                                                                                                       |
| **🔊 / 🔇 (silenciar)**      | 🔊 (sin silenciar) | Botón pulsador. Un clic silencia/activa el sonido de esta slice. Doble clic silencia/activa el sonido de todas las slices propias. El icono cambia cuando la radio lo confirma.                        |
| **Ganancia AF**            | 70              | Deslizador (0-100) para la ganancia de salida de audio de la slice.                                                                                                                                  |
| **Panorámica L / R**       | 50 (centro)     | Deslizador (0-100) para la posición de panorámica estéreo. Doble clic restablece al centro. El relleno del deslizador ahora se pinta desde el centro hacia afuera para una mejor retroalimentación visual (v26.6.1). |
| **SQL**                    | Apagado         | Botón de alternancia para habilitar el squelch. Se desactiva automáticamente en modos RTTY, DIGU, DIGL, NT, CW y CWL. En modos RTTY y digitales, el squelch también se desactiva automáticamente para evitar el bloqueo de señales FSK (#2504). |
| **Nivel de squelch**       | 20              | Deslizador (0-100) para establecer el umbral de squelch. Deshabilitado en modos RTTY, DIGU, DIGL, NT, CW y CWL.                                                                                      |
| **Modo AGC**               | Med             | Apagado, Lento, Med, Rápido. Oculto en modos de la familia FM.                                                                                                                                       |
| **Umbral AGC**             | 65              | Deslizador (0-100). Establece el umbral AGC (o el nivel de AGC apagado cuando el modo AGC está en Apagado). Haga clic derecho para calibrar contra el piso de ruido (consulte a continuación).         |
| **Antena RX**              | ANT1            | Cuadro combinado que lista las antenas de recepción disponibles. Se completa desde `ant_list` de la radio, `rxAntennaList()` de la slice cuando está disponible, y tokens de antena virtual del administrador de KiwiSDR. Etiqueta de color azul. |
| **Antena TX**              | ANT1            | Cuadro combinado que lista las antenas con capacidad TX. Los puertos de solo RX (prefijo 'RX') se filtran. Etiqueta de color rojo.                                                                    |
| **TX (insignia)**          | —               | Botón de alternancia. Haga clic para establecer esta slice como la slice de TX.                                                                                                                      |
| **RIT**                    | —               | Botón de alternancia. Activa/desactiva la Sintonía Incremental de Recepción.                                                                                                                         |
| **RIT 0**                  | —               | Botón pulsador. Pone a cero el offset de RIT.                                                                                                                                                        |
| **Offset RIT**             | +0 Hz           | Spinbox (paso 10 Hz). Ajusta el offset de RIT.                                                                                                                                                       |
| **XIT**                    | —               | Botón de alternancia. Activa/desactiva la Sintonía Incremental de Transmisión.                                                                                                                       |
| **XIT 0**                  | —               | Botón pulsador. Pone a cero el offset de XIT.                                                                                                                                                        |
| **Offset XIT**             | +0 Hz           | Spinbox (paso 10 Hz). Ajusta el offset de XIT.                                                                                                                                                       |
| **QSK**                    | —               | Indicador. Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado a través del applet CW.                                                                              |
| **Etiqueta de ancho de filtro** | 2.7K         | Indicador. Muestra el ancho de banda del filtro actual (p. ej., '2.7K', '3.3K', '500', '6.0K').                                                                                                      |

## Calibración de ruido AGC-T

El deslizador de umbral AGC ahora admite una función de calibración del piso de ruido. Esto le ayuda a establecer un umbral AGC óptimo basado en el piso de ruido actual.

**Para calibrar:**
1. Haga clic derecho en el deslizador **AGC threshold**.
2. Seleccione **Calibrate AGC-T against noise floor…** en el menú contextual.
3. El proceso de calibración muestrea el piso de ruido y ajusta el deslizador de umbral AGC a un nivel apropiado.

El menú contextual con clic derecho está disponible independientemente de la configuración del modo AGC. La información sobre herramientas del deslizador ahora incluye un recordatorio: "Right-click to calibrate against the noise floor".

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. El filtro es fijo para esos modos.
- Después de cambiar a FM o NFM, los controles de tono CTCSS y offset de repetidor (**Tone mode**, **Offset**, **−**, **Simplex**, **+**, **REV**) se vuelven visibles. Consulte [Work an FM repeater with CTCSS tone and +/- offset](work-an-fm-repeater-with-ctcss-tone-and-offset.md) para obtener más detalles.
- Después de cambiar a CW, el indicador **QSK** en el encabezado se vuelve relevante. Su estado se controla desde el applet CW, no desde Controles RX.
- Los controles del modo AGC están ocultos cuando un modo de la familia FM está activo.
- Los preajustes de filtro ahora se almacenan en formato `lo:hi` (p. ej., `300:3000`) además del formato anterior de ancho simple. Ambos formatos se leen correctamente. Si ha guardado preajustes personalizados de una versión anterior, siguen funcionando sin necesidad de ninguna acción de su parte.
- El método `stepFilterWidth()` recorre la lista de preajustes por modo, de modo que los atajos de teclado para ensanchar/estrechar producen una geometría de borde correcta para el modo. Esto asegura que cuando ensancha o estrecha el filtro usando atajos de teclado, el filtro permanece dentro de los límites de preajuste apropiados para el modo actual.
- Al cambiar a RTTY o modos digitales (DIGU, DIGL), el squelch se desactiva y apaga automáticamente. Esto evita que el squelch elimine los caracteres FSK e interrumpa la decodificación (#2504).
- El nivel de squelch manual se conserva entre sesiones. El último valor elegido por el usuario se almacena en la configuración `LastManualSquelchLevel` y se restaura al iniciar. Esto preserva la preferencia manual del operador a través de los ciclos de modo, ya que el modo automático podría sobrescribir el `squelchLevel` de la slice con valores sugeridos por el algoritmo (#2606).
- La insignia de slice ahora admite formato de texto enriquecido (HTML) para la letra de la slice (#2606).

## Comportamiento del botón de silencio (v26.5.3)

El botón de silencio (🔊 / 🔇) funciona como un botón pulsador, no como un botón de alternancia. El comportamiento sigue la **Política de Configuración Autoritativa de la Radio (#2489)**: el estado de silencio NO se guarda ni restaura al reconectar; la radio es la fuente de verdad para el silencio de audio.

**Un clic:** Silencia o activa el sonido de la slice actual. La acción se aplaza por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularla. El icono se actualiza solo cuando la radio confirma el cambio a través de `SliceModel::audioMuteChanged`.

**Doble clic:** Silencia o activa el sonido de todas las slices propias. El manejador de doble clic se implementa en el método `eventFilter` y cancela el temporizador de un clic, evitando que la acción de un clic se ejecute.

Cuando ocurre una secuencia de doble clic, la segunda pulsación no emite una señal `clicked()`: eventFilter devuelve true en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. Esto asegura una discriminación clara entre un clic y doble clic.

## Relleno del deslizador de panorámica L/R (v26.6.1)

El deslizador de panorámica L/R ahora usa un **relleno anclado al centro** en lugar del relleno predeterminado de Qt de izquierda a derecha. Esto significa que la parte coloreada de la ranura del deslizador se extiende desde la marca central hacia afuera hasta la posición del control, dando una indicación visual clara del sesgo panorámico. Esto es solo un cambio visual; el comportamiento del control no cambia.

El punto de la marca central (pequeño círculo azul-gris en el punto medio) permanece para mostrar la posición neutral de un vistazo. El doble clic restablece el deslizador al centro.

## Comportamiento de la pestaña de slice (v0.9.5.1)

Cuando la radio informa un cambio en el número de slices disponibles, el
