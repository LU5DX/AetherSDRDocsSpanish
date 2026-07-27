# Diálogo de Configuración de la Radio

## Resumen

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona acceso a la información de la radio, ajustes de red, GPS, configuración de transmisión, ajustes de teléfono/CW, calibración de recepción, audio, filtros, transvertores, cables USB, periféricos, puertos serie, gestión de certificados anclados de SmartLink, configuración del receptor KiwiSDR y ajustes de APD.

Para abrir el diálogo, haga clic en `Settings > Radio Setup...`. El diálogo requiere una conexión activa con la radio.

## Pestaña Radio

La pestaña Radio muestra información de identificación de la radio, detalles de licencia y controles de actualización de firmware.

### Campos de Información

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Radio SN | Indicador | Número de serie del chasis (solo lectura). Incluye un botón para copiar al portapapeles junto al valor. |
| Region | Indicador | Región reglamentaria de la radio. |
| HW Version | Indicador | Cadena de la versión del hardware. Incluye un botón para copiar al portapapeles. |
| Options | Indicador | Muestra las opciones de radio licenciadas. Incluye un botón para copiar al portapapeles. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado habilitado de multiFLEX. |
| Model | Indicador | Modelo de la radio. Incluye un botón para copiar al portapapeles. |
| Nickname | Campo de texto | Apodo descriptivo de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa por defecto el nombre de host del SO. Se almacena como `StationName` en AppSettings. Se envía a la radio como 'client station <nombre>'. |
| License Info (Subscription / Expiration / Radio ID / Licensed version) | Indicador | Muestra los detalles de la licencia de la radio. Cada campo incluye un botón para copiar al portapapeles. |

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Remote On | Botón pulsador | Habilita el encendido remoto / remote-on. |
| Check for Update | Botón pulsador | Consulta si hay actualizaciones de firmware. |
| Select Installer... | Botón pulsador | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite el progreso. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones avanzadas de red.

### Campos de Información

| Control | Tipo | Comportamiento |
|---------|------|----------|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón para copiar al portapapeles. |

### Controles

| Control | Tipo | Valor por defecto | Rango válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Enforce Private IP Connections: | Botón de conmutación | Habilitado | - | Rechaza pares que no sean RFC1918. |
| Network MTU: | Spinbox | 1450 | 576-9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena como `NetworkMtu` en AppSettings. |
| DHCP / Static | Botón de conmutación | - | - | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | - | - | Campos de configuración de IP estática. |
| Apply | Botón pulsador | - | - | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS e información de posición en vivo, incluyendo latitud, longitud, altitud, hora y número de satélites.

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall y el comportamiento de seguimiento entre slice y TX.

### Controles

| Control | Tipo | Valor por defecto | Rango válido | Comportamiento |
|---------|------|---------|-------------|----------|
| TX Band Settings | Botón pulsador | - | - | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms) | Spinbox | - | - | Tiempos de espera/retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de conmutación | - | - | Habilita las entradas de enclavamiento RCA y accessory. |
| Max Power: | Spinbox | - | 0-100 % | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode: | Cuadro combinado | - | - | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de conmutación | - | - | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | Falso | - | TX sigue al slice activo. Es mutuamente excluyente con 'Active Slice Follows TX'. Se desactiva automáticamente durante una operación en Split. |
| Active Slice Follows TX | Botón pulsador | Falso | - | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con 'TX Follows Active Slice'. |

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Controles

| Control | Tipo | Valor por defecto | Rango válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Enable/Disable the Level Meter During Receive | Botón de conmutación | - | - | Muestra el medidor de nivel del micrófono incluso en RX. |
| Iambic: | Botón de conmutación | - | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode: A / B | Botón pulsador | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| Swap: | Botón de conmutación | - | - | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | - | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX: | Botón de conmutación | - | - | Habilita el macrokeying CWX. |
| Decode: | Botón de conmutación | Verdadero | - | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. |
| RTTY Mark Default: | Spinbox | - | - | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona calibración del desplazamiento de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

### Controles

| Control | Tipo | Valor por defecto | Rango válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Cal Frequency (MHz): | Spinbox | - | - | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | - | - | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | - | - | Desplazamiento de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Auto | Auto / TCXO / GPSDO / External | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Pestaña Audio

La pestaña Audio gestiona las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Controles

| Control | Tipo | Valor por defecto | Rango válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Line Out: | Deslizador | - | - | Ganancia de la salida de línea. |
| Mute (Line Out) | Botón pulsador | - | - | Silencia la salida de línea. |
| Headphone: | Deslizador | - | - | Ganancia de los auriculares. |
| Mute (Headphone) | Botón pulsador | - | - | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | - | - | Silencia el altavoz frontal (depende del modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Auto | - | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | Falso | - | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en los flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | - | - | Selecciona los dispositivos de audio de entrada/salida del host. |
| Audio Boost: | Botón de conmutación | - | - | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| Audio Buffer: | Campo de texto | 200 | 50-1000 ms | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Se almacena como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Botón pulsador | Radio Side | Radio Side / Client Side | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. |
| Save to: | Campo de texto | - | - | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`. |
| ... | Botón pulsador | - | - | Navega para seleccionar la carpeta de grabaciones. |
| Auto-record on TX | Casilla de verificación | Falso | - | Graba automáticamente mientras se transmite. Se almacena como `QsoRecordingAutoRecord`. |
| Idle timeout: | Spinbox | 120 | 10-3600 seg | Segundos de silencio antes de que se detenga la grabación. Se almacena como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Botón pulsador | - | - | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Filters

La pestaña Filters proporciona opciones de filtros de baja latencia y nítidos por ancho de banda.

### Controles

| Control | Tipo | Valor por defecto | Rango válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Voice / CW / Digital filter sharpness sliders | Deslizador | - | 0-3 | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está habilitado. |
| Auto (Voice / CW / Digital) | Botón de conmutación | - | - | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. |
| Use Low Latency Filters for Digital Modes | Casilla de verificación | - | - | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR configura ajustes por transverter, incluyendo Solo RX, válido, eliminar y crear nuevo transverter.

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| RX Only: | Botón de conmutación | Fuerza solo RX en ese transverter. |
| Remove (xvtr) | Botón pulsador | Elimina la definición del transverter. |
| Create New Transverter | Botón pulsador | Añade una nueva entrada de transverter. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Cables list / Status | Indicador | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Cuadro combinado | Parámetros serie y comportamiento por cable. |

## Pestaña Peripherals

La pestaña Peripherals gestiona dispositivos externos mediante conexión IP manual (TGXL, PGXL, Antenna Genius).

### Controles

| Control | Tipo | Valor por defecto | Comportamiento |
|---------|------|---------|----------|
| Connect / Disconnect (TGXL) | Botón pulsador | Connect | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Es necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón pulsador | Connect | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón pulsador | Connect | Abre/cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

## Pestaña APD

La pestaña APD proporciona selección del puerto de muestra de Predistorsión Adaptativa externa por antena de TX. La pestaña está oculta a menos que la radio informe `apd configurable=1` (FLEX-8x00 con SmartSDR 4.2.18+).

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| ANT1: / ANT2: / XVTA: / XVTB: | Cuadro combinado | Selecciona el puerto de muestra (INTERNAL, RX_A, RX_B, XVTA, XVTB) que la radio utiliza para la realimentación de APD en esa antena de TX. INTERNAL muestrea dentro de la radio; los puertos externos requieren una señal de realimentación acoplada desde la salida del amplificador lineal. |
| Reset (APD Equalizer) | Botón pulsador | Borra todos los datos de entrenamiento de APD por antena en la radio. |

## Pestaña KiwiSDR

La pestaña KiwiSDR gestiona la conexión a receptores públicos KiwiSDR para capacidades de RX remotas.

### Controles

| Control | Tipo | Valor por defecto | Comportamiento |
|---------|------|---------|----------|
| KiwiSDR Receiver URL | Campo de texto | - | URL del receptor KiwiSDR al que conectarse. |
| Connect / Disconnect | Botón pulsador | Connect | Establece o finaliza la conexión con el receptor KiwiSDR configurado. |
