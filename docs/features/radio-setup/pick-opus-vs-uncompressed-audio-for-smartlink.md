# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, APD, temas, serie (FlexControl), nombres de antenas y gestión de certificados SmartLink anclados.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio para acceder a la mayoría de las pestañas.
- Abra `Settings > Radio Setup...`.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

| Control                                             | Valor predeterminado                | Comportamiento                                                                                                                                                                        |
|-----------------------------------------------------|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Radio SN                                            | Número de serie del chasis (solo lectura). | Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. Nuevo en v26.5.3 (#2976).                                                                               |
| Region                                              | USA                                 | Región regulatoria de la radio.                                                                                                                                                       |
| HW Version                                          | Cadena de versión de hardware.      | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                                                                     |
| Remote On                                           | —                                   | Habilita el encendido/activación remota.                                                                                                                                              |
| Options                                             | Muestra las opciones de radio licenciadas. | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                                                                     |
| FlexControl                                         | —                                   | Estado detectado del hardware FlexControl.                                                                                                                                            |
| multiFLEX                                           | —                                   | Estado habilitado de multiFLEX.                                                                                                                                                       |
| Model                                               | Modelo de radio.                    | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                                                                     |
| Nickname                                            | —                                   | Apodo amigable para la radio.                                                                                                                                                         |
| Callsign                                            | —                                   | Indicativo de la estación.                                                                                                                                                            |
| Station Name                                        | —                                   | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto es el nombre de host del SO si está vacío. Almacenado como `StationName`.                           |
| License Info                                        | —                                   | Muestra los detalles de la licencia de la radio (Suscripción / Vencimiento / ID de radio / Versión licenciada). Haga clic en el botón de copia para copiar al portapapeles.           |
| Check for Update                                    | —                                   | Consulta actualizaciones de firmware.                                                                                                                                                 |
| Select Installer...                                 | —                                   | Elige un archivo de imagen de firmware (`.msi`, `.exe` o `.ssdr`).                                                                                                                    |
| Upload Firmware                                     | —                                   | Inicia la carga del firmware con barra de progreso y estado.                                                                                                                          |
| Reboot Radio                                        | —                                   | Solicita confirmación, luego reinicia la radio conectada. AetherSDR se desconecta durante el reinicio. Se reconecta automáticamente en LAN; SmartLink/WAN requiere reconexión manual. El botón se deshabilita cuando la radio no está conectada. Nuevo en v26.6.3. |
| SmartLink (tab)                                     | —                                   | Gestión de certificados TLS de SmartLink anclados. Enumera cada certificado anclado (host, huella SHA-256, fecha de anclaje) con botones Forget y Forget All por fila. Se construye de forma diferida al hacer clic por primera vez. |
| Pinned SmartLink Certificates (section)             | —                                   | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Enumera todos los hosts que este cliente ha anclado en la primera conexión (confianza en el primer uso). |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | —                                   | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)').                                               |
| Forget selected                                     | —                                   | Elimina la huella del certificado anclado del host seleccionado para que la siguiente conexión lo ancle silenciosamente de nuevo.                                                     |
| Forget all                                          | —                                   | Borra todos los certificados anclados (con confirmación). La próxima conexión a cada radio los volverá a anclar silenciosamente.                                                       |

### Botones de copia de valor

Cada indicador de solo lectura (Radio SN, HW Version, License Info, etc.) ahora muestra un pequeño botón de copia superpuesto al pasar el ratón o enfocar. Al hacer clic en el botón, se copia el valor mostrado al portapapeles del sistema. Aparece un breve mensaje emergente "copiado" cerca del botón tras una copia exitosa.

### Estado de carga de firmware

El área de carga de firmware muestra una barra de progreso y un texto de estado durante una carga activa. Cuando no hay una carga en curso, el área de estado está vacía.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación antes de que proceda el reinicio. AetherSDR se desconecta durante el reinicio:

- **Conexión LAN:** AetherSDR se reconecta automáticamente una vez que la radio termina de iniciar.
- **Conexión SmartLink/WAN:** Debe reconectarse manualmente después de que la radio inicie.

El botón se deshabilita cuando la radio no está conectada. Se actualiza automáticamente cuando cambia el estado de la conexión, por lo que no es necesario reabrir el diálogo.

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

| Control | Valor predeterminado | Comportamiento |
|---------|----------------------|----------------|
| IP Address / Mask / MAC Address | — | Direcciones de red de solo lectura. |
| Enforce Private IP Connections | — | Rechaza pares que no sean RFC1918. |
| Network MTU | 1450 | Establece el tamaño máximo de paquete VITA-49 UDP saliente en bytes (576–9000). Almacenado como `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| DHCP / Static | — | Cambia entre modos DHCP e IP estática. |
| IP Address / Mask / Gateway | — | Campos de configuración de IP estática. |
| Apply | — | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña TX configura temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y configuración de banda de TX.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| TX Band Settings | — | — | Abre el diálogo dedicado de potencia/sintonía por banda. |
| ACC TX | — | — | Retardo de mantenimiento de TX en milisegundos. |
| TX Delay | — | — | Retardo de TX en milisegundos. |
| RCA TX1 | — | — | Retardo RCA TX1 en milisegundos. |
| Timeout (sec) | — | — | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |
| RCA TX2 | — | — | Retardo RCA TX2 en milisegundos. |
| Interlocks - TX REQ: RCA / Accessory | — | — | Habilita las entradas de enclavamiento RCA y de accesorio. |
| Max Power | — | 0–100 % | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode | — | — | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall | — | — | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Falso | — | TX sigue el slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se desactiva automáticamente durante la operación Split. |
| Active Slice Follows TX | Falso | — | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

### Campos de temporización

Los campos de temporización en la pestaña TX aceptan valores en milisegundos, excepto Timeout (sec) que muestra y acepta valores en segundos para facilitar la lectura. La radio almacena el valor de tiempo de espera internamente en milisegundos.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| Enable/Disable the Level Meter During Receive | — | — | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic | — | Enabled / Disabled | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode: A / B | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local por software. |
| Swap | — | — | Intercambia dit/dah. |
| Sideband | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX | — | — | Habilita el macro-keying CWX. |
| Decode | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. Almacenado como `CwDecodeOverlay`. |
| RTTY Mark Default | — | — | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona calibración de compensación de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| Cal Frequency (MHz) | — | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| Start | — | — | Establece la frecuencia de calibración, reinicia `freq_error_ppb` a 0, luego inicia el barrido de calibración del PLL de la radio. El botón se deshabilita y etiqueta como **Busy** mientras la calibración está en ejecución. |
| Freq Offset (ppb) | — | — | Compensación de frecuencia manual en partes por billón. |
| 10 MHz Reference Source | Auto | Auto / TCXO / GPSDO / External 10 MHz | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. |

### 10 MHz Reference Source

El combo se completa dinámicamente cada vez que se abre el diálogo o la radio informa el estado del oscilador:

- **Auto** siempre está presente.
- **TCXO** aparece cuando la radio informa cualquier estado del oscilador, cuando `tcxoPresent` es verdadero, o cuando el valor actual o configurado es `tcxo`.
- **GPSDO** aparece cuando `gpsdoPresent` es verdadero o el valor actual o configurado es `gpsdo`.
- **External 10 MHz** aparece cuando la radio informa cualquier estado del oscilador, cuando `extPresent` es verdadero, o cuando el valor actual o configurado es `external`.

El combo preselecciona el valor que coincide con la configuración actual de la radio (`oscSetting`). Si ese valor no está en la lista, se utiliza el elemento previamente seleccionado; si ninguno está presente, se selecciona **Auto**.

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| Line Out | — | — | Control deslizante de ganancia de salida de línea. |
| Mute (Line Out) | — | — | Silencia la salida de línea. |
| Headphone | — | — | Control deslizante de ganancia de auriculares. |
| Mute (Headphone) | — | — | Silencia los auriculares. |
| Front Speaker / Mute | — | — | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink) | Auto | Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. Almacenado como `AudioCompression`. |
| Prevent system sleep while connected | Falso | — | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en los flujos de audio/TCP/UDP durante la inactividad. Almacenado como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input / Output | — | — | Elige los dispositivos de audio de entrada/salida del host. |
| Audio Boost | — | — | Habilita ganancia adicional en la ruta de audio del cliente. Almacenado como `AudioBoost`. |
| Audio Buffer | 200 ms | 50–1000 ms | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Almacenado como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Radio Side | Radio Side / Client Side | Elige la grabación del lado de la radio o del lado del cliente. Almacenado como `RecordingMode`. |
| Save to | — | — | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. Almacenado como `QsoRecordingDir`. |
| ... (browse) | — | — | Navega para seleccionar la carpeta de grabación. |
| Auto-record on TX | Falso | — | Graba automáticamente mientras transmite. Almacenado como `QsoRecordingAutoRecord`. |
| Idle timeout | 120 seg | 10–3600 seg | Segundos de silencio antes de que la grabación se detenga. Almacenado como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | — | — | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Antennas

La pestaña Antennas (nueva en v26.5.2.1) permite nombrar y configurar antenas. Esta pestaña se construye de forma diferida al hacer clic por primera vez.

## Pestaña Filters

La pestaña Filters proporciona opciones de filtro de baja latencia / nítido por ancho de banda.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| Control deslizantes de nitidez de filtro Voice / CW / Digital | — | 0–3 | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. |
| Auto (Voice / CW / Digital) | — | — | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. |
| Use Low Latency Filters for Digital Modes | — | — | Fuerza filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transvertedor con pestañas anidadas, una por transvertedor, más una pestaña '+' para crear nuevos transvertedores.

| Control | Valor predeterminado | Comportamiento |
|---------|----------------------|----------------|
| RX Only | — | Fuerza solo RX en ese transvertedor. |
| Remove | — | Elimina la definición del transvertedor. |
| Create New Transverter | — | Agrega una nueva entrada de transvertedor. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control
