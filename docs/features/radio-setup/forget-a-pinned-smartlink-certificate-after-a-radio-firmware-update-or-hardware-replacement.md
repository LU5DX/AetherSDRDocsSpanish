# Referencia del diálogo de configuración de la radio

El diálogo **Radio Setup** es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, configuración de red, GPS, TX, Phone/CW, RX, audio, filtros, transverters, cables USB, periféricos, APD, temas, gestión de certificados SmartLink y configuración de puertos serie.

## Abrir el diálogo

1. Haga clic en **Settings > Radio Setup...** en el menú principal.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

Muchos valores de solo lectura (número de serie, versión de HW, opciones, modelo, detalles de suscripción, dirección IP, dirección MAC, versión de firmware) incluyen un botón de copia al portapapeles junto a la etiqueta. Haga clic en este botón para copiar el valor a su portapapeles y compartirlo con el soporte técnico.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Radio SN | Indicador | Número de serie del chasis (solo lectura). Incluye botón de copia al portapapeles. |
| Region | Indicador | Región regulatoria de la radio. Valor predeterminado: USA. |
| HW Version | Indicador | Cadena de versión del hardware. Incluye botón de copia al portapapeles. |
| Remote On | Botón pulsador | Habilita el encendido/activación remota. |
| Options | Indicador | Opciones de radio licenciadas. Incluye botón de copia al portapapeles. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado habilitado de multiFLEX. |
| Model | Indicador | Modelo de la radio. Incluye botón de copia al portapapeles. |
| Nickname | Campo de texto | Apodo amigable de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Por defecto, usa el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como 'client station <name>'. |
| License Info | Indicador | Muestra detalles de la licencia, incluyendo Suscripción, Vencimiento, ID de radio y Versión licenciada. Cada campo incluye un botón de copia al portapapeles. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Select Installer... | Botón pulsador | Abre un diálogo de archivo para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae la carga útil .ssdr y emite el progreso. La etiqueta cambió de 'Browse .ssdr...' en v26.5.3. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |

## Pestaña Network

La pestaña **Network** muestra la información de red de la radio y opciones avanzadas de red.

| Control | Tipo | Descripción |
|---------|------|-------------|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |
| Enforce Private IP Connections: | Botón de alternancia | Rechaza pares que no sean RFC1918. |
| Network MTU: | Control giratorio | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Valor predeterminado: 1450. Rango válido: 576-9000 bytes. Se almacena en AppSettings como `NetworkMtu`. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña **TX** configura los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y proporciona un acceso directo a la Configuración de Banda de TX.

| Control | Tipo | Descripción |
|---------|------|-------------|
| TX Band Settings | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms) | Control giratorio | Tiempos de retención/retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y de accesorio. |
| Max Power: | Control giratorio | Establece el límite de potencia de TX a nivel de radio. Rango válido: 0-100%. |
| Tune Mode: | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | Valor predeterminado: False. TX sigue la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se desactiva automáticamente durante una operación en Split. Se almacena como `TxFollowsActiveSlice`. |
| Active Slice Follows TX | Botón pulsador | Valor predeterminado: False. Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. Se almacena como `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el manipulador iambic en la radio. En v0.9.1, se agregaron los botones Mode A y Mode B junto al interruptor Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el nuevo manipulador iambic local por software (IambicKeyer) que refleja el estado iambic de la radio para un tono lateral inferior a 5 ms. |
| Iambic Mode: A / B | Botón pulsador | Valor predeterminado: A. Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente añadido en v0.9.1. |
| Swap: | Botón de alternancia | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | Selecciona la banda lateral del tono CW. Opciones: LSB, USB. |
| CWX: | Botón de alternancia | Habilita la activación de macros CWX. |
| Decode: | Botón de alternancia | Valor predeterminado: True. Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. |
| RTTY Mark Default: | Control giratorio | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña **RX** configura la calibración del desplazamiento de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Cal Frequency (MHz): | Control giratorio | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Control giratorio | Desplazamiento de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Valor predeterminado: Auto. Las opciones dependen del hardware instalado: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos del PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Line Out: | Deslizador | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone: | Deslizador | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Valor predeterminado: Auto. Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | Valor predeterminado: False. Mantiene el SO activo mientras la radio está conectada para evitar caídas en los flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | Selecciona los dispositivos de audio de entrada/salida del host. |
| Audio Boost: | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| Audio Buffer: | Campo de texto | Valor predeterminado: 200. Aumenta el búfer de audio en milisegundos para compensar la fluctuación en VPN/SmartLink. Rango válido: 50-1000 ms. Se almacena como `AudioBufferMs`. Se aplica a AudioEngine::setRxBufferCapMs(). |
| Recording: Radio Side / Client Side | Botón pulsador | Valor predeterminado: Radio Side. Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. |
| Save to: | Campo de texto | Carpeta para grabaciones guardadas (solo lado del cliente). Por defecto, Documents/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`. |
| ... | Botón pulsador | Navega para seleccionar la carpeta de grabación. |
| Auto-record on TX | Casilla de verificación | Valor predeterminado: False. Graba automáticamente mientras se transmite. Se almacena como `QsoRecordingAutoRecord`. |
| Idle timeout: | Control giratorio | Valor predeterminado: 120. Segundos de silencio antes de que se detenga la grabación. Rango válido: 10-3600 seg. Se almacena como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Botón pulsador | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Filters

La pestaña **Filters** configura opciones de filtro de baja latencia y filtro nítido por ancho de banda.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Voice / CW / Digital filter sharpness sliders | Deslizador | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo. El deslizador está deshabilitado cuando Auto está habilitado. Los comandos se envían como 'radio filter_sharpness <mode> level=<N>'. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo. Deshabilita el deslizador de nitidez manual. Los comandos se envían como 'radio filter_sharpness <mode> auto_level=1'. |
| Use Low Latency Filters for Digital Modes | Casilla de verificación | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña **XVTR** configura ajustes por transverter. Contiene pestañas anidadas, una por transverter, y una pestaña '+' para crear nuevas.

| Control | Tipo | Descripción |
|---------|------|-------------|
| RX Only: | Botón de alternancia | Fuerza solo RX en ese transverter. |
| Remove (xvtr) | Botón pulsador | Elimina la definición del transverter. |
| Create New Transverter | Botón pulsador | Agrega una nueva entrada de transverter. |

## Pestaña USB Cables

La pestaña **USB Cables** asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Cables list / Status | Indicador | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Cuadro combinado | Parámetros serie y comportamiento por cable. |

## Pestaña Peripherals

La pestaña **Peripherals** configura la conexión IP manual de dispositivos externos para TGXL, PGXL y Antenna Genius.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Connect / Disconnect (TGXL) | Botón pulsador | Valor predeterminado: Connect. Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en TGXL_ManualIp y TGXL_ManualPort al conectar, para que AetherSDR se reconecte automáticamente al inicio. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta rota del lado de la radio. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón pulsador | Valor predeterminado: Connect. Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en PGXL_ManualIp y PGXL_ManualPort. |
| Connect / Disconnect (Antenna Genius) | Botón pulsador | Valor predeterminado: Connect. Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en AG_ManualIp y AG_ManualPort. |

## Pestaña APD

La pestaña **APD** configura la selección del puerto de muestra de Predistorsión Adaptativa externa por antena de TX (ANT1, ANT2, XVTA, XVTB). Esta pestaña está oculta a menos que la radio informe apd configurable=1 (FLEX-8x00 con SmartSDR 4.2.18+). Añadida en v26.5.1 (#2186). Se crea de forma diferida solo cuando se hace clic en la pestaña por primera vez.

| Control | Tipo | Descripción |
|---------|------|-------------|
| ANT1: / ANT2: / XVTA: / XVTB: | Cuadro combinado | Selecciona el puerto de muestra (INTERNAL, RX_A, RX_B, XVTA, XVTB) que la radio utiliza para la retroalimentación APD en esa antena de TX. INTERNAL muestrea dentro de la radio; los puertos externos requieren una señal de retroalimentación acoplada desde la salida del amplificador lineal. Al cambiar, se envía setApdSamplerPort() a la radio. |
| Reset (APD Equalizer) | Botón pulsador | Limpia todos los datos de entrenamiento APD por antena en la radio. Envía resetApdEqualizer() al TransmitModel de la radio. |

## Pestaña Themes

La pestaña **Themes** configura los ajustes de apariencia de la interfaz
