# Resumen de controles de RX

El applet de Controles de RX le brinda control por segmento sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, AGC, audio, silenciador, RIT/XIT y configuración de repetidor FM. Ábralo siempre que necesite configurar cómo un segmento recibe o transmite.

## Cómo funciona

El applet RX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja RX. Cuando la radio admite más de un segmento, aparece una fila de pestañas de segmento (A a H) en la parte superior; al hacer clic en una pestaña se vincula el applet a ese segmento. Todos los controles debajo de la fila de pestañas afectan únicamente al segmento seleccionado actualmente.

Las predefiniciones de ancho de filtro son la única configuración que persiste entre sesiones y se almacenan bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del segmento

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Pestañas de segmento (A..H) | — | Seleccionan qué segmento controla el applet. La fila de pestañas se oculta cuando la radio tiene un solo segmento. Los bordes de los botones y los fondos activos siguen el color por segmento establecido en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de segmento estática. Las conexiones de clic en los botones de segmento están protegidas contra manejadores de señal duplicados en reconexiones (v0.9.5.1, #2254). |
| Insignia de segmento | A | Muestra la letra del segmento activo. La letra del segmento puede representarse como HTML (#2606). El color lo define SliceColorManager; los colores personalizables por segmento persisten entre sesiones y se reflejan aquí, en los botones de pestaña de segmento, los widgets VFO y las barras de medidor. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía. Un segmento bloqueado ignora los cambios de frecuencia provenientes del panadapter y otras fuentes. |
| TX (insignia) | — | Haga clic para designar este segmento como el segmento de TX. |

### Frecuencia y modo

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Combo Modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si el indicador de compilación HAVE_RADE está activado) | Establece el modo del segmento. Cambiar de modo reconfigura automáticamente las predefiniciones de filtro y paso. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el silenciador se desactiva automáticamente para evitar que se recorten los caracteres FSK (#2504). Al cambiar del modo RADE mediante el combo Modo, el applet emite `radeActivated(false)` solo si el segmento estaba realmente en RADE (#2376), lo que evita señales de desactivación obsoletas al cambiar de modo en un segmento que no es RADE. Seleccionar un modo de radio real también elimina cualquier superposición activa de demodulación por software WFM en este segmento. |
| Botón WFM | — | — | Alterna el demodulador de FM por software (WFM) activado o desactivado para este segmento. Utiliza IQ de DAX a través del Cable Hi-Fi. Activo cuando está marcado (fondo verde). Seleccionar cualquier modo de radio real del combo Modo desactiva automáticamente WFM para este segmento. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 50000.000 MHz en XVTR, o cuando la entrada supera 54 MHz y es MHz explícito) | Escriba una frecuencia en MHz y presione Enter para sintonizar y re-centrar. Admite escalado automático de kHz/Hz: las entradas superiores a 54000 se tratan como Hz, superiores a 54 como kHz (a menos que la entrada sea MHz explícito). En antenas XVTR, se admiten accesos directos de 3 dígitos para bandas de 2 m/70 cm (p. ej., 1446 → 144.6 MHz). Presione Escape para cancelar y restaurar la frecuencia anterior. La entrada de frecuencia utiliza `FrequencyEntryParser::normalizedMhzText()` e `isExplicitMhzEntry()` para un análisis coherente en toda la aplicación. |
| PASO | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian con el modo. Tanto la señal `stepSizeChanged` como `stepSizeChangedByUser` se emiten cuando el usuario cambia el paso. |

### Selección de antena

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles. El menú se completa con la lista `rxAntennaList()` del segmento si está disponible; de lo contrario, con la lista de antenas de la radio. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Seleccionar un elemento establece la antena RX usando el nombre completo de la antena. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas capaces de TX. Solo se incluyen antenas cuyos nombres comiencen con "ANT", "TX" o "XVTR"; los puertos solo RX (nombres que comiencen con "RX") quedan excluidos. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Seleccionar un elemento establece la antena TX usando el nombre completo de la antena. La etiqueta es roja. |

### Filtro

| Control | Valor predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Predefiniciones de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como predefinición. Los botones se ocultan en modos FM, NFM y DFM. Las predefiniciones se almacenan como un valor de ancho simple o como un par de banda de paso `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica una predefinición o se arrastra la banda de paso. Solo lectura. La lógica de formato se comparte con VfoWidget a través de `RxApplet::formatFilterWidth()` y utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda de paso de filtro | — | — | Arrastre el borde inferior o superior para establecer una banda de paso de filtro personalizada. |
| Ampliar (acción de acceso directo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de predefiniciones por modo para ampliar la banda de paso del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |
| Reducir (acción de acceso directo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de predefiniciones por modo para reducir la banda de paso del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |

### AGC

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta del AGC. Oculto en modos de la familia FM. |
| Umbral AGC | 65 | 0–100 | Establece el umbral del AGC. Cuando el modo AGC está en Off, ajusta el nivel de apagado del AGC en su lugar. Haga clic derecho en el control deslizante para abrir un menú contextual con la opción "Calibrar AGC-T contra el piso de ruido…" (la información sobre herramientas también anuncia esta acción). |

### Audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (sin silenciar) | — | Un solo clic silencia/activa el sonido de este segmento. Doble clic silencia/activa el sonido de todos los segmentos propietarios. El ícono se actualiza solo cuando la radio lo confirma (según la Política de Configuración Autoritativa de la Radio, #2489). La acción de un solo clic se difiere por el intervalo de doble clic de la plataforma (~400 ms predeterminado) para que un doble clic pueda anularlo. El estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del segmento. Muestra una información sobre herramientas "X%" con el valor porcentual actual. |
| Panorámica L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Muestra información sobre herramientas "L##", "C" (centro) o "R##". Doble clic para restablecer al centro (50). El relleno del control deslizante se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura para referencia visual. |
| SQL | — | — | Activa el silenciador al nivel establecido por el control deslizante de silenciador. Desactivado y forzado a apagado en modos RTTY y digitales (DIGU, DIGL), donde el silenciador recortaría los caracteres FSK (#2504). |
| Nivel de silenciador | 20 | 0–100 | Establece el umbral del silenciador. Solo tiene efecto cuando SQL está activado. El nivel de silenciador manual persiste entre sesiones en el lado del cliente como `LastManualSquelchLevel` — esto conserva su preferencia a través de ciclos de modo e inicios, ya que el modo automático puede sobrescribir el valor de silenciador del segmento. |

### RIT y XIT

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Alterna la Sintonización Incremental de Recepción activada o desactivada. |
| RIT 0 | — | Pone a cero el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | off | Alterna la Sintonización Incremental de Transmisión activada o desactivada. |
| XIT 0 | — | Pone a cero el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Botones de reducción de ruido y filtro DSP

Los siguientes botones de filtro DSP son visibles en modos que no son FM. La disponibilidad de los botones depende de la serie de la radio.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Oculto en modos de la familia FM. |
| NR2 | Todas las series | Activa el modo de reducción de ruido 2. Oculto en modos de la familia FM. |
| NB | Todas las series | Activa el eliminador de ruido. Oculto en modos de la familia FM. |
| NRL | Todas las series (incluyendo la serie 6000) | Activa la reducción de ruido (algoritmo NRL). Oculto en modos de la familia FM. Disponible en radios de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Oculto en modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Oculto en modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Oculto en modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando la interrupción total de CW está activa. Controlado desde el applet CW; solo lectura aquí. |
| Etiqueta de ancho de filtro | p. ej., '2.7K', '3.3K', '500', '6.0K' | Ancho de banda del filtro del segmento actual. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del segmento es FM, NFM o DFM.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS en transmisión. |
| Valor de tono CTCSS | — | 67.0–254.1 Hz (41 tonos EIA/TIA-603 estándar) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia de TX por debajo de la frecuencia de RX en la cantidad de desplazamiento. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia de TX por encima de la frecuencia de RX en la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar con un par de repetidores invertido. |

## Pestaña Periféricos — conexión IP manual

La pestaña Periféricos en el cuadro de diálogo Configuración de Radio le permite conectarse manualmente a dispositivos externos por dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Conectado" se muestra solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es en realidad a un ShackSwitch, la fila AG se muestra como desconectada y la fila ShackSwitch se muestra como conectada en su lugar.

### ShackSwitch — fila 4 (añadido en V0.9.4)

| Control | Clave de configuración | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Campo de dirección IP |
