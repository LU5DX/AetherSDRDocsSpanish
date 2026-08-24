# Controles de RX (RxApplet)

Controles de recepción por slice: modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/pan de AF, squelch, RIT/XIT y ajustes de dúplex para repetidoras FM. Un clic en el botón de silencio silencia este slice; doble clic silencia/activa el sonido de todos los slices propiedad del usuario. El formateador de ancho de filtro se comparte con el panel VFO para lecturas consistentes (#2197), y el método stepFilterWidth() recorre las listas de preajustes por modo para que los atajos de ampliar/reducir produzcan una geometría de bordes correcta según el modo. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el squelch se desactiva automáticamente; de lo contrario, recortaría los caracteres FSK y rompería la decodificación (#2504). Al salir del modo RADE mediante el combo de modos, el applet emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE.

## Pestañas de slice

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Pestañas de slice | A..H | ninguno | 1-8 botones (limitado por el máximo de slices del hardware) | Selecciona el slice al que está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectarse (v0.9.5.1, #2254). Las conexiones de clic en los botones de slice están protegidas contra manejadores de señal duplicados entre reconexiones. |
| Insignia de slice | A | A/B/C/D/E/F/G/H | ninguno | Muestra la letra del slice vinculado actualmente. | Coloreada según la identidad del slice. |

## Sintonización de frecuencia

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Bloqueo de sintonía | 🔓 / 🔒 | 🔓 (desbloqueado) | ninguno | Alterna el bloqueo de sintonía en el slice; un slice bloqueado ignora los cambios de frecuencia. | El icono alterna entre candado abierto y cerrado. |
| Etiqueta de frecuencia | 0.000.000 | ninguno | Muestra la frecuencia VFO actual con agrupación de puntos. | Haga clic para entrar en modo de edición. |
| Edición de frecuencia | ninguno | 0.001-54.000 MHz (hasta 50000 MHz en XVTR) | Ingrese MHz y presione Enter para sintonizar y recentrar; admite autoescalado kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor (v0.9.0, #1954). | Compatible con XVTR: acepta hasta 50.000 MHz cuando el slice está en una antena XVTR. Conveniencia de banda de 3 dígitos: en 2m/70cm (100-999 MHz), una inserción de dígito formatea 1446 como 144.6. |
| STEP | 100 Hz (índice 2) | lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | < / > o la rueda del ratón recorren los tamaños de paso por modo; emite stepSizeChanged. | La lista de pasos depende del modo del slice. |

## Selección de antena

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Antena RX | ANT1 | de ant_list, más los tokens de antena virtual KiwiSDR asignados | Abre un menú que lista las antenas disponibles; seleccionar establece slice->setRxAntenna, o enruta a un perfil de receptor KiwiSDR asignado cuando se elige un token de antena virtual. | Se completa con la lista de antenas del equipo más cualquier token de antena virtual KiwiSDR del administrador Kiwi; etiqueta de color azul. Retrocede a ANT1/ANT2 cuando la lista está vacía. |
| Antena TX | ANT1 | de ant_list, excluyendo puertos solo RX | Abre un menú que lista las antenas con capacidad TX; establece slice->setTxAntenna. | Etiqueta de color rojo; los puertos de antena solo RX (prefijo 'RX') se filtran. |

## Modo y filtro

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Combo de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DSTR, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE; WFM mediante botón de bandera VFO) | Establece el modo del slice; remodela los preajustes de filtro y paso para el nuevo modo. | La opción RADE requiere la bandera de compilación HAVE_RADE. Los modos DSTR y FreeDV se filtran cuando el modelo no los admite. Seleccionar un modo de radio real elimina una superposición activa de demodulación de software WFM (WFM se alterna desde el botón de bandera WFM del VFO, no desde este combo). |
| Ancho de filtro | 2.7K | ninguno | Muestra el ancho de filtro actual en kHz. | Se actualiza cuando se aplica un preajuste de filtro. |
| Preajustes de ancho de filtro | ninguno | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; AM/SAM: 5600-14000 Hz; CW: 50/100/250/400 Hz; DIG: 100-2000 Hz; RTTY: 250-1000 Hz | Haga clic para aplicar un ancho de filtro preajustado; clic derecho para guardar el ancho actual como preajuste. | Botones ocultos en modos FM/NFM/DFM; los preajustes son por modo. La lectura de ancho (compartida con VfoWidget a través de RxApplet::formatFilterWidth) usa lógica sensible al modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de preajustes por modo para ampliar/reducir correctamente según el modo (#2208). |
| Widget de banda de paso del filtro | ninguno | ninguno | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). | ninguno |

## Indicador de break-in CW

| Control | Etiqueta | Predeterminado | Comportamiento | Notas |
|---------|----------|----------------|----------------|-------|
| Indicador QSK | QSK | ninguno | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. | Solo lectura; controlado mediante el botón Breakin del applet CW. |

## Selección de slice TX

| Control | Etiqueta | Comportamiento | Notas |
|---------|----------|----------------|-------|
| Insignia TX | TX | Haga clic para establecer este slice como slice TX (llama a slice->setTxSlice). | ninguno |

## Controles de audio

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Alternar silencio | 🔊 / 🔇 | 🔊 (con sonido) | ninguno | Un clic silencia/activa el sonido de este slice (diferido por el intervalo de discriminación de clic de la plataforma, configurable en Radio Setup → Slice Controls). Doble clic silencia/activa el sonido de todos los slices propiedad del usuario mediante la señal muteAllToggled. El icono cambia cuando la radio lo confirma a través de SliceModel::audioMuteChanged. | Según la Política de Configuración Autoritativa de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. El clic único se difiere por clickDiscriminationIntervalMs() (configurable en Radio Setup → Slice Controls, intervalo predeterminado de doble clic de la plataforma ~400 ms, #3009) para que un doble clic pueda anularlo. El manejador de doble clic está en eventFilter y cancela el temporizador de clic único. |
| Ganancia AF | 70 | 0-100 | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. | ninguno |
| Pan L / R | 50 | 0-100 | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). | Doble clic restablece a 50 (centro). |

## Squelch

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| SQL / AUTO | Off | Off, SQL (Manual), AUTO | Botón de ciclo de tres posiciones: cada clic avanza Off → SQL (umbral manual) → AUTO (el algoritmo rastrea el piso de ruido) → Off. En modo AUTO, el botón muestra 'AUTO' en ámbar; en modo manual, 'SQL' en verde. Deshabilitado (y desactivado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504). | Manual y Auto activan el squelch de la radio. El algoritmo de squelch automático reside en el panadapter; el nivel es el margen en dB por encima del piso de ruido medido. Reflejado por un botón idéntico en la pestaña Audio del panel VFO. |
| Nivel de squelch | 20 | Manual: 0-100 (o 0-99 en recepción de reemplazo Kiwi); Auto: 5-20 dB de margen | En modo Manual ajusta el umbral de squelch (tiene efecto solo cuando el squelch está activado). En modo AUTO establece el margen en dB por encima del piso de ruido medido donde se abre la puerta, persistido en AutoSqlMarginDb. | En modo Manual, el nivel es autoritativo de la radio por slice (no se persiste); en modo Auto, el margen se persiste. Deshabilitado en modos RTTY y digitales y en modo Off. Clic derecho en el control deslizante de umbral AGC para calibración de ruido AGC-T. |

## Controles AGC

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece el modo AGC del slice. | Oculto en modos de la familia FM. |
| Umbral AGC | 65 | 0-100 | Establece el umbral AGC (o el nivel de apagado AGC cuando el modo AGC es Off). | La información sobre herramientas refleja qué valor se está ajustando. Clic derecho abre un comando 'Calibrate AGC-T against noise floor…' que inicia el diálogo de calibración de ruido AGC-T (deshabilitado mientras una recepción de reemplazo Kiwi está activa). |

## RIT/XIT

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Alternar RIT | RIT | ninguno | ninguno | Activa/desactiva la sintonía incremental de recepción. | ninguno |
| RIT cero | RIT 0 | ninguno | ninguno | Pone a cero el desplazamiento RIT. | ninguno |
| Desplazamiento RIT | +0 Hz | paso 10 Hz | < / > o la rueda del ratón ajustan el desplazamiento RIT en pasos de 10 Hz. | ninguno |
| Alternar XIT | XIT | ninguno | ninguno | Activa/desactiva la sintonía incremental de transmisión. | ninguno |
| XIT cero | XIT 0 | ninguno | ninguno | Pone a cero el desplazamiento XIT. | ninguno |
| Desplazamiento XIT | +0 Hz | paso 10 Hz | < / > o la rueda del ratón ajustan el desplazamiento XIT en pasos de 10 Hz. | ninguno |

## Configuración de repetidora FM

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------|----------------|--------------|----------------|-------|
| Modo de tono | Off | Off, CTCSS TX | Selecciona el modo de tono CTCSS en FM/NFM/DFM. | Visible solo en modos de la familia FM. |
| Tono CTCSS | ninguno | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz) | Selecciona la frecuencia del tono CTCSS enviada con la transmisión. | Habilitado solo cuando Modo de tono = CTCSS TX. |
| Desplazamiento | 0.0 MHz | 0.0-100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento de repetidora FM en MHz. | ninguno |
| Desplazamiento hacia abajo | − | ninguno | ninguno | Establece la dirección de desplazamiento de repetidora a 'hacia abajo' (TX por debajo de RX). | ninguno |
| Simplex | Simplex | marcado | ninguno | Establece la dirección de desplazamiento de repetidora a simplex (TX = RX). | ninguno |
| Desplazamiento hacia arriba | + | ninguno | ninguno | Establece la dirección de desplazamiento de repetidora a 'hacia arriba' (TX por encima de RX). | ninguno |
| REV / XFC | REV | ninguno | REV (alternar) o XFC (momentáneo) | Para operación de repetidora FM, REV invierte el signo del desplazamiento TX para trabajar un par de repetidora invertido. En backends que admiten una verificación de frecuencia de transmisión, el botón se renombra a XFC: al presionarlo, mantiene la verificación de frecuencia de transmisión mientras dure la presión, y mientras está presionado, fuerza brevemente la radio hacia la frecuencia de transmisión para confirmar cobertura. | El botón alterna REV (marcable) normalmente, o se convierte en un botón momentáneo XFC cuando el backend de radio conectado anuncia hasTransmitFrequencyCheck. El XFC mantenido se libera al ocultar, desactivar, cambiar capacidad o desconectar. |

---

# El estado de silencio no se restaura al reconectar (política autoritativa de la radio #2489)

Cuando silencia un slice con el botón de silencio en el applet Controles de RX, el estado de silencio no se guarda ni se restaura después de una desconexión y reconexión de la radio. Esto es por diseño: AetherSDR trata a la radio como la fuente autoritativa para el estado de silencio de audio.

## Pasos

1. Haga clic en el botón de silencio (🔊 / 🔇) en el applet Controles de RX para silenciar o activar el sonido del slice.
2. Desconecte y vuelva a conectar la radio — el botón de silencio vuelve a su estado predeterminado con sonido (🔊).

## Qué hace cada control

| Control     | Etiqueta                                                                                                                                                                                                                                                                                                                                                    | Predeterminado                                                                                                                                                                                                                                    |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Alternar silencio | 🔊 / 🔇                                                                                                                                                                                                                                                                                                                                                    | 🔊 (con sonido)                                                                                                                                                                                                                                |
| REV / XFC   | Para operación de repetidora FM, REV invierte el signo del desplazamiento TX para trabajar un par de repetidora invertido. En backends que admiten una verificación de frecuencia de transmisión
