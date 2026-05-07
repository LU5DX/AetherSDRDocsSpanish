# Descripción general de los controles de RX

El applet de Controles de RX le permite controlar por slice cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, CAG, audio, silenciador, RIT/XIT y configuración de repetidores FM. Ábralo siempre que necesite configurar cómo un slice recibe o transmite.

## Cómo funciona

El applet de RX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de la bandeja de RX. Cuando la radio admite más de un slice, aparece una fila de pestañas de slice (A a la H) en la parte superior; al hacer clic en una pestaña, el applet se vincula a ese slice. Todos los controles debajo de la fila de pestañas afectan únicamente al slice seleccionado actualmente.

Los preajustes de ancho de filtro son la única configuración que persiste entre sesiones, almacenada bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del slice

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona qué slice controla el applet. La fila de pestañas se oculta cuando la radio tiene un solo slice. Los bordes de los botones y los fondos activos siguen el color por slice establecido en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestañas generados y restaura la insignia de slice estática. Las conexiones de clic en los botones de slice están protegidas contra manejadores de señales duplicados en reconexiones (v0.9.5.1, #2254). |
| Insignia de slice | A | Muestra la letra del slice activo. El color lo determina SliceColorManager; los colores por slice personalizables persisten entre sesiones y se reflejan aquí, en los botones de pestañas de slice, los widgets de VFO y las barras de medidor. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia del panadapter y de otras fuentes. |
| TX (insignia) | — | Haga clic para designar este slice como el slice de TX. |

### Frecuencia y modo

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Menú desplegable de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, NT, RTTY (+ RADE si la marca de compilación HAVE_RADE está activada) | Establece el modo del slice. Cambiar el modo reconfigura automáticamente los preajustes de filtro y paso. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia actual del VFO con agrupación punteada. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 450.000 MHz en XVTR) | Escriba una frecuencia en MHz y presione Enter para sintonizar y re-centrar. Presione Escape para cancelar y restaurar la frecuencia anterior. |
| PASO | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones triangulares izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian con el modo. |

### Selección de antena

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles de la lista de antenas de la radio. Seleccione para configurar la antena RX para este slice. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas capaces de TX. Los puertos solo RX (nombres que comienzan con `RX`) se excluyen. La etiqueta es roja. |

### Filtro

| Control | Valor predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Preajustes de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como preajuste. Los botones se ocultan en modos FM, NFM y DFM. Los preajustes se almacenan como un valor de ancho simple o un par de banda de paso `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica un preajuste o se arrastra la banda de paso. Solo lectura. La lógica de formato se comparte con VfoWidget mediante `RxApplet::formatFilterWidth()` y usa lógica según el modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). |
| Widget de banda de paso del filtro | — | — | Arrastre el borde bajo o alto para configurar una banda de paso de filtro personalizada. |
| Ampliar (acción de atajo) | — | — | El método `stepFilterWidth(+1)` recorre la lista de preajustes por modo para ampliar la banda de paso del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |
| Reducir (acción de atajo) | — | — | El método `stepFilterWidth(-1)` recorre la lista de preajustes por modo para reducir la banda de paso del filtro con geometría de borde correcta según el modo. Accesible mediante atajo de teclado (v0.9.8, #2208). |

### CAG

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo CAG | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta del CAG. Oculto en modos de la familia FM. |
| Umbral CAG | 65 | 0–100 | Establece el umbral del CAG. Cuando el modo CAG está en Off, ajusta el nivel de CAG desactivado. |

### Audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (sin silenciar) | — | Silencia o reactiva la salida de audio del slice. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. |
| Panorámica L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Haga doble clic para restablecer al centro (50). |
| SQL | — | — | Activa el silenciador al nivel establecido por el control deslizante de silenciador. Deshabilitado y forzado a desactivado en modos DIGU, DIGL, NT, CW y CWL. |
| Nivel de silenciador | 20 | 0–100 | Establece el umbral del silenciador. Solo tiene efecto cuando SQL está activado. |

### RIT y XIT

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Activa o desactiva la sintonización incremental de recepción. |
| RIT 0 | — | Pone el desplazamiento RIT a cero inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | off | Activa o desactiva la sintonización incremental de transmisión. |
| XIT 0 | — | Pone el desplazamiento XIT a cero inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Reducción de ruido y botones de filtro DSP

Los siguientes botones de filtro DSP son visibles en modos que no son FM. La disponibilidad del botón depende de la serie de la radio.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Oculto en modos de la familia FM. |
| NR2 | Todas las series | Activa el modo de reducción de ruido 2. Oculto en modos de la familia FM. |
| NB | Todas las series | Activa el eliminador de ruido. Oculto en modos de la familia FM. |
| NRL | Todas las series (incluyendo serie 6000) | Activa la reducción de ruido (algoritmo NRL). Oculto en modos de la familia FM. Disponible en radios de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Oculto en modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Oculto en modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Oculto en modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando el full break-in de CW está activo. Controlado desde el applet de CW; solo lectura aquí. |
| Etiqueta de ancho de filtro | p. ej., '2.7K', '3.3K', '500', '6.0K' | Ancho de banda del filtro del slice actual. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del slice es FM, NFM o DFM.

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

La pestaña Periféricos en el diálogo de Configuración de Radio le permite conectarse manualmente a dispositivos externos por dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Se conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Conectado" se muestra solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es en realidad a un ShackSwitch, la fila AG se muestra como desconectada y la fila ShackSwitch se muestra como conectada.

### ShackSwitch — fila 4 (agregado en V0.9.4)

| Control | Clave de configuración | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Campo de dirección IP | `SS_ManualIp` | — | Ingrese la dirección IP del ShackSwitch. |
| Campo de puerto | `SS_ControlPort` | 9007 | Puerto utilizado para el protocolo de control AG. Siempre se conecta en el puerto 9007 independientemente del valor ingresado. |
| Botón Conectar | — | — | Se conecta al ShackSwitch en la IP especificada en el puerto 9007 usando el protocolo de control AG. |
| Botón Desconectar | — | — | Se desconecta del ShackSwitch. |
| Estado Conectado | — | — | Muestra "Conectado" solo cuando la conexión activa es a un dispositivo ShackSwitch. |
| Botón ⚙ Interfaz web | `SS_ManualIp`, `SS_WebPort` | puerto 5000 | Abre la interfaz web del ShackSwitch en su navegador. Usa la dirección del peer activo si un ShackSwitch está actualmente conectado. Usa `SS_WebPort` de la configuración si está establecido y es mayor que 1024; de lo contrario, recurre al `webPort` anunciado por el dispositivo si es válido (>1024), y luego se establece por defecto al puerto 5000. No hace nada si no se puede determinar una dirección IP. |

Tanto la fila AG como la ShackSwitch comparten la conexión subyacente `AntennaGeniusModel`. Conectarse a uno se reflejará como desconectado en el otro.

## Métodos de acceso y visibilidad del AppletPanel

Los siguientes métodos de acceso y ayudantes de visibilidad están disponibles en `AppletPanel`. Se utilizan internamente y por código que coordina la presencia del dispositivo con el estado del applet.

### Accesores de applet

| Método | Devuelve | Descripción |
|---|---|---|
| `tciApplet()` | `TciApplet*` | Devuelve la instancia del applet TCI. |
| `daxIqApplet()` | `DaxIqApplet*` | Devuelve la instancia del applet DAX IQ. |
| `agApplet()` | `AntennaGeniusApplet*` | Devuelve la instancia del applet Antenna Genius. |
| `ssApplet()` | `ShackSwitchApplet*` | Devuelve la instancia del applet ShackSwitch. Agregado en V0.9.4. |
| `meterApplet()` | `MeterApplet*` | Devuelve la instancia del applet de medidor. |
| `mqttApplet()` | `MqttApplet*` | Devuelve la instancia del applet MQTT. Disponible solo en compilaciones HAVE_MQTT. |

### Ayudantes de visibilidad

| Método | Descripción |
|---|---|
| `setAgVisible(bool visible)` | Muestra u oculta el botón y el applet de Antenna Genius según la presencia del dispositivo. |
| `setShackSwitchVisible(bool visible)` | Muestra u oculta el applet de ShackSwitch según la presencia del dispositivo. Agregado en V0.9.4. |
