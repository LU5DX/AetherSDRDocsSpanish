# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, APD, temas, serie (FlexControl) y nombres de antenas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio para acceder a la mayoría de las pestañas.
- Abra `Settings > Radio Setup...`.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

| Control | Valor predeterminado | Comportamiento |
|---------|---------|----------|
| Radio SN | — | Número de serie del chasis (solo lectura). |
| Region | USA | Región regulatoria de la radio. |
| HW Version | — | Cadena de versión del hardware. |
| Remote On | — | Habilita el encendido remoto. |
| Options | — | Muestra las opciones de radio licenciadas. |
| FlexControl | — | Estado detectado del hardware FlexControl. |
| multiFLEX | — | Estado habilitado de multiFLEX. |
| Model | — | Modelo de la radio. |
| Nickname | — | Apodo descriptivo de la radio. |
| Callsign | — | Indicativo de la estación. |
| Station Name | — | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Se usa el nombre del sistema operativo si está vacío. Se almacena como `StationName`. |
| License Info | — | Muestra los detalles de la licencia de la radio (Suscripción / Vencimiento / ID de la radio / Versión licenciada). |
| Check for Update | — | Consulta actualizaciones de firmware. |
| Select Installer... | — | Selecciona un archivo de imagen de firmware (`.msi`, `.exe`, o `.ssdr`). |
| Upload Firmware | — | Inicia la carga del firmware con barra de progreso y estado. |

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

| Control | Valor predeterminado | Comportamiento |
|---------|---------|----------|
| IP Address / Mask / MAC Address | — | Direcciones de red de solo lectura. |
| Enforce Private IP Connections | — | Rechaza pares que no sean RFC1918. |
| Network MTU | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576–9000). Almacenado como `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| DHCP / Static | — | Cambia entre modos DHCP e IP estática. |
| IP Address / Mask / Gateway | — | Campos de configuración de IP estática. |
| Apply | — | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña TX configura tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y configuraciones de banda de TX.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| TX Band Settings | — | — | Abre el diálogo dedicado de potencia/sintonía por banda. |
| ACC TX | — | — | Retardo de colgado de TX en milisegundos. |
| TX Delay | — | — | Retardo de TX en milisegundos. |
| RCA TX1 | — | — | Retardo de RCA TX1 en milisegundos. |
| Timeout (sec) | — | — | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |
| RCA TX2 | — | — | Retardo de RCA TX2 en milisegundos. |
| Interlocks - TX REQ: RCA / Accessory | — | — | Habilita las entradas de enclavamiento RCA y accessory. |
| Max Power | — | 0–100 % | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode | — | — | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall | — | — | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | False | — | TX sigue al slice activo. Excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante una operación de división (Split). |
| Active Slice Follows TX | False | — | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Excluyente con 'TX Follows Active Slice'. |

### Campos de tiempo

Los campos de tiempo en la pestaña TX aceptan valores en milisegundos, excepto Timeout (sec) que muestra y acepta valores en segundos para facilitar la lectura. La radio almacena el valor de tiempo de espera internamente en milisegundos.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| Enable/Disable the Level Meter During Receive | — | — | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic | — | Enabled / Disabled | Habilita o deshabilita el manipulador iámbico en la radio. |
| Iambic Mode: A / B | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local de software. |
| Swap | — | — | Intercambia dit/dah. |
| Sideband | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX | — | — | Habilita el keying de macros CWX. |
| Decode | True | — | Habilita la superposición de decodificación CW en el panadapter. Almacenado como `CwDecodeOverlay`. |
| RTTY Mark Default | — | — | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona calibración de offset de frecuencia con GPSDO y selección de la fuente de referencia de 10 MHz.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| Cal Frequency (MHz) | — | — | Frecuencia usada para calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| Start | — | — | Establece la frecuencia de calibración, reinicia `freq_error_ppb` a 0, luego inicia el barrido de calibración del PLL de la radio. El botón se deshabilita y etiqueta como **Busy** mientras la calibración se ejecuta. |
| Freq Offset (ppb) | — | — | Offset de frecuencia manual en partes por billón. |
| 10 MHz Reference Source | Auto | Auto / TCXO / GPSDO / External 10 MHz | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. |

### 10 MHz Reference Source

El combo se llena dinámicamente cada vez que se abre el diálogo o la radio informa el estado del oscilador:

- **Auto** está siempre presente.
- **TCXO** aparece cuando la radio informa cualquier estado del oscilador, cuando `tcxoPresent` es verdadero, o cuando el valor actual o configurado es `tcxo`.
- **GPSDO** aparece cuando `gpsdoPresent` es verdadero o el valor actual o configurado es `gpsdo`.
- **External 10 MHz** aparece cuando la radio informa cualquier estado del oscilador, cuando `extPresent` es verdadero, o cuando el valor actual o configurado es `external`.

El combo preselecciona el valor que coincide con la configuración actual de la radio (`oscSetting`). Si ese valor no está en la lista, se usa el elemento previamente seleccionado; si ninguno está presente, se selecciona **Auto**.

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| Line Out | — | — | Control deslizante de ganancia de salida de línea. |
| Mute (Line Out) | — | — | Silencia la salida de línea. |
| Headphone | — | — | Control deslizante de ganancia de auriculares. |
| Mute (Headphone) | — | — | Silencia los auriculares. |
| Front Speaker / Mute | — | — | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink) | Auto | Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. Almacenado como `AudioCompression`. |
| Prevent system sleep while connected | False | — | Mantiene el SO activo mientras la radio está conectada para evitar caídas en los flujos de audio/TCP/UDP durante la inactividad. Almacenado como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input / Output | — | — | Selecciona los dispositivos de audio de entrada/salida del host. |
| Audio Boost | — | — | Habilita ganancia adicional en la ruta de audio del cliente. Almacenado como `AudioBoost`. |
| Audio Buffer | 200 ms | 50–1000 ms | Aumenta el búfer de audio en milisegundos para fluctuaciones en VPN/SmartLink. Almacenado como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Radio Side | Radio Side / Client Side | Selecciona la grabación del lado de la radio o del lado del cliente. Almacenado como `RecordingMode`. |
| Save to | — | — | Carpeta para grabaciones guardadas (solo lado del cliente). Valor predeterminado: Documents/AetherSDR/Recordings. Almacenado como `QsoRecordingDir`. |
| ... (browse) | — | — | Navega para seleccionar la carpeta de grabación. |
| Auto-record on TX | False | — | Graba automáticamente mientras transmite. Almacenado como `QsoRecordingAutoRecord`. |
| Idle timeout | 120 sec | 10–3600 sec | Segundos de silencio antes de detener la grabación. Almacenado como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | — | — | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Antennas

La pestaña Antennas (nueva en v26.5.2.1) permite nombrar y configurar antenas. Esta pestaña se construye de forma diferida al hacer clic por primera vez.

## Pestaña Filters

La pestaña Filters proporciona opciones de filtro de baja latencia / nítido por ancho de banda.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| Voice / CW / Digital filter sharpness sliders | — | 0–3 | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. |
| Auto (Voice / CW / Digital) | — | — | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. |
| Use Low Latency Filters for Digital Modes | — | — | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transverter con pestañas anidadas, una por transverter, más una pestaña '+' para crear nuevos transverters.

| Control | Valor predeterminado | Comportamiento |
|---------|---------|----------|
| RX Only | — | Fuerza solo RX en ese transverter. |
| Remove | — | Elimina la definición del transverter. |
| Create New Transverter | — | Agrega una nueva entrada de transverter. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Comportamiento |
|---------|----------|
| Cables list / Status | Cables USB detectados por tipo con estado Plugged/Unplugged. |
| Name / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Parámetros serie y comportamiento por cable. |

## Pestaña Peripherals

La pestaña Peripherals configura conexiones IP manuales de dispositivos externos (TGXL, PGXL, Antenna Genius).

| Control | Valor predeterminado | Comportamiento |
|---------|---------|----------|
| Connect / Disconnect (TGXL) | Connect | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de enclavamiento de hardware. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Connect | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Connect | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |

### Cómo borrar IP guardadas

Cuando se hace clic en el botón **Connect** mientras el campo IP está vacío, la IP manual y el puerto guardados para ese dispositivo se eliminan de la configuración. Si cierra el diálogo Radio Setup con un campo IP vacío y existe una IP manual previamente guardada, AetherSDR elimina automáticamente esa IP y puerto guardados de la configuración y desconecta el dispositivo si está actualmente conectado.

## Pestaña APD

La pestaña APD (External Adaptive Pre-Distortion) configura la selección del puerto de muestreo por antena de TX. La pestaña está oculta a menos que la radio informe `apd configurable=1` (FLEX-8x00 con SmartSDR 4.2.18+). Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible.

| Control | Valor predeterminado | Comportamiento |
|---------|---------|----------|
| ANT1 / ANT2 / XVTA / XVTB sampler combos | INTERNAL | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF de salida para el entrenamiento de APD para esa antena de TX. Opciones: INTERNAL, RX_A, RX_B, XVTA, XVTB. INTERNAL muestrea dentro de la radio; los puertos externos requieren una señal de realimentación acoplada desde el amplificador lineal.
