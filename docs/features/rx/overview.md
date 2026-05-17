# Descripción general de los controles RX

El applet RX Controls le brinda control por slice sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, AGC, audio, squelch, RIT/XIT y configuración de repetidor FM. Ábralo siempre que necesite configurar cómo un slice recibe o transmite.

## Cómo funciona

El applet RX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja RX. Cuando la radio admite más de un slice, aparece una fila de pestañas de slice (A a H) en la parte superior; al hacer clic en una pestaña, se vincula el applet a ese slice. Todos los controles debajo de la fila de pestañas afectan únicamente al slice seleccionado actualmente.

Las preconfiguraciones de ancho de filtro son la única opción que persiste entre sesiones y se almacenan bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del slice

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona qué slice controla el applet. La fila de pestañas se oculta cuando la radio tiene un solo slice. Los bordes de los botones y los fondos activos siguen el color por slice configurado en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de slice estática. Las conexiones de clic en los botones de slice están protegidas contra manejadores de señal duplicados entre reconexiones (v0.9.5.1, #2254). |
| Insignia de slice | A | Muestra la letra del slice activo. La letra del slice puede representarse como HTML (#2606). El color lo controla SliceColorManager; los colores personalizables por slice persisten entre sesiones y se reflejan aquí, en los botones de pestaña de slice, los widgets VFO y las tiras de medidores. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia del panadapter y otras fuentes. |
| TX (insignia) | — | Haga clic para designar este slice como el slice de TX. |

### Frecuencia y modo

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Menú desplegable de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si la marca de compilación HAVE_RADE está activa) | Establece el modo del slice. Cambiar el modo reconfigura automáticamente las preconfiguraciones de filtro y paso. Al cambiar a RTTY o modos digitales (DIGU, DIGL), el squelch se desactiva automáticamente para evitar eliminar los caracteres FSK (#2504). |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0,001–54,000 MHz (hasta 450,000 MHz en XVTR) | Escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar. Presione Escape para cancelar y restaurar la frecuencia anterior. |
| STEP | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian según el modo. |

### Selección de antena

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles. El menú se completa con `rxAntennaList()` del slice si está disponible; de lo contrario, con la lista de antenas de la radio. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas. Al seleccionar un elemento, se establece la antena RX usando el nombre completo de la antena. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas capaces de TX. Solo se incluyen antenas cuyos nombres comienzan con "ANT", "TX" o "XVTR"; los puertos solo RX (nombres que comienzan con "RX") quedan excluidos. Los elementos del menú muestran una etiqueta corta con el nombre completo de la antena en la información sobre herramientas. Al seleccionar un elemento, se establece la antena TX usando el nombre completo de la antena. La etiqueta es roja. |

### Filtro

| Control | Rango / valor predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|
| Preconfiguraciones de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como preconfiguración. Los botones se ocultan en los modos FM, NFM y DFM. Las preconfiguraciones se almacenan como un valor de ancho simple o un par de banda pasante `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica una preconfiguración o se arrastra la banda pasante. Solo lectura. La lógica de formato se comparte con VfoWidget a través de `RxApplet::formatFilterWidth()` y utiliza lógica dependiente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda pasante del filtro | — | — | Arrastre el borde inferior o superior para establecer una banda pasante de filtro personalizada. |
| Ensanchar (acción de acceso directo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de preconfiguraciones por modo para ensanchar la banda pasante del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |
| Estrechar (acción de acceso directo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de preconfiguraciones por modo para estrechar la banda pasante del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |

### AGC

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta del AGC. Oculto en modos de la familia FM. |
| Umbral AGC | 65 | 0–100 | Establece el umbral del AGC. Cuando el modo AGC es Off, ajusta el nivel de off-level del AGC. |

### Audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silenciar) | 🔊 (sin silenciar) | — | Silencia o reactiva la salida de audio del slice. El estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio (#2489). |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. |
| Panorámica L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Haga doble clic para restablecer al centro (50). |
| SQL | — | — | Activa el squelch al nivel establecido por el control deslizante de squelch. Desactivado y forzado a off en modos RTTY y digitales (DIGU, DIGL) donde el squelch eliminaría los caracteres FSK (#2504). |
| Nivel de squelch | 20 | 0–100 | Establece el umbral de squelch. Solo tiene efecto cuando SQL está activado. El nivel de squelch manual persiste entre sesiones en el lado del cliente como `LastManualSquelchLevel` — esto conserva su preferencia entre ciclos de modo e inicios, ya que el modo automático puede sobrescribir el valor de squelch del slice. |

### RIT y XIT

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Activa o desactiva la sintonía incremental de recepción. |
| RIT 0 | — | Pone a cero el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | off | Activa o desactiva la sintonía incremental de transmisión. |
| XIT 0 | — | Pone a cero el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Reducción de ruido y botones de filtro DSP

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
| QSK | Gris / ámbar | Se ilumina en ámbar cuando el full break-in de CW está activo. Controlado desde el applet CW; solo lectura aquí. |
| Etiqueta de ancho de filtro | p. ej., '2.7K', '3.3K', '500', '6.0K' | Ancho de banda del filtro del slice actual. |

### Controles de repetidor FM

Estos controles solo son visibles cuando el modo del slice es FM, NFM o DFM.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS en transmisión. |
| Valor de tono CTCSS | — | 67,0–254,1 Hz (41 tonos EIA/TIA-603 estándar) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0,0 MHz | 0,0–100,0 MHz (paso 0,1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia de TX por debajo de la frecuencia de RX en la cantidad de desplazamiento. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia de TX por encima de la frecuencia de RX en la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar un par de repetidores invertido. |

## Pestaña Peripherals — conexión IP manual

La pestaña Peripherals del cuadro de diálogo Radio Setup le permite conectarse manualmente a dispositivos externos mediante dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Connected" solo se muestra cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es realmente a un ShackSwitch, la fila AG se muestra como desconectada y la fila ShackSwitch se muestra como conectada.

### ShackSwitch — fila 4 (agregada en V0.9.4)

| Control | Clave de configuración | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Campo de dirección IP | `SS_ManualIp` | — | Ingrese la dirección IP del ShackSwitch. |
| Campo de puerto | `SS_ControlPort` | 9007 | Puerto utilizado para el protocolo de control AG. Siempre se conecta en el puerto 9007 independientemente del valor ingresado. |
| Botón Connect | — | — | Se conecta al ShackSwitch en la IP especificada en el puerto 9007 usando el protocolo de control AG. |
| Botón Disconnect | — | — | Se desconecta del ShackSwitch. |
| Estado Connected | — | — | Muestra "Connected" solo cuando la conexión activa es a un dispositivo ShackSwitch. |
| Botón ⚙ Web UI | `SS_ManualIp`, `SS_WebPort` | puerto 5000 | Abre la interfaz web del ShackSwitch en su navegador. Utiliza la dirección del peer activo si hay un ShackSwitch conectado actualmente. Usa `SS_WebPort` de la configuración si está definido y es mayor que 1024; de lo contrario, recurre al `webPort` anunciado por el dispositivo si es válido (>1024), y luego usa el puerto 5000 como valor predeterminado. No hace nada si no se puede determinar ninguna dirección IP. |

Tanto la fila AG como la fila ShackSwitch comparten la conexión subyacente `AntennaGeniusModel`. Conectarse a una se reflejará como desconectado en la otra.

## Métodos de acceso y visibilidad de AppletPanel

Los siguientes métodos de acceso y ayudantes de visibilidad están disponibles en `AppletPanel`. Se utilizan internamente y por código que coordina la presencia del dispositivo con el estado del applet.

### Accesores de applet

| Método | Devuelve | Descripción |
|---|---|---|
| `tciApplet()` | `TciApplet*` | Devuelve la instancia del applet TCI. |
| `daxIqApplet()` | `DaxIqApplet*` | Devuelve la instancia del applet DAX IQ. |
| `agApplet()` | `AntennaGeniusApplet*` | Devuelve la instancia del applet Antenna Genius. |
| `ssApplet()` | `ShackSwitchApplet*` | Devuelve la instancia del applet ShackSwitch. Agregado en V0.9.4. |
| `meterApplet()` | `MeterApplet*` | Devuelve la instancia del applet de medidores. |
| `mqttApplet()` | `MqttApplet*` | Devuelve la instancia del applet MQTT. Disponible solo en compilaciones HAVE_MQTT. |

### Ayudantes de visibilidad

| Método | Desc
