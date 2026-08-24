# Descripción general de los controles RX

El applet RX Controls le brinda control por slice sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, AGC, audio, squelch, RIT/XIT y configuración de repetidor FM. Ábralo siempre que necesite configurar cómo un slice recibe o transmite.

## Cómo funciona

El applet RX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja RX. Cuando la radio admite más de un slice, aparece una fila de pestañas de slice (A a H) en la parte superior; al hacer clic en una pestaña, el applet se vincula a ese slice. Todos los controles debajo de la fila de pestañas afectan únicamente al slice seleccionado actualmente.

Los preajustes de ancho de filtro son la única configuración que persiste entre sesiones y se almacenan en la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del slice

| Control | Predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona qué slice controla el applet. La fila de pestañas se oculta cuando la radio tiene un solo slice. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de slice estática. Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados entre reconexiones (v0.9.5.1, #2254). |
| Insignia de slice | A | Muestra la letra del slice activo. El color está determinado por la identidad del slice. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia provenientes del panadapter y otras fuentes. |
| TX (insignia) | — | Haga clic para designar este slice como el slice de TX. |

### Frecuencia y modo

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Combinación de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DSTR, DIGU, DIGL, RTTY (+ RADE si la marca de compilación HAVE_RADE está configurada; WFM mediante el botón de indicador de VFO) | Establece el modo del slice. Cambiar de modo reforma los preajustes de filtro y paso automáticamente. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el squelch se desactiva automáticamente para evitar el recorte de caracteres FSK (#2504). Al salir del modo RADE mediante la combinación de modo, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), lo que evita señales de desactivación obsoletas al cambiar de modo en un slice que no es RADE. Seleccionar un modo de radio real también elimina cualquier superposición activa de demodulación de software WFM en este slice. Los modos DSTR y FreeDV se filtran cuando el modelo no los admite. |
| Botón WFM | — | — | Alterna el demodulador de FM por software (WFM) activado o desactivado para este slice. Utiliza DAX IQ a través del cable Hi-Fi. Activo cuando está marcado (fondo verde). Seleccionar cualquier modo de radio real desde la combinación de modo desactiva automáticamente WFM para este slice. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia actual del VFO con agrupación de puntos. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 50000.000 MHz en XVTR, o cuando la entrada supera 54 MHz y es MHz explícito) | Escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar. Admite escala automática de kHz/Hz: las entradas superiores a 54000 se tratan como Hz, y superiores a 54 como kHz (a menos que la entrada sea MHz explícito). En antenas XVTR, se admiten accesos directos de banda de 3 dígitos para 2m/70cm (p. ej., 1446 → 144.6 MHz). Presione Escape para cancelar y restaurar la frecuencia anterior. La entrada de frecuencia utiliza `FrequencyEntryParser::normalizedMhzText()` e `isExplicitMhzEntry()` para un análisis coherente en toda la aplicación. |
| STEP | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian según el modo. Tanto las señales `stepSizeChanged` como `stepSizeChangedByUser` se emiten cuando el usuario cambia el paso. |

### Selección de antena

| Control | Predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles. El menú se completa con la lista de antenas de la radio más cualquier token de antena virtual KiwiSDR del administrador Kiwi. Seleccionar una antena Flex establece la antena RX del slice; seleccionar una antena virtual KiwiSDR enruta al perfil de receptor KiwiSDR asignado. Utiliza ANT1/ANT2 como respaldo cuando la lista está vacía. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas con capacidad TX. Los puertos de antena solo RX (nombres que comienzan con "RX") se filtran. Seleccionar un elemento establece la antena TX. La etiqueta es roja. |

### Filtro

| Control | Predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Preajustes de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como preajuste. Los botones se ocultan en modos FM, NFM y DFM. Los preajustes se almacenan como un valor de ancho simple o un par de banda de paso `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda de filtro actual. Se actualiza cuando se aplica un preajuste o se arrastra la banda de paso. Solo lectura. La lógica de formato se comparte con VfoWidget mediante `RxApplet::formatFilterWidth()` y utiliza lógica según el modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda de paso de filtro | — | — | Arrastre el borde inferior o superior para establecer una banda de paso de filtro personalizada. |
| Ensanchar (acción de acceso directo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de preajustes por modo para ensanchar la banda de paso del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |
| Estrechar (acción de acceso directo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de preajustes por modo para estrechar la banda de paso del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |

### AGC

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta del AGC. Se oculta en los modos de la familia FM. |
| Umbral AGC | 65 | 0–100 | Establece el umbral del AGC. Cuando el modo AGC es Off, ajusta en su lugar el nivel de AGC desactivado. Haga clic derecho en el deslizador para abrir un menú contextual con una opción "Calibrate AGC-T against noise floor…" (deshabilitada mientras una recepción de reemplazo Kiwi esté activa). |

### Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silenciar) | 🔊 (sin silenciar) | — | Un clic silencia/activa el audio de este slice. Doble clic silencia/activa el audio de todos los slices propios. El icono se actualiza solo cuando la radio lo confirma (según la Política de Configuración Autoritativa de la Radio, #2489). La acción de un clic se difiere por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularla. El estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad para el silencio de audio. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. Muestra una información sobre herramientas "X%" con el valor porcentual actual. |
| Panorámica L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Muestra información sobre herramientas "L##", "C" (centro) o "R##". Doble clic para restablecer al centro (50). El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura como referencia visual. |
| SQL / AUTO | Off | Off, SQL (manual), AUTO | Botón de ciclo de tres vías: cada clic avanza Off → SQL (umbral manual) → AUTO (el algoritmo sigue el piso de ruido) → Off. En modo AUTO, el botón muestra 'AUTO' en ámbar; en modo manual, 'SQL' en verde. Deshabilitado (y desactivado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504). Reflejado por un botón idéntico en la pestaña Audio del panel VFO. |
| Nivel de squelch | 20 | Manual: 0–100 (o 0–99 en recepción de reemplazo Kiwi); Auto: margen de 5–20 dB | En modo Manual, ajusta el umbral de squelch (solo tiene efecto cuando el squelch está activado). En modo AUTO, establece el margen en dB por encima del piso de ruido medido donde se abre la puerta, persistido en `AutoSqlMarginDb`. En modo Manual, el nivel es autoritativo de la radio por slice (no persistido); en modo Auto, el margen se persiste. Deshabilitado en modos RTTY y digitales y en modo Off. Haga clic derecho en el deslizador de umbral AGC para la calibración de ruido AGC-T. |

### RIT y XIT

| Control | Predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Activa o desactiva el Sintonizador Incremental de Recepción. |
| RIT 0 | — | Pone a cero el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | off | Activa o desactiva el Sintonizador Incremental de Transmisión. |
| XIT 0 | — | Pone a cero el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Reducción de ruido y botones de filtro DSP

Los siguientes botones de filtro DSP son visibles en modos que no son FM. La disponibilidad de los botones depende de la serie de la radio.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Se oculta en los modos de la familia FM. |
| NR2 | Todas las series | Activa el modo 2 de reducción de ruido. Se oculta en los modos de la familia FM. |
| NB | Todas las series | Activa el eliminador de ruido. Se oculta en los modos de la familia FM. |
| NRL | Todas las series (incluida la serie 6000) | Activa la reducción de ruido (algoritmo NRL). Se oculta en los modos de la familia FM. Disponible en radios de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Se oculta en los modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Se oculta en modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Se oculta en los modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se enciende en ámbar cuando el break-in completo de CW está activo. Se controla desde el applet CW; aquí es solo lectura. |
| Etiqueta de ancho de filtro | p. ej., '2.7K', '3.3K', '500', '6.0K' | Ancho de banda de filtro actual del slice. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del slice es FM, NFM o DFM.

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS en transmisión. |
| Valor de tono CTCSS | — | 67.0–254.1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando el modo de tono es CTCSS TX. |
| Offset (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de offset del repetidor FM. |
| − (offset hacia abajo) | — | — | Establece la frecuencia TX por debajo de la frecuencia RX en la cantidad del offset. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin offset). |
| + (offset hacia arriba) | — | — | Establece la frecuencia TX por encima de la frecuencia RX en la cantidad del offset. |
| REV / XFC | — | REV (alternar) o XFC (momentáneo) | Para operación de repetidor FM, REV invierte el signo del offset TX para trabajar un par de repetidor invertido. En backends que admiten una verificación de frecuencia de transmisión, el botón se reetiqueta como XFC: al presionarlo, mantiene la verificación de frecuencia de transmisión durante la duración de la presión y, mientras está presionado, fuerza brevemente la radio hacia la frecuencia de transmisión para confirmar la cobertura. El XFC mantenido se libera al ocultar, desactivar, cambio de capacidad o desconexión. |

## Pestaña Peripherals — conexión IP manual

La pestaña Peripherals en el diálogo Radio Setup le permite conectarse manualmente a dispositivos externos mediante dirección IP. Están disponibles las siguientes filas.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados.
