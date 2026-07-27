# Comprenda por qué el estado de silencio no se restaura al reconectar (política de autoridad del radio #2489)

Cuando silencia un slice usando el botón de silencio en el applet RX Controls, el estado de silencio no se guarda ni se restaura después de una desconexión y reconexión del radio. Esto es intencional: AetherSDR trata al radio como la fuente autoritativa para el estado de silencio de audio.

## Pasos

1. Haga clic en el botón de silencio (🔊 / 🔇) en el applet RX Controls para silenciar o reactivar el audio del slice.
2. Desconéctese y reconéctese al radio — el botón de silencio regresa a su estado predeterminado sin silencio (🔊).

## Qué hace cada control

| Control       | Etiqueta | Predeterminado |
|---------------|----------|----------------|
| Alternar silencio | 🔊 / 🔇 | 🔊 (sin silencio) |

## Detalles del comportamiento

- Un solo clic en el botón de silencio alterna el silencio para este slice. El ícono (🔊 o 🔇) se actualiza solo cuando el radio confirma el cambio de estado a través de `SliceModel::audioMuteChanged`.
- Un doble clic en el botón de silencio alterna el silencio para todos los slices propios simultáneamente.
- La acción de un solo clic se difiere durante el intervalo de discriminación de doble clic de la plataforma (aproximadamente 400 ms). Este retraso permite que un doble clic sobrescriba al de un solo clic y alterne todos los slices en su lugar.
- El clic simple se difiere mediante `clickDiscriminationIntervalMs()` (configurable en Radio Setup → Slice Controls, predeterminado de la plataforma ~400 ms, #3009) para que un doble clic pueda sobrescribirlo. El controlador de doble clic está en `eventFilter` y cancela el temporizador de clic simple.
- No se necesita una bandera de supresión para la señal `clicked()` final de una secuencia de doble clic. El `eventFilter` devuelve `true` en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. El botón nunca entra en estado presionado en la segunda pulsación, y la segunda liberación no emite `clicked()`.

## Consejos

- El botón de silencio solo controla el audio para el slice seleccionado actualmente. Cada slice tiene su propia alternancia de silencio.
- Si necesita que el audio comience silenciado después de una reconexión, silencie manualmente el slice después de conectarse, o use el silencio por hardware del radio si está disponible.

## Relacionado

- [Descripción general de RX Controls](../../features/rx/overview.md)
- [Sintonice el radio a una frecuencia (escriba MHz en el visor)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)

---

# RX Controls (RxApplet)

Controles de recepción por slice: modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/panorámica de AF, silenciador, RIT/XIT y configuración de dúplex para repetidores de FM. Un solo clic en el botón de silencio silencia este slice; un doble clic silencia/reactiva todos los slices propios. El formateador de ancho de filtro se comparte con el panel VFO para lecturas consistentes (#2197), y el método stepFilterWidth() recorre listas preestablecidas por modo para que los atajos de ensanchar/estrechar produzcan una geometría de borde correcta según el modo. Al cambiar a modos RTTY o digitales (DIGU, DIGL), el silenciador se desactiva automáticamente; de lo contrario, eliminaría los caracteres FSK y rompería la decodificación (#2504). Al salir del modo RADE a través del combo de modos, el applet emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar modos en un slice que no es RADE.

## Pestañas de slice

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Pestañas de slice | A..H | ninguno | 1-8 botones (limitado por el máximo de slices del hardware) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic en los botones de slice están protegidas contra controladores de señal duplicados en reconexiones. |
| Insignia de slice | A | A/B/C/D/E/F/G/H | ninguno | Muestra la letra del slice vinculado actualmente. | Coloreada según la identidad del slice. |

## Sintonización de frecuencia

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Bloqueo de sintonía | 🔓 / 🔒 | 🔓 (desbloqueado) | ninguno | Alterna el bloqueo de sintonía en el slice; el slice bloqueado ignora los cambios de frecuencia. | El ícono cambia entre candado abierto y cerrado. |
| Etiqueta de frecuencia | 0.000.000 | 0.001-54.000 MHz (450.000 MHz en XVTR) | Muestra la frecuencia VFO actual con agrupación por puntos. | Haga clic para cambiar al modo de edición. |
| Edición de frecuencia | ninguno | 0.001-54.000 MHz (450.000 MHz en XVTR) | Ingrese MHz y presione Enter para sintonizar y recentrar; soporta escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor (v0.9.0, #1954). | Consciente de XVTR: acepta hasta 450 MHz cuando el slice está en una antena XVTR. Usa FreqLineEdit para un manejo de entrada mejorado. |
| PASO | 100 Hz (índice 2) | lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | < / > o rueda del ratón recorre los tamaños de paso por modo; emite stepSizeChanged. | La lista de pasos depende del modo del slice. Los cambios de paso también emiten stepSizeChangedByUser para sincronización externa. |

## Selección de antena

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Antena RX | ANT1 | de ant_list en el estado del panadapter | Abre un menú listando las antenas disponibles; seleccionar establece slice->setRxAntenna. | Se completa desde la ant_list del radio; etiqueta de color azul. Cuando un KiwiSDR está activo, se añaden tokens de antena virtual al menú. Seleccionar una antena virtual KiwiSDR emite kiwiRxAntennaSelected(sliceId, profileId); seleccionar una antena Flex emite flexRxAntennaSelected(sliceId). |
| Antena TX | ANT1 | de ant_list, excluyendo puertos solo RX | Abre un menú listando antenas capaces de TX; establece slice->setTxAntenna. | Etiqueta de color rojo; los puertos de antena solo RX (prefijo 'RX') se filtran. |

## Modo y filtro

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Combo de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE) | Establece el modo del slice; remodela los preestablecidos de filtro y paso para el nuevo modo. | Seleccionar un modo emite wfmActivated(false) para eliminar cualquier superposición de demodulación de software WFM. La opción RADE requiere la bandera de compilación HAVE_RADE. |
| Botón WFM | WFM | desmarcado | On/Off | Alternar para habilitar el demodulador FM por software a través de DAX IQ → Hi-Fi Cable para recepción FM de banda ancha. | Posicionado junto al combo de modo. Cuando se activa, emite wfmActivated(true) con el ID del slice actual. |
| Ancho de filtro | 2.7K | ninguno | Muestra el ancho de filtro actual en kHz. | Se actualiza cuando se aplica un preestablecido de filtro. |
| Preestablecidos de ancho de filtro | ninguno | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; AM/SAM: 5600-14000 Hz; CW: 50/100/250/400/500/600 Hz; DIG: 100-2000 Hz; RTTY: 250-1000 Hz | Haga clic para aplicar un ancho de filtro preestablecido; clic derecho para guardar el ancho actual como preestablecido. | Botones ocultos para modos FM/NFM/DFM; los preestablecidos son por modo. Los preestablecidos de CW ahora incluyen 500 Hz y 600 Hz (primeros 6 de los 8 preestablecidos de VfoWidget). La lectura de ancho (compartida con VfoWidget a través de RxApplet::formatFilterWidth) usa lógica consciente del modo. El método stepFilterWidth(direction) recorre la lista preestablecida por modo para ensanchar/estrechar correctos según el modo (#2208). |
| Widget de banda de paso de filtro | ninguno | ninguno | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). | ninguno |

## Indicador de break-in CW

| Control       | Etiqueta | Predeterminado | Comportamiento | Notas |
|---------------|----------|----------------|----------------|-------|
| Indicador QSK | QSK | ninguno | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. | Solo lectura; controlado a través del botón Breakin del applet CW. |

## Selección de slice TX

| Control       | Etiqueta | Comportamiento | Notas |
|---------------|----------|----------------|-------|
| Insignia TX | TX | Haga clic para establecer este slice como el slice TX (llama a slice->setTxSlice). | ninguno |

## Controles de audio

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Alternar silencio | 🔊 / 🔇 | 🔊 (sin silencio) | ninguno | Un solo clic silencia/reactiva este slice (diferido por el intervalo de discriminación de clic de la plataforma, configurable en Radio Setup → Slice Controls). Un doble clic silencia/reactiva todos los slices propios a través de la señal muteAllToggled. El ícono cambia cuando el radio confirma a través de SliceModel::audioMuteChanged. | Según la Política de Configuración de Autoridad del Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — el radio es la fuente de verdad para el silencio de audio. El clic simple se difiere mediante clickDiscriminationIntervalMs() (configurable en Radio Setup → Slice Controls, predeterminado de la plataforma ~400 ms, #3009) para que un doble clic pueda sobrescribirlo. El controlador de doble clic está en eventFilter y cancela el temporizador de clic simple. |
| Ganancia AF | 70 | 0-100 | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. | ninguno |
| Panorámica L / R | 50 | 0-100 | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). | Doble clic restablece a 50 (centro). |

## Silenciador

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Alternar SQL | SQL | ninguno | ninguno | Habilita el silenciador al nivel actual del deslizador. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el silenciador eliminaría los caracteres FSK (#2504). | ninguno |
| Nivel de silenciador | 20 | 0-100 | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. | ninguno |

## Controles AGC

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece el modo AGC del slice. | Oculto en modos de la familia FM. |
| Umbral AGC | 65 | 0-100 | Establece el umbral AGC (o el nivel de AGC apagado cuando el modo AGC es Off). | Haga clic derecho en el deslizador para abrir un menú contextual y seleccione "Calibrar AGC-T contra el piso de ruido…" para establecer automáticamente el umbral basado en el piso de ruido actual. La información sobre herramientas refleja qué valor se está ajustando y anuncia la calibración con clic derecho. |

## RIT/XIT

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Alternar RIT | RIT | ninguno | ninguno | Activa/desactiva la Sintonización Incremental de Recepción. | ninguno |
| Cero RIT | RIT 0 | ninguno | ninguno | Pone a cero el desplazamiento RIT. | ninguno |
| Desplazamiento RIT | +0 Hz | paso 10 Hz | < / > o rueda del ratón ajusta el desplazamiento RIT en pasos de 10 Hz. | ninguno |
| Alternar XIT | XIT | ninguno | ninguno | Activa/desactiva la Sintonización Incremental de Transmisión. | ninguno |
| Cero XIT | XIT 0 | ninguno | ninguno | Pone a cero el desplazamiento XIT. | ninguno |
| Desplazamiento XIT | +0 Hz | paso 10 Hz | < / > o rueda del ratón ajusta el desplazamiento XIT en pasos de 10 Hz. | ninguno |

## Configuración de repetidor FM

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------------|----------|----------------|--------------|----------------|-------|
| Modo de tono | Off | Off, CTCSS TX | Selecciona el modo de tono CTCSS en FM/NFM/DFM. | Visible solo en modos de la familia FM. |
| Tono CTCSS | ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz) | Selecciona la frecuencia del tono CTCSS enviada con la transmisión. | Habilitado solo cuando Modo de tono = CTCSS TX. |
| Desplazamiento | 0.0 MHz | 0.0-100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM en MHz. | ninguno |
| Desplazamiento hacia abajo | − | ninguno | ninguno | Establece la dirección de desplazamiento del repetidor como 'hacia abajo' (TX debajo de RX). | ninguno |
| Símplex | Simplex | marcado | ninguno | Establece la dirección de desplazamiento del repetidor como símplex (TX = RX). | ninguno |
| Desplazamiento hacia arriba | + | ninguno | ninguno | Establece la dirección de desplazamiento del repetidor como 'hacia arriba' (
