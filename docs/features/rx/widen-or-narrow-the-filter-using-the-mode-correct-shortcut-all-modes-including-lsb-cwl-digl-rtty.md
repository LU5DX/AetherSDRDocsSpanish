# Applet de controles RX

El applet de controles RX proporciona controles de recepción por slice. Aparece al hacer clic en el botón de la bandeja **RX** en la barra lateral derecha.

## Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---------|------|---------|----------|
| **Pestañas de slice (A..H)** | pestaña | — | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. La fila se oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia estática de slice al desconectar (v0.9.5.1, #2254). Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados a través de reconexiones. |
| **Insignia de slice** | indicador | A | Muestra la letra del slice actualmente vinculado. Coloreada según la identidad del slice. |
| **🔓 / 🔒** | botón de alternancia | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía en el slice; un slice bloqueado ignora los cambios de frecuencia. El icono alterna entre candado abierto y cerrado. |
| **ANT1 (antena RX)** | cuadro combinado | ANT1 | Abre un menú que lista las antenas disponibles; al seleccionar se establece slice->setRxAntenna. Se rellena desde ant_list de la radio y los tokens de antena virtual KiwiSDR. Etiqueta de color azul. Cuando se asigna un perfil KiwiSDR al slice seleccionado, el token de antena virtual correspondiente aparece marcado en el menú. Seleccionar una antena virtual KiwiSDR emite kiwiRxAntennaSelected(sliceId, profileId); seleccionar una antena de radio emite flexRxAntennaSelected(sliceId) y luego establece la antena del slice. Vuelve a ANT1/ANT2 cuando la lista está vacía. |
| **ANT1 (antena TX)** | cuadro combinado | ANT1 | Abre un menú que lista las antenas con capacidad TX; los puertos solo RX (prefijo 'RX') se filtran. Al seleccionar se establece slice->setTxAntenna. Etiqueta de color rojo. |
| **2.7K (ancho de filtro)** | indicador | 2.7K | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un preajuste de filtro. |
| **QSK** | indicador | apagado (gris) | Se enciende en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; se controla mediante el botón Breakin del applet CW. |
| **TX (insignia)** | botón de alternancia | — | Haga clic para establecer este slice como slice TX (llama a slice->setTxSlice). |
| **Cuadro combinado de modo** | cuadro combinado | USB | Establece el modo del slice; remodela los preajustes de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE; WFM mediante el botón de bandera VFO). La opción RADE requiere la bandera de compilación HAVE_RADE. Los modos DSTR y FreeDV se filtran cuando el modelo no los admite. Seleccionar un modo de radio real elimina una superposición activa de demodulación de software WFM (WFM se alterna desde el botón WFM de bandera VFO, no desde este cuadro combinado). |
| **WFM** | botón pulsador | apagado | Botón de alternancia para el demodulador de FM por software mediante DAX IQ → Hi-Fi Cable. Cuando está habilitado, el botón brilla en verde; cuando está deshabilitado, se vuelve gris. Emite la señal wfmActivated con el ID del slice. |
| **Etiqueta de frecuencia** | indicador | 0.000.000 | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para cambiar al modo de edición. Se publican eventos de cambio de valor de accesibilidad en la etiqueta cuando cambia el texto de frecuencia, lo que permite que la tecnología de asistencia anuncie las actualizaciones. |
| **Edición de frecuencia** | campo de texto | — | Ingrese MHz y presione Enter para sintonizar y recentrar; admite autoescalado de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor (v0.9.0, #1954). Usa FreqLineEdit con texto de sugerencia "MHz". Compatible con XVTR: acepta hasta 50,000 MHz cuando el slice está en una antena XVTR. Conveniencia de banda de 3 dígitos: en 2m/70cm (100-999 MHz) una inserción de dígito formatea 1446 como 144.6. |
| **STEP** | cuadro de giro | 100 Hz (índice 2) | < / > o la rueda del ratón recorren los tamaños de paso según el modo; emite stepSizeChanged y stepSizeChangedByUser. La lista de pasos depende del modo del slice. |
| **Preajustes de ancho de filtro** | botón pulsador | — | Haga clic para aplicar un ancho de filtro preajustado; haga clic derecho para guardar el ancho actual como preajuste. Los botones se ocultan en modos FM/NFM/DFM. La lectura de ancho (compartida con VfoWidget mediante RxApplet::formatFilterWidth) usa lógica según el modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de preajustes según el modo para ensanchar/estrechar correctamente (#2208). |
| **Widget de banda pasante de filtro** | manija de arrastre | — | Arrastre los bordes lo/hi para ajustar la banda pasante del filtro; emite filterChanged (lo, hi). |
| **Modo de tono (FM)** | cuadro combinado | Off | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. |
| **Valor de tono CTCSS** | cuadro combinado | — | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Incluye los 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz) más frecuencias intermedias adicionales (69.3, 159.8, 165.5, 171.3, 177.3, 183.5, 189.9, 196.6, 199.5 Hz) para compatibilidad con repetidores heredados. Se habilita solo cuando el modo de tono = CTCSS TX. |
| **Offset (FM)** | cuadro de giro | 0.0 Mhz | Establece la frecuencia de offset del repetidor FM en MHz. Rango 0.0-100.0 MHz (paso 0.1). |
| **− (offset hacia abajo)** | botón de alternancia | — | Establece la dirección del offset del repetidor a 'hacia abajo' (TX por debajo de RX). |
| **Simplex** | botón de alternancia | marcado | Establece la dirección del offset del repetidor a simplex (TX = RX). |
| **+ (offset hacia arriba)** | botón de alternancia | — | Establece la dirección del offset del repetidor a 'hacia arriba' (TX por encima de RX). |
| **REV / XFC** | botón pulsador | — | Para operación de repetidor FM, REV invierte el signo del offset TX para trabajar un par de repetidor invertido. En backend que admiten una verificación de frecuencia de transmisión, el botón se reetiqueta como XFC: presionarlo mantiene la verificación de frecuencia de transmisión durante la duración de la pulsación, y mientras se mantiene, fuerza brevemente la radio hacia la frecuencia de transmisión para confirmar la cobertura. El botón alterna REV (marcable) normalmente, o se convierte en un botón momentáneo XFC hacia abajo cuando el backend de radio conectado anuncia hasTransmitFrequencyCheck. El XFC mantenido se libera al ocultar, desactivar, cambio de capacidad o desconexión. |
| **🔊 / 🔇 (silencio)** | botón pulsador | 🔊 (sin silencio) | Un clic silencia/activa el sonido de este slice (diferido por el intervalo de discriminación de clic de la plataforma, configurable en Radio Setup → Slice Controls). Doble clic silencia/activa el sonido de todos los slices propios mediante la señal muteAllToggled. El icono cambia cuando la radio lo confirma mediante SliceModel::audioMuteChanged. Según la Política de ajustes autoritativos de la radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. El clic único se difiere por clickDiscriminationIntervalMs() (configurable en Radio Setup → Slice Controls, intervalo de doble clic predeterminado de la plataforma ~400 ms, #3009) para que un doble clic pueda anularlo. El manejador de doble clic está en eventFilter y cancela el temporizador de clic único. |
| **Ganancia AF** | deslizador | 70 | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. Rango 0-100. |
| **Pan L / R** | deslizador | 50 | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). El relleno del deslizador se ancla desde el centro hacia afuera — la posición neutra muestra un punto de marca central en la ranura. |
| **SQL / AUTO** | botón de alternancia | Off | Botón de ciclo de tres posiciones: cada clic avanza Off → SQL (umbral manual) → AUTO (el algoritmo rastrea el piso de ruido) → Off. En modo AUTO el botón muestra 'AUTO' en ámbar; en modo manual 'SQL' en verde. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504). Manual y AUTO activan el squelch de la radio. El algoritmo de squelch automático reside en el panadapter; el nivel es el margen en dB por encima del piso de ruido medido. Se refleja en un botón idéntico en la pestaña Audio del panel VFO. |
| **Nivel de squelch** | deslizador | 20 | En modo Manual ajusta el umbral de squelch (surte efecto solo cuando el squelch está activado). En modo AUTO establece el margen en dB por encima del piso de ruido medido donde se abre la puerta, persistido en AutoSqlMarginDb. Manual: 0-100 (o 0-99 en recepción de reemplazo Kiwi); Auto: margen de 5-20 dB. En modo Manual el nivel es autoritativo de radio por slice (no se persiste); en modo Auto el margen se persiste. Deshabilitado en modos RTTY y digitales y en modo Off. Haga clic derecho en el deslizador de umbral AGC para calibrar el ruido AGC-T. |
| **Modo AGC** | cuadro combinado | Med | Establece el modo AGC del slice. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. |
| **Umbral AGC** | deslizador | 65 | Establece el umbral AGC (o nivel de apagado AGC cuando el modo AGC es Off). La información sobre herramientas refleja qué valor se está ajustando e incluye una pista sobre la calibración con clic derecho. El clic derecho abre un comando 'Calibrate AGC-T against noise floor…' que inicia el diálogo de calibración de ruido AGC-T (deshabilitado mientras está activa una recepción de reemplazo Kiwi). |
| **RIT** | botón de alternancia | — | Activa/desactiva el sintonizado incremental de recepción. |
| **RIT 0** | botón pulsador | — | Pone a cero el offset RIT. |
| **Offset RIT** | cuadro de giro | +0 Hz | < / > o la rueda del ratón ajustan el offset RIT en pasos de 10 Hz. |
| **XIT** | botón de alternancia | — | Activa/desactiva el sintonizado incremental de transmisión. |
| **XIT 0** | botón pulsador | — | Pone a cero el offset XIT. |
| **Offset XIT** | cuadro de giro | +0 Hz | < / > o la rueda del ratón ajustan el offset XIT en pasos de 10 Hz. |

## Comportamiento del squelch en modos digitales y RTTY

El squelch se deshabilita automáticamente en los siguientes modos:

- **RTTY**
- **DIGU, DIGL**

Al cambiar a cualquiera de estos modos, el squelch se apaga y el botón y deslizador SQL se deshabilitan. Esto evita que el squelch limite las señales FSK débiles y rompa la decodificación, particularmente en modos RTTY y digitales donde el squelch recortaría los caracteres FSK (#2504).

## Demodulador de software WFM

El botón **WFM** proporciona un demodulador de FM por software para recibir señales FM de banda ancha (radiodifusión). Esto usa transmisión DAX IQ a un dispositivo Hi-Fi Cable.

- Haga clic en el botón **WFM** para habilitar o deshabilitar el demodulador WFM para el slice actual.
- Cuando está habilitado, el botón brilla en verde. Cuando está deshabilitado, aparece gris.
- Seleccionar cualquier otro modo desde el **cuadro combinado de modo** deshabilita automáticamente el demodulador WFM para ese slice.
- El estado del botón se sincroniza en las reconexiones — si WFM estaba activo en un slice antes de desconectar, se volverá a activar cuando se restaure el slice.

## Calibrar AGC-T contra el piso de ruido

El deslizador **Umbral AGC** admite un menú contextual con clic derecho para la calibración del piso de ruido.

1. Haga clic derecho en el deslizador **Umbral AGC**.
2. Seleccione **Calibrate AGC-T against noise floor…** en el menú contextual.
3. Aparece un panel de calibración — siga las instrucciones en pantalla para medir el piso de ruido actual y ajustar el umbral AGC-T automáticamente.

La información sobre herramientas del deslizador **Umbral AGC** indica qué valor se está ajustando (umbral AGC o nivel de apagado AGC) y anuncia la función de calibración con clic derecho.

## Comportamiento del modo RADE (si está habilitado)

Cuando el modo RADE (detección de radar) está disponible (requiere la bandera de compilación HAVE_RADE), seleccionar RADE desde el cuadro combinado de modo activa el subsistema de detección de radar para el slice actual. Al cambiar fuera del modo RADE mediante el cuadro combinado de modo, el applet emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice sin RADE. El modo RADE es solo del lado del cliente — la radio devuelve el modo real (DIGL/DIGU) inmediatamente después de establecer RADE, por lo que el modo() del slice nunca será "RADE" después de que la radio responda.

## Comportamiento del botón de silencio

El botón **🔊 / 🔇 (silencio)** usa un botón pulsador (no marcable) con discriminación de clic:

- **Clic único**: alterna el silencio solo para este slice. La acción se difiere por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularla.
- **Doble clic**: alterna el silencio
