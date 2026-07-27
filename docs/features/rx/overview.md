# Descripción de los controles RX

El applet de Controles RX le ofrece control por slice sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, CAG, audio, silenciador, RIT/XIT y ajustes de repetidor FM. Ábralo siempre que necesite configurar cómo recibe o transmite un slice.

## Cómo funciona

El applet RX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja RX. Cuando la radio admite más de un slice, aparece una fila de pestañas de slice (A a H) en la parte superior; al hacer clic en una pestaña, el applet se vincula a ese slice. Todos los controles debajo de la fila de pestañas afectan únicamente al slice seleccionado actualmente.

Los preajustes de ancho de filtro son la única configuración que persiste entre sesiones y se almacenan bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del slice

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona qué slice controla el applet. La fila de pestañas se oculta cuando la radio tiene solo un slice. Los bordes de los botones y los fondos activos siguen el color por slice establecido en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de slice estática. Las conexiones de clic en los botones de slice están protegidas contra manejadores de señal duplicados en reconexiones (v0.9.5.1, #2254). |
| Insignia de slice | A | Muestra la letra del slice activo. La letra del slice puede mostrarse como HTML (#2606). El color lo gestiona SliceColorManager; los colores personalizables por slice persisten entre sesiones y se reflejan aquí, en los botones de pestaña de slice, los widgets VFO y las barras de medidor. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia del panadapter y de otras fuentes. |
| TX (insignia) | — | Haga clic para designar este slice como el slice de TX. |

### Frecuencia y modo

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Combo de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si la marca de compilación HAVE_RADE está activa) | Establece el modo del slice. Cambiar el modo reconfigura automáticamente los preajustes de filtro y paso. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el silenciador se desactiva automáticamente para evitar eliminar caracteres FSK (#2504). Al salir del modo RADE mediante el combo de modo, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE. Seleccionar un modo de radio real también elimina cualquier superposición activa de demodulación por software WFM en este slice. |
| Botón WFM | — | — | Activa o desactiva el demodulador FM por software (WFM) para este slice. Utiliza DAX IQ a través de Hi-Fi Cable. Activo cuando está marcado (fondo verde). Seleccionar cualquier modo de radio real desde el combo de modo desactiva automáticamente WFM para este slice. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0,001–54,000 MHz (hasta 50000,000 MHz en XVTR, o cuando la entrada supera 54 MHz y es MHz explícito) | Escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar. Admite escalado automático de kHz/Hz: las entradas superiores a 54000 se tratan como Hz, las superiores a 54 como kHz (a menos que la entrada sea MHz explícito). En antenas XVTR, se admiten accesos directos de 3 dígitos para bandas de 2m/70cm (p. ej., 1446 → 144,6 MHz). Presione Escape para cancelar y restaurar la frecuencia anterior. La entrada de frecuencia utiliza `FrequencyEntryParser::normalizedMhzText()` e `isExplicitMhzEntry()` para un análisis consistente en toda la aplicación. |
| PASO | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian según el modo. Tanto la señal `stepSizeChanged` como `stepSizeChangedByUser` se emiten cuando el usuario cambia el paso. |

### Selección de antena

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles. El menú se completa con la `rxAntennaList()` del slice si está disponible; de lo contrario, con la lista de antenas de la radio. Cuando KiwiSDR está activo, también se añaden tokens de antena virtual de KiwiSDRManager. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Seleccionar una antena virtual KiwiSDR emite `kiwiRxAntennaSelected` con el ID del slice y el ID del perfil. Seleccionar una antena Flex emite `flexRxAntennaSelected` y llama a `slice->setRxAntenna()`. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas con capacidad TX. Solo se incluyen antenas con nombres que comienzan con "ANT", "TX" o "XVTR"; los puertos solo RX (nombres que comienzan con "RX") quedan excluidos. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Seleccionar un elemento establece la antena TX usando el nombre completo de la antena. La etiqueta es roja. |

### Filtro

| Control | Valor predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Preajustes de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400/500/600 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como preajuste. Los botones se ocultan en modos FM, NFM y DFM. El modo CW ahora incluye preajustes de 500 Hz y 600 Hz. Los preajustes se almacenan como un valor de ancho simple o como un par de banda pasante `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2,7K | — | Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica un preajuste o se arrastra la banda pasante. Solo lectura. La lógica de formato se comparte con VfoWidget a través de `RxApplet::formatFilterWidth()` y usa lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda pasante del filtro | — | — | Arrastre el borde inferior o superior para establecer una banda pasante de filtro personalizada. |
| Ampliar (acción de acceso directo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de preajustes por modo para ampliar la banda pasante del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |
| Reducir (acción de acceso directo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de preajustes por modo para reducir la banda pasante del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |

### CAG

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo CAG | Med | Desactivado, Lento, Med, Rápido | Establece la velocidad de respuesta del CAG. Oculto en modos de la familia FM. |
| Umbral CAG | 65 | 0–100 | Establece el umbral del CAG. Cuando el modo CAG está en Desactivado, ajusta el nivel de CAG desactivado. Haga clic derecho en el control deslizante para abrir un menú contextual con una opción "Calibrar CAG-T contra el nivel de ruido…" (la información sobre herramientas también anuncia esta acción). |

### Audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (sin silenciar) | — | Un solo clic silencia/activa el sonido de este slice. Doble clic silencia/activa el sonido de todos los slices propios. El icono se actualiza solo cuando la radio lo confirma (según la Política de Configuración Autoritativa de la Radio, #2489). La acción de un solo clic se difiere por el intervalo de doble clic de la plataforma (predeterminado ~400 ms) para que un doble clic pueda anularla. El estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad para el silencio de audio. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. Muestra una información sobre herramientas "X%" con el valor porcentual actual. |
| Panorámica L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Muestra información sobre herramientas "L##", "C" (centro) o "R##". Doble clic para restablecer al centro (50). El control deslizante se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura como referencia visual. |
| SQL | — | — | Activa el silenciador al nivel establecido por el control deslizante de silenciador. Desactivado y forzado a apagado en modos RTTY y digitales (DIGU, DIGL) donde el silenciador eliminaría caracteres FSK (#2504). |
| Nivel de silenciador | 20 | 0–100 | Establece el umbral del silenciador. Solo tiene efecto cuando SQL está activado. El nivel de silenciador manual persiste entre sesiones en el lado del cliente como `LastManualSquelchLevel` — esto conserva su preferencia entre ciclos de modo e inicios, ya que el modo automático puede sobrescribir el valor de silenciador del slice. |

### RIT y XIT

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| RIT | desactivado | Activa o desactiva la Sintonización Incremental de Recepción. |
| RIT 0 | — | Pone a cero el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | desactivado | Activa o desactiva la Sintonización Incremental de Transmisión. |
| XIT 0 | — | Pone a cero el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Reducción de ruido y botones de filtro DSP

Los siguientes botones de filtro DSP son visibles en modos que no son FM. La disponibilidad de los botones depende de la serie de la radio.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Oculto en modos de la familia FM. |
| NR2 | Todas las series | Activa la reducción de ruido modo 2. Oculto en modos de la familia FM. |
| NB | Todas las series | Activa el eliminador de ruido. Oculto en modos de la familia FM. |
| NRL | Todas las series (incluye serie 6000) | Activa la reducción de ruido (algoritmo NRL). Oculto en modos de la familia FM. Disponible en radios de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Oculto en modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Oculto en modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Oculto en modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando el break-in completo de CW está activo. Controlado desde el applet CW; aquí es solo lectura. |
| Etiqueta de ancho de filtro | p. ej., '2,7K', '3,3K', '500', '6,0K' | Ancho de banda del filtro del slice actual. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del slice es FM, NFM o DFM.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Desactivado | Desactivado, CTCSS TX | Selecciona si se envía un tono CTCSS en transmisión. |
| Valor de tono CTCSS | — | 67,0–254,1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0,0 MHz | 0,0–100,0 MHz (paso 0,1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia TX por debajo de la frecuencia RX en la cantidad de desplazamiento. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia TX por encima de la frecuencia RX en la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar con un par de repetidor invertido. |

## Pestaña Periféricos — conexión IP manual

La pestaña Periféricos en el diálogo de Configuración de Radio le permite conectarse manualmente a dispositivos externos por dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Conectado" se muestra solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es en realidad a un ShackSwitch, la fila AG se muestra como desconectada y la fila ShackSwitch se muestra como conectada en su lugar.

### ShackSwitch — fila 4 (añadido en V
