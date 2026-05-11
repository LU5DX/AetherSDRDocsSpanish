# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona controles para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, serie (FlexControl), APD y Temas.

## Abrir el diálogo

1. Seleccione `Settings > Radio Setup...` del menú principal.
2. El diálogo se abre como una ventana sin marco con una barra de título personalizada en plataformas compatibles. Puede arrastrarlo por la barra de título.
3. Cierre el diálogo haciendo clic en el botón **X** de la barra de título o presionando `Escape`.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Información de la radio (solo lectura)

| Control | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis. |
| **Region** | Región reglamentaria de la radio. |
| **HW Version** | Cadena de versión del hardware. |
| **Model** | Modelo de la radio. |
| **Options** | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado de habilitación de multiFLEX. |
| **License Info** | Muestra suscripción, vencimiento, ID de radio y detalles de la versión licenciada. |

### Campos de identificación

| Control | Comportamiento |
|---|---|
| **Nickname** | Apodo amigable de la radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si está vacío. Se almacena en la configuración `StationName`. Se envía a la radio como "client station <nombre>". |

### Encendido remoto

Haga clic en **Remote On** para habilitar la capacidad de activación/encendido remoto.

### Actualización de firmware

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` preextraído. El gestor detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. Aparece un indicador de progreso mientras se completa la preparación.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio.

## Pestaña Network

La pestaña **Network** muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red (solo lectura)

| Control | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Apagado | - | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | 1450 | 576-9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 de salida en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en la configuración `NetworkMtu`. |
| **DHCP / Static** | DHCP | - | Alterna entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | - | - | Campos de configuración de IP estática (se muestran cuando se selecciona el modo Static). |
| **Apply** | - | - | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña **TX** controla los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en cascada, seguimiento de slice/TX y proporciona un acceso directo a la Configuración de Banda de TX.

### Configuración de Banda de TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Controles de TX

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | - | - | Tiempos de retención/retardo de TX. |
| **Interlocks - TX REQ: RCA / Accessory** | Apagado | - | Habilita las entradas de enclavamiento RCA y accessory. |
| **Max Power:** | - | 0-100 % | Establece el límite de potencia de TX a nivel de radio. |
| **Tune Mode:** | - | - | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** | Apagado | - | Dibuja la señal de TX en la cascada. |
| **TX Follows Active Slice** | Falso | - | TX sigue la slice activa. Mutuamente excluyente con "Active Slice Follows TX". Se deshabilita automáticamente durante la operación en Split. Se almacena en la configuración `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Falso | - | Cambia la slice activa cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con "TX Follows Active Slice". Se almacena en la configuración `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de audio

| Control | Comportamiento |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Iambic:** | Deshabilitado | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. |
| **Swap:** | Apagado | - | Intercambia dit/dah. |
| **Sideband:** | - | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | Apagado | - | Habilita la activación de macros CWX. |
| **Decode:** | Verdadero | - | Habilita la superposición de decodificación CW en el panadapter. Se almacena en la configuración `CwDecodeOverlay`. |

### RTTY

| Control | Comportamiento |
|---|---|
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña **RX** proporciona calibración de compensación de frecuencia GPSDO y selección de fuente de referencia de 10 MHz.

### Calibración de frecuencia

En la versión v0.9.2.1, los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo indica:
- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y etiqueta como **Busy** mientras un barrido está en progreso. |
| **Freq Offset (ppb):** | Compensación de frecuencia manual en partes por billón. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de calibración: Iniciando, texto de progreso o error. Se actualiza en vivo durante el barrido. |

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** selecciona qué oscilador utiliza la radio como referencia de frecuencia.

#### Población del cuadro combinado

El cuadro combinado se puebla dinámicamente según lo que informa la radio. Los elementos aparecen según las siguientes reglas:

| Etiqueta del elemento | Cuándo se muestra |
|---|---|
| Auto | Siempre presente. |
| TCXO | Presente cuando la radio ha informado algún estado de oscilador, cuando la radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Presente cuando la radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Presente cuando la radio ha informado algún estado de oscilador, cuando la radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

El cuadro combinado selecciona el elemento que coincide con el `oscSetting` actual de la radio. Si ese valor no está en la lista, el cuadro combinado retrocede a la selección actual, y luego a **Auto**.

#### Etiqueta de estado de bloqueo

La etiqueta a la derecha del cuadro combinado muestra el estado actual del oscilador y la condición de bloqueo.

| Condición | Texto de la etiqueta | Color |
|---|---|---|
| Aún no se ha recibido estado | Waiting for oscillator status | Gris |
| La configuración es Auto, la radio ha seleccionado una fuente | Auto -> \<fuente\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración difiere del estado activo | \<configuración\> -> \<activo\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración coincide con el estado activo | \<fuente\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| External seleccionado pero no se detecta señal externa | \<texto\> (not detected) añadido | Verde (bloqueado) / Rojo (desbloqueado) |

La radio envía `ext` para la fuente externa en algunas respuestas de firmware. AetherSDR normaliza esto a `external` antes de mostrarlo, por lo que la etiqueta siempre muestra **External 10 MHz** en lugar de **Ext**.

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de radio

| Control | Comportamiento |
|---|---|
| **Line Out:** | Control deslizante de ganancia de línea de salida. |
| **Mute (Line Out)** | Silencia la línea de salida. |
| **Headphone:** | Control deslizante de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Auto | Selecciona el códec de audio para SmartLink/LAN. Se almacena en la configuración `AudioCompression`. |

### Gestión de energía

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Prevent system sleep while connected** | Falso | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en flujos de audio/TCP/UDP durante la inactividad. Se almacena en la configuración `InhibitSleepWhileConnected`. |

### Dispositivos de audio del PC

| Control | Comportamiento |
|---|---|
| **PC Audio Devices: Input: / Output:** | Selecciona los dispositivos de audio de entrada/salida del host. |

### Refuerzo y búfer de audio

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Audio Boost:** | Apagado | - | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en la configuración `AudioBoost`. |
| **Audio Buffer:** | 200 | 50-1000 ms | Aumenta el búfer de audio en milisegundos para fluctuación en VPN/SmartLink. Se almacena en la configuración `AudioBufferMs`. |

### Grabación

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Recording: Radio Side / Client Side** | Radio Side | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena en la configuración `RecordingMode`. |
| **Save to:** | Documents/AetherSDR/Recordings | Carpeta para grabaciones guardadas (solo lado del cliente). Se almacena en la configuración `QsoRecordingDir`. |
| **...** | - | Examina para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | Falso | Graba automáticamente mientras transmite. Se almacena en la configuración `QsoRecordingAutoRecord`. |
| **Idle timeout:** | 120 | 10-3600 seg | Segundos de silencio antes de que la grabación se detenga. Se almacena en la configuración `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

| Control | Comportamiento |
|---|---|
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. El punto de estado indica Ejecutando/Detenido/Desconocido. |

## Pestaña Filters

La pestaña **Filters** proporciona opciones de filtro de baja latencia / nítidos por ancho de banda.

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Voice / CW / Digital filter sharpness sliders** | - | 0-3 | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Apagado | - | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharmess <modo> auto_level=1`. |
| **Use Low Latency Filters for Digital Modes** | Apagado | - | Fuerza filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña **XVTR** proporciona configuración por transverter.

### Crear un nuevo transverter

1. Haga clic en **Create New Transverter**.
2. Aparece una nueva pestaña anidada. Configure los campos para la nueva entrada en esa pestaña.
3. Para restringir la entrada solo a recepción, establezca **RX Only:** en el estado habilitado.
4. Para eliminar una entrada que ya no necesita, haga clic en **Remove** en la pestaña de esa entrada.

### Controles por transverter

| Control | Comportamiento |
|---|---|
| **RX Only:** | Fuerza el transverter a solo recepción, evitando TX a través de él. |
| **Remove** | Elimina permanentemente la definición del transverter seleccionado. |
| **Create New Transverter** | Agrega una nueva entrada de transverter y abre su pestaña de configuración. |

## Pestaña USB Cables

La pestaña **USB Cables** asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Comportamiento |
|---|---|
| **Cables list / Status** | C
