# Applet de Controles de RX (v26.6.1)

El applet de Controles de RX proporciona controles de recepción por slice, incluyendo selección de modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/pan de AF, squelch, RIT/XIT y configuración de duplex para repetidores FM. Un solo clic en el botón de silencio silencia este slice; un doble clic silencia/reactiva todos los slices propios. El formateador de ancho de filtro se comparte con el panel VFO para lecturas consistentes (#2197), y el método stepFilterWidth() recorre las listas de preajustes por modo, de modo que los atajos de teclado de ampliar/reducir produzcan una geometría de bordes correcta según el modo. Al cambiar a modos RTTY o digitales (DIGU, DIGL), el squelch se desactiva automáticamente ya que, de lo contrario, eliminaría los caracteres FSK e interrumpiría la decodificación (#2504). Al salir del modo RADE mediante el combo de modos, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE.

## Antes de comenzar

- Asegúrese de que el applet RX esté visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Los controles mostrados dependen del slice actualmente seleccionado y de su modo.

## Función de cada control

| Control | Comportamiento | Predeterminado | Notas |
|---------|----------------|----------------|-------|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1 | clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados en reconexiones. |
| Insignia de slice | Muestra la letra del slice vinculado actualmente. Se muestra en todo momento; es el único indicador de slice visible cuando la fila de pestañas está oculta. Admite formato de texto enriquecido para la letra del slice (#2606). | A | Coloreada por identidad del slice. |
| 🔓 / 🔒 | Alterna el bloqueo de sintonía en el slice; un slice bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) | El icono cambia entre un candado abierto y uno cerrado. |
| ANT1 (antena RX) | Abre un menú con las antenas disponibles; al seleccionar, se ejecuta slice->setRxAntenna. Se completa desde la ant_list de la radio o desde rxAntennaList del slice. Los elementos del menú se muestran con etiquetas de número de puerto opcionales para mayor claridad. | ANT1 | Etiqueta de color azul. Los elementos del menú muestran tanto el token de la antena como una etiqueta legible (ej. "ANT1 - 1"). |
| ANT1 (antena TX) | Abre un menú con las antenas capacitadas para TX; establece slice->setTxAntenna. Los puertos de antena solo RX (prefijo 'RX') se filtran. Los elementos del menú se muestran con etiquetas de número de puerto opcionales para mayor claridad. | ANT1 | Etiqueta de color rojo. Los elementos del menú muestran tanto el token de la antena como una etiqueta legible. El método txAntennaOptions() devuelve todos los puertos ANT*, TX* y XVTR, excluyendo los puertos solo RX. |
| 2.7K (ancho de filtro) | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un preajuste de filtro. | 2.7K | La lectura de ancho utiliza lógica consciente del modo, por lo que los modos SSB/digitales muestran el ancho etiquetado correcto (#2197). |
| QSK | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; se controla mediante el botón Breakin del applet CW. | apagado (gris) | Solo lectura. |
| TX (insignia) | Haga clic para establecer este slice como el slice de TX (llama a slice->setTxSlice). | Ninguno | |
| Combo de modo | Establece el modo del slice; reconfigura los preajustes de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). | USB | La opción RADE requiere la bandera de compilación HAVE_RADE. |
| Etiqueta de frecuencia | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. | 0.000.000 | |
| Edición de frecuencia | Ingrese MHz y presione Enter para sintonizar y re-centrar; admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor (v0.9.0, #1954). Ingresar un valor superior a 54.0 MHz que incluya un punto decimal (ej. "144.0") ahora se trata como una entrada explícita en MHz y se permite para operación VHF/UHF sin necesidad de una antena XVTR. | Ninguno | Consciente de XVTR: acepta hasta 50000 MHz cuando el slice está en una antena XVTR. Ingresar un valor superior a 54.0 MHz sin punto decimal (ej. "144000") se divide por 1e3 para la conversión de kHz a MHz. |
| STEP | `<` / `>` o la rueda del ratón recorren los tamaños de paso por modo; emite stepSizeChanged. La lista de pasos depende del modo del slice. | 100 Hz (índice 2) | |
| Preajustes de ancho de filtro | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como un preajuste. La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto. Las palabras clave Widen/Narrow (si están asignadas a atajos de teclado) recorren la lista de preajustes por modo para una geometría de bordes correcta según el modo. | Lista por modo | Los botones están ocultos para los modos FM/NFM/DFM; los preajustes son por modo. El método stepFilterWidth(direction) recorre la lista de preajustes por modo para ampliar/reducir correctamente según el modo (#2208). Los botones de preajuste de filtro ahora usan hojas de estilo tokenizadas conscientes del tema a través de ThemeManager, por lo que se re-tematizan junto con el resto de la interfaz. |
| Widget de banda de paso del filtro | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). | Ninguno | |
| Modo de tono (FM) | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Off | |
| Valor de tono CTCSS | Selecciona la frecuencia del tono CTCSS enviada en transmisión. Habilitado solo cuando el modo de tono = CTCSS TX. | Ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). |
| Offset (FM) | Establece la frecuencia de offset del repetidor FM en MHz. | 0.0 MHz | Rango 0.0-100.0 MHz (paso 0.1). |
| − (offset hacia abajo) | Establece la dirección del offset del repetidor a 'down' (TX por debajo de RX). | Ninguno | |
| Simplex | Establece la dirección del offset del repetidor a simplex (TX = RX). | marcado | |
| + (offset hacia arriba) | Establece la dirección del offset del repetidor a 'up' (TX por encima de RX). | Ninguno | |
| REV | Invierte el signo del offset de TX para trabajar con un par de repetidores invertido. | Ninguno | |
| 🔊 / 🔇 (silencio) | Un solo clic silencia/reactiva el sonido de este slice (diferido por el intervalo de doble clic de la plataforma). Un doble clic silencia/reactiva el sonido de todos los slices propios mediante la señal muteAllToggled. El icono cambia cuando la radio lo confirma a través de SliceModel::audioMuteChanged. | 🔊 (con sonido) | Según la Política de Ajustes Autoritativos de la Radio (#2489), el estado de silencio NO se guarda/restaura en la reconexión; la radio es la fuente de verdad para el silencio de audio. El clic único se difiere por clickDiscriminationIntervalMs() (intervalo de doble clic predeterminado de la plataforma, ~400 ms) para que un doble clic pueda anularlo. El botón ya no es seleccionable; la actualización del icono es impulsada por el reconocimiento de la radio, no por el evento de clic. |
| Ganancia AF | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. Muestra el valor actual como un porcentaje (ej. "70%"). | 70 (70%) | Rango 0-100. |
| L / R pan | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Muestra la posición actual de pan: "C" para el centro, "L{n}" para pan izquierdo, "R{n}" para pan derecho. El doble clic restablece a 50 (C). El deslizador usa una subclase CenterMarkSlider que dibuja el relleno desde el centro hacia afuera, de modo que solo se acentúa la región (centro → manija). Se pinta un pequeño punto de marca central en la ranura como punto de referencia visual para la posición neutral. | 50 (C) | Rango 0-100. El CenterMarkSlider sobrepinta la mitad izquierda del relleno de subpágina predeterminado con el color de la ranura, luego agrega un relleno de color de acento desde el centro hasta la manija. El disco de píxeles de la manija se recorta de la sobrepintura para evitar sangrado visual. |
| SQL | Activa el squelch en el nivel actual del deslizador. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch eliminaría los caracteres FSK (#2504). | Ninguno | |
| Nivel de squelch | Ajusta el umbral del squelch; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. El nivel de squelch manual se conserva del lado del cliente como la configuración `LastManualSquelchLevel` (predeterminado 20). | 20 | Rango 0-100. El último umbral de squelch manual elegido por el usuario se guarda entre sesiones y se restaura al iniciar, porque el modo automático sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo. |
| Modo AGC | Establece el modo AGC del slice. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. | Med | |
| Umbral AGC | Establece el umbral AGC (o el nivel de apagado AGC cuando el modo AGC es Off). La información sobre herramientas refleja qué valor se está ajustando. | 65 | Rango 0-100. |
| RIT | Activa/desactiva la Sintonización Incremental de Recepción. | Ninguno | |
| RIT 0 | Pone a cero el offset de RIT. | Ninguno | |
| Offset RIT | `<` / `>` o la rueda del ratón ajustan el offset RIT en pasos de 10 Hz. | +0 Hz | |
| XIT | Activa/desactiva la Sintonización Incremental de Transmisión. | Ninguno | |
| XIT 0 | Pone a cero el offset de XIT. | Ninguno | |
| Offset XIT | `<` / `>` o la rueda del ratón ajustan el offset XIT en pasos de 10 Hz. | +0 Hz | |

## Comportamiento dependiente del modo

### Squelch en modos digitales y RTTY

El squelch se deshabilita y se apaga automáticamente en los siguientes modos para evitar eliminar caracteres FSK e interferir con decodificadores externos:
- **DIGU** (Digital Upper)
- **DIGL** (Digital Lower)
- **RTTY** (Radio Teletype)

Al cambiar a cualquiera de estos modos, el squelch se apaga automáticamente si estaba activado. El estado guardado del squelch se conserva y se restaurará al volver a un modo donde el squelch tenga sentido. El nivel de squelch manual se conserva del lado del cliente como la configuración `LastManualSquelchLevel` y se restaura al iniciar la aplicación, porque el modo automático sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo.

### Visibilidad de QSK

El indicador QSK solo es visible cuando el modo del slice está configurado en **CW** o **CWL**.

### Manejo del modo RADE

El modo RADE es solo del lado del cliente: la radio devuelve inmediatamente el modo real (DIGL/DIGU). Al salir del modo RADE mediante el combo de modos, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE. Al entrar en el modo RADE, el applet emite `radeActivated(true, sliceId)` y no llama a `setMode()` de la radio, ya que RADE es solo del lado del cliente.

## Etiquetas de lectura de los deslizadores

Los deslizadores de ganancia AF y pan ahora muestran sus valores actuales como etiquetas de texto junto a los controles deslizantes (v26.5.3):

- **Ganancia AF** — Muestra el valor actual como un porcentaje (ej. "70%" para un valor de 70).
- **L / R pan** — Muestra la posición actual de pan:
  - "C" cuando el deslizador está en el centro (valor 50).
  - "L{n}" cuando se desplaza a la izquierda, donde {n} es la diferencia desde el centro (ej. "L20" para valor 30).
  - "R{n}" cuando se desplaza a la derecha, donde {n} es la diferencia desde el centro (ej. "R30" para valor 80).

## Relleno anclado al centro del deslizador L/R pan

El deslizador L/R pan (v26.6.1) utiliza una clase `CenterMarkSlider` que pinta el relleno del deslizador desde el centro hacia afuera, a diferencia de los deslizadores horizontales estándar que pintan desde el borde izquierdo. Esto proporciona una retroalimentación visual intuitiva:

- Cuando la manija está a la izquierda del centro, el relleno de color de acento aparece entre la manija y el centro.
- Cuando la manija está a la derecha del centro, el relleno de color de acento aparece entre el centro y la manija.
- Se pinta un pequeño punto de marca central (de color #608090) en la ranura como punto de referencia visual para la posición neutral.
- El disco de píxeles de la manija se recorta de la sobrepintura para evitar sangrado visual en el área de la manija.

## Mejoras en la entrada de frecuencia

El campo de edición de frecuencia incluye varias mejoras para la operación VHF/UHF (v26.5.3):

- Ingresar un valor superior a 54.0 MHz que incluya un punto decimal (ej. "144.0" o "432.100") ahora se trata como una entrada explícita en MHz y se permite sin necesidad de una antena XVTR. Esto permite la sintonización directa a frecuencias VHF/UHF
