# Applet de Controles de RX (v26.5.1)

El applet Controles de RX proporciona controles de recepción por slice, incluyendo selección de modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, CAG, ganancia/panorama de AF, silenciador, RIT/XIT y ajustes de dúplex para repetidores FM.

## Antes de comenzar

- Asegúrese de que el applet RX esté visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Los controles mostrados dependen del slice seleccionado actualmente y de su modo.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---------|---------------|----------------------|-------|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1 | clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic en el botón de slice están protegidas contra manejadores de señal duplicados durante reconexiones. |
| Insignia de slice | Muestra la letra del slice vinculado actualmente. Se muestra en todo momento; es el único indicador de slice visible cuando la fila de pestañas está oculta. | A | Coloreada según la identidad del slice. |
| 🔓 / 🔒 | Activa/desactiva el bloqueo de sintonía en el slice; un slice bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) | El icono alterna entre candado abierto y cerrado. |
| ANT1 (antena RX) | Abre un menú que lista las antenas disponibles; al seleccionar, establece slice->setRxAntenna. Se completa desde ant_list de la radio. | ANT1 | Etiqueta de color azul. |
| ANT1 (antena TX) | Abre un menú que lista las antenas con capacidad de TX; establece slice->setTxAntenna. Los puertos de antena solo RX (prefijo 'RX') se filtran. | ANT1 | Etiqueta de color rojo. |
| 2.7K (ancho de filtro) | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un preajuste de filtro. | 2.7K | La lectura de ancho utiliza lógica consciente del modo, por lo que los modos SSB/digitales muestran el ancho etiquetado correcto (#2197). |
| QSK | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. | Apagado (gris) | Solo lectura. |
| TX (insignia) | Haga clic para establecer este slice como el slice de TX (llama a slice->setTxSlice). | Ninguno | |
| Menú desplegable de modo | Establece el modo del slice; reajusta los preajustes de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). | USB | La opción RADE requiere la marca de compilación HAVE_RADE. |
| Etiqueta de frecuencia | Muestra la frecuencia actual del VFO con agrupación de puntos. Haga clic para cambiar al modo de edición. | 0.000.000 | |
| Edición de frecuencia | Introduzca MHz y presione Enter para sintonizar y re-centrar; admite escala automática de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor (v0.9.0, #1954). | Ninguno | Consciente de XVTR: acepta hasta 450 MHz cuando el slice está en una antena XVTR. |
| PASO | `<` / `>` o la rueda del ratón recorre los tamaños de paso según el modo; emite stepSizeChanged. La lista de pasos depende del modo del slice. | 100 Hz (índice 2) | |
| Preajustes de ancho de filtro | Haga clic para aplicar un ancho de filtro preajustado; haga clic derecho para guardar el ancho actual como preajuste. La lectura de ancho utiliza lógica consciente del modo, por lo que los modos SSB/digitales muestran el ancho etiquetado correcto. Las palabras clave Ampliar/Reducir (si están asignadas a atajos de teclado) recorren la lista de preajustes según el modo para una geometría de bordes correcta según el modo. | Lista por modo | Los botones están ocultos para modos FM/NFM/DFM; los preajustes son por modo. El método stepFilterWidth(direction) recorre la lista de preajustes por modo para ampliar/reducir correctamente según el modo (#2208). |
| Widget de banda de paso del filtro | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). | Ninguno | |
| Modo de tono (FM) | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Desactivado | |
| Valor del tono CTCSS | Selecciona la frecuencia del tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono = CTCSS TX. | Ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). |
| Desplazamiento (FM) | Establece la frecuencia de desplazamiento del repetidor FM en MHz. | 0.0 MHz | Rango 0.0-100.0 MHz (paso 0.1). |
| − (desplazamiento hacia abajo) | Establece la dirección del desplazamiento del repetidor hacia 'abajo' (TX por debajo de RX). | Ninguno | |
| Símplex | Establece la dirección del desplazamiento del repetidor a símplex (TX = RX). | Marcado | |
| + (desplazamiento hacia arriba) | Establece la dirección del desplazamiento del repetidor hacia 'arriba' (TX por encima de RX). | Ninguno | |
| REV | Invierte el signo del desplazamiento TX para trabajar con un par de repetidor invertido. | Ninguno | |
| 🔊 / 🔇 (silencio) | Silencia la salida de audio del slice. | 🔊 (sin silenciar) | |
| Ganancia de AF | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. | 70 | Rango 0-100. |
| Panorámica L / R | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). | 50 | Rango 0-100. |
| SQL | Activa el silenciador en el nivel actual del deslizador. Deshabilitado (y desactivado automáticamente) en modos RTTY, digitales (DIGU, DIGL) y CW donde el silenciador eliminaría los caracteres FSK (#2504). | | |
| Nivel de silenciador | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY, digitales y CW. | 20 | Rango 0-100. |
| Modo CAG | Establece el modo CAG del slice. Opciones: Desactivado, Lento, Medio, Rápido. Oculto en modos de la familia FM. | Medio | |
| Umbral CAG | Establece el umbral CAG (o el nivel de CAG desactivada cuando el modo CAG es Desactivado). La información sobre herramientas refleja qué valor se está ajustando. | 65 | Rango 0-100. |
| RIT | Activa/desactiva la Sintonización Incremental de Recepción. | Ninguno | |
| RIT 0 | Pone a cero el desplazamiento RIT. | Ninguno | |
| Desplazamiento RIT | `<` / `>` o la rueda del ratón ajusta el desplazamiento RIT en pasos de 10 Hz. | +0 Hz | |
| XIT | Activa/desactiva la Sintonización Incremental de Transmisión. | Ninguno | |
| XIT 0 | Pone a cero el desplazamiento XIT. | Ninguno | |
| Desplazamiento XIT | `<` / `>` o la rueda del ratón ajusta el desplazamiento XIT en pasos de 10 Hz. | +0 Hz | |

## Comportamiento dependiente del modo

### Silenciador en modos digitales, RTTY y CW

El silenciador está deshabilitado y se desactiva automáticamente en los siguientes modos para evitar eliminar caracteres FSK e interferir con decodificadores externos:
- **DIGU** (Digital Upper)
- **DIGL** (Digital Lower)
- **RTTY** (Radio Teletipo)
- **NT** (Telegrafía de banda estrecha)
- **CW** (Código Morse)
- **CWL** (Código Morse, banda lateral inferior)

Al cambiar a cualquiera de estos modos, el silenciador se desactiva automáticamente si estaba activado. El estado guardado del silenciador se conserva y se restaurará al volver a un modo donde el silenciador sea relevante.

### Visibilidad de QSK

El indicador QSK solo es visible cuando el modo del slice está configurado en **CW** o **CWL**.

### Manejo del modo RADE

Cuando se selecciona el modo **RADE** y la compilación incluye `HAVE_RADE`, el modo del slice se establece primero antes de emitir la señal `radeActivated`. Al cambiar de RADE a otro modo, la señal de desactivación solo se emite si el slice estaba realmente en modo RADE, evitando desactivaciones espurias en reasignaciones de slice, activaciones externas y escenarios de múltiples paneles.

## Consejos

- Los atajos de teclado **Ampliar** y **Reducir** (o las acciones MIDI/GPIO equivalentes) recorren la banda de paso del filtro del slice activo a través de la lista de preajustes según el modo mediante `stepFilterWidth()`. Esto garantiza que todos los modos produzcan una geometría de bordes correcta según el modo.
- La lectura de ancho de filtro utiliza lógica consciente del modo, por lo que los modos SSB/digitales muestran el ancho etiquetado correcto (#2197).
- Los puertos de antena solo RX (con prefijo 'RX') se filtran del menú de selección de antena TX.

## Solución de problemas

- **La lectura de ancho de filtro parece incorrecta después de un cambio de modo** — Intente recorrer los preajustes de filtro para actualizar el valor mostrado.
- **El silenciador parece no funcionar** — Verifique que no esté en un modo digital, RTTY o CW donde el silenciador esté deshabilitado.
- **El modo RADE no aparece** — La opción RADE requiere una compilación con la marca `HAVE_RADE`.
- **Las pestañas de slice obsoletas persisten después de reconectar** — Desconecte usando `Settings > Connect to Radio...`, espere a que la insignia de slice reaparezca y luego reconecte.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de Controles de RX](overview.md)
- [Comprender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
