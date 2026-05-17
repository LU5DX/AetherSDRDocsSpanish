# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información del radio, configuración de red, GPS, configuración de TX, Telefonía/CW, calibración de RX, audio, nombres de antenas, filtros, transverters, cables USB, periféricos, puertos serie, APD y temas.

## Abrir el diálogo de Configuración de Radio

- Seleccione `Settings > Radio Setup...` en el menú principal.

## Pestaña Radio

La pestaña Radio muestra la identificación del radio, información de licencia y controles de actualización de firmware.

### Información del radio (solo lectura)

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis. |
| **Region** | Región regulatoria (EE. UU. por defecto). |
| **HW Version** | Cadena de versión del hardware. |
| **Options** | Opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo del radio. |

### Campos configurables por el usuario

| Control | Descripción | Notas |
|---|---|---|
| **Nickname** | Apodo amigable del radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. | Por defecto es el nombre de host del SO si está vacío. Se almacena en AppSettings con la clave `StationName`. Se envía al radio como "client station <nombre>". |

### Información de licencia

La sección **License Info** muestra el estado de suscripción, fecha de vencimiento, ID del radio y versión licenciada.

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Browse .ssdr...** | Selecciona un archivo de imagen de firmware. |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. |
| **Firmware status** | Vacío hasta que comience una carga de firmware; luego muestra el progreso y el texto del resultado. |

### Control remoto

| Control | Descripción |
|---|---|
| **Remote On** | Habilita el despertado remoto/encendido remoto. |

## Pestaña Network

La pestaña Network muestra información de red del radio y ofrece opciones de configuración de red.

### Información de red (solo lectura)

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Por defecto | Rango | Clave de Ajuste | Descripción |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | | | | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | 1450 | 576-9000 bytes | `NetworkMtu` | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor por defecto 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static** | | | | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | | | | Campos de configuración de IP estática (visibles solo en modo Static). |
| **Apply** | | | | Envía la configuración de red al radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS y datos de posición en vivo.

| Control | Descripción |
|---|---|
| GPS status | Muestra información de lat/lon/alt/hora/satélites cuando hay un GPS instalado y activo. |

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, bloqueos, límites de potencia, modos de sintonía y el comportamiento de seguimiento de slice/TX.

### Ajustes de banda TX

| Control | Descripción |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. |

### Tiempos

| Control | Descripción |
|---|---|
| **Timings** | Tiempos de retención/retardo de TX. |

| Campo | Descripción | Notas |
|---|---|---|
| **ACC TX:** | Retardo de ACC TX en milisegundos. | Comando: `interlock set acc_tx_delay=<ms>` |
| **TX Delay:** | Retardo de TX en milisegundos. | Comando: `interlock set tx_delay=<ms>` |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos. | Comando: `interlock set tx1_delay=<ms>` |
| **Timeout (sec):** | Tiempo de espera del bloqueo en segundos. Se muestra e ingresa en segundos enteros; el radio almacena el valor internamente en milisegundos. | Comando: `interlock set timeout=<segundos * 1000>` |

### Bloqueos

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de bloqueo RCA. |
| **TX REQ: Accessory** | Habilita la entrada de bloqueo del accesorio. |

### Potencia y sintonía

| Control | Por defecto | Rango | Descripción |
|---|---|---|---|
| **Max Power:** | | 0-100% | Establece el límite de potencia TX a nivel de radio. |
| **Tune Mode:** | | | Selecciona cómo se comporta el botón de sintonía. |

### Visualización en el Waterfall

| Control | Descripción |
|---|---|
| **Show TX in Waterfall:** | Cuando está habilitado, la señal TX se dibuja en la visualización del waterfall. |

### Comportamiento de seguimiento Slice/TX

| Control | Por defecto | Clave de Ajuste | Descripción |
|---|---|---|---|
| **TX Follows Active Slice** | False | `TxFollowsActiveSlice` | TX sigue la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante una operación Split. |
| **Active Slice Follows TX** | False | `ActiveFollowsTxSlice` | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de nivel

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel del micrófono incluso en RX. |

### Manipulador CW

| Control | Por defecto | Rango | Descripción |
|---|---|---|---|
| **Iambic:** | | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iambic en el radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iambic Curtis A o B tanto para el radio como para el manipulador de software local. Par mutuamente excluyente. |
| **Swap:** | | | Intercambia dit/dah. |
| **Sideband:** | | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | | | Habilita la activación de macros CWX. |

### Decodificación

| Control | Por defecto | Clave de Ajuste | Descripción |
|---|---|---|---|
| **Decode:** | True | `CwDecodeOverlay` | Habilita la superposición de decodificación CW en el panadapter. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona controles de calibración de frecuencia y selección de fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración son visibles independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, una línea de estado verde muestra "GPSDO installed. Manual frequency offset calibration available."
- Si no hay ningún GPSDO instalado, una línea de estado amarilla muestra "Manual frequency offset calibration available."

#### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración. Una etiqueta de estado a la derecha del botón muestra el texto de progreso.
   - "Starting…" aparece inmediatamente.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no comienza.
4. Espere a que la etiqueta de estado indique la finalización. El botón **Start** se vuelve a habilitar automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración, ingresada en MHz con seis decimales. | Se envía al radio como `radio set cal_freq=<valor>`. |
| **Start** | Inicia el barrido de calibración. Se deshabilita y se etiqueta como **Busy** mientras una calibración está en progreso. | Restablece `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (ppb):** | Corrección manual del desplazamiento de frecuencia en partes por mil millones. | |

### Referencia de 10 MHz

| Control | Por defecto | Rango | Descripción | Notas |
|---|---|---|---|---|
| **10 MHz Reference Source:** | Auto | Auto / TCXO / GPSDO / External | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. Cuando se selecciona Auto y el radio ha resuelto una fuente específica, la etiqueta muestra "Auto -> <fuente>" para indicar el hardware activo. Si se selecciona una fuente External de 10 MHz pero no se detecta señal externa, la etiqueta agrega "(not detected)". La etiqueta muestra "Waiting for oscillator status" hasta que el radio informe su primer estado del oscilador. |

## Pestaña Audio

La pestaña Audio configura las salidas de audio del radio, la compresión, los dispositivos de PC, el refuerzo, el búfer, la grabación y NVIDIA BNR.

### Salidas de audio del radio

| Control | Descripción |
|---|---|
| **Line Out:** | Control deslizante de ganancia de salida de línea. |
| **Mute (Line Out)** | Silencia la salida de línea. |
| **Headphone:** | Control deslizante de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker:** / **Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Por defecto | Clave de Ajuste | Descripción |
|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | `AudioCompression` | Selecciona el códec de audio para SmartLink/LAN: Auto, Uncompressed u Opus. |

### Suspensión del sistema

| Control | Por defecto | Clave de Ajuste | Descripción |
|---|---|---|---|
| **Prevent system sleep while connected** | False | `InhibitSleepWhileConnected` | Mantiene el SO despierto mientras el radio está conectado para evitar caídas de flujo de audio/TCP/UDP durante la inactividad. |

### Dispositivos de audio del PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del host. |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del host. |

### Refuerzo y búfer de audio

| Control | Por defecto | Rango | Clave de Ajuste | Descripción |
|---|---|---|---|---|
| **Audio Boost:** | | | `AudioBoost` | Habilita ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | 200 | 50-1000 ms | `AudioBufferMs` | Aumenta el búfer de audio en milisegundos para fluctuaciones en VPN/SmartLink. |

### Grabación

| Control | Por defecto | Rango | Clave de Ajuste | Descripción |
|---|---|---|---|---|
| **Recording:** | Radio Side | Radio Side / Client Side | `RecordingMode` | Selecciona grabación del lado del radio o del lado del cliente. |
| **Save to:** | | | `QsoRecordingDir` | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto es Documents/AetherSDR/Recordings. |
| **...** | | | | Busca la carpeta de grabación. |
| **Auto-record on TX** | False | | `QsoRecordingAutoRecord` | Graba automáticamente mientras transmite. |
| **Idle timeout:** | 120 | 10-3600 sec | `QsoRecordingIdleTimeout` | Segundos de silencio antes de que se detenga la grabación. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **NVIDIA BNR: Autostart Container** | Habilita el inicio automático del contenedor. |
| **NVIDIA BNR: Start / Stop** | Inicia o detiene manualmente el contenedor de eliminación de ruido NVIDIA Broadcast. |
| **NVIDIA BNR: Check Status** | Verifica el estado del contenedor. |
| **NVIDIA BNR status dot** | Punto de color que indica el estado del contenedor: Running/Stopped/Unknown. |

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres amigables a cada puerto de antena en el radio para una identificación más fácil. Esta pestaña se construye de forma diferida cuando se hace clic en ella por primera vez.

### Asignación de nombres de antena

| Control | Descripción | Notas |
|---|---|---|
| **Antenna Name fields (ANT1, ANT2, ANT3, ANT4, XVTA, XVTB)** | Campos de texto para cada puerto de antena. Ingrese un nombre personalizado (p. ej., "20m Beam", "80m Dipole"). | Los nombres se almacenan en AppSettings como `AntennaName_ANT1`, etc., y se muestran en el selector de antena de la barra de radio y en la cinta del Main Waterfall. |

## Pestaña Filters

La pestaña Filters configura la nitidez del filtro por modo.

### Nitidez del filtro

| Control | Rango | Descripción | Notas |
|---|---|---|---|
| **Voice / CW / Digital filter sharpness sliders** | 0-3 | Establece la nitidez del filtro por modo (0=menor latencia a 3=más nítido). El control deslizante se deshabilita cuando Auto está habilitado. | Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **Use Low Latency Filters for Digital Modes** | | Fuerza filtros de baja latencia en DIGU/DIGL. | |

## Pestaña XVTR

La pestaña XVTR gestiona la configuración por transverter.

| Control | Descripción |
|---|---|
| **RX Only:** | Fuerza solo RX en ese transverter. |
| **Remove (xvtr)** | Elimina la definición del transverter. |
| **Create New Transverter** | Agrega una nueva entrada de transverter. |

La pestaña contiene pestañas anidadas, una por cada transverter configurado, más una pestaña "+" para crear nuevos transverters.

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a CAT,
