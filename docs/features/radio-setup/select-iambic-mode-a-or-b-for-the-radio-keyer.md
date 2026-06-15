# Diálogo de configuración de la radio

Esta página describe cada control en el diálogo **Radio Setup** (`Settings > Radio Setup...`). El diálogo tiene una barra de pestañas en la parte superior; cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. |
| **Model** | Modelo de la radio (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **HW Version** | Cadena de versión de hardware (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **Region** | Región regulatoria; predeterminado EE. UU. (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **License Info** | Muestra la suscripción, vencimiento, ID de radio y versión licenciada de la radio (solo lectura). Cada campo incluye un botón de copia al portapapeles junto al valor. |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo de radio fácil de usar. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se almacena en `StationName`. Se predetermina al nombre de host del SO si se deja vacío. Se envía a la radio como `client station <name>`. |

### Botones de copia

Cada indicador de solo lectura en la pestaña Radio ahora tiene un pequeño **botón de copia al portapapeles** (icono de documentos superpuestos) a su derecha. Haga clic en el botón para copiar el valor del indicador al portapapeles del sistema. Aparece una breve etiqueta emergente ("¡Copiado!") cerca del botón después de una copia exitosa. El botón se atenúa visualmente cuando el valor está vacío o es un marcador de posición de guion.

| Indicador con botón de copia | Valor copiado |
|---|---|
| **Radio SN** | El número de serie del chasis, o el número de serie de la radio si el número de serie del chasis está vacío. |
| **Model** | La cadena del modelo de la radio. |
| **HW Version** | La cadena de versión de hardware, con prefijo "v" si no está presente. |
| **Region** | La cadena de la región regulatoria. |
| **FlexControl** | La cadena del estado de detección de FlexControl. |
| **multiFLEX** | La cadena del estado habilitado de multiFLEX. |
| **Options** | La cadena de opciones licenciadas; si está vacía, muestra "GPS" o "GPS, PGXL" según la presencia del amplificador. |
| **License Info** | La cadena completa de detalles de licencia tal como se muestra. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita el encendido remoto / activación remota. |
| **Check for Update** | Consulta las actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado dice: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta dice: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador SmartSDR `.msi` (formato WiX de FlexRadio v4.2+), un instalador autoextraíble `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. encabezado MZ de PE/COFF) y extrae la carga útil `.ssdr` sin herramientas externas. Anteriormente etiquetado **Browse .ssdr...** (cambiado en v26.5.3). |
| **Upload Firmware** | Inicia la carga del firmware. Una barra de progreso y una etiqueta de estado siguen el progreso. Se habilita solo después de que se haya preparado un archivo válido mediante **Select Installer...**. |
| **Reboot Radio** | Solicita confirmación: *Reboot the connected radio now?* El texto de advertencia difiere para conexiones WAN (SmartLink) vs. LAN. En LAN, AetherSDR se reconectará automáticamente después de que la radio arranque. En WAN, debe reconectarse manualmente. Al hacer clic en Aceptar, se envía el comando de reinicio y se cierra el diálogo. Deshabilitado cuando la radio no está conectada. Estilizado con un fondo rojizo para indicar la naturaleza destructiva de la acción. |

### Preparación de una actualización de firmware

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from \<filename\>...* mientras el preparador extrae la carga útil.
4. Cuando la preparación se complete, la etiqueta de estado confirma que está listo y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

---

## Pestaña Network

Muestra las direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura informadas por la radio. Cada una incluye un botón de copia al portapapeles. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | Habilitado | Rechaza peers no RFC1918. Siempre muestra "Enabled" cuando está activado. |
| **Network MTU:** | Spinbox | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango válido 576–9000. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Almacenado en `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — | Campos de configuración de IP estática. |
| **Apply** | Botón pulsador | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

Muestra la presencia de GPS y datos de posición en vivo cuando un receptor GPS está conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y conteo de satélites. Actualizado en tiempo real. |

---

## Pestaña TX

Controla los tiempos de TX, enclavamientos, límites de potencia, modo de sintonía y comportamiento de seguimiento de slices.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Campos Spinbox | — | Tiempos de retención y retardo de TX. Campos: ACC TX (ms), TX Delay (ms), RCA TX1 (ms). |
| **Timeout (sec):** | Spinbox | — | Tiempo de espera de enclavamiento en segundos. El valor se envía a la radio en milisegundos (multiplicado por 1000). |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y de accesorio. |
| **Max Power:** | Spinbox | — | Límite de potencia de TX a nivel de radio (0–100%). |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal de TX en la visualización del waterfall. |
| **TX Follows Active Slice** | Botón pulsador | Falso | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Deshabilitado automáticamente durante la operación Split. Almacenado en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón pulsador | Falso | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Almacenado en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón pulsador | — | Abre el diálogo dedicado de potencia y sintonía por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Manipulador iambic

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** muestra **Enabled**. Si muestra **Disabled**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iambic Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iambic en la radio. Siempre muestra "Enabled" cuando está activado. |
| **Iambic Mode: A / B** | Botón pulsador (par mutuamente excluyente) | A | Selecciona el modo iambic Curtis A o B tanto para el manipulador de hardware de la radio como para el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. |
| **Swap:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Sideband:** | Cuadro combinado | — | Selecciona la banda lateral del tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita la activación por macro CWX. |
| **Decode:** | Botón de alternancia | Verdadero | Habilita la superposición de decodificación CW en el panadapter. Almacenado en `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | — | Frecuencia predeterminada de marca RTTY. |

**Modo A vs. Modo B:** El modo A (Curtis A) libera el último elemento cuando se sueltan ambas paletas durante un apretón intermedio. El modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador de software local refleja el modo que seleccione, proporcionando una respuesta de tono lateral inferior a 5 ms independiente de la latencia de la red.

---

## Pestaña RX

Proporciona calibración de compensación de frecuencia GPSDO y selección de fuente de referencia de 10 MHz.

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo dice:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - La etiqueta de estado informa el progreso (Starting… y estados posteriores).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración se completa, el botón se rehabilita y la etiqueta de estado se actualiza con el resultado.
6. Si **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | — | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón pulsador | — | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Deshabilitado y etiquetado como Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Spinbox | — | Compensación de frecuencia manual en partes por billón. Se aplica directamente sin ejecutar un barrido. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador. El cuadro combinado se completa dinámicamente según el hardware instalado y el estado actual del oscilador: **Auto**, **TCXO**, **GPSDO** y **External 10 MHz** aparecen solo cuando se detecta el hardware correspondiente o se seleccionó previamente. Cuando **Auto** está activo, la etiqueta de estado muestra la fuente resuelta (por ejemplo, *Auto -> GPSDO*). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, *GPSDO -> TCXO*). El estado de bloqueo (**Locked** / **Unlocked**) se agrega y se actualiza en vivo; si se selecciona **External 10 MHz** pero no se detecta ninguna señal externa, se agrega *(not detected)*. |

---

## Pestaña Antennas

Configura nombres de antena definidos por el usuario para cada puerto de antena TX.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **ANT1 / ANT2 / XVTA / XVTB** | Campos de texto | — | Ingrese un nombre personalizado (hasta 20 caracteres) para cada puerto de antena. Los nombres se envían a la radio y se muestran en los botones de band-stack y el selector de antena de slice. |

---

## Pestaña Audio

Configura las salidas de audio de la radio, los dispositivos de audio de la PC, la grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Line Out:** | Deslizador | — | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón pulsador | — | Silencia la salida de línea. |
| **Headphone:** | Deslizador | — | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón pulsador | — | Silencia la salida de auriculares. |
| **Front Speaker: / Mute** | Botón pulsador | — | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón pulsador | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Almacenado en `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | Falso | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujo de audio/TCP/UDP durante la inactividad. Almacenado en `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Com
