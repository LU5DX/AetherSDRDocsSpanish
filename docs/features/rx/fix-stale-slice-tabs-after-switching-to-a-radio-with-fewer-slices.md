# Applet de Controles de RX (v26.7.4)

El applet de Controles de RX proporciona controles de recepción por slice, que incluyen selección de modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/panorámica de AF, silenciador, RIT/XIT y configuración de dúplex para repetidores de FM. Un solo clic en el botón de silencio silencia este slice; un doble clic silencia/reactiva el audio de todos los slices propios. El formateador de ancho de filtro se comparte con el panel VFO para lecturas consistentes (#2197), y el método stepFilterWidth() recorre listas predefinidas por modo, de modo que los atajos de expandir/estrechar produzcan una geometría de bordes correcta según el modo. Al cambiar a modos RTTY o digitales (DIGU, DIGL), el silenciador se desactiva automáticamente; de lo contrario, recortaría los caracteres FSK e interrumpiría la decodificación (#2504). Al salir del modo RADE mediante el combo de modo, el applet emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar modos en un slice que no está en RADE.

## Antes de comenzar

- Asegúrese de que el applet de RX esté visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Los controles mostrados dependen del slice seleccionado actualmente y de su modo.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---------|----------------|----------------------|-------|
| Pestañas de slice (A..H) | Selecciona el slice al que está vinculado el applet de RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1 | clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic en los botones de slice están protegidas contra duplicados de manejadores de señal entre reconexiones. |
| Insignia de slice | Muestra la letra del slice vinculado actualmente. | A | Coloreada según la identidad del slice. |
| 🔓 / 🔒 | Alterna el bloqueo de sintonización en el slice; un slice bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) | El ícono cambia entre un candado abierto y uno cerrado. |
| ANT1 (antena RX) | Abre un menú que lista las antenas disponibles y antenas virtuales de KiwiSDR; al seleccionar una, se configura la antena RX del slice o se activa un perfil de KiwiSDR. El menú se completa con la ant_list de la radio, la rxAntennaList del slice y cualquier token de antena virtual de KiwiSDR. Las entradas de perfil de KiwiSDR se resaltan en el menú cuando están activas. | ANT1 | Etiqueta de color azul. Los elementos del menú muestran tanto el token de la antena como una etiqueta legible (ej. "ANT1 - 1"). Las antenas virtuales de KiwiSDR se agregan al menú si hay un administrador de KiwiSDR disponible. Cuando se selecciona un perfil de KiwiSDR, el applet emite `kiwiRxAntennaSelected(sliceId, profileId)`. Cuando se selecciona una antena Flex, emite `flexRxAntennaSelected(sliceId)`. |
| ANT1 (antena TX) | Abre un menú que lista las antenas capaces de transmitir; establece slice->setTxAntenna. Los puertos de antena solo RX (prefijo 'RX') se filtran. Los elementos del menú se muestran con etiquetas de número de puerto opcionales para mayor claridad. | ANT1 | Etiqueta de color rojo. Los elementos del menú muestran tanto el token de la antena como una etiqueta legible. El método txAntennaOptions() devuelve todos los puertos ANT*, TX* y XVTR, excluyendo los puertos solo RX. |
| 2.7K (ancho de filtro) | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un preajuste de filtro. | 2.7K | La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| QSK | Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. | apagado (gris) | Solo lectura. |
| TX (insignia) | Haga clic para establecer este slice como el slice de TX (llama a slice->setTxSlice). | Ninguno | |
| Combo de modo | Establece el modo del slice; reconfigura los preajustes de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). | USB | La opción RADE requiere la bandera de compilación HAVE_RADE. |
| Etiqueta de frecuencia | Muestra la frecuencia actual del VFO con agrupación de puntos. Haga clic para pasar al modo de edición. | 0.000.000 | |
| Edición de frecuencia | Ingrese MHz y presione Enter para sintonizar y recentrar; admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor (v0.9.0, #1954). Utiliza el widget FreqLineEdit con texto de sugerencia "MHz". Ingresar un valor superior a 54.0 MHz que incluya un punto decimal (ej. "144.0") ahora se trata como una entrada explícita en MHz y se permite para operación VHF/UHF sin requerir una antena XVTR. | Ninguno | Compatible con XVTR: acepta hasta 50000 MHz cuando el slice está en una antena XVTR. Ingresar un valor superior a 54.0 MHz sin punto decimal (ej. "144000") se divide por 1e3 para la conversión de kHz a MHz. |
| STEP | Los botones `<` / `>` o la rueda del ratón recorren los tamaños de paso por modo; emite stepSizeChanged y stepSizeChangedByUser. La lista de pasos depende del modo del slice. | 100 Hz (índice 2) | La señal stepSizeChangedByUser se emite además de stepSizeChanged cuando el usuario cambia manualmente el tamaño del paso. |
| Preajustes de ancho de filtro | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como preajuste. La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto. Las palabras clave Widen/Narrow (si están asignadas a atajos de teclado) recorren la lista de preajustes por modo para una geometría de bordes correcta según el modo. | Lista por modo | Botones ocultos para modos FM/NFM/DFM; los preajustes son por modo. Los preajustes de CW ahora incluyen opciones de 500 y 600 Hz para un conformado más fino (#2208). El método stepFilterWidth(direction) recorre la lista de preajustes por modo para expandir/estrechar correctos según el modo (#2208). Los botones de preajuste de filtro ahora usan hojas de estilo tokenizadas compatibles con el tema a través de ThemeManager, por lo que se re-thematizan junto con el resto de la interfaz. |
| Widget de banda de paso de filtro | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). | Ninguno | |
| Modo de tono (FM) | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Off | |
| Valor de tono CTCSS | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono = CTCSS TX. | Ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). |
| Offset (FM) | Establece la frecuencia de offset del repetidor de FM en MHz. | 0.0 MHz | Rango 0.0-100.0 MHz (paso 0.1). |
| − (offset hacia abajo) | Establece la dirección del offset del repetidor como 'hacia abajo' (TX por debajo de RX). | Ninguno | |
| Simplex | Establece la dirección del offset del repetidor como simplex (TX = RX). | marcado | |
| + (offset hacia arriba) | Establece la dirección del offset del repetidor como 'hacia arriba' (TX por encima de RX). | Ninguno | |
| REV | Invierte el signo del offset de TX para trabajar con un par de repetidor inverso. | Ninguno | |
| 🔊 / 🔇 (silencio) | Un solo clic silencia/reactiva el audio de este slice (diferido por el intervalo de discriminación de clic de la plataforma, configurable en Radio Setup → Slice Controls). Un doble clic silencia/reactiva el audio de todos los slices propios a través de la señal muteAllToggled. El ícono cambia cuando la radio lo confirma mediante SliceModel::audioMuteChanged. | 🔊 (audio activo) | Según la Política de Ajustes con Autoridad de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. El clic único se difiere por clickDiscriminationIntervalMs() (configurable en Radio Setup → Slice Controls, intervalo de doble clic predeterminado de la plataforma ~400 ms, #3009) para que un doble clic pueda anularlo. El manejador de doble clic está en eventFilter y cancela el temporizador de clic único. |
| Ganancia AF | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. Muestra el valor actual como un porcentaje (ej. "70%"). | 70 (70%) | Rango 0-100. |
| Panorámica L / R | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Muestra la posición de panorámica actual: "C" para centro, "L{n}" para panorámica izquierda, "R{n}" para panorámica derecha. El doble clic restablece a 50 (C). El deslizador utiliza una subclase CenterMarkSlider que dibuja el relleno desde el centro hacia afuera, de modo que solo se acentúa la región (centro → manija). Se pinta un pequeño punto de marca central en la ranura como referencia visual para la posición neutral. | 50 (C) | Rango 0-100. El CentreMarkSlider sobrepinta la mitad izquierda del relleno de subpágina predeterminado con el color de la ranura, luego agrega un relleno de color de acento desde el centro hasta la manija. El disco de píxeles de la manija se recorta del sobrepintado para evitar sangrado visual. |
| SQL | Activa el silenciador en el nivel actual del deslizador. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el silenciador recortaría los caracteres FSK (#2504). | Ninguno | |
| Nivel de silenciador | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. El nivel de silenciador manual se persiste en el lado del cliente como el ajuste `LastManualSquelchLevel` (predeterminado 20). | 20 | Rango 0-100. El último umbral de silenciador manual elegido por el usuario se guarda entre sesiones y se restaura al iniciar, porque el modo automático sobrescribe squelchLevel del slice con valores sugeridos por el algoritmo. |
| Modo AGC | Establece el modo AGC del slice. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. | Med | |
| Umbral AGC | Establece el umbral AGC (o el nivel de apagado de AGC cuando el modo AGC está en Off). La información sobre herramientas refleja qué valor se está ajustando e incluye una nota sobre la calibración con clic derecho. Haga clic derecho para abrir un menú contextual con una opción "Calibrar AGC-T contra el piso de ruido…", que emite calibrateAgcTRequested(sliceId). | 65 | Rango 0-100. Ejemplos de información sobre herramientas: "Umbral AGC: 65\nHaga clic derecho para calibrar contra el piso de ruido" o "Nivel de apagado AGC: 65\nHaga clic derecho para calibrar contra el piso de ruido". |
| RIT | Activa/desactiva la Sintonización Incremental de Recepción. | Ninguno | |
| RIT 0 | Pone a cero el offset de RIT. | Ninguno | |
| Offset RIT | Los botones `<` / `>` o la rueda del ratón ajustan el offset de RIT en pasos de 10 Hz. | +0 Hz | |
| XIT | Activa/desactiva la Sintonización Incremental de Transmisión. | Ninguno | |
| XIT 0 | Pone a cero el offset de XIT. | Ninguno | |
| Offset XIT | Los botones `<` / `>` o la rueda del ratón ajustan el offset de XIT en pasos de 10 Hz. | +0 Hz | |

## Comportamiento dependiente del modo

### Silenciador en modos digitales y RTTY

El silenciador se deshabilita y se apaga automáticamente en los siguientes modos para evitar recortar los caracteres FSK e interferir con decodificadores externos:
- **DIGU** (Digital Upper)
- **DIGL** (Digital Lower)
- **RTTY** (Radio Teletype)

Al cambiar a cualquiera de estos modos, el silenciador se apaga automáticamente si estaba encendido. El estado guardado del silenciador se conserva y se restaurará al volver a un modo donde el silenciador tenga sentido. El nivel de silenciador manual se persiste en el lado del cliente como el ajuste `LastManualSquelchLevel` y se restaura al iniciar la aplicación, porque el modo automático sobrescribe squelchLevel del slice con valores sugeridos por el algoritmo.

### Visibilidad de QSK

El indicador QSK solo es visible cuando el modo del slice está configurado en **CW** o **CWL**.

### Manejo del modo RADE

El modo RADE es solo del lado del cliente — la radio devuelve inmediatamente el modo real (DIGL/DIGU). Al salir del modo RADE mediante el combo de modo, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar modos en un slice que no está en RADE. Al entrar en el modo RADE, el applet emite `radeActivated(true, sliceId)` y no llama a `setMode()` de la radio, ya que RADE es solo del lado del cliente.

### Antenas virtuales de KiwiSDR

Si hay un administrador de KiwiSDR disponible, el menú de antena RX incluye tokens de antena virtual de servidores KiwiSDR conectados. Seleccionar una antena virtual de KiwiSDR activa el perfil de KiwiSDR correspondiente para el slice actual a través de la señal `kiwiRxAntennaSelected`. El perfil de KiwiSDR activo para un slice se muestra como marcado en el menú junto con las selecciones regulares de antena Flex.

## Etiquetas de lectura de deslizadores

Los deslizadores de Ganancia AF y Panorámica muestran sus valores actuales como etiquetas formateadas:
- **Ganancia AF**: Valor porcentual (ej. "70%") que se muestra junto al deslizador.
- **Panorámica**: Indicador de posición que muestra "C" para centro, "L
