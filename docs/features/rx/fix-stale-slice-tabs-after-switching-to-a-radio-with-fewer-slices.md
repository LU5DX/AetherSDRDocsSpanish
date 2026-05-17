# Applet de Controles de RX (v26.5.2.1)

El applet de Controles de RX proporciona controles por segmento (slice) que incluyen selección de modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/paneo de AF, silenciador, RIT/XIT y configuración de dúplex para repetidores FM. El formateador de ancho de filtro se comparte con el panel VFO para lecturas coherentes (#2197), y el método stepFilterWidth() recorre listas de preajustes por modo para que los atajos de ampliar/estrechar produzcan una geometría de bordes correcta según el modo. Al cambiar a modos RTTY o digitales (DIGU, DIGL), el silenciador se desactiva automáticamente; de lo contrario, recortaría los caracteres FSK e interrumpiría la decodificación (#2504).

## Antes de comenzar

- Asegúrese de que el applet RX esté visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Los controles mostrados dependen del segmento seleccionado actualmente y de su modo.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Notas |
|---------|----------------|----------------|-------|
| Pestañas de segmento (A..H) | Selecciona a qué segmento está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1 | clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de segmento estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic en los botones de segmento están protegidas contra manejadores de señal duplicados en reconexiones. |
| Insignia de segmento | Muestra la letra del segmento vinculado actualmente. Siempre visible; el único indicador de segmento visible cuando la fila de pestañas está oculta. Admite formato de texto enriquecido para la letra del segmento (#2606). | A | Coloreada según la identidad del segmento. |
| 🔓 / 🔒 | Alterna el bloqueo de sintonía en el segmento; un segmento bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) | El icono cambia entre candado abierto y cerrado. |
| ANT1 (antena RX) | Abre un menú que lista las antenas disponibles; al seleccionar, establece slice->setRxAntenna. Se completa desde ant_list de la radio o desde rxAntennaList del segmento. Los elementos del menú muestran etiquetas opcionales con números de puerto para mayor claridad. | ANT1 | Etiqueta de color azul. Los elementos del menú muestran tanto el token de antena como una etiqueta legible (ej. "ANT1 - 1"). |
| ANT1 (antena TX) | Abre un menú que lista las antenas con capacidad TX; establece slice->setTxAntenna. Los puertos solo RX (prefijo 'RX') se filtran. Los elementos del menú muestran etiquetas opcionales con números de puerto para mayor claridad. | ANT1 | Etiqueta de color rojo. Los elementos del menú muestran tanto el token de antena como una etiqueta legible. El método txAntennaOptions() devuelve todos los puertos ANT*, TX* y XVTR, excluyendo los puertos solo RX. |
| 2.7K (ancho de filtro) | Muestra el ancho de filtro actual en kHz. Se actualiza al aplicar un preajuste de filtro. | 2.7K | La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| QSK | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. | apagado (gris) | Solo lectura. |
| TX (insignia) | Haga clic para establecer este segmento como segmento TX (llama a slice->setTxSlice). | Ninguno | |
| Menú desplegable de modo | Establece el modo del segmento; reconfigura los preajustes de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). | USB | La opción RADE requiere la marca de compilación HAVE_RADE. |
| Etiqueta de frecuencia | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. | 0.000.000 | |
| Edición de frecuencia | Ingrese MHz y presione Enter para sintonizar y recentrar; admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor (v0.9.0, #1954). | Ninguno | Consciente de XVTR: acepta hasta 450 MHz cuando el segmento está en una antena XVTR. |
| PASO | `<` / `>` o la rueda del ratón recorren los tamaños de paso por modo; emite stepSizeChanged. La lista de pasos depende del modo del segmento. | 100 Hz (índice 2) | |
| Preajustes de ancho de filtro | Haga clic para aplicar un ancho de filtro preajustado; clic derecho para guardar el ancho actual como preajuste. La lectura de ancho utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto. Las palabras clave Ampliar/Estrechar (si están asignadas a atajos de teclado) recorren la lista de preajustes por modo para una geometría de bordes correcta según el modo. | Lista por modo | Botones ocultos para modos FM/NFM/DFM; los preajustes son por modo. El método stepFilterWidth(dirección) recorre la lista de preajustes por modo para ampliar/estrechar correctamente según el modo (#2208). |
| Widget de banda pasante de filtro | Arrastre los bordes inferior/superior para ajustar la banda pasante del filtro; emite filterChanged (inferior, superior). | Ninguno | |
| Modo de tono (FM) | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Desactivado | |
| Valor de tono CTCSS | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono = CTCSS TX. | Ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). |
| Desplazamiento (FM) | Establece la frecuencia de desplazamiento del repetidor FM en MHz. | 0.0 MHz | Rango 0.0-100.0 MHz (paso 0.1). |
| − (desplazamiento hacia abajo) | Establece la dirección del desplazamiento del repetidor a 'abajo' (TX por debajo de RX). | Ninguno | |
| Simplex | Establece la dirección del desplazamiento del repetidor a simplex (TX = RX). | Marcado | |
| + (desplazamiento hacia arriba) | Establece la dirección del desplazamiento del repetidor a 'arriba' (TX por encima de RX). | Ninguno | |
| REV | Invierte el signo del desplazamiento TX para trabajar un par de repetidor invertido. | Ninguno | |
| 🔊 / 🔇 (silenciar) | Silencia la salida de audio del segmento. | 🔊 (sin silenciar) | Según la Política de Ajustes de Autoridad de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. |
| Ganancia AF | Ajusta la ganancia de salida de audio del segmento; emite afGainChanged. | 70 | Rango 0-100. |
| Paneo L / R | Desplaza el audio del segmento entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). | 50 | Rango 0-100. |
| SQL | Activa el silenciador en el nivel actual del control deslizante. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el silenciador recortaría los caracteres FSK (#2504). | | |
| Nivel de silenciador | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. El nivel de silenciador manual se persiste del lado del cliente como la configuración `LastManualSquelchLevel` (predeterminado 20). | 20 | Rango 0-100. El último umbral de silenciador manual elegido por el usuario se guarda entre sesiones y se restaura al iniciar, porque el modo automático sobrescribe el squelchLevel del segmento con valores sugeridos por el algoritmo. |
| Modo AGC | Establece el modo AGC del segmento. Opciones: Desactivado, Lento, Medio, Rápido. Oculto en modos de la familia FM. | Medio | |
| Umbral AGC | Establece el umbral AGC (o el nivel de desactivación AGC cuando el modo AGC está Desactivado). La información sobre herramientas refleja qué valor se está ajustando. | 65 | Rango 0-100. |
| RIT | Activa/desactiva la Sintonización Incremental de Recepción. | Ninguno | |
| RIT 0 | Pone a cero el desplazamiento RIT. | Ninguno | |
| Desplazamiento RIT | `<` / `>` o la rueda del ratón ajustan el desplazamiento RIT en pasos de 10 Hz. | +0 Hz | |
| XIT | Activa/desactiva la Sintonización Incremental de Transmisión. | Ninguno | |
| XIT 0 | Pone a cero el desplazamiento XIT. | Ninguno | |
| Desplazamiento XIT | `<` / `>` o la rueda del ratón ajustan el desplazamiento XIT en pasos de 10 Hz. | +0 Hz | |

## Comportamiento dependiente del modo

### Silenciador en modos digitales y RTTY

El silenciador se desactiva y se apaga automáticamente en los siguientes modos para evitar recortar caracteres FSK e interferir con decodificadores externos:
- **DIGU** (Digital Superior)
- **DIGL** (Digital Inferior)
- **RTTY** (Radio Teletype)

Al cambiar a cualquiera de estos modos, el silenciador se apaga automáticamente si estaba activado. El estado guardado del silenciador se conserva y se restablecerá al volver a un modo donde el silenciador sea significativo. El nivel de silenciador manual se persiste del lado del cliente como la configuración `LastManualSquelchLevel` y se restaura al iniciar la aplicación, porque el modo automático sobrescribe el squelchLevel del segmento con valores sugeridos por el algoritmo.

### Visibilidad de QSK

El indicador QSK solo es visible cuando el modo del segmento está configurado en **CW** o **CWL**.

### Manejo del modo RADE

El modo **RADE** es solo del lado del cliente — la radio devuelve inmediatamente el modo real (DIGL/DIGU), por lo que la señal `radeActivated(false)` nunca se emite al salir de RADE. Anteriormente, el applet verificaba `m_slice->mode() == "RADE"` antes de emitir, pero como la radio informa inmediatamente el modo digital subyacente, esta condición nunca era verdadera.

## Selección de antena

### Menú de antena RX

El menú de antena RX muestra todas las antenas disponibles, ya sea desde `ant_list` del panadaptador o desde `rxAntennaList()` del segmento (si está disponible). Los elementos del menú muestran tanto el token de antena como una etiqueta legible (ej. "ANT1 - 1") para mayor claridad. La antena seleccionada se establece mediante `slice->setRxAntenna()` usando el valor del token subyacente, no la etiqueta mostrada.

### Menú de antena TX

El menú de antena TX filtra los puertos solo RX (los que comienzan con "RX"). El método `txAntennaOptions()` devuelve solo los tokens de antena que comienzan con "ANT", "TX" o son iguales a "XVTR". Los elementos del menú muestran tanto el token de antena como una etiqueta legible (ej. "ANT1 - 1") para mayor claridad. La antena seleccionada se establece mediante `slice->setTxAntenna()` usando el valor del token subyacente, no la etiqueta mostrada.

### Persistencia del silenciador manual

El control de nivel de silenciador almacena el último umbral manual elegido por el usuario en la configuración de la aplicación bajo la clave `LastManualSquelchLevel` (predeterminado 20). Este valor se recupera al iniciar la aplicación porque el modo automático sobrescribe el squelchLevel del segmento con valores sugeridos por el algoritmo, y no se puede confiar en que la radio preserve la preferencia manual del operador entre ciclos de modo o inicios.

## Consejos

- Los atajos de teclado **Ampliar** y **Estrechar** (o acciones MIDI/GPIO equivalentes) recorren la banda pasante del filtro del segmento activo a través de la lista de preajustes por modo mediante `stepFilterWidth()`. Esto asegura que todos los modos produzcan una geometría de bordes correcta según el modo.
- La lectura de ancho de filtro utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197).
- Los puertos de antena solo RX (con prefijo 'RX') se filtran del menú de selección de antena TX.
- La insignia de segmento ahora admite formato de texto enriquecido, lo que permite que la letra del segmento se renderice como HTML (#2606).

## Solución de problemas

- **La lectura del ancho de filtro parece incorrecta después de un cambio de modo** — Intente recorrer los preajustes de filtro para actualizar el valor mostrado.
- **El silenciador parece no funcionar** — Verifique que no esté en un modo digital o RTTY donde el silenciador esté deshabilitado.
- **El modo RADE no aparece** — La opción RADE requiere una compilación con la marca `HAVE_RADE`.
- **Quedan pestañas de segmento obsoletas después de reconectar** — Desconecte usando `Settings > Connect to Radio...`, espere a que la insignia de segmento reaparezca y luego reconecte.
- **Las etiquetas de los elementos del menú de antena parecen confusas** — Los elementos del menú muestran el token de antena (ej. "ANT1") con una etiqueta legible (ej. "- 1") para mayor claridad. El valor del token subyacente se utiliza para la selección.

## Relacionado

- [Switch between multiple slices using the A..H tab row](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [RX Controls overview](overview.md)
- [Understanding slices and VFOs](../../getting-started/concepts/understanding-slices.md)
