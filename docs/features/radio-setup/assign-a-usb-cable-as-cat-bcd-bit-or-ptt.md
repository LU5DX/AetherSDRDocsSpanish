# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, configuración de red, GPS, configuración de TX, Phone/CW, calibración de RX, audio, nombres de antenas, filtros, transvertidores, cables USB, periféricos, puertos serie, APD, temas y gestión de certificados SmartLink anclados.

## Abrir el diálogo de Configuración de la Radio

- Seleccione `Settings > Radio Setup...` desde el menú principal.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Información de la radio (solo lectura)

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis. Haga clic en el botón de copiar junto al valor para copiar el número de serie al portapapeles. |
| **Region** | Región regulatoria (EE. UU. por defecto). |
| **HW Version** | Cadena de versión del hardware. |
| **Options** | Opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo de la radio. |

Cada campo de valor de solo lectura tiene un botón de copiar. Haga clic en el icono del portapapeles para copiar el valor al portapapeles del sistema. Un breve mensaje emergente "Copied" confirma la acción. Los botones de copiar se atenúan visualmente cuando el valor está vacío o no disponible.

### Campos configurables por el usuario

| Control | Descripción | Notas |
|---|---|---|
| **Nickname** | Apodo amigable de la radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. | Por defecto, es el nombre del host del SO si está vacío. Se almacena en AppSettings con la clave `StationName`. Se envía a la radio como "client station <nombre>". |

### Información de licencia

La sección **License Info** muestra el estado de la suscripción, la fecha de expiración, el ID de la radio y la versión licenciada.

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta si hay actualizaciones de firmware. |
| **Browse .ssdr...** | Selecciona un archivo de imagen de firmware. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |
| **Firmware status** | Vacío hasta que comienza una carga de firmware, luego muestra el progreso y el texto del resultado. |

### Control remoto

| Control | Descripción |
|---|---|
| **Remote On** | Habilita el encendido remoto / remoto-activado. |

## Pestaña SmartLink

La pestaña SmartLink gestiona los certificados TLS de SmartLink anclados. Enumera cada certificado anclado con el host, la huella SHA-256 y la fecha de anclaje. Una discrepancia en el anclaje del certificado ahora pausa firmemente el handshake con un diálogo modal.

### Certificados SmartLink Anclados

| Control | Descripción |
|---|---|
| **Pinned SmartLink Certificates (sección)** | Encabezado de sección para la tabla de certificados anclados. Enumera cada host que este cliente ha anclado en la primera conexión (trust-on-first-use). |
| **Host / SHA-256 fingerprint / Pinned (columnas de la tabla)** | Tabla de solo lectura de 3 columnas: Host (nombre del host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o "(pre-phase 2)"). |
| **Forget selected** | Elimina la huella del certificado anclado del host seleccionado para que la próxima conexión lo vuelva a anclar silenciosamente. |
| **Forget all** | Limpia todos los certificados anclados (con confirmación). La próxima conexión a cada radio los volverá a anclar silenciosamente. Muestra un diálogo de confirmación antes de borrar. |

## Pestaña Network

La pestaña Network muestra la información de red de la radio y proporciona opciones de configuración de red.

### Información de red (solo lectura)

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | | | | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | 1450 | 576-9000 bytes | `NetworkMtu` | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static** | | | | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | | | | Campos de configuración de IP estática (visibles solo en modo Static). |
| **Apply** | | | | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS y los datos de posición en vivo.

| Control | Descripción |
|---|---|
| GPS status | Muestra información de latitud/longitud/altitud/hora/satélites cuando hay un GPS instalado y activo. |

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, los enclavamientos, los límites de potencia, los modos de sintonía y el comportamiento de seguimiento slice/TX.

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
| **ACC TX:** | Retardo de TX ACC en milisegundos. | Comando: `interlock set acc_tx_delay=<ms>` |
| **TX Delay:** | Retardo de TX en milisegundos. | Comando: `interlock set tx_delay=<ms>` |
| **RCA TX1:** | Retardo de TX1 RCA en milisegundos. | Comando: `interlock set tx1_delay=<ms>` |
| **Timeout (sec):** | Tiempo de espera del enclavamiento en segundos. Se muestra e ingresa en segundos enteros; la radio almacena el valor internamente en milisegundos. | Comando: `interlock set timeout=<segundos * 1000>` |

### Enclavamientos

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de enclavamiento RCA. |
| **TX REQ: Accessory** | Habilita la entrada de enclavamiento del accesorio. |

### Potencia y sintonía

| Control | Valor predeterminado | Rango | Descripción |
|---|---|---|---|
| **Max Power:** | | 0-100% | Establece el límite de potencia de TX a nivel de radio. |
| **Tune Mode:** | | | Selecciona cómo se comporta el botón de sintonía. |

### Visualización en waterfall

| Control | Descripción |
|---|---|
| **Show TX in Waterfall:** | Cuando está habilitado, la señal de TX se dibuja en la visualización del waterfall. |

### Comportamiento de seguimiento Slice/TX

| Control | Valor predeterminado | Clave de configuración | Descripción |
|---|---|---|---|
| **TX Follows Active Slice** | False | `TxFollowsActiveSlice` | TX sigue la slice activa. Es mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | False | `ActiveFollowsTxSlice` | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. |

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulado CW y los valores predeterminados de RTTY.

### Indicador de nivel

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el indicador de nivel del micrófono incluso en RX. |

### Manipulado CW

| Control | Valor predeterminado | Rango | Descripción |
|---|---|---|---|
| **Iambic:** | | Enabled / Disabled | Habilita o deshabilita el manipulado iambic en la radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local de software. Par mutuamente excluyente. |
| **Swap:** | | | Intercambia dit/dah. |
| **Sideband:** | | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | | | Habilita el manipulado por macros CWX. |

### Decodificación

| Control | Valor predeterminado | Clave de configuración | Descripción |
|---|---|---|---|
| **Decode:** | True | `CwDecodeOverlay` | Habilita la superposición de decodificación CW en el panadapter. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona controles de calibración de frecuencia y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración son visibles independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, una línea de estado verde indica "GPSDO installed. Manual frequency offset calibration available."
- Si no hay un GPSDO instalado, una línea de estado amarilla indica "Manual frequency offset calibration available."

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
| **Start** | Comienza el barrido de calibración. Se deshabilita y etiqueta como **Busy** mientras una calibración está en curso. | Restablece `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (ppb):** | Corrección manual del desplazamiento de frecuencia en partes por billón. | |

### Referencia de 10 MHz

| Control | Valor predeterminado | Rango | Descripción | Notas |
|---|---|---|---|---|
| **10 MHz Reference Source:** | Auto | Auto / TCXO / GPSDO / External | Selecciona la fuente del oscilador de referencia. Las opciones mostradas dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. Cuando se selecciona Auto y la radio ha resuelto una fuente específica, la etiqueta muestra "Auto -> <fuente>" para indicar el hardware activo. Si se selecciona una fuente External de 10 MHz pero no se detecta ninguna señal externa, la etiqueta añade "(not detected)". La etiqueta muestra "Waiting for oscillator status" hasta que la radio informa su primer estado del oscilador. |

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

| Control | Valor predeterminado | Clave de configuración | Descripción |
|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | `AudioCompression` | Selecciona el códec de audio para SmartLink/LAN: Auto, Uncompressed, u Opus. |

### Suspensión del sistema

| Control | Valor predeterminado | Clave de configuración | Descripción |
|---|---|---|---|
| **Prevent system sleep while connected** | False | `InhibitSleepWhileConnected` | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. |

### Dispositivos de audio del PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del host. |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del host. |

### Refuerzo de audio y búfer

| Control | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---|---|---|---|---|
| **Audio Boost:** | | | `AudioBoost` | Habilita ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | 200 | 50-1000 ms | `AudioBufferMs` | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. |

### Grabación

| Control | Valor predeterminado | Rango | Clave de configuración | Descripción |
|---|---|---|---|---|
| **Recording:** | Radio Side | Radio Side / Client Side | `RecordingMode` | Selecciona la grabación del lado de la radio o del lado del cliente. |
| **Save to:** | | | `QsoRecordingDir` | Carpeta para grabaciones guardadas (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. |
| **...** | | | | Examina la carpeta de grabación. |
| **Auto-record on TX** | False | | `QsoRecordingAutoRecord` | Graba automáticamente mientras se transmite. |
| **Idle timeout:** | 120 | 10-3600 seg | `QsoRecordingIdleTimeout` | Segundos de silencio antes de que se detenga la grabación. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **NVIDIA BNR: Autostart Container** | Habilita el inicio automático del contenedor. |
| **NVIDIA BNR: Start / Stop** | Inicia o detiene manualmente el contenedor de eliminación de ruido NVIDIA Broadcast. |
| **NVIDIA BNR: Check Status** | Verifica el estado del contenedor. |
| **NVIDIA BNR status dot** | Punto de color que indica el estado del contenedor: Running/Stopped/Unknown. |

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres amigables a cada puerto de antena en la radio para una identificación más fácil. Esta pestaña se construye de forma diferida cuando se hace clic en ella por primera vez.

### Asignación de nombres de antenas

| Control | Descripción | Notas |
|---|---|---|
| **Campos de nombre de antena (ANT1, ANT2, ANT3, ANT4, XVTA, XVTB)** | Campos de texto para cada puerto de antena. Ingrese un nombre personalizado (p. ej., "20m Beam", "80m Dipole"). | Los nombres se almacenan en App
