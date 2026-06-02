# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, APD, temas, serial (FlexControl), nombres de antenas y gestión de certificados anclados de SmartLink.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio para acceder a la mayoría de las pestañas.
- Abra `Settings > Radio Setup...`.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

| Control | Valor predeterminado | Comportamiento |
|---------|---------------------|----------------|
| Radio SN | — | Número de serie del chasis (solo lectura). Haga clic en el botón de copia (icono superpuesto) para copiar el número de serie al portapapeles. |
| Region | USA | Región regulatoria de la radio. |
| HW Version | — | Cadena de versión del hardware. Haga clic en el botón de copia para copiar al portapapeles. |
| Remote On | — | Habilita el encendido remoto / activación remota. |
| Options | — | Muestra las opciones de radio licenciadas. |
| FlexControl | — | Estado detectado del hardware FlexControl. |
| multiFLEX | — | Estado de habilitación de multiFLEX. |
| Model | — | Modelo de la radio. |
| Nickname | — | Apodo amigable de la radio. |
| Callsign | — | Indicativo de la estación. |
| Station Name | — | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto toma el nombre del host del SO si está vacío. Se almacena como `StationName`. |
| License Info | — | Muestra los detalles de la licencia de la radio (Suscripción / Vencimiento / ID de Radio / Versión licenciada). Haga clic en el botón de copia para copiar al portapapeles. |
| Check for Update | — | Consulta actualizaciones de firmware. |
| Select Installer... | — | Elige un archivo de imagen de firmware (`.msi`, `.exe` o `.ssdr`). |
| Upload Firmware | — | Inicia la carga del firmware con barra de progreso y estado. |
| SmartLink (pestaña) | — | Gestión de certificados TLS anclados de SmartLink. Lista cada certificado anclado (host, huella SHA-256, fecha de anclaje) con botones por fila Olvidar y Olvidar todo. Se construye de forma diferida al hacer clic por primera vez. |
| Pinned SmartLink Certificates (sección) | — | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Lista todos los hosts que este cliente ha anclado en la primera conexión (confianza en el primer uso). |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | — | Tabla de solo lectura de 3 columnas: Host (nombre de host), huella SHA-256 (monoespaciado), Anclado (AAAA-MM-DD o '(pre-phase 2)'). |
| Forget selected | — | Elimina la huella del certificado anclado del host seleccionado para que la próxima conexión lo vuelva a anclar silenciosamente. |
| Forget all | — | Limpia todos los certificados anclados (con confirmación). La próxima conexión a cada radio los volverá a anclar silenciosamente. |

### Botones de copia de valor

Cada indicador de solo lectura (Radio SN, HW Version, License Info, etc.) ahora muestra un pequeño botón de copia superpuesto al pasar el ratón o al enfocar. Al hacer clic en el botón, se copia el valor mostrado al portapapeles del sistema. Aparece un breve mensaje emergente "copiado" cerca del botón después de una copia exitosa.

### Estado de carga de firmware

El área de carga de firmware muestra una barra de progreso y texto de estado durante una carga activa. Cuando no hay ninguna carga en curso, el área de estado está vacía.

## Pestaña Red

La pestaña Red muestra información de red de la radio y opciones avanzadas de red.

| Control | Valor predeterminado | Comportamiento |
|---------|---------------------|----------------|
| IP Address / Mask / MAC Address | — | Direcciones de red de solo lectura. |
| Enforce Private IP Connections | — | Rechaza pares que no sean RFC1918. |
| Network MTU | 1450 | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes (576–9000). Se almacena como `NetworkMtu`. 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| DHCP / Static | — | Cambia entre modos DHCP e IP estática. |
| IP Address / Mask / Gateway | — | Campos de configuración de IP estática. |
| Apply | — | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña TX configura temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y configuración de banda de TX.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| TX Band Settings | — | — | Abre el diálogo dedicado de potencia/sintonía por banda. |
| ACC TX | — | — | Retardo de cola de TX en milisegundos. |
| TX Delay | — | — | Retardo de TX en milisegundos. |
| RCA TX1 | — | — | Retardo de RCA TX1 en milisegundos. |
| Timeout (sec) | — | — | Tiempo de espera del enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |
| RCA TX2 | — | — | Retardo de RCA TX2 en milisegundos. |
| Interlocks - TX REQ: RCA / Accessory | — | — | Habilita las entradas de enclavamiento RCA y accesorio. |
| Max Power | — | 0–100 % | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode | — | — | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall | — | — | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Falso | — | TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante operación en Split. |
| Active Slice Follows TX | Falso | — | Cambia la slice activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

### Campos de temporización

Los campos de temporización en la pestaña TX aceptan valores en milisegundos excepto Timeout (sec), que muestra y acepta valores en segundos para facilitar la lectura. La radio almacena el valor de tiempo de espera internamente en milisegundos.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Enable/Disable the Level Meter During Receive | — | — | Muestra el medidor de nivel de micrófono incluso en recepción. |
| Iambic | — | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en la radio. |
| Iambic Mode: A / B | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local del software. |
| Swap | — | — | Intercambia dit/dah. |
| Sideband | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX | — | — | Habilita la activación de macros CWX. |
| Decode | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. |
| RTTY Mark Default | — | — | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona calibración de compensación de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Cal Frequency (MHz) | — | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| Start | — | — | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración del PLL de la radio. El botón se deshabilita y se etiqueta **Busy** mientras la calibración está en ejecución. |
| Freq Offset (ppb) | — | — | Compensación de frecuencia manual en partes por billón. |
| 10 MHz Reference Source | Auto | Auto / TCXO / GPSDO / External 10 MHz | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. |

### 10 MHz Reference Source

El combo se completa dinámicamente cada vez que se abre el diálogo o la radio informa el estado del oscilador:

- **Auto** siempre está presente.
- **TCXO** aparece cuando la radio informa cualquier estado del oscilador, cuando `tcxoPresent` es verdadero, o cuando el valor actual o configurado es `tcxo`.
- **GPSDO** aparece cuando `gpsdoPresent` es verdadero o el valor actual o configurado es `gpsdo`.
- **External 10 MHz** aparece cuando la radio informa cualquier estado del oscilador, cuando `extPresent` es verdadero, o cuando el valor actual o configurado es `external`.

El combo preselecciona el valor que coincide con la configuración actual de la radio (`oscSetting`). Si ese valor no está en la lista, se usa el elemento seleccionado anteriormente; si ninguno está presente, se selecciona **Auto**.

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Line Out | — | — | Control deslizante de ganancia de salida de línea. |
| Mute (Line Out) | — | — | Silencia la salida de línea. |
| Headphone | — | — | Control deslizante de ganancia de auriculares. |
| Mute (Headphone) | — | — | Silencia los auriculares. |
| Front Speaker / Mute | — | — | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink) | Auto | Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. |
| Prevent system sleep while connected | Falso | — | Mantiene el SO despierto mientras la radio está conectada para evitar caídas en flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input / Output | — | — | Selecciona los dispositivos de audio de entrada/salida del host. |
| Audio Boost | — | — | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| Audio Buffer | 200 ms | 50–1000 ms | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Se almacena como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Radio Side | Radio Side / Client Side | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. |
| Save to | — | — | Carpeta para grabaciones guardadas (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`. |
| ... (browse) | — | — | Navega para buscar la carpeta de grabación. |
| Auto-record on TX | Falso | — | Graba automáticamente mientras se transmite. Se almacena como `QsoRecordingAutoRecord`. |
| Idle timeout | 120 s | 10–3600 s | Segundos de silencio antes de detener la grabación. Se almacena como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | — | — | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Antenas

La pestaña Antenas (nueva en v26.5.2.1) permite nombrar y configurar antenas. Esta pestaña se construye de forma diferida al hacer clic por primera vez.

## Pestaña Filtros

La pestaña Filtros proporciona opciones de filtro de baja latencia / nítido por ancho de banda.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Control deslizante de nitidez de filtro Voice / CW / Digital | — | 0–3 | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. |
| Auto (Voice / CW / Digital) | — | — | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. |
| Use Low Latency Filters for Digital Modes | — | — | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transverter con pestañas anidadas, una por transverter, más una pestaña '+' para crear nuevos transverters.

| Control | Valor predeterminado | Comportamiento |
|---------|---------------------|----------------|
| RX Only | — | Fuerza solo RX en ese transverter. |
| Remove | — | Elimina la definición del transverter. |
| Create New Transverter | — | Agrega una nueva entrada de transverter. |

## Pestaña Cables USB

La pestaña Cables USB asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Comportamiento |
|---------|----------------|
| Cables list / Status | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| Name / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Parámetros serie y comportamiento por cable. |

## Pestaña Periféricos

La pestaña Periféricos configura conexiones IP manuales de dispositivos externos (TGXL, PGXL, Antenna Genius).

| Control | Valor predeterminado | Comportamiento |
|---------|---------------------|----------------|
| Connect / Disconnect (TGXL) | Connect | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL acciona el PTT de la radio a través de su cable de enclavamiento de hardware. Si el campo IP está vacío y la radio ha descubierto el TGXL, se rellena previamente la IP descubierta. |
| Connect / Disconnect (PGXL) | Connect | Abre/cierra una conexión TCP directa al Power
