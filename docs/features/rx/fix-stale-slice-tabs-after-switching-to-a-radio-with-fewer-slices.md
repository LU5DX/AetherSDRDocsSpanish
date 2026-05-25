# Applet de Controles de RX (v26.5.3)

El applet de Controles de RX proporciona controles de recepción por slice, incluidos selección de modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/panorámica de AF, silenciador, RIT/XIT y configuración de dúplex para repetidores de FM. Un solo clic en el botón de silencio silencia este slice; un doble clic silencia/activa el sonido de todos los slices propios. El formato del ancho de filtro se comparte con el panel VFO para lecturas consistentes (#2197), y el método stepFilterWidth() recorre las listas predefinidas por modo para que los atajos de ensanchar/estrechar produzcan una geometría de borde correcta según el modo. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el silenciador se desactiva automáticamente; de lo contrario, recortaría los caracteres FSK e interrumpiría la decodificación (#2504). Al salir del modo RADE mediante el combo de modos, el applet emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE.

## Antes de comenzar

- Asegúrese de que el applet RX esté visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Los controles mostrados dependen del slice seleccionado actualmente y de su modo.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Notas |
|---------|---------------|----------------|-------|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1 | clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic del botón de slice están protegidas contra manejadores de señal duplicados en reconexiones. |
| Insignia de slice | Muestra la letra del slice vinculado actualmente. Se muestra siempre; es el único indicador de slice visible cuando la fila de pestañas está oculta. Admite formato de texto enriquecido para la letra del slice (#2606). | A | Coloreada según la identidad del slice. |
| 🔓 / 🔒 | Alterna el bloqueo de sintonía en el slice; el slice bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) | El icono cambia entre un candado abierto y uno cerrado. |
| ANT1 (antena RX) | Abre un menú con las antenas disponibles; al seleccionar, establece slice->setRxAntenna. Se completa desde ant_list de la radio o desde rxAntennaList del slice. Los elementos del menú se muestran con etiquetas opcionales de número de puerto para mayor claridad. | ANT1 | Etiqueta de color azul. Los elementos del menú muestran tanto el token de antena como una etiqueta legible (ej. "ANT1 - 1"). |
| ANT1 (antena TX) | Abre un menú con antenas compatibles con TX; establece slice->setTxAntenna. Los puertos de antena solo RX (prefijo 'RX') se filtran. Los elementos del menú se muestran con etiquetas opcionales de número de puerto para mayor claridad. | ANT1 | Etiqueta de color rojo. Los elementos del menú muestran tanto el token de antena como una etiqueta legible. El método txAntennaOptions() devuelve todos los puertos ANT*, TX* y XVTR, excluyendo los puertos solo RX. |
| 2.7K (ancho de filtro) | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un filtro predefinido. | 2.7K | La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| QSK | Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. | apagado (gris) | Solo lectura. |
| TX (insignia) | Haga clic para establecer este slice como el slice TX (llama a slice->setTxSlice). | Ninguno | |
| Combo de modo | Establece el modo del slice; reconfigura el filtro y los pasos predefinidos para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). | USB | La opción RADE requiere el indicador de compilación HAVE_RADE. |
| Etiqueta de frecuencia | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. | 0.000.000 | |
| Editor de frecuencia | Ingrese MHz y presione Enter para sintonizar y recentrar; admite autoescalado de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor (v0.9.0, #1954). Ingresar un valor superior a 54.0 MHz que incluya un punto decimal (ej. "144.0") ahora se trata como una entrada explícita en MHz y se permite para operación en VHF/UHF sin requerir una antena XVTR. | Ninguno | Consciente de XVTR: acepta hasta 50000 MHz cuando el slice está en una antena XVTR. Ingresar un valor superior a 54.0 MHz sin punto decimal (ej. "144000") se divide por 1e3 para conversión de kHz a MHz. |
| PASO | `<` / `>` o la rueda del ratón recorren los tamaños de paso según el modo; emite stepSizeChanged. La lista de pasos depende del modo del slice. | 100 Hz (índice 2) | |
| Predefinidos de ancho de filtro | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como predefinido. La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto. Las palabras clave Ensanchar/Estrechar (si están asignadas a atajos de teclado) recorren la lista de predefinidos del modo para una geometría de borde correcta según el modo. | Lista por modo | Botones ocultos para modos FM/NFM/DFM; los predefinidos son por modo. El método stepFilterWidth(direction) recorre la lista de predefinidos del modo para ensanchar/estrechar correctos según el modo (#2208). |
| Widget de banda pasante de filtro | Arrastre los bordes inferior/superior para ajustar la banda pasante del filtro; emite filterChanged (lo, hi). | Ninguno | |
| Modo de tono (FM) | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Off | |
| Valor de tono CTCSS | Selecciona la frecuencia de tono CTCSS enviada en transmisión. Habilitado solo cuando Modo de tono = CTCSS TX. | Ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). |
| Offset (FM) | Establece la frecuencia de offset del repetidor FM en MHz. | 0.0 MHz | Rango 0.0-100.0 MHz (paso 0.1). |
| − (offset hacia abajo) | Establece la dirección del offset del repetidor como 'abajo' (TX por debajo de RX). | Ninguno | |
| Símplex | Establece la dirección del offset del repetidor como símplex (TX = RX). | marcado | |
| + (offset hacia arriba) | Establece la dirección del offset del repetidor como 'arriba' (TX por encima de RX). | Ninguno | |
| REV | Invierte el signo del offset de TX para trabajar con un par de repetidor invertido. | Ninguno | |
| 🔊 / 🔇 (silencio) | Un solo clic silencia/activa el sonido de este slice (diferido por el intervalo de doble clic de la plataforma). Un doble clic silencia/activa el sonido de todos los slices propios mediante la señal muteAllToggled. El icono cambia cuando la radio lo confirma a través de SliceModel::audioMuteChanged. | 🔊 (sonido activado) | Según la Política de Configuración Controlada por la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. El clic simple se difiere por clickDiscriminationIntervalMs() (intervalo de doble clic predeterminado de la plataforma, ~400 ms) para que un doble clic pueda anularlo. El botón ya no es seleccionable; la actualización del icono está impulsada por el reconocimiento de la radio, no por el evento de clic. |
| Ganancia AF | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. Muestra el valor actual como un porcentaje (ej. "70%"). | 70 (70%) | Rango 0-100. |
| Panorámica L / R | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Muestra la posición de panorámica actual: "C" para centro, "L{n}" para panorámica izquierda, "R{n}" para panorámica derecha. Un doble clic restablece a 50 (C). | 50 (C) | Rango 0-100. |
| SQL | Activa el silenciador en el nivel deslizante actual. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el silenciador recortaría los caracteres FSK (#2504). | Ninguno | |
| Nivel de silenciador | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. El nivel de silenciador manual se persiste del lado del cliente como la configuración `LastManualSquelchLevel` (predeterminado 20). | 20 | Rango 0-100. El último umbral de silenciador manual elegido por el usuario se guarda entre sesiones y se restaura al iniciar, porque el modo automático sobrescribe squelchLevel del slice con valores sugeridos por el algoritmo. |
| Modo AGC | Establece el modo AGC del slice. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. | Med | |
| Umbral AGC | Establece el umbral AGC (o el nivel de AGC apagado cuando el modo AGC es Off). La información sobre herramientas refleja qué valor se está ajustando. | 65 | Rango 0-100. |
| RIT | Activa/desactiva la Sintonización Incremental de Recepción. | Ninguno | |
| RIT 0 | Pone a cero el offset de RIT. | Ninguno | |
| Offset de RIT | `<` / `>` o la rueda del ratón ajustan el offset de RIT en pasos de 10 Hz. | +0 Hz | |
| XIT | Activa/desactiva la Sintonización Incremental de Transmisión. | Ninguno | |
| XIT 0 | Pone a cero el offset de XIT. | Ninguno | |
| Offset de XIT | `<` / `>` o la rueda del ratón ajustan el offset de XIT en pasos de 10 Hz. | +0 Hz | |

## Comportamiento dependiente del modo

### Silenciador en modos digitales y RTTY

El silenciador se desactiva y se apaga automáticamente en los siguientes modos para evitar recortar caracteres FSK e interferir con decodificadores externos:
- **DIGU** (Digital Upper)
- **DIGL** (Digital Lower)
- **RTTY** (Radio Teletype)

Al cambiar a cualquiera de estos modos, el silenciador se apaga automáticamente si estaba encendido. El estado guardado del silenciador se conserva y se restaurará al volver a un modo donde el silenciador sea relevante. El nivel de silenciador manual se persiste del lado del cliente como la configuración `LastManualSquelchLevel` y se restaura al iniciar la aplicación, porque el modo automático sobrescribe squelchLevel del slice con valores sugeridos por el algoritmo.

### Visibilidad de QSK

El indicador QSK solo es visible cuando el modo del slice está configurado en **CW** o **CWL**.

### Manejo del modo RADE

El modo RADE es solo del lado del cliente — la radio devuelve inmediatamente el modo real (DIGL/DIGU). Al salir del modo RADE mediante el combo de modos, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE. Al entrar en modo RADE, el applet emite `radeActivated(true, sliceId)` y no llama a `setMode()` de la radio, ya que RADE es solo del lado del cliente.

## Etiquetas de lectura de deslizadores

Los deslizadores de Ganancia AF y Panorámica ahora muestran sus valores actuales como etiquetas de texto junto a los controles deslizantes (v26.5.3):

- **Ganancia AF** — Muestra el valor actual como un porcentaje (ej. "70%" para un valor de 70).
- **Panorámica L / R** — Muestra la posición de panorámica actual:
  - "C" cuando el deslizador está en el centro (valor 50).
  - "L{n}" cuando se desplaza a la izquierda, donde {n} es la diferencia desde el centro (ej. "L20" para valor 30).
  - "R{n}" cuando se desplaza a la derecha, donde {n} es la diferencia desde el centro (ej. "R30" para valor 80).

## Mejoras en la entrada de frecuencia

El campo de edición de frecuencia incluye varias mejoras para operación en VHF/UHF (v26.5.3):

- Ingresar un valor superior a 54.0 MHz que incluya un punto decimal (ej. "144.0" o "432.100") ahora se trata como una entrada explícita en MHz y se permite sin requerir una antena XVTR. Esto permite la sintonización directa a frecuencias VHF/UHF.
- Ingresar un valor superior a 54.0 MHz sin punto decimal (ej. "144000") se divide por 1e3 para conversión de kHz a MHz.
- La frecuencia máxima permitida cuando no se está en una antena XVTR es 50000 MHz cuando se detecta una entrada explícita en MHz superior a 54.0.
- La operación XVTR aún permite ingresar hasta 50000 MHz e incluye la función de conveniencia de banda de 3 dígitos (ej. "1446" → 144.6 MHz) para las bandas de 2m/70cm.

## Selección de antena

### Menú de antena RX

El menú de antena RX muestra todas las antenas disponibles, ya sea desde `ant_list` del panadapter o desde `rxAntennaList()` del slice (si está disponible). Los elementos del menú muestran tanto el token de antena como una etiqueta legible (ej. "ANT1 - 1") para mayor claridad. La antena seleccionada se establece mediante `slice->setRxAntenna()` utilizando el valor del token subyacente, no la etiqueta mostrada.

### Menú de antena TX

El menú de antena TX filtra los puertos solo RX (los que comienzan con "RX"). El método `txAntennaOptions()` devuelve solo los tokens de antena que comienzan con "ANT", "TX" o son iguales a "XVTR". Los elementos del menú muestran tanto el token de antena como una etiqueta legible (ej. "ANT1 - 1") para mayor claridad. La antena seleccionada se establece mediante `slice->setTxAntenna()` utilizando el valor del token subyacente, no la etiqueta mostrada.

##
