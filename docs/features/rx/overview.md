# Descripción general de controles RX

El applet Controles RX le brinda control por segmento sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, AGC, audio, silenciador, RIT/XIT y configuración de repetidor FM. Ábralo cuando necesite configurar cómo un segmento recibe o transmite.

## Cómo funciona

El applet RX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja RX. Cuando la radio admite más de un segmento, aparece una fila de pestañas de segmento (A a H) en la parte superior; al hacer clic en una pestaña, el applet se vincula a ese segmento. Todos los controles debajo de la fila de pestañas afectan únicamente al segmento seleccionado actualmente.

Los preajustes de ancho de filtro son la única configuración que persiste entre sesiones y se almacena bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del segmento

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Pestañas de segmento (A..H) | — | Selecciona qué segmento controla el applet. La fila de pestañas se oculta cuando la radio tiene solo un segmento. Los bordes de los botones y los fondos activos siguen el color por segmento configurado en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de segmento estática. Las conexiones de clic en los botones de segmento están protegidas contra manejadores de señal duplicados durante reconexiones (v0.9.5.1, #2254). |
| Insignia de segmento | A | Muestra la letra del segmento activo. El color lo controla SliceColorManager; los colores por segmento personalizables persisten entre sesiones y se reflejan aquí, en los botones de pestaña de segmento, los widgets VFO y las tiras de medidores. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía. Un segmento bloqueado ignora los cambios de frecuencia del panadapter y otras fuentes. |
| TX (insignia) | — | Haga clic para designar este segmento como el segmento de TX. |

### Frecuencia y modo

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Combo de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, NT, RTTY (+ RADE si el indicador de compilación HAVE_RADE está configurado) | Establece el modo del segmento. Cambiar el modo reajusta automáticamente los preajustes de filtro y paso. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el silenciador se desactiva automáticamente para evitar que se recorten los caracteres FSK (#2504). |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para ingresar al modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 450.000 MHz en XVTR) | Escriba una frecuencia en MHz y presione Enter para sintonizar y volver a centrar. Presione Escape para cancelar y restaurar la frecuencia anterior. |
| PASO | 100 Hz | Lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian según el modo. |

### Selección de antena

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles de la lista de antenas de la radio. Seleccione para configurar la antena RX para este segmento. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas capaces de TX. Los puertos solo RX (nombres que comienzan con `RX`) están excluidos. La etiqueta es roja. |

### Filtro

| Control | Valor predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Preajustes de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como un preajuste. Los botones se ocultan en modos FM, NFM y DFM. Los preajustes se almacenan como un valor de ancho simple o un par de banda de paso `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica un preajuste o se arrastra la banda de paso. Solo lectura. La lógica de formato se comparte con VfoWidget a través de `RxApplet::formatFilterWidth()` y utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda de paso del filtro | — | — | Arrastre el borde inferior o superior para configurar una banda de paso de filtro personalizada. |
| Anchar (acción de acceso directo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de preajustes por modo para anchar la banda de paso del filtro con geometría de borde correcta para el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |
| Estrechar (acción de acceso directo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de preajustes por modo para estrechar la banda de paso del filtro con geometría de borde correcta para el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |

### AGC

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta del AGC. Oculto en modos de la familia FM. |
| Umbral AGC | 65 | 0–100 | Establece el umbral del AGC. Cuando el modo AGC es Off, ajusta en su lugar el nivel de AGC desactivado. |

### Audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silenciar) | 🔊 (sin silenciar) | — | Silencia o reactiva la salida de audio del segmento. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del segmento. |
| Pan L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Haga doble clic para restablecer al centro (50). |
| SQL | — | — | Activa el silenciador al nivel establecido por el deslizador de silenciador. Desactivado y forzado a apagado en modos DIGU, DIGL, NT, RTTY, CW y CWL. RTTY se agregó a la lista de desactivados en v26.5.1 (#2504) para evitar que se recorten los caracteres FSK. |
| Nivel de silenciador | 20 | 0–100 | Establece el umbral del silenciador. Solo tiene efecto cuando SQL está activado. |

### RIT y XIT

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Activa o desactiva la Sintonización Incremental de Recepción. |
| RIT 0 | — | Pone a cero el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | off | Activa o desactiva la Sintonización Incremental de Transmisión. |
| XIT 0 | — | Pone a cero el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Botones de reducción de ruido y filtro DSP

Los siguientes botones de filtro DSP son visibles en modos que no son FM. La disponibilidad de los botones depende de la serie de la radio.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Oculto en modos de la familia FM. |
| NR2 | Todas las series | Activa el modo 2 de reducción de ruido. Oculto en modos de la familia FM. |
| NB | Todas las series | Activa el eliminador de ruido. Oculto en modos de la familia FM. |
| NRL | Todas las series (incluida la serie 6000) | Activa la reducción de ruido (algoritmo NRL). Oculto en modos de la familia FM. Disponible en radios de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Oculto en modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Oculto en modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Oculto en modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando el QSK de CW está activo. Controlado desde el applet CW; solo lectura aquí. |
| Etiqueta de ancho de filtro | ej. '2.7K', '3.3K', '500', '6.0K' | Ancho de banda del filtro del segmento actual. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del segmento es FM, NFM o DFM.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS en transmisión. |
| Valor de tono CTCSS | — | 67.0–254.1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia de TX por debajo de la frecuencia de RX en la cantidad de desplazamiento. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia de TX por encima de la frecuencia de RX en la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar un par de repetidor invertido. |

## Pestaña Periféricos — conexión IP manual

La pestaña Periféricos en el diálogo Configuración de Radio le permite conectarse manualmente a dispositivos externos mediante dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Conectado" se muestra solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es realmente a un ShackSwitch, la fila AG se muestra como desconectada y la fila ShackSwitch se muestra como conectada.

### ShackSwitch — fila 4 (agregado en V0.9.4)

| Control | Clave de configuración | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Campo de dirección IP | `SS_ManualIp` | — | Ingrese la dirección IP del ShackSwitch. |
| Campo de puerto | `SS_ControlPort` | 9007 | Puerto utilizado para el protocolo de control AG. Siempre se conecta en el puerto 9007 independientemente del valor ingresado. |
| Botón Conectar | — | — | Se conecta al ShackSwitch en la IP especificada en el puerto 9007 utilizando el protocolo de control AG. |
| Botón Desconectar | — | — | Se desconecta del ShackSwitch. |
| Estado Conectado | — | — | Muestra "Conectado" solo cuando la conexión activa es a un dispositivo ShackSwitch. |
| Botón ⚙ Web UI | `SS_ManualIp`, `SS_WebPort` | puerto 5000 | Abre la interfaz web del ShackSwitch en su navegador. Utiliza la dirección del par activo si hay un ShackSwitch actualmente conectado. Utiliza `SS_WebPort` de la configuración si está establecido y es mayor que 1024; de lo contrario, recurre al `webPort` anunciado por el dispositivo si es válido (>1024), y luego utiliza el puerto 5000 como predeterminado. No hace nada si no se puede determinar ninguna dirección IP. |

Tanto la fila AG como la fila ShackSwitch comparten la conexión subyacente `AntennaGeniusModel`. Conectarse a una se reflejará como desconectado en la otra.

## Accesos y métodos de visibilidad de AppletPanel

Los siguientes métodos de acceso y ayudantes de visibilidad están disponibles en `AppletPanel`. Se utilizan internamente y por código que coordina la presencia del dispositivo con el estado del applet.

### Accesos de applet

| Método | Retorna | Descripción |
|---|---|---|
| `tciApplet()` | `TciApplet*` | Retorna la instancia del applet TCI. |
| `daxIqApplet()` | `DaxIqApplet*` | Retorna la instancia del applet DAX IQ. |
| `agApplet()` | `AntennaGeniusApplet*` | Retorna la instancia del applet Antenna Genius. |
| `ssApplet()` | `ShackSwitchApplet*` | Retorna la instancia del applet ShackSwitch. Agregado en V0.9.4. |
| `meterApplet()` | `MeterApplet*` | Retorna la instancia del applet de medidor. |
| `mqttApplet()` | `MqttApplet*` | Retorna la instancia del applet MQTT. Disponible solo en compilaciones HAVE_MQTT. |

### Ayudantes de visibilidad

| Método | Descripción |
|---|---|
| `setAgVisible(bool visible)` | Muestra u oculta el botón y applet Antenna Genius según la presencia del dispositivo. |
| `setShackSwitchVisible(bool visible)` | Muestra u oculta el applet ShackSwitch según la presencia del dispositivo. Agregado en V0.9.4. |
