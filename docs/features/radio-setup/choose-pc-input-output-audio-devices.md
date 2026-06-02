# Elegir dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué dispositivos de audio del PC utiliza AetherSDR para la salida de audio de recepción de radio y la entrada de micrófono. Debe hacer esto cuando configure AetherSDR por primera vez o cuando cambie de auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- La radio debe estar conectada. Los controles de configuración de radio no están disponibles sin una conexión activa.
- Sepa qué dispositivos de entrada y salida de audio expone su PC (consulte la configuración de audio de su sistema operativo si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo de configuración de radio.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en la lista desplegable **Input:** y seleccione el dispositivo que desea usar para la entrada de micrófono o audio.
4. Haga clic en la lista desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones surten efecto de inmediato.

## Qué hace cada control

| Control | Qué hace | Predeterminado |
|---------|----------|----------------|
| **Radio SN** | Número de serie del chasis (solo lectura). | — |
| **Region** | Región regulatoria de la radio. | USA |
| **HW Version** | Cadena de versión del hardware. | — |
| **Remote On** | Habilita el encendido/activación remota. | — |
| **Options** | Muestra las opciones de radio licenciadas. | — |
| **FlexControl** | Estado detectado del hardware FlexControl. | — |
| **multiFLEX** | Estado habilitado de multiFLEX. | — |
| **Model** | Modelo de la radio. | — |
| **Nickname** | Apodo descriptivo de la radio. | — |
| **Callsign** | Indicativo de la estación. | — |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se predetermina al nombre de host del SO si está vacío. Se almacena en AppSettings. Se envía a la radio como 'client station <name>'. | — |
| **License Info** | Muestra los detalles de la licencia (suscripción, vencimiento, ID de radio, versión licenciada) desde la radio. | — |
| **Check for Update** | Consulta actualizaciones de firmware. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (mágica OLE/MSI vs. MZ PE/COFF) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. | — |
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918. | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de las túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red a la radio. | — |
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonización por banda. | — |
| **Timings (in ms)** | Tiempos de retardo/espera de TX. | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y de accesorio. | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio. Rango 0-100%. | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonización. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |
| **TX Follows Active Slice** | TX sigue la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. | False |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | False |
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. En v0.9.1, se agregaron los botones Modo A y Modo B junto al interruptor de habilitación. Modo A = Curtis A; Modo B = Curtis B. Estos también controlan el nuevo manipulador iámbico de software local (IambicKeyer) que refleja el estado iámbico de la radio para un tono de vigilancia inferior a 5 ms. | Enabled |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente agregado en v0.9.1. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW. | — |
| **CWX:** | Habilita el accionamiento de macros CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. | True |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. | — |
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. | — |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en ppb. | — |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/Externo). El estado de bloqueo (Locked/Unlocked) se muestra junto al combo y se actualiza en vivo. | Auto |
| **Line Out:** | Ganancia de salida de línea. | — |
| **Mute (Line Out)** | Silencia la salida de línea. | — |
| **Headphone:** | Ganancia de auriculares. | — |
| **Mute (Headphone)** | Silencia los auriculares. | — |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | — |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`. | Auto |
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada para evitar la caída de flujos de audio/TCP/UDP durante la inactividad. | False |
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del host (micrófono, interfaz de audio, etc.). | System default |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del host (altavoces, auriculares, interfaz de audio, etc.). | System default |
| **Audio Boost:** | Aplica ganancia extra en la ruta de audio del cliente. Se almacena en AppSettings como `AudioBoost`. | Off |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente en milisegundos para jitter de VPN/SmartLink. Rango 50-1000 ms. Se almacena como `AudioBufferMs`. | 200 ms |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en la radio o en el cliente. Se almacena en AppSettings como `RecordingMode`. | Radio Side |
| **Save to:** | Carpeta para grabaciones guardadas (solo del lado del cliente). Se predetermina a Documents/AetherSDR/Recordings. Se almacena en AppSettings como `QsoRecordingDir`. | — |
| **...** | Abre un explorador de carpetas para seleccionar el directorio de grabación. | — |
| **Auto-record on TX** | Graba automáticamente mientras transmite. Se almacena en AppSettings como `QsoRecordingAutoRecord`. | False |
| **Idle timeout:** | Segundos de silencio antes de que se detenga la grabación. Rango 10-3600 seg. Se almacena en AppSettings como `QsoRecordingIdleTimeout`. | 120 s |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. | — |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo. Se deshabilita cuando Auto está habilitado para ese modo. Los comandos se envían como 'radio filter_sharpness <mode> level=<N>'. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. Los comandos se envían como 'radio filter_sharpness <mode> auto_level=1'. | — |
| **Use Low Latency Filters for Digital Modes** | Fuerza filtros de baja latencia en DIGU/DIGL. | — |
| **RX Only:** (por transvertidor) | Fuerza solo RX en ese transvertidor. | — |
| **Remove** (por transvertidor) | Elimina la definición del transvertidor. | — |
| **Create New Transverter** | Agrega una nueva entrada de transvertidor. | — |
| **Cables list / Status** | Cables USB detectados por tipo con estado Conectado/Desconectado. | — |
| **Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7)** | Parámetros y comportamiento serial por cable. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio, que está rota en firmware 4.2. El TGXL acciona el PTT de la radio a través de su cable de enclavamiento de hardware; no se necesita manipulación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. | Connect |
| **APD (tab)** | Configuración del muestreador de Predistorsión Adaptativa Externa: selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo series FLEX-8x00 con SmartSDR 4.2.18+. | — |
