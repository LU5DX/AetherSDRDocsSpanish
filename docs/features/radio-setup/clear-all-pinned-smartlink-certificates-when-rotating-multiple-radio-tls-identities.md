# Diálogo de Configuración de Radio

El diálogo de **Configuración de Radio** es la ventana maestra de configuración por radio. Contiene información de la radio, ajustes de red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, puerto serie de periféricos, gestión de certificados fijados de SmartLink y ajustes de receptores públicos KiwiSDR.

## Abrir el diálogo

1. Haga clic en **Settings > Radio Setup...** en el menú principal.

## Radio (pestaña)

La pestaña Radio muestra la identificación de la radio, información de licencia y proporciona controles de actualización de firmware.

### Indicadores de solo lectura con botones de copia

Todos los campos de solo lectura incluyen un botón de copia al portapapeles (icono de bandeja) junto a la etiqueta para facilitar su uso compartido con soporte técnico.

| Control | Comportamiento |
|---------|----------------|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles. |
| **Region** | Región regulatoria de la radio (solo lectura). Incluye un botón de copia al portapapeles. |
| **HW Version** | Cadena de versión del hardware (solo lectura). Incluye un botón de copia al portapapeles. |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). Incluye un botón de copia al portapapeles. |
| **Model** | Modelo de la radio (solo lectura). Incluye un botón de copia al portapapeles. |
| **License Info** campos | Muestra Suscripción, Vencimiento, ID de Radio y Versión licenciada. Cada uno incluye un botón de copia al portapapeles. |

### Otros controles en la pestaña Radio

| Control | Comportamiento | Clave de ajuste |
|---------|----------------|-----------------|
| **FlexControl** | Estado detectado del hardware FlexControl. | (ninguna) |
| **multiFLEX** | Estado habilitado de multiFLEX. | (ninguna) |
| **Nickname** | Apodo amigable de la radio. | (ninguna) |
| **Callsign** | Indicativo de la estación. | (ninguna) |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre del host del sistema operativo si está vacío. | `StationName` |
| **Remote On** | Habilita el encendido remoto / remote-on. | (ninguna) |
| **Check for Update** | Consulta actualizaciones de firmware. | (ninguna) |
| **Select Installer...** | Abre un diálogo de archivo para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr pre-extraído. | (ninguna) |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. | (ninguna) |

## Network (pestaña)

Configuración de red avanzada para la radio.

| Control | Comportamiento | Clave de ajuste |
|---------|----------------|-----------------|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. | (ninguna) |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918. El botón de alternancia muestra "Enabled" cuando está marcado. | (ninguna) |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576-9000). Valor predeterminado 1450. | `NetworkMtu` |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | (ninguna) |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática (se muestran cuando está seleccionado el modo Static). | (ninguna) |
| **Apply** | Envía la configuración de red a la radio. | (ninguna) |
| **Reboot Radio** | Abre un diálogo de confirmación antes de reiniciar la radio. AetherSDR se desconecta y, para conexiones LAN, se reconecta automáticamente después de que la radio arranque. SmartLink/WAN requiere reconexión manual. El botón está deshabilitado cuando la radio está desconectada. | (ninguna) |

## GPS (pestaña)

Muestra la presencia del GPS e información en vivo de ubicación/hora/satélites.

## TX (pestaña)

Configuración de transmisión que incluye temporizaciones, enclavamientos, límites de potencia y comportamiento de seguimiento de slice.

| Control | Comportamiento | Clave de ajuste |
|---------|----------------|-----------------|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | (ninguna) |
| **Timings (in ms)** | Temporizaciones de retención/retardo de TX. | (ninguna) |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y accessory. | (ninguna) |
| **Max Power:** | Establece el límite máximo de potencia de TX a nivel de radio (0-100%). | (ninguna) |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | (ninguna) |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | (ninguna) |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante operación en Split. | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | `ActiveFollowsTxSlice` |

## Phone/CW (pestaña)

Valores predeterminados de micrófono, keyer CW y RTTY.

| Control | Comportamiento | Clave de ajuste |
|---------|----------------|-----------------|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | (ninguna) |
| **Iambic:** | Habilita o deshabilita el keyer iambic en la radio. | (ninguna) |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente excluyente. | (ninguna) |
| **Swap:** | Intercambia dit/dah. | (ninguna) |
| **Sideband:** | Selecciona la banda lateral de tono CW (LSB/USB). | (ninguna) |
| **CWX:** | Habilita la activación de macros CWX. | (ninguna) |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. | `CwDecodeOverlay` |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. | (ninguna) |

## RX (pestaña)

Calibración de offset de frecuencia GPSDO y fuente de referencia de 10 MHz.

| Control | Comportamiento |
|---------|----------------|
| **Cal Frequency (MHz):** | Frecuencia utilizada para calibración manual. |
| **Start** | Inicia el barrido de calibración de frecuencia. |
| **Freq Offset (ppb):** | Offset de frecuencia manual en ppb. |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador (Auto/TCXO/GPSDO/External). El estado de bloqueo se muestra junto a la selección. |

## Audio (pestaña)

Salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y contenedor NVIDIA BNR.

| Control | Comportamiento | Clave de ajuste |
|---------|----------------|-----------------|
| **Line Out:** | Control deslizante de ganancia de salida de línea. | (ninguna) |
| **Mute (Line Out)** | Silencia la salida de línea. | (ninguna) |
| **Headphone:** | Control deslizante de ganancia de auriculares. | (ninguna) |
| **Mute (Headphone)** | Silencia los auriculares. | (ninguna) |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | (ninguna) |
| **Audio Compression (SmartLink):** | Selecciona el códec de audio para SmartLink/LAN (Auto/Uncompressed/Opus). | `AudioCompression` |
| **Prevent system sleep while connected** | Mantiene el sistema operativo despierto mientras la radio está conectada. | `InhibitSleepWhileConnected` |
| **PC Audio Devices: Input: / Output:** | Selecciona los dispositivos de audio de entrada/salida del host. | (ninguna) |
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para jitter de VPN/SmartLink (50-1000 ms). Valor predeterminado 200. | `AudioBufferMs` |
| **Recording: Radio Side / Client Side** | Selecciona grabación del lado de la radio o del lado del cliente. | `RecordingMode` |
| **Save to:** | Carpeta para grabaciones guardadas (solo lado del cliente). Por defecto Documents/AetherSDR/Recordings. | `QsoRecordingDir` |
| **...** | Examina para seleccionar la carpeta de grabaciones. | (ninguna) |
| **Auto-record on TX** | Graba automáticamente mientras transmite. | `QsoRecordingAutoRecord` |
| **Idle timeout:** | Segundos de silencio antes de detener la grabación (10-3600 seg). Valor predeterminado 120. | `QsoRecordingIdleTimeout` |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. | (ninguna) |

## Filters (pestaña)

Opciones de filtro de baja latencia y filtros nítidos por ancho de banda.

| Control | Comportamiento |
|---------|----------------|
| **Control deslizante de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0=mínima latencia a 3=máxima nitidez) por modo; el control deslizante está deshabilitado cuando Auto está habilitado. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. |
| **Use Low Latency Filters for Digital Modes** | Fuerza filtros de baja latencia en DIGU/DIGL. |

## XVTR (pestaña)

Configuración por transverter.

| Control | Comportamiento |
|---------|----------------|
| **RX Only:** | Fuerza solo RX en ese transverter. |
| **Remove (xvtr)** | Elimina la definición del transverter. |
| **Create New Transverter** | Agrega una nueva entrada de transverter. |

## USB Cables (pestaña)

Asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Comportamiento |
|---------|----------------|
| **Cables list / Status** | Cables USB detectados por tipo con estado Plugged/Unplugged. |
| **Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7)** | Parámetros serie y comportamiento por cable. |

## Peripherals (pestaña)

Conexión IP manual de dispositivos externos.

| Control | Comportamiento | Clave de ajuste |
|---------|----------------|-----------------|
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en la configuración. | `TGXL_ManualIp`, `TGXL_ManualPort` |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). | `PGXL_ManualIp`, `PGXL_ManualPort` |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión al Antenna Genius (puerto predeterminado 9007). | `AG_ManualIp`, `AG_ManualPort` |

## APD (pestaña)

Selección de puerto de muestra de Predistorsión Adaptativa Externa por antena de TX. La pestaña está oculta a menos que la radio informe que APD es configurable (FLEX-8x00 con SmartSDR 4.2.18+).

| Control | Comportamiento |
|---------|----------------|
| **ANT1: / ANT2: / XVTA: / XVTB:** | Selecciona el puerto de muestra (INTERNAL, RX_A, RX_B, XVTA, XVTB) que la radio utiliza para la retroalimentación de APD en esa antena de TX. |
| **Reset (APD Equalizer)** | Borra todos los datos de entrenamiento de APD por antena en la radio. |

## Themes (pestaña)

Configuración de apariencia de la interfaz de usuario, incluyendo anulaciones de color por slice.

| Control | Comportamiento |
|---------|----------------|
| **Use Aether defaults** | Utiliza la paleta de colores de slice incorporada (cian/magenta/verde/amarillo/naranja/verde azulado/coral/lavanda). |
| **Custom colors** | Habilita selectores de color por slice (A-H). |
| **Botones de color A/B/C/D/E/F/G/H** | Haga clic para abrir un selector de color para esa letra de slice. El fondo del botón refleja el color actualmente asignado. |
| **Reset All to Defaults** | Restablece cada color personalizado por slice a su valor predeterminado incorporado. |

## SmartLink (pestaña)

Gestión de certificados TLS fijados de SmartLink. Lista cada certificado fijado con controles **Forget** por fila y **Forget All**.

| Control | Comportamiento |
|---------|----------------|
| **Sección Pinned SmartLink Certificates** | Lista cada host que este cliente ha fijado en la primera conexión. Muestra Host, huella SHA-256 y fecha de fijación. |
| **Host / SHA-256 fingerprint / Pinned** (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespacio), Pinned (AAAA-MM-DD o '(pre-phase 2)'). |
| **Forget selected** | Elimina el certificado fijado del host seleccionado. La siguiente conexión a ese host lo vuelve a fijar silenciosamente. |
| **Forget all** | Borra todos los certificados fijados después de una solicitud de confirmación. La siguiente conexión a cada radio los vuelve a fijar silenciosamente. |

## Serial (pestaña)

Configuración del puerto serie FlexControl (compilado condicionalmente por `HAVE_SERIALPORT`).

| Control | Comportamiento |
|---------|----------------|
| **Port / Refresh / Path** | Selecciona/edita el dispositivo serie. |
| **Baud / Data / Parity / Stop** | Parámetros de línea serie. |
| **DTR / RTS: Function / Polarity** | Asigna función y polaridad de la señal. |
| **Paddle Swap (swap dit/dah)** | Intercambia dit/dah para el paddle. |
| **Auto-open serial port on startup** | Vuelve a abrir el puerto al iniciar la aplicación. |
| **FlexControl Tuning Knob: Detect / Close** | Detecta o cierra una perilla FlexControl. |
| **Auto-detect on startup / Invert tuning direction** | Preferencias de inicio y dirección de sintonía de FlexControl. |

## KiwiSDR (pestaña) — nuevo en v26.7.4

Configuración de receptores públicos KiwiSDR. Esta pestaña proporciona ajustes para conectarse a receptores públicos KiwiSDR y gestionar conexiones puente de automatización.
