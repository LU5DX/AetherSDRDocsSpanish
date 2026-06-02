# Resumen de controles RX

El applet de Controles RX le brinda control por slice sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, AGC, audio, silenciador, RIT/XIT y configuraciones de repetidor FM. Ábralo siempre que necesite configurar cómo un slice recibe o transmite.

## Cómo funciona

El applet RX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja RX. Cuando la radio admite más de un slice, aparece una fila de pestañas de slice (A a la H) en la parte superior; al hacer clic en una pestaña, se vincula el applet a ese slice. Todos los controles debajo de la fila de pestañas afectan únicamente al slice seleccionado actualmente.

Las preconfiguraciones de ancho de filtro son la única configuración que persiste entre sesiones y se almacenan bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del slice

| Control | Predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona qué slice controla el applet. La fila de pestañas se oculta cuando la radio tiene solo un slice. Los bordes de los botones y los fondos activos siguen el color por slice definido en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de slice estática. Las conexiones de clic en los botones de slice están protegidas contra controladores de señal duplicados en las reconexiones (v0.9.5.1, #2254). |
| Insignia de slice | A | Muestra la letra del slice activo. La letra del slice puede renderizarse como HTML (#2606). El color lo define SliceColorManager; los colores personalizables por slice persisten entre sesiones y se reflejan aquí, en los botones de pestaña de slice, los widgets VFO y las tiras de medidor. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia provenientes del panadapter y otras fuentes. |
| TX (insignia) | — | Haga clic para designar este slice como el slice de TX. |

### Frecuencia y modo

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Combo de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si la marca de compilación HAVE_RADE está configurada) | Establece el modo del slice. Cambiar de modo reconfigura automáticamente las preconfiguraciones de filtro y paso. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el silenciador se desactiva automáticamente para evitar eliminar caracteres FSK (#2504). Al salir del modo RADE mediante el combo de modo, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia actual del VFO con agrupación por puntos. Haga clic para ingresar al modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 50000.000 MHz en XVTR, o cuando la entrada supera 54 MHz y es MHz explícito) | Escriba una frecuencia en MHz y presione Enter para sintonizar y volver a centrar. Admite escalado automático de kHz/Hz: las entradas superiores a 54000 se tratan como Hz, las superiores a 54 como kHz (a menos que la entrada sea MHz explícito). En antenas XVTR, se admiten accesos directos de banda de 2m/70cm de 3 dígitos (p. ej., 1446 → 144.6 MHz). Presione Escape para cancelar y restaurar la frecuencia anterior. La entrada de frecuencia usa `FrequencyEntryParser::normalizedMhzText()` y `isExplicitMhzEntry()` para un análisis consistente en toda la aplicación. |
| PASO | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian según el modo. |

### Selección de antena

| Control | Predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles. El menú se completa desde `rxAntennaList()` del slice si está disponible; de lo contrario, desde la lista de antenas de la radio. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Al seleccionar un elemento, se establece la antena RX usando el nombre completo de la antena. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas capaces de TX. Solo se incluyen antenas cuyos nombres comienzan con "ANT", "TX" o "XVTR"; los puertos solo RX (nombres que comienzan con "RX") quedan excluidos. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Al seleccionar un elemento, se establece la antena TX usando el nombre completo de la antena. La etiqueta es roja. |

### Filtro

| Control | Predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Preconfiguraciones de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como una preconfiguración. Los botones se ocultan en modos FM, NFM y DFM. Las preconfiguraciones se almacenan como un valor de ancho simple o un par de banda de paso `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica una preconfiguración o se arrastra la banda de paso. Solo lectura. La lógica de formato se comparte con VfoWidget a través de `RxApplet::formatFilterWidth()` y utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda de paso del filtro | — | — | Arrastre el borde inferior o superior para establecer una banda de paso de filtro personalizada. |
| Ampliar (acción de acceso directo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de preconfiguraciones por modo para ampliar la banda de paso del filtro con una geometría de borde correcta para el modo. Accesible mediante acceso directo de teclado (v0.9.8, #2208). |
| Reducir (acción de acceso directo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de preconfiguraciones por modo para reducir la banda de paso del filtro con una geometría de borde correcta para el modo. Accesible mediante acceso directo de teclado (v0.9.8, #2208). |

### AGC

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta del AGC. Oculto en modos de la familia FM. |
| Umbral AGC | 65 | 0–100 | Establece el umbral del AGC. Cuando el modo AGC está en Off, ajusta el nivel de AGC desactivado en su lugar. |

### Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (sin silenciar) | — | Un solo clic silencia/reactiva el sonido de este slice. Doble clic silencia/reactiva el sonido de todos los slices propios. El icono se actualiza solo cuando la radio lo confirma (según la Política de Configuración Autoritativa de la Radio, #2489). La acción de un solo clic se aplaza por el intervalo de doble clic de la plataforma (predeterminado ~400 ms) para que un doble clic pueda anularlo. El estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad para el silencio de audio. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. Muestra una información sobre herramientas "X%" con el valor porcentual actual. |
| Panorámica L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Muestra información sobre herramientas "L##", "C" (centro) o "R##". Haga doble clic para restablecer al centro (50). El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura como referencia visual. |
| SQL | — | — | Activa el silenciador al nivel establecido por el deslizador de silenciador. Desactivado y forzado a apagado en modos RTTY y digitales (DIGU, DIGL) donde el silenciador eliminaría los caracteres FSK (#2504). |
| Nivel de silenciador | 20 | 0–100 | Establece el umbral del silenciador. Solo tiene efecto cuando SQL está activado. El nivel de silenciador manual persiste entre sesiones en el lado del cliente como `LastManualSquelchLevel`; esto preserva su preferencia a través de ciclos de modo e inicios, ya que el modo automático puede sobrescribir el valor de silenciador del slice. |

### RIT y XIT

| Control | Predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Activa o desactiva la Sintonización Incremental de Recepción. |
| RIT 0 | — | Pone a cero el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | off | Activa o desactiva la Sintonización Incremental de Transmisión. |
| XIT 0 | — | Pone a cero el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Reducción de ruido y botones de filtro DSP

Los siguientes botones de filtro DSP son visibles en modos que no son FM. La disponibilidad del botón depende de la serie de la radio.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Oculto en modos de la familia FM. |
| NR2 | Todas las series | Activa el modo de reducción de ruido 2. Oculto en modos de la familia FM. |
| NB | Todas las series | Activa el eliminador de ruido. Oculto en modos de la familia FM. |
| NRL | Todas las series (incluida la serie 6000) | Activa la reducción de ruido (algoritmo NRL). Oculto en modos de la familia FM. Disponible en radios de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Oculto en modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Oculto en modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Oculto en modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando el full break-in de CW está activo. Controlado desde el applet CW; aquí es solo lectura. |
| Etiqueta de ancho de filtro | p. ej., '2.7K', '3.3K', '500', '6.0K' | Ancho de banda del filtro del slice actual. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del slice es FM, NFM o DFM.

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS en transmisión. |
| Valor de tono CTCSS | — | 67.0–254.1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia de TX por debajo de la frecuencia de RX en la cantidad de desplazamiento. |
| Símplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia de TX por encima de la frecuencia de RX en la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar con un par de repetidor invertido. |

## Pestaña Periféricos — conexión IP manual

La pestaña Periféricos en el diálogo Configuración de Radio le permite conectarse manualmente a dispositivos externos mediante dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Conectado" se muestra solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es realmente a un ShackSwitch, la fila AG se muestra como desconectada y la fila ShackSwitch se muestra como conectada en su lugar.

### ShackSwitch — fila 4 (añadido en V0.9.4)

| Control | Clave de configuración | Predeterminado | Comportamiento |
|---|---|---|---|
| Campo de dirección IP | `SS_ManualIp` | — | Ingrese la dirección IP del ShackSwitch. |
| Campo de puerto | `SS_ControlPort` | 9007 | Puerto utilizado para el protocolo de control AG. Siempre se conecta en el puerto 9007 independientemente del valor ingresado. |
| Botón Conectar | — | — | Se conecta al ShackSwitch en la IP especificada en el puerto 9007 usando el protocolo de control AG. |
| Botón Desconectar | — | — | Se desconecta del ShackSwitch. |
| Estado Conectado | — | — | Muestra "Conectado" solo cuando la conexión activa es a un dispositivo ShackSwitch. |
| Botón ⚙ Interfaz web | `SS_ManualIp`, `SS_WebPort` | puerto 5000 | Abre la interfaz web del ShackSwitch en su navegador. Utiliza la dirección del peer activo si un ShackSwitch está actualmente conectado. Utiliza `SS_WebPort` de la configuración
