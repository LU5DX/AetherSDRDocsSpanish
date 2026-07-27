# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, configuración de red, GPS, configuración de TX, Phone/CW, calibración de RX, audio, nombres de antenas, filtros, transverters, cables USB, periféricos, puertos serie, APD, temas, gestión de certificados anclados de SmartLink y receptores KiwiSDR.

## Abrir el diálogo de Configuración de Radio

- Seleccione `Settings > Radio Setup...` desde el menú principal.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Información de la radio (solo lectura)

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis. Haga clic en el botón de copia junto al valor para copiar el número de serie al portapapeles. |
| **Region** | Región regulatoria (EE. UU. por defecto). |
| **HW Version** | Cadena de versión de hardware. |
| **Options** | Opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo de radio. |

Cada campo de valor de solo lectura tiene un botón de copia. Haga clic en el icono del portapapeles para copiar el valor al portapapeles del sistema. Un breve mensaje emergente "Copied" confirma la acción. Los botones de copia se muestran atenuados visualmente cuando el valor está vacío o no está disponible.

### Campos configurables por el usuario

| Control | Descripción | Notas |
|---|---|---|
| **Nickname** | Apodo descriptivo de la radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. | Se establece por defecto al nombre del host del SO si está vacío. Se almacena en AppSettings con la clave `StationName`. Se envía a la radio como "client station <nombre>". |

### Información de licencia

La sección **License Info** muestra el estado de la suscripción, la fecha de vencimiento, el ID de la radio y la versión licenciada. Cada campo incluye un botón de copia al portapapeles junto al valor.

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta si hay actualizaciones de firmware. |
| **Select Installer...** | Abre un diálogo de archivo para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae la carga útil .ssdr y emite el progreso. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |
| **Firmware status** | Vacío hasta que comienza una carga de firmware, luego muestra el progreso y el texto del resultado. |

### Control remoto y reinicio

| Control | Descripción | Notas |
|---|---|---|
| **Remote On** | Habilita el encendido remoto / activación remota. | |
| **Reboot Radio** | Reinicia la radio conectada. | Solo se habilita cuando la radio está conectada. Al hacer clic, muestra un diálogo de confirmación. En conexiones WAN/SmartLink, debe reconectarse manualmente después de que la radio termine de iniciar. En conexiones LAN, AetherSDR se reconecta automáticamente. El diálogo se cierra después de iniciar el reinicio. |

### Pestaña SmartLink

La pestaña SmartLink gestiona los certificados TLS anclados de SmartLink. Enumera cada certificado anclado con el host, la huella SHA-256 y la fecha de anclaje. Una discrepancia en el anclaje del certificado ahora pausa firmemente el handshake con un diálogo modal.

#### Certificados SmartLink Anclados

| Control | Descripción |
|---|---|
| **Pinned SmartLink Certificates (sección)** | Encabezado de sección para la tabla de certificados anclados. Enumera todos los hosts que este cliente ha anclado en la primera conexión (confianza en el primer uso). |
| **Host / SHA-256 fingerprint / Pinned (columnas de tabla)** | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o "(pre-phase 2)"). |
| **Forget selected** | Elimina la huella del certificado anclado del host seleccionado para que la próxima conexión lo vuelva a anclar silenciosamente. |
| **Forget all** | Limpia todos los certificados anclados (con confirmación). La próxima conexión a cada radio los volverá a anclar silenciosamente. Muestra un diálogo de confirmación antes de borrar. |

## Pestaña Network

La pestaña Network muestra la información de red de la radio y proporciona opciones de configuración de red.

### Información de red (solo lectura)

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |

### Configuración de red

| Control | Valor predeterminado | Rango | Clave de Configuración | Descripción |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | | | | Rechaza pares que no sean RFC1918. El botón de alternancia muestra "Enabled" cuando está marcado. |
| **Network MTU:** | 1450 | 576-9000 bytes | `NetworkMtu` | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static** | | | | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | | | | Campos de configuración de IP estática (visibles solo en modo Static). |
| **Apply** | | | | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS y los datos de posición en vivo.

| Control | Descripción |
|---|---|
| GPS status | Muestra información de latitud/longitud/altitud/hora/satélites cuando hay un GPS instalado y activo. |

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, los enclavamientos, los límites de potencia, los modos de sintonía y el comportamiento de seguimiento de slice/TX.

### Configuración de banda TX

| Control | Descripción |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. |

### Temporizaciones

| Control | Descripción |
|---|---|
| **Timings** | Temporizaciones de retención/retardo de TX. |

| Campo | Descripción | Notas |
|---|---|---|
| **ACC TX:** | Retardo de ACC TX en milisegundos. | Comando: `interlock set acc_tx_delay=<ms>` |
| **TX Delay:** | Retardo de TX en milisegundos. | Comando: `interlock set tx_delay=<ms>` |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos. | Comando: `interlock set tx1_delay=<ms>` |
| **Timeout (sec):** | Tiempo de espera del enclavamiento en segundos. Se muestra e ingresa en segundos enteros; la radio almacena el valor internamente en milisegundos. | Comando: `interlock set timeout=<segundos * 1000>` |

### Enclavamientos

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de enclavamiento RCA. |
| **TX REQ: Accessory** | Habilita la entrada de enclavamiento del accesorio. |

### Potencia y sintonía

| Control | Valor predeterminado | Rango | Descripción |
|---|---|---|---|
| **Max Power:** | | 0-100% | Establece el límite máximo de potencia de TX a nivel de radio. |
| **Tune Mode:** | | | Selecciona cómo se comporta el botón de sintonía. |

### Visualización en waterfall

| Control | Descripción |
|---|---|
| **Show TX in Waterfall:** | Cuando está habilitado, la señal de TX se dibuja en la visualización del waterfall. |

### Comportamiento de seguimiento Slice/TX

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **TX Follows Active Slice** | Falso | `TxFollowsActiveSlice` | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Falso | `ActiveFollowsTxSlice` | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de nivel

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel del micrófono incluso en RX. |

### Manipulador CW

| Control | Valor predeterminado | Rango | Descripción |
|---|---|---|---|
| **Iambic:** | | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| **Swap:** | | | Intercambia dit/dah. |
| **Sideband:** | | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | | | Habilita el accionamiento de macros CWX. |

### Decodificación

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **Decode:** | Verdadero | `CwDecodeOverlay` | Habilita la superposición de decodificación CW en el panadapter. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona controles de calibración de frecuencia y selección de fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración son visibles independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, una línea de estado verde dice "GPSDO installed. Manual frequency offset calibration available."
- Si no hay un GPSDO instalado, una línea de estado amarilla dice "Manual frequency offset calibration available."

#### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras la calibración se ejecuta. Una etiqueta de estado a la derecha del botón muestra el texto de progreso.
   - "Starting…" aparece inmediatamente.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no comienza.
4. Espere a que la etiqueta de estado indique la finalización. El botón **Start** se vuelve a habilitar automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración, ingresada en MHz con seis decimales. | Se envía a la radio como `radio set cal_freq=<valor>`. |
| **Start** | Inicia el barrido de calibración. Se deshabilita y etiqueta como **Busy** mientras una calibración está en curso. | Restablece `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (ppb):** | Corrección manual de desviación de frecuencia en partes por billón. | |

### Referencia de 10 MHz

| Control | Valor predeterminado | Rango | Descripción | Notas |
|---|---|---|---|---|
| **10 MHz Reference Source:** | Auto | Auto / TCXO / GPSDO / External | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. Cuando se selecciona Auto y la radio ha resuelto una fuente específica, la etiqueta muestra "Auto -> <fuente>" para indicar el hardware activo. Si se selecciona una fuente 10 MHz External pero no se detecta ninguna señal externa, la etiqueta añade "(not detected)". La etiqueta muestra "Waiting for oscillator status" hasta que la radio informa su primer estado del oscilador. |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, la compresión, los dispositivos de PC, el refuerzo, el búfer, la grabación y NVIDIA BNR.

### Salidas de audio de la radio

| Control | Descripción |
|---|---|
| **Line Out:** | Control deslizante de ganancia de salida de línea. |
| **Mute (Line Out)** | Silencia la salida de línea. |
| **Headphone:** | Control deslizante de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker:** / **Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | `AudioCompression` | Selecciona el códec de audio para SmartLink/LAN: Auto, Uncompressed u Opus. |

### Suspensión del sistema

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **Prevent system sleep while connected** | Falso | `InhibitSleepWhileConnected` | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. |

### Dispositivos de audio del PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del host. |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del host. |

### Refuerzo y búfer de audio

| Control | Valor predeterminado | Rango | Clave de Configuración | Descripción |
|---|---|---|---|---|
| **Audio Boost:** | | | `AudioBoost` | Habilita ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | 200 | 50-1000 ms | `AudioBufferMs` | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. |

### Grabación

| Control | Valor predeterminado | Rango | Clave de Configuración | Descripción |
|---|---|---|---|---|
| **Recording:** | Radio Side | Radio Side / Client Side | `RecordingMode` | Selecciona la grabación del lado de la radio o del lado del cliente. |
| **Save to:** | | | `QsoRecordingDir` | Carpeta para grabaciones guardadas (solo lado del cliente). Valor predeterminado: Documentos/AetherSDR/Recordings. |
| **...** | | | | Examina para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | Falso | | `QsoRecordingAutoRecord` | Graba automáticamente mientras transmite. |
| **Idle timeout:** | 120 | 10-3600 seg | `QsoRecordingIdleTimeout` | Segundos de silencio antes de que se detenga la grabación. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **NVIDIA BNR: Autostart Container** | Habilita el inicio automático del contenedor. |
| **
