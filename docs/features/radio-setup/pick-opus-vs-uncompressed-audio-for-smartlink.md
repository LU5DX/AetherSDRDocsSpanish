# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, APD, temas, serie (FlexControl), nombres de antenas, gestión de certificados SmartLink y acceso a receptores públicos KiwiSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio para acceder a la mayoría de las pestañas.
- Abra `Settings > Radio Setup...`.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, la información de licencia y los controles de actualización de firmware.

| Control | Valor Predeterminado | Comportamiento |
|---------|---------------------|----------------|
| Radio SN | Número de serie del chasis (solo lectura). | Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. Nuevo en v26.5.3 (#2976). |
| Region | USA | Región regulatoria de la radio. |
| HW Version | Cadena de versión del hardware. | Incluye un botón de copia al portapapeles junto al valor (#2976). |
| Remote On | — | Activa el encendido remoto / remote-on. |
| Options | Muestra las opciones de radio licenciadas. | Incluye un botón de copia al portapapeles junto al valor (#2976). |
| FlexControl | — | Estado detectado del hardware FlexControl. |
| multiFLEX | — | Estado de multiFLEX habilitado. |
| Model | Modelo de la radio. | Incluye un botón de copia al portapapeles junto al valor (#2976). |
| Nickname | — | Apodo de la radio fácil de usar. |
| Callsign | — | Indicativo de la estación. |
| Station Name | — | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Usa el nombre de host del sistema operativo si está vacío. Se almacena como `StationName`. |
| License Info | — | Muestra los detalles de la licencia de la radio (Suscripción / Vencimiento / ID de Radio / Versión con licencia). Haga clic en el botón de copia para copiarlo al portapapeles. |
| Check for Update | — | Consulta actualizaciones de firmware. |
| Select Installer... | — | Elige un archivo de imagen de firmware (`.msi`, `.exe` o `.ssdr`). |
| Upload Firmware | — | Inicia la carga del firmware con barra de progreso y estado. |
| Reboot Radio | — | Solicita confirmación, luego reinicia la radio conectada. AetherSDR se desconecta durante el reinicio. Se reconecta automáticamente en LAN; SmartLink/WAN requiere reconexión manual. El botón está deshabilitado cuando la radio no está conectada. Nuevo en v26.6.3. |

### Botones de copiar valor

Cada indicador de solo lectura (Radio SN, HW Version, License Info, etc.) ahora muestra un pequeño botón de copia superpuesto al pasar el cursor o enfocarlo. Al hacer clic en el botón, se copia el valor mostrado al portapapeles del sistema. Aparece un breve mensaje emergente "copiado" cerca del botón después de una copia exitosa.

### Estado de carga del firmware

El área de carga de firmware muestra una barra de progreso y texto de estado durante una carga activa. Cuando no hay ninguna carga en curso, el área de estado está vacía.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación antes de que proceda el reinicio. AetherSDR se desconecta durante el reinicio:

- **Conexión LAN:** AetherSDR se reconecta automáticamente una vez que la radio termina de iniciarse.
- **Conexión SmartLink/WAN:** Debe reconectarse manualmente después de que la radio se inicie.

El botón está deshabilitado cuando la radio no está conectada. Se actualiza automáticamente cuando el estado de la conexión cambia, por lo que no necesita volver a abrir el diálogo.

## Pestaña Red

La pestaña Red muestra la información de red de la radio y opciones de red avanzadas.

| Control | Valor Predeterminado | Comportamiento |
|---------|---------------------|----------------|
| IP Address / Mask / MAC Address | — | Direcciones de red de solo lectura. |
| Enforce Private IP Connections | — | Rechaza pares que no sean RFC1918. |
| Network MTU | 1450 | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes (576–9000). Se almacena como `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de las VPN/túneles SD-WAN. |
| DHCP / Static | — | Cambia entre los modos DHCP e IP estática. |
| IP Address / Mask / Gateway | — | Campos de configuración de IP estática. |
| Apply | — | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña TX configura los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y configuración de banda TX.

| Control | Valor Predeterminado | Rango Válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| TX Band Settings | — | — | Abre el diálogo dedicado de potencia/sintonía por banda. |
| ACC TX | — | — | Retardo de hang de TX en milisegundos. |
| TX Delay | — | — | Retardo de TX en milisegundos. |
| RCA TX1 | — | — | Retardo de RCA TX1 en milisegundos. |
| Timeout (sec) | — | — | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |
| RCA TX2 | — | — | Retardo de RCA TX2 en milisegundos. |
| Interlocks - TX REQ: RCA / Accessory | — | — | Activa las entradas de enclavamiento RCA y de accesorio. |
| Max Power | — | 0–100 % | Establece el límite de potencia TX a nivel de radio. |
| Tune Mode | — | — | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall | — | — | Dibuja la señal TX en el waterfall. |
| TX Follows Active Slice | Falso | — | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Falso | — | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

### Campos de temporización

Los campos de temporización en la pestaña TX aceptan valores en milisegundos, excepto Timeout (sec), que muestra y acepta valores en segundos para facilitar la lectura. La radio almacena el valor de tiempo de espera internamente en milisegundos.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Valor Predeterminado | Rango Válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Enable/Disable the Level Meter During Receive | — | — | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic | — | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en la radio. |
| Iambic Mode: A / B | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. |
| Swap | — | — | Intercambia dit/dah. |
| Sideband | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX | — | — | Habilita la activación por macros CWX. |
| Decode | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. |
| RTTY Mark Default | — | — | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona calibración de desviación de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

| Control | Valor Predeterminado | Rango Válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Cal Frequency (MHz) | — | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| Start | — | — | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0, luego inicia el barrido de calibración del PLL de la radio. El botón está deshabilitado y etiquetado como **Busy** mientras la calibración se está ejecutando. |
| Freq Offset (ppb) | — | — | Desviación de frecuencia manual en partes por billón. |
| 10 MHz Reference Source | Auto | Auto / TCXO / GPSDO / External 10 MHz | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. |

### 10 MHz Reference Source

El combo se llena dinámicamente cada vez que se abre el diálogo o la radio informa el estado del oscilador:

- **Auto** siempre está presente.
- **TCXO** aparece cuando la radio informa cualquier estado del oscilador, cuando `tcxoPresent` es verdadero, o cuando el valor actual o configurado es `tcxo`.
- **GPSDO** aparece cuando `gpsdoPresent` es verdadero o el valor actual o configurado es `gpsdo`.
- **External 10 MHz** aparece cuando la radio informa cualquier estado del oscilador, cuando `extPresent` es verdadero, o cuando el valor actual o configurado es `external`.

El combo preselecciona el valor que coincide con la configuración actual de la radio (`oscSetting`). Si ese valor no está en la lista, se usa el elemento seleccionado previamente; si ninguno está presente, se selecciona **Auto**.

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Valor Predeterminado | Rango Válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Line Out | — | — | Control deslizante de ganancia de salida de línea. |
| Mute (Line Out) | — | — | Silencia la salida de línea. |
| Headphone | — | — | Control deslizante de ganancia de auriculares. |
| Mute (Headphone) | — | — | Silencia los auriculares. |
| Front Speaker / Mute | — | — | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink) | Auto | Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. |
| Prevent system sleep while connected | Falso | — | Mantiene el sistema operativo despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input / Output | — | — | Elige los dispositivos de entrada/salida de audio del host. |
| Audio Boost | — | — | Activa ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| Audio Buffer | 200 ms | 50–1000 ms | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Se almacena como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Radio Side | Radio Side / Client Side | Elige la grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. |
| Save to | — | — | Carpeta para las grabaciones guardadas (solo del lado del cliente). El valor predeterminado es Documentos/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`. |
| ... (browse) | — | — | Navega para buscar la carpeta de grabaciones. |
| Auto-record on TX | Falso | — | Graba automáticamente mientras transmite. Se almacena como `QsoRecordingAutoRecord`. |
| Idle timeout | 120 seg | 10–3600 seg | Segundos de silencio antes de que se detenga la grabación. Se almacena como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | — | — | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Antennas

La pestaña Antennas (nueva en v26.5.2.1) permite nombrar y configurar antenas. Esta pestaña se construye de forma diferida cuando se hace clic en ella por primera vez.

## Pestaña Filters

La pestaña Filters proporciona opciones de filtro de baja latencia/nítido por ancho de banda.

| Control | Valor Predeterminado | Rango Válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | — | 0–3 | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo; el control deslizante está deshabilitado cuando Auto está activado. |
| Auto (Voice / CW / Digital) | — | — | Activa la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. |
| Use Low Latency Filters for Digital Modes | — | — | Fuerza filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transvertedor con pestañas anidadas, una por transvertedor, más una pestaña '+' para crear nuevos transvertedores.

| Control | Valor Predeterminado | Comportamiento |
|---------|---------------------|----------------|
| RX Only | — | Fuerza solo RX en ese transvertedor. |
| Remove | — | Elimina la definición del transvertedor. |
| Create New Transverter | — | Añade una nueva entrada de transvertedor. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Comportamiento |
|---------|----------------|
| Lista de cables / Estado | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| Name / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Parámetros serie y comportamiento por cable. |

## Pestaña Peripherals

La pestaña Peripherals (nueva en v26.7.4) proporciona conexiones TCP directas a amplificadores externos (TGXL, PGXL, ACOM) y controladores de antena (Antenna Genius) para estaciones donde el descubrimiento nativo de FlexRadio no está disponible o no funciona.

| Control | Valor Predeterminado | Comportamiento |
|---------|---------------------|----------------|
| Connect / Disconnect (TGXL) | Connect | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. |
| Connect / Disconnect (PGXL) | Connect | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (ACOM) | Connect | Abre/cierra
