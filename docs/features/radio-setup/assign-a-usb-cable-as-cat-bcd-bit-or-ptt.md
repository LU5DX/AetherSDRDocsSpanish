# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, configuración de red, GPS, configuración de TX, Phone/CW, calibración de RX, audio, filtros, transverters, cables USB, periféricos, puertos serie, APD y temas.

## Abrir el diálogo de Configuración de la Radio

- Seleccione `Settings > Radio Setup...` en el menú principal.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Información de la radio (solo lectura)

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis. |
| **Región** | Región regulatoria (EE. UU. por defecto). |
| **HW Version** | Cadena de versión del hardware. |
| **Options** | Opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo de la radio. |

### Campos configurables por el usuario

| Control | Descripción | Notas |
|---|---|---|
| **Nickname** | Apodo amigable de la radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente AetherSDR para otras estaciones multiFLEX. | Por defecto es el nombre del host del sistema operativo si está vacío. Se almacena en AppSettings con la clave `StationName`. Se envía a la radio como "client station <nombre>". |

### Información de licencia

La sección **License Info** muestra el estado de la suscripción, fecha de vencimiento, ID de la radio y versión licenciada.

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Select Installer...** | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El stagedor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |
| **Firmware status** | Vacío hasta que comienza una carga de firmware, luego muestra el progreso y el texto del resultado. |

### Control remoto

| Control | Descripción |
|---|---|
| **Remote On** | Habilita el encendido remoto / remote-on. |

## Pestaña Red

La pestaña Red muestra la información de red de la radio y proporciona opciones de configuración de red.

### Información de red (solo lectura)

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Valor predeterminado | Rango | Clave de Configuración | Descripción |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | | | | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | 1450 | 576-9000 bytes | `NetworkMtu` | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static** | | | | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | | | | Campos de configuración de IP estática (visibles solo en modo Static). |
| **Apply** | | | | Aplica la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS y los datos de posición en vivo.

| Control | Descripción |
|---|---|
| GPS status | Muestra información de latitud/longitud/altitud/hora/satélites cuando hay un GPS instalado y activo. |

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, enclavamientos, límites de potencia, modos de sintonización y el comportamiento de seguimiento slice/TX.

### Configuración de banda TX

| Control | Descripción |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonización por banda. |

### Temporizaciones

| Control | Descripción |
|---|---|
| **Timings (in ms)** | Temporizaciones de retención/retardo de TX. |

### Enclavamientos

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de enclavamiento RCA. |
| **TX REQ: Accessory** | Habilita la entrada de enclavamiento del accesorio. |

### Potencia y sintonización

| Control | Valor predeterminado | Rango | Descripción |
|---|---|---|---|
| **Max Power:** | | 0-100% | Establece el límite de potencia de TX a nivel de radio. |
| **Tune Mode:** | | | Selecciona cómo se comporta el botón de sintonización. |

### Visualización en waterfall

| Control | Descripción |
|---|---|
| **Show TX in Waterfall:** | Cuando está habilitado, la señal de TX se dibuja en la visualización de waterfall. |

### Comportamiento de seguimiento Slice/TX

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **TX Follows Active Slice** | False | `TxFollowsActiveSlice` | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | False | `ActiveFollowsTxSlice` | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |

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
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local de software. Par mutuamente excluyente. |
| **Swap:** | | | Intercambia dit/dah. |
| **Sideband:** | | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | | | Habilita la activación de macros CWX. |

### Decodificación

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **Decode:** | True | `CwDecodeOverlay` | Habilita la superposición de decodificación CW en el panadapter. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default:** | Frecuencia predeterminada de la marca RTTY. |

## Pestaña RX

La pestaña RX proporciona controles de calibración de frecuencia y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración son visibles independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, una línea de estado verde dice "GPSDO installed. Manual frequency offset calibration available."
- Si no hay un GPSDO instalado, una línea de estado amarilla dice "Manual frequency offset calibration available."

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
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración, ingresada en MHz con seis decimales. | Se envía a la radio como `radio set cal_freq=<valor>`. |
| **Start** | Inicia el barrido de calibración. Se deshabilita y etiqueta como **Busy** mientras la calibración está en progreso. | Reinicia `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (ppb):** | Corrección manual de desplazamiento de frecuencia en partes por billón. | |

### Referencia de 10 MHz

| Control | Valor predeterminado | Rango | Descripción | Notas |
|---|---|---|---|---|
| **10 MHz Reference Source:** | Auto | Auto / TCXO / GPSDO / External | Selecciona la fuente del oscilador de referencia. Las opciones mostradas dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. Cuando se selecciona Auto y la radio ha resuelto a una fuente específica, la etiqueta muestra "Auto -> <fuente>" para indicar el hardware activo. Si se selecciona una fuente externa de 10 MHz pero no se detecta ninguna señal externa, la etiqueta añade "(not detected)". La etiqueta muestra "Waiting for oscillator status" hasta que la radio informa su primer estado del oscilador. |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, la compresión, los dispositivos de PC, el refuerzo, el búfer, la grabación y NVIDIA BNR.

### Salidas de audio de la radio

| Control | Descripción |
|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea. |
| **Mute (Line Out)** | Silencia la salida de línea. |
| **Headphone:** | Deslizador de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker:** / **Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | `AudioCompression` | Selecciona el códec de audio para SmartLink/LAN: Auto, Uncompressed u Opus. |

### Suspensión del sistema

| Control | Valor predeterminado | Clave de Configuración | Descripción |
|---|---|---|---|
| **Prevent system sleep while connected** | False | `InhibitSleepWhileConnected` | Mantiene el sistema operativo despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. |

### Dispositivos de audio del PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del host. |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del host. |

### Refuerzo y búfer de audio

| Control | Valor predeterminado | Rango | Clave de Configuración | Descripción |
|---|---|---|---|---|
| **Audio Boost:** | | | `AudioBoost` | Habilita ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | 200 | 50-1000 ms | `AudioBufferMs` | Aumenta el búfer de audio en milisegundos para fluctuaciones de VPN/SmartLink. |

### Grabación

| Control | Valor predeterminado | Rango | Clave de Configuración | Descripción |
|---|---|---|---|---|
| **Recording:** | Radio Side | Radio Side / Client Side | `RecordingMode` | Selecciona la grabación del lado de la radio o del lado del cliente. |
| **Save to:** | | | `QsoRecordingDir` | Carpeta para grabaciones guardadas (solo del lado del cliente). Por defecto en Documentos/AetherSDR/Recordings. |
| **...** | | | | Examina para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | False | | `QsoRecordingAutoRecord` | Graba automáticamente mientras se transmite. |
| **Idle timeout:** | 120 | 10-3600 seg | `QsoRecordingIdleTimeout` | Segundos de silencio antes de que la grabación se detenga. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **NVIDIA BNR: Autostart Container** | Habilita el inicio automático del contenedor. |
| **NVIDIA BNR: Start / Stop** | Inicia o detiene manualmente el contenedor de eliminación de ruido NVIDIA Broadcast. |
| **NVIDIA BNR: Check Status** | Verifica el estado del contenedor. |
| **NVIDIA BNR status dot** | Punto de color que indica el estado del contenedor: Running/Stopped/Unknown. |

## Pestaña Filters

La pestaña Filters configura la nitidez del filtro por modo.

### Nitidez del filtro

| Control | Rango | Descripción | Notas |
|---|---|---|---|
| **Voice / CW / Digital filter sharpness sliders** | 0-3 | Establece la nitidez del filtro por modo (0=menor latencia a 3=más nítido). El deslizador está deshabilitado cuando Auto está habilitado. | Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. | Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **Use Low Latency Filters for Digital Modes** | | Fuerza filtros de baja latencia en DIGU/DIGL. | |

## Pestaña XVTR

La pestaña XVTR gestiona la configuración por transverter.

| Control | Descripción |
|---|---|
| **RX Only:** | Fuerza solo RX en ese transverter. |
| **Remove (xvtr)** | Elimina la definición del transverter. |
| **Create New Transverter** | Añade una nueva entrada de transverter. |

La pestaña contiene pestañas anidadas, una por transverter configurado, más una pestaña "+" para crear nuevos transverters.

## Pestaña USB Cables

Use esta pestaña para configurar los adaptadores serie USB conectados a su FLEX-8600 y asignar a cada uno una función.

### Antes de comenzar

- Conecte los adaptadores serie USB a la computadora que ejecuta AetherSDR antes de abrir el diálogo.
- AetherSDR debe estar conectado a la radio. La pestaña USB Cables no está disponible sin una conexión activa a la radio.

### Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo de Configuración de la Radio directamente en la pestaña USB Cables. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice la lista de cables en el lado izquierdo de la pestaña. Cada cable USB detectado aparece con su nombre y un indicador de estado **Plugged** o **Unplugged**.
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Establezca el tipo de cable usando el campo **Name:** y el selector de tipo asociado. Elija entre CAT, BCD, bit o PTT dependiendo de la función de este cable.
