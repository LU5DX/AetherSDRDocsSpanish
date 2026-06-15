# Applet de Controles RX (v26.6.3)

El applet de Controles RX proporciona controles de recepción por slice, incluyendo selección de modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/panorámica de AF, silenciador, RIT/XIT, demodulador por software WFM y configuración de dúplex para repetidores de FM. Un solo clic en el botón de silencio silencia este slice; un doble clic silencia/activa el sonido de todos los slices propios. El formateador de ancho de filtro se comparte con el panel VFO para lecturas coherentes (#2197), y el método stepFilterWidth() recorre las listas predefinidas por modo para que los atajos de ampliar/reducir produzcan una geometría de bordes correcta según el modo. Al cambiar a modos RTTY o digitales (DIGU, DIGL), el silenciador se desactiva automáticamente, ya que de lo contrario recortaría los caracteres FSK y rompería la decodificación (#2504). Al salir del modo RADE mediante el selector de modo, el applet emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE. Seleccionar cualquier modo de radio real en el selector de modo elimina cualquier superposición activa del demodulador por software WFM en ese slice.

## Antes de comenzar

- Asegúrese de que el applet RX esté visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Los controles mostrados dependen del slice seleccionado actualmente y de su modo.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---------|----------------|----------------------|-------|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1 | clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic en los botones de slice están protegidas contra manejadores de señal duplicados entre reconexiones. |
| Insignia de slice | Muestra la letra del slice vinculado actualmente. Se muestra en todo momento; es el único indicador de slice visible cuando la fila de pestañas está oculta. Admite formato de texto enriquecido para la letra del slice (#2606). | A | Coloreada según la identidad del slice. |
| 🔓 / 🔒 | Activa/desactiva el bloqueo de sintonía en el slice; el slice bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) | El icono cambia entre un candado abierto y uno cerrado. |
| ANT1 (antena RX) | Abre un menú que lista las antenas disponibles; al seleccionar una, se establece slice->setRxAntenna. Se completa con la ant_list de la radio o la rxAntennaList del slice. Los elementos del menú se muestran con etiquetas de número de puerto opcionales para mayor claridad. | ANT1 | Etiqueta de color azul. Los elementos del menú muestran tanto el token de antena como una etiqueta legible (ej. "ANT1 - 1"). |
| ANT1 (antena TX) | Abre un menú que lista las antenas con capacidad de TX; establece slice->setTxAntenna. Los puertos de antena solo RX (prefijo 'RX') se filtran. Los elementos del menú se muestran con etiquetas de número de puerto opcionales para mayor claridad. | ANT1 | Etiqueta de color rojo. Los elementos del menú muestran tanto el token de antena como una etiqueta legible. El método txAntennaOptions() devuelve todos los puertos ANT*, TX* y XVTR, excluyendo los puertos solo RX. |
| 2.7K (ancho de filtro) | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un filtro predefinido. | 2.7K | La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| QSK | Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. | apagado (gris) | Solo lectura. |
| TX (insignia) | Haga clic para establecer este slice como el slice de TX (llama a slice->setTxSlice). | Ninguno | |
| Selector de modo | Establece el modo del slice; reconfigura los predefinidos de filtro y paso para el nuevo modo. Seleccionar cualquier modo de radio real elimina cualquier superposición activa del demodulador por software WFM en este slice. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). | USB | La opción RADE requiere la bandera de compilación HAVE_RADE. |
| WFM | Activa/desactiva el demodulador por software WFM para este slice. Usa audio DAX IQ enrutado a través de un Cable Hi-Fi. Al activarse, emite wfmActivated(true, sliceId); al desactivarse, emite wfmActivated(false, sliceId). | desactivado (sin marcar) | Un botón de alternancia separado junto al selector de modo. No aparece en el selector de modo; tiene su propio botón de 36x20 píxeles. Acento verde cuando está marcado. Información sobre herramientas: "Demodulador FM por software vía DAX IQ → Cable Hi-Fi". |
| Etiqueta de frecuencia | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. | 0.000.000 | |
| Edición de frecuencia | Ingrese MHz y presione Enter para sintonizar y centrar nuevamente; admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor (v0.9.0, #1954). Utiliza el widget FreqLineEdit con texto de sugerencia "MHz". Ingresar un valor superior a 54.0 MHz que incluya un punto decimal (ej. "144.0") ahora se trata como una entrada explícita en MHz y se permite para operación en VHF/UHF sin necesidad de una antena XVTR. | Ninguno | Consciente de XVTR: acepta hasta 50000 MHz cuando el slice está en una antena XVTR. Ingresar un valor superior a 54.0 MHz sin un punto decimal (ej. "144000") se divide por 1e3 para la conversión de kHz a MHz. |
| PASO | `<` / `>` o la rueda del ratón recorren los tamaños de paso según el modo; emite stepSizeChanged y stepSizeChangedByUser. La lista de pasos depende del modo del slice. | 100 Hz (índice 2) | La señal stepSizeChangedByUser se emite además de stepSizeChanged cuando el usuario cambia manualmente el tamaño de paso. |
| Predefinidos de ancho de filtro | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como predefinido. La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto. Las palabras clave Ampliar/Reducir (si se asignan a atajos de teclado) recorren la lista de predefinidos por modo para una geometría de bordes correcta según el modo. | Lista por modo | Los botones están ocultos para los modos FM/NFM/DFM; los predefinidos son por modo. El método stepFilterWidth(dirección) recorre la lista de predefinidos por modo para ampliar/reducir correctamente según el modo (#2208). Los botones de filtro predefinido ahora usan hojas de estilo tokenizadas conscientes del tema a través de ThemeManager, por lo que se re-thematizan junto con el resto de la interfaz. |
| Widget de banda pasante del filtro | Arrastre los bordes inferior/superior para ajustar la banda pasante del filtro; emite filterChanged (inf, sup). | Ninguno | |
| Modo de tono (FM) | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Desactivado | |
| Valor de tono CTCSS | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando Modo de tono = CTCSS TX. | Ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). |
| Offset (FM) | Establece la frecuencia de offset del repetidor FM en MHz. | 0.0 MHz | Rango 0.0-100.0 MHz (paso 0.1). |
| − (offset hacia abajo) | Establece la dirección del offset del repetidor como 'hacia abajo' (TX por debajo de RX). | Ninguno | |
| Símplex | Establece la dirección del offset del repetidor como símplex (TX = RX). | marcado | |
| + (offset hacia arriba) | Establece la dirección del offset del repetidor como 'hacia arriba' (TX por encima de RX). | Ninguno | |
| REV | Invierte el signo del offset de TX para trabajar con un par de repetidor invertido. | Ninguno | |
| 🔊 / 🔇 (silencio) | Un solo clic silencia/activa el sonido de este slice (diferido por el intervalo de doble clic de la plataforma). Un doble clic silencia/activa el sonido de todos los slices propios a través de la señal muteAllToggled. El icono cambia cuando la radio lo confirma a través de SliceModel::audioMuteChanged. | 🔊 (sonido activado) | Según la Política de Configuración de Autoridad de Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. El clic simple se difiere por clickDiscriminationIntervalMs() (intervalo de doble clic predeterminado de la plataforma, ~400 ms) para que un doble clic pueda anularlo. El botón ya no es marcable; la actualización del icono está impulsada por la confirmación de la radio, no por el evento de clic. |
| Ganancia AF | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. Muestra el valor actual como un porcentaje (ej. "70%"). | 70 (70%) | Rango 0-100. |
| Panorámica L / R | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Muestra la posición de panorámica actual: "C" para centro, "L{n}" para panorámica izquierda, "R{n}" para panorámica derecha. El doble clic restablece a 50 (C). El control deslizante utiliza una subclase CenterMarkSlider que dibuja el relleno desde el centro hacia afuera, de modo que solo se acentúa la región (centro → manija). Se dibuja un pequeño punto de marca central en la ranura como referencia visual para la posición neutra. | 50 (C) | Rango 0-100. El CenterMarkSlider sobrepinta la mitad izquierda del relleno de subpágina predeterminado con el color de la ranura, luego agrega un relleno de color de acento desde el centro hasta la manija. El disco de píxeles de la manija se recorta de la sobrepintura para evitar sangrado visual. |
| SQL | Activa el silenciador al nivel actual del control deslizante. Deshabilitado (y desactivado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el silenciador recortaría los caracteres FSK (#2504). | Ninguno | |
| Nivel de silenciador | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. El nivel de silenciador manual se persiste en el lado del cliente como la configuración `LastManualSquelchLevel` (valor predeterminado 20). | 20 | Rango 0-100. El último umbral de silenciador manual elegido por el usuario se guarda entre sesiones y se restaura al iniciar, porque el modo automático sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo. |
| Modo AGC | Establece el modo AGC del slice. Opciones: Desactivado, Lento, Medio, Rápido. Oculto en modos de la familia FM. | Medio | |
| Umbral AGC | Establece el umbral AGC (o el nivel de AGC desactivado cuando el modo AGC es Desactivado). La información sobre herramientas refleja qué valor se está ajustando e incluye una nota sobre la calibración con clic derecho. Haga clic derecho para abrir un menú contextual con una opción "Calibrar AGC-T contra el piso de ruido…", que emite calibrateAgcTRequested(sliceId). | 65 | Rango 0-100. Ejemplos de información sobre herramientas: "Umbral AGC: 65\nHaga clic derecho para calibrar contra el piso de ruido" o "Nivel AGC Desactivado: 65\nHaga clic derecho para calibrar contra el piso de ruido". |
| RIT | Activa/desactiva la Sintonización Incremental de Recepción. | Ninguno | |
| RIT 0 | Pone a cero el offset de RIT. | Ninguno | |
| Offset RIT | `<` / `>` o la rueda del ratón ajustan el offset de RIT en pasos de 10 Hz. | +0 Hz | |
| XIT | Activa/desactiva la Sintonización Incremental de Transmisión. | Ninguno | |
| XIT 0 | Pone a cero el offset de XIT. | Ninguno | |
| Offset XIT | `<` / `>` o la rueda del ratón ajustan el offset de XIT en pasos de 10 Hz. | +0 Hz | |

## Comportamiento dependiente del modo

### Demodulador por software WFM

Se muestra un botón de alternancia **WFM** junto al selector de modo en cada slice. Esto activa un demodulador FM por software que utiliza audio DAX IQ enrutado a través de un Cable Hi-Fi:

- Haga clic para activar/desactivar. Cuando está activo, el botón muestra un fondo verde.
- Información sobre herramientas: "Demodulador FM por software vía DAX IQ → Cable Hi-Fi".
- Seleccionar cualquier modo de radio real en el selector de modo elimina automáticamente cualquier superposición WFM activa en ese slice.
- Cuando la radio confirma un cambio de estado WFM para este slice (a través de setWfmActive()), el estado del botón se actualiza en consecuencia.
- El estado WFM es por slice y se rastrea por ID de slice.

### Silenciador en modos digitales y RTTY

El silenciador se deshabilita y se desactiva automáticamente en los siguientes modos para evitar recortar los caracteres FSK e interferir con decodificadores externos:
- **DIGU** (Digital Superior)
- **DIGL** (Digital Inferior)
- **RTTY** (Radio Téletipo)

Al cambiar a cualquiera de estos modos, el silenciador se desactiva automáticamente si estaba activado. El estado guardado del silenciador se conserva y se restaurará al volver a un modo donde el silenciador tenga sentido. El nivel de silenciador manual se persiste en el lado del cliente como la configuración `LastManualSquelchLevel` y se restaura al iniciar la aplicación, porque el modo automático sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo.

### Visibilidad de QSK

El indicador QSK solo es visible cuando el modo del slice está configurado en **CW** o **CWL**.

### Manejo del modo RADE

El modo RADE es solo del lado del cliente — la radio devuelve inmediatamente el modo real (DIGL/DIGU). Al salir del modo
