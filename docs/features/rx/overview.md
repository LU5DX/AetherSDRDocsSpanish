# Resumen de controles RX

El applet Controles RX le ofrece control por segmento sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, CAG, audio, silenciador, RIT/XIT y configuración de repetidor FM. Ábralo cuando necesite configurar cómo un segmento recibe o transmite.

## Cómo funciona

El applet RX está siempre presente en el Panel de applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja RX. Cuando la radio admite más de un segmento, aparece una fila de pestañas de segmento (A a H) en la parte superior; al hacer clic en una pestaña, se vincula el applet a ese segmento. Todos los controles debajo de la fila de pestañas afectan únicamente al segmento seleccionado actualmente.

Las preconfiguraciones de ancho de filtro son el único parámetro que persiste entre sesiones y se almacenan bajo la clave `FilterPresets`. El resto de controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del segmento

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Pestañas de segmento (A..H) | — | Selecciona qué segmento controla el applet. La fila de pestañas se oculta cuando la radio tiene solo un segmento. Los bordes de los botones y los fondos activos siguen el color por segmento configurado en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de segmento estática. Las conexiones de clic en los botones de segmento están protegidas contra manejadores de señal duplicados entre reconexiones (v0.9.5.1, #2254). |
| Insignia de segmento | A | Muestra la letra del segmento activo. La letra del segmento se puede representar como HTML (#2606). El color está controlado por SliceColorManager; los colores personalizables por segmento persisten entre sesiones y se reflejan aquí, en los botones de pestaña de segmento, los widgets de VFO y las barras de medidor. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía. Un segmento bloqueado ignora los cambios de frecuencia del panadapter y otras fuentes. |
| TX (insignia) | — | Haga clic para designar este segmento como el segmento de TX. |

### Frecuencia y modo

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Menú desplegable de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si la marca de compilación HAVE_RADE está configurada) | Establece el modo del segmento. Cambiar el modo reconfigura automáticamente las preconfiguraciones de filtro y paso. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el silenciador se desactiva automáticamente para evitar que se eliminen los caracteres FSK (#2504). Al salir del modo RADE mediante el menú desplegable de modo, el applet emite `radeActivated(false)` solo si el segmento estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un segmento que no es RADE. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia actual del VFO con agrupación por puntos. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0,001–54.000 MHz (hasta 50000.000 MHz en XVTR, o cuando la entrada supera 54 MHz y es MHz explícito) | Escriba una frecuencia en MHz y presione Intro para sintonizar y volver a centrar. Admite escalado automático de kHz/Hz: las entradas superiores a 54000 se tratan como Hz, las superiores a 54 como kHz (a menos que la entrada sea MHz explícito). En antenas XVTR, se admiten accesos directos de banda de 2 m/70 cm de 3 dígitos (ej. 1446 → 144,6 MHz). Presione Escape para cancelar y restaurar la frecuencia anterior. La entrada de frecuencia usa `FrequencyEntryParser::normalizedMhzText()` y `isExplicitMhzEntry()` para un análisis coherente en toda la aplicación. |
| PASO | 100 Hz | Lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian con el modo. |

### Selección de antena

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles. El menú se completa desde `rxAntennaList()` del segmento si está disponible; de lo contrario, desde la lista de antenas de la radio. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Al seleccionar un elemento, se establece la antena RX usando el nombre completo de la antena. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas capaces de TX. Solo se incluyen antenas cuyos nombres comienzan con "ANT", "TX" o "XVTR"; los puertos solo RX (nombres que comienzan con "RX") quedan excluidos. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas y la sugerencia de estado. Al seleccionar un elemento, se establece la antena TX usando el nombre completo de la antena. La etiqueta es roja. |

### Filtro

| Control | Valor predeterminado / rango | Clave de ajuste | Comportamiento |
|---|---|---|---|
| Preconfiguraciones de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como una preconfiguración. Los botones están ocultos en modos FM, NFM y DFM. Las preconfiguraciones se almacenan como un valor de ancho simple o un par de banda de paso `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica una preconfiguración o se arrastra la banda de paso. Solo lectura. La lógica de formato se comparte con VfoWidget mediante `RxApplet::formatFilterWidth()` y utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda de paso del filtro | — | — | Arrastre el borde inferior o superior para establecer una banda de paso de filtro personalizada. |
| Ampliar (acción de acceso directo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de preconfiguraciones por modo para ampliar la banda de paso del filtro con geometría de borde correcta para el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |
| Reducir (acción de acceso directo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de preconfiguraciones por modo para reducir la banda de paso del filtro con geometría de borde correcta para el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |

### CAG

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo CAG | Med | Apagado, Lento, Med, Rápido | Establece la velocidad de respuesta del CAG. Oculto en modos de la familia FM. |
| Umbral CAG | 65 | 0–100 | Establece el umbral del CAG. Cuando el modo CAG está en Apagado, ajusta el nivel de CAG desactivado en su lugar. |

### Audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (con audio) | — | Un solo clic silencia/activa el audio de este segmento. Doble clic silencia/activa el audio de todos los segmentos propios. El ícono se actualiza solo cuando la radio lo confirma (según la Política de ajustes con autoridad de la radio, #2489). La acción de un solo clic se retrasa por el intervalo de doble clic de la plataforma (~400 ms predeterminado) para que un doble clic pueda anularlo. El estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad para el silencio de audio. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del segmento. Muestra una información sobre herramientas "X%" con el valor porcentual actual. |
| Balance L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Muestra información sobre herramientas "L##", "C" (centro) o "R##". Doble clic para restablecer al centro (50). |
| SQL | — | — | Activa el silenciador al nivel establecido por el control deslizante de silenciador. Desactivado y forzado a apagado en modos RTTY y digitales (DIGU, DIGL) donde el silenciador eliminaría los caracteres FSK (#2504). |
| Nivel de silenciador | 20 | 0–100 | Establece el umbral del silenciador. Solo tiene efecto cuando SQL está activado. El nivel de silenciador manual persiste entre sesiones en el cliente como `LastManualSquelchLevel` — esto conserva su preferencia entre ciclos de modo e inicios, ya que el modo automático puede sobrescribir el valor de silenciador del segmento. |

### RIT y XIT

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| RIT | Apagado | Activa o desactiva la sintonización incremental de recepción. |
| RIT 0 | — | Pone a cero el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | Apagado | Activa o desactiva la sintonización incremental de transmisión. |
| XIT 0 | — | Pone a cero el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Botones de reducción de ruido y filtro DSP

Los siguientes botones de filtro DSP son visibles en modos que no son FM. La disponibilidad del botón depende de la serie de la radio.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Oculto en modos de la familia FM. |
| NR2 | Todas las series | Activa el modo 2 de reducción de ruido. Oculto en modos de la familia FM. |
| NB | Todas las series | Activa el eliminador de ruido. Oculto en modos de la familia FM. |
| NRL | Todas las series (incluyendo serie 6000) | Activa la reducción de ruido (algoritmo NRL). Oculto en modos de la familia FM. Disponible en radios de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Oculto en modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Oculto en modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Oculto en modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando la interrupción total de CW está activa. Controlado desde el applet CW; solo lectura aquí. |
| Etiqueta de ancho de filtro | ej. '2.7K', '3.3K', '500', '6.0K' | Ancho de banda del filtro del segmento actual. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del segmento es FM, NFM o DFM.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Apagado | Apagado, CTCSS TX | Selecciona si se envía un tono CTCSS en la transmisión. |
| Valor del tono CTCSS | — | 67,0–254,1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0,0 MHz | 0,0–100,0 MHz (paso 0,1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia de TX por debajo de la frecuencia de RX en la cantidad de desplazamiento. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia de TX por encima de la frecuencia de RX en la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar un par de repetidores invertido. |

## Pestaña Periféricos — conexión IP manual

La pestaña Periféricos en el cuadro de diálogo Configuración de radio le permite conectarse manualmente a dispositivos externos por dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Conectado" se muestra solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es realmente a un ShackSwitch, la fila AG se muestra como desconectada y la fila ShackSwitch se muestra como conectada en su lugar.

### ShackSwitch — fila 4 (añadido en V0.9.4)

| Control | Clave de ajuste | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Campo de dirección IP | `SS_ManualIp` | — | Introduzca la dirección IP del ShackSwitch. |
| Campo de puerto | `SS_ControlPort` | 9007 | Puerto utilizado para el protocolo de control AG. Siempre se conecta en el puerto 9007 independientemente del valor introducido. |
| Botón Conectar | — | — | Se conecta al ShackSwitch en la IP especificada en el puerto 9007 usando el protocolo de control AG. |
| Botón Desconectar | — | — | Se desconecta del ShackSwitch. |
| Estado Conectado | — | — | Muestra "Conectado" solo cuando la conexión activa es a un dispositivo ShackSwitch. |
| Botón ⚙ Interfaz web | `SS_ManualIp`, `SS_WebPort` | puerto 5000 | Abre la interfaz web del ShackSwitch en su navegador. Usa la dirección del par activo si un ShackSwitch está actualmente conectado. Usa `SS_WebPort` de
