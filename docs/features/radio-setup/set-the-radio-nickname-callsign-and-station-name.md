# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona acceso a todos los ajustes a nivel de radio, incluidos identificación, configuración de red, GPS, parámetros de transmisión, configuración de teléfono/CW, calibración de recepción, configuración de audio, filtros, transverters, cables USB, periféricos y gestión de certificados SmartLink.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La mayoría de los controles no están disponibles sin una conexión activa.

## Abrir el diálogo

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como una ventana persistente. Su posición y tamaño se guardan automáticamente al cerrarlo y se restauran la próxima vez que lo abra. La geometría se almacena en AppSettings bajo la clave `RadioSetupDialogGeometry`.

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, datos de licencia y controles de actualización de firmware.

### Información de la Radio

La sección de información de la radio muestra indicadores de solo lectura:

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Region** | Región regulatoria de la radio (ej., USA). |
| **HW Version** | Cadena de versión del hardware. |
| **Model** | Modelo de la radio. |
| **Options** | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado de habilitación de multiFLEX. |

### Identificación de la Radio

Establezca un apodo legible, su indicativo y un nombre de estación en el FLEX-8600 conectado. Estos valores identifican la radio y este cliente ante otras estaciones multiFLEX en la red.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como nombre de la radio. | Nombre reportado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(en blanco)_ |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se almacena en AppSettings. Se envía a la radio como 'client station <nombre>'. | Nombre del host del SO |

### Pasos para configurar la identificación de la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el campo **Nickname**, escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio de inmediato.
5. En el campo **Callsign**, escriba su indicativo de estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica a este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en el botón de cerrar de la ventana o presione Escape para descartar el diálogo.

### Información de la Licencia

La sección **License Info** muestra detalles de la suscripción, fecha de vencimiento, ID de la radio y versión licenciada desde la radio.

### Encendido Remoto

Haga clic en **Remote On** para habilitar la capacidad de encendido remoto.

### Actualización de Firmware

Use los controles de actualización de firmware para verificar y aplicar actualizaciones de firmware a la radio.

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (mágica OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |

#### Para verificar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que descargue el instalador SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

#### Para preparar y cargar firmware

1. Descargue el instalador SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Abrir.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<nombrearchivo\>..." y aparece la barra de progreso.
   - El preparador de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (mágica OLE/MSI para .msi, PE/COFF MZ para .exe, o CTRL+Z para .ssdr) y extrae el .ssdr sin herramientas externas.
3. Espere a que la preparación termine. La etiqueta de estado muestra "Ready to upload \<nombrearchivo\>".
4. Haga clic en **Upload Firmware**.
   - Aparece un diálogo de confirmación: "This will restart the radio. Are you sure you want to upload \<nombrearchivo\>?"
5. Haga clic en **Yes** para confirmar.
   - La carga comienza. La etiqueta de estado muestra "Uploading... (X%)" y la barra de progreso se actualiza.
   - La radio se reinicia después de que la carga se complete. La etiqueta de estado muestra "Upload and reboot successful."
6. Haga clic en el botón de cerrar de la ventana o presione Escape para descartar el diálogo.

## Pestaña Network

La pestaña **Network** muestra información de red de la radio y proporciona opciones avanzadas de red.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. | — |
| **Enforce Private IP Connections:** | Rechaza pares no RFC1918. | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red a la radio. | — |

### Para configurar IP estática

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Haga clic en **DHCP / Static** para cambiar al modo Estático.
4. Ingrese los valores de **IP Address**, **Mask** y **Gateway**.
5. Haga clic en **Apply** para enviar la configuración a la radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de latitud, longitud, altitud, hora y satélites.

## Pestaña TX

La pestaña **TX** proporciona controles de temporización de transmisión, interbloqueos, potencia máxima, modo de sintonía, visualización en waterfall, comportamiento de seguimiento slice/TX y un acceso directo a los Ajustes de Banda de TX.

### Ajustes de Banda de TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

Los controles de temporización incluyen campos para retrasos de interbloqueo y tiempo de espera. El campo de tiempo de espera se muestra en segundos para facilitar la lectura, pero se almacena y transmite a la radio en milisegundos.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **ACC TX:** | Retraso de transmisión ACC en milisegundos. | — |
| **TX Delay:** | Retraso de TX en milisegundos. | — |
| **RCA TX1:** | Retraso de RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de interbloqueo mostrado en segundos. La radio almacena este valor en milisegundos internamente. | — |

### Interbloqueos

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de interbloqueo RCA. |
| **TX REQ: Accessory** | Habilita la entrada de interbloqueo del accesorio. |

### Potencia y Sintonía

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0-100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |

### Comportamiento de Seguimiento Slice/TX

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se desactiva automáticamente durante la operación en Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | False |

## Pestaña Phone/CW

La pestaña **Phone/CW** proporciona configuraciones predeterminadas de micrófono, manipulador CW y RTTY.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local de software. Par mutuamente excluyente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral de tono CW (LSB o USB). | — |
| **CWX:** | Habilita la activación de macros CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. | True |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. | — |

## Pestaña RX

La pestaña **RX** proporciona calibración de desviación de frecuencia GPSDO y selección de fuente de referencia de 10 MHz.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. | — |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en ppb. | — |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado (TCXO/GPSDO/External). El estado de bloqueo (Locked/Unlocked) se muestra junto al combo y se actualiza en vivo. | Auto |

## Pestaña Audio

La pestaña **Audio** proporciona salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y controles del contenedor NVIDIA BNR.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea. | — |
| **Mute (Line Out)** | Silencia la salida de línea. | — |
| **Headphone:** | Deslizador de ganancia de auriculares. | — |
| **Mute (Headphone)** | Silencia los auriculares. | — |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | — |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings. | Auto |
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada para evitar caídas en los flujos de audio/TCP/UDP durante la inactividad. | False |
| **PC Audio Devices: Input: / Output:** | Selecciona dispositivos de audio de entrada/salida del host. | — |
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en AppSettings. | — |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para compensar la fluctuación en VPN/SmartLink. Se almacena como `AudioBufferMs`. | 200 |
| **Recording: Radio Side / Client Side** | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena en AppSettings. | Radio Side |
| **Save to:** | Carpeta para las grabaciones guardadas (solo lado del cliente). Predeterminada a Documentos/AetherSDR/Recordings. | — |
| **...** | Navega para seleccionar la carpeta de grabación. | — |
| **Auto-record on TX** | Graba automáticamente mientras se transmite. | False |
| **Idle timeout:** | Segundos de silencio antes de que se detenga la grabación. | 120 |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. | — |

## Pestaña Filters

La pestaña **Filters** proporciona opciones de filtros de baja latencia y filtros nítidos por ancho de banda.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Use Low Latency Filters for Digital Modes** | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. | — |

## Pestaña XVTR

La pestaña **XVTR** proporciona configuración por transverter. Contiene pestañas anidadas, una por transverter, más una pestaña '+' para crear nuevos transverters.

| Control | Descripción |
|---|---|
| **RX Only:** | Fuerza solo RX en ese transverter. |
| **Remove (xvtr)** | Elimina la definición del transverter. |
| **Create New Transverter** | Agrega una nueva entrada de transverter. |

## Pestaña USB Cables

La pestaña **USB Cables** asigna adaptadores de serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Descripción |
|---|---|
| **Cables list / Status** | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| **Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source
