# Diálogo de Configuración de Radio

## Descripción General

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona acceso a información de la radio, ajustes de red, GPS, configuración de transmisión, ajustes de teléfono/CW, calibración de recepción, audio, filtros, transverters, cables USB, periféricos, puertos serie y gestión de certificados SmartLink.

Para abrir el diálogo, haga clic en `Settings > Radio Setup...`. El diálogo requiere una conexión activa con la radio.

## Pestaña Radio

La pestaña Radio muestra información de identificación de la radio, detalles de licencia y controles de actualización de firmware.

### Campos de Información

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Radio SN | Indicador | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| Región | Indicador | Región regulatoria de la radio. |
| HW Version | Indicador | Cadena de versión de hardware. Incluye un botón de copia al portapapeles. |
| Opciones | Indicador | Muestra las opciones de radio licenciadas. Incluye un botón de copia al portapapeles. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. |
| Modelo | Indicador | Modelo de la radio. Incluye un botón de copia al portapapeles. |
| Apodo | Campo de texto | Apodo de la radio definido por el usuario. |
| Indicativo | Campo de texto | Indicativo de la estación. |
| Nombre de Estación | Campo de texto | Identifica a este cliente AetherSDR frente a otras estaciones multiFLEX. Por defecto usa el nombre del host del SO si está vacío. Se almacena como `StationName` en AppSettings. Se envía a la radio como 'estación cliente <nombre>'. |
| Información de Licencia (Suscripción / Vencimiento / ID de Radio / Versión Licenciada) | Indicador | Muestra los detalles de la licencia desde la radio. Cada campo incluye un botón de copia al portapapeles. |

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Remote On | Botón pulsador | Habilita el encendido remoto / activación remota. |
| Reboot Radio | Botón pulsador | Envía un comando de reinicio a la radio conectada. Deshabilitado cuando la radio no está conectada. Muestra un diálogo de confirmación antes de reiniciar. En conexiones LAN, AetherSDR se reconecta automáticamente después del reinicio. En conexiones SmartLink/WAN, debe reconectarse manualmente. El diálogo se cierra tras la confirmación. Nuevo en v26.6.3. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Select Installer... | Botón pulsador | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae la carga útil .ssdr y emite progreso. |
| Upload Firmware | Botón pulsador | Inicia la carga de firmware con barra de progreso y estado. |

## Pestaña Red

La pestaña Red muestra información de red de la radio y opciones avanzadas de red.

### Campos de Información

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Dirección IP / Máscara / Dirección MAC | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Enforce Private IP Connections: | Botón de alternancia | Habilitado | - | Rechaza pares que no sean RFC1918. |
| Network MTU: | Spinbox | 1450 | 576-9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena como `NetworkMtu` en AppSettings. |
| DHCP / Static | Botón de alternancia | - | - | Alterna entre modos DHCP e IP estática. |
| Dirección IP: / Máscara: / Puerta de Enlace: | Campo de texto | - | - | Campos de configuración de IP estática. |
| Apply | Botón pulsador | - | - | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información de posición en vivo, incluyendo latitud, longitud, altitud, hora y conteo de satélites.

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall y el comportamiento de seguimiento entre slice y TX.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| TX Band Settings | Botón pulsador | - | - | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (en ms) | Spinbox | - | - | Tiempos de espera / retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | - | - | Habilita las entradas de enclavamiento RCA y Accessory. |
| Max Power: | Spinbox | - | 0-100 % | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode: | Cuadro combinado | - | - | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | - | - | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | Falso | - | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante una operación Split. |
| Active Slice Follows TX | Botón pulsador | Falso | - | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | - | - | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic: | Botón de alternancia | - | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode: A / B | Botón pulsador | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. |
| Swap: | Botón de alternancia | - | - | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | - | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX: | Botón de alternancia | - | - | Habilita el tecleo por macros CWX. |
| Decode: | Botón de alternancia | Verdadero | - | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. |
| RTTY Mark Default: | Spinbox | - | - | Frecuencia predeterminada de marca RTTY. |

## Pestaña RX

La pestaña RX proporciona calibración del desvío de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Cal Frequency (MHz): | Spinbox | - | - | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | - | - | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | - | - | Desvío de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Auto | Auto / TCXO / GPSDO / External | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Pestaña Audio

La pestaña Audio gestiona las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Line Out: | Deslizador | - | - | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | - | - | Silencia la salida de línea. |
| Headphone: | Deslizador | - | - | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | - | - | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | - | - | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Auto | - | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | Falso | - | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | - | - | Selecciona los dispositivos de audio de entrada/salida del host. |
| Audio Boost: | Botón de alternancia | - | - | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| Audio Buffer: | Campo de texto | 200 | 50-1000 ms | Aumenta el búfer de audio en milisegundos para mitigar la fluctuación en VPN/SmartLink. Se almacena como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Botón pulsador | Radio Side | Radio Side / Client Side | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. |
| Save to: | Campo de texto | - | - | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`. |
| ... | Botón pulsador | - | - | Examina para seleccionar la carpeta de grabaciones. |
| Auto-record on TX | Casilla de verificación | Falso | - | Graba automáticamente mientras se transmite. Se almacena como `QsoRecordingAutoRecord`. |
| Idle timeout: | Spinbox | 120 | 10-3600 segundos | Segundos de silencio antes de que se detenga la grabación. Se almacena como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Botón pulsador | - | - | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Filtros

La pestaña Filtros proporciona opciones de filtros de baja latencia y filtros nítidos por ancho de banda.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Deslizadores de nitidez de filtros Voice / CW / Digital | Deslizador | - | 0-3 | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. |
| Auto (Voice / CW / Digital) | Botón de alternancia | - | - | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. |
| Use Low Latency Filters for Digital Modes | Casilla de verificación | - | - | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR configura los ajustes por transverter, incluyendo RX Only, valid, remove y creación de nuevos transverters.

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| RX Only: | Botón de alternancia | Fuerza solo RX en ese transverter. |
| Remove (xvtr) | Botón pulsador | Elimina la definición del transverter. |
| Create New Transverter | Botón pulsador | Añade una nueva entrada de transverter. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Cables list / Estado | Indicador | Cables USB detectados por tipo con estado Plugged/Unplugged. |
| Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Cuadro combinado | Parámetros serie y comportamiento por cable. |

## Pestaña Periféricos

La pestaña Periféricos gestiona dispositivos externos mediante conexión IP manual (TGXL, PGXL, Antenna Genius).

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---------|------|---------|----------|
| Connect / Disconnect (TGXL) | Botón pulsador | Connect | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio, que está rota en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón pulsador | Connect | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón pulsador | Connect | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

## Pestaña APD

La pestaña APD proporciona selección del puerto de muestreo externo de Adaptive Pre-Distortion por antena de TX. La pestaña está oculta a menos que la radio informe `apd configurable=1` (FLEX-8x00 con SmartSDR 4.2.18+).

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| ANT1: / ANT2: / XVTA: / XVTB: | Cuadro combinado | Selecciona el puerto de muestreo (INTERNAL, RX_A, RX_B, XVTA, XVTB) que la radio utiliza para la realimentación de APD en esa antena de TX. INTERNAL muestrea dentro de la radio; los puertos externos requieren una señal de realimentación acoplada desde la salida del amplificador lineal. |
| Reset (APD Equalizer) | Botón pulsador | Limpia todos los datos de entrenamiento de APD por antena en la radio. |

## Pestaña Temas

La pesta
