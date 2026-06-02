# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona controles para información de radio, red, GPS, TX, antenas, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, serie (FlexControl), APD, Temas y gestión de certificados anclados de SmartLink.

## Abrir el diálogo

1. Seleccione `Settings > Radio Setup...` desde el menú principal.
2. El diálogo se abre como una ventana persistente que recuerda su posición y tamaño entre sesiones. Puede arrastrarla por la barra de título.
3. Cierre el diálogo haciendo clic en el botón **X** de la barra de título o presionando `Escape`.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, la información de licencia y los controles de actualización de firmware.

### Información de la radio (solo lectura)

Cada campo de solo lectura incluye un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar. Haga clic en el botón para copiar el valor del campo al portapapeles del sistema. Una breve ventana emergente "¡Copiado!" confirma la acción.

| Control | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis. Haga clic en el botón de copia para copiar. |
| **Region** | Región regulatoria de la radio. |
| **HW Version** | Cadena de versión de hardware. Haga clic en el botón de copia para copiar. |
| **Model** | Modelo de radio. |
| **Options** | Muestra las opciones de radio licenciadas. Haga clic en el botón de copia para copiar. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **License Info** | Muestra suscripción, vencimiento, ID de Radio (haga clic en el botón de copia para copiar) y detalles de la versión licenciada. |

### Campos de identificación

| Control | Comportamiento |
|---|---|
| **Nickname** | Apodo amigable de la radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto es el nombre de host del SO si está vacío. Se almacena en la configuración `StationName`. Se envía a la radio como "client station <nombre>". |

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de encendido / activación remota.

### Actualización de firmware

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que debe descargar el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Browse .ssdr...** y seleccione el instalador descargado o un archivo `.ssdr` previamente extraído. El gestor detecta el formato de archivo automáticamente y extrae el firmware sin herramientas externas. Aparece un indicador de progreso mientras se completa la preparación.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio.

## Pestaña Network

La pestaña **Network** muestra la información de red de la radio y proporciona opciones de red avanzadas.

### Información de red (solo lectura)

| Control | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada campo incluye un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar. Haga clic en el botón para copiar el valor al portapapeles del sistema. |

### Configuración de red

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Off | - | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | 1450 | 576-9000 bytes | Establece el tamaño máximo de paquete UDP VITA-49 de salida en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en la configuración `NetworkMtu`. |
| **DHCP / Static** | DHCP | - | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | - | - | Campos de configuración de IP estática (se muestran cuando se selecciona el modo Estática). |
| **Apply** | - | - | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña **TX** controla tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y proporciona un acceso directo a la Configuración de Banda TX.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones de TX

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | - | - | Temporizaciones de pausa/retardo de TX. |

### Otros controles de TX

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Interlocks - TX REQ: RCA / Accessory** | Off | - | Habilita las entradas de enclavamiento RCA y Accesorio. |
| **Max Power:** | - | 0-100 % | Establece el límite de potencia de TX a nivel de radio. |
| **Tune Mode:** | - | - | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** | Off | - | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | False | - | TX sigue al slice activo. Se excluye mutuamente con 'Active Slice Follows TX'. Se desactiva automáticamente durante la operación en Split. Se almacena en la configuración `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | False | - | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Se excluye mutuamente con 'TX Follows Active Slice'. Se almacena en la configuración `ActiveFollowsTxSlice`. |

## Pestaña Antennas

La pestaña **Antennas** le permite asignar nombres personalizados a cada puerto de antena de la radio. Esta pestaña se construye de forma diferida al hacer clic por primera vez.

### Campos de nombre de antena

| Control | Comportamiento |
|---|---|
| **ANT1 - ANT8** | Campos de texto para asignar nombres amigables a cada puerto de antena. Los nombres se almacenan en la radio. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de audio

| Control | Comportamiento |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Iambic:** | Disabled | Enabled / Disabled | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| **Swap:** | Off | - | Intercambia dit/dah. |
| **Sideband:** | - | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | Off | - | Habilita el macreo de macros CWX. |
| **Decode:** | True | - | Habilita la superposición de decodificación CW en el panadapter. Se almacena en la configuración `CwDecodeOverlay`. |

### RTTY

| Control | Comportamiento |
|---|---|
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. |

## Pestaña RX

La pestaña **RX** proporciona la calibración del offset de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo muestra:
- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Deshabilitado y etiquetado como **Busy** mientras un barrido está en progreso. |
| **Freq Offset (ppb):** | Offset de frecuencia manual en partes por billón. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de calibración: Starting, texto de progreso o error. Se actualiza en vivo durante el barrido. |

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** selecciona qué oscilador utiliza la radio como referencia de frecuencia.

#### Población del cuadro combinado

El cuadro combinado se llena dinámicamente según lo que informa la radio. Los elementos aparecen según las siguientes reglas:

| Etiqueta del elemento | Cuándo se muestra |
|---|---|
| Auto | Siempre presente. |
| TCXO | Presente cuando la radio ha informado algún estado de oscilador, cuando la radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Presente cuando la radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Presente cuando la radio ha informado algún estado de oscilador, cuando la radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

El cuadro combinado selecciona el elemento que coincide con el `oscSetting` actual de la radio. Si ese valor no está en la lista, el cuadro combinado vuelve a la selección actual y luego a **Auto**.

#### Etiqueta de estado de bloqueo

La etiqueta a la derecha del cuadro combinado muestra el estado actual del oscilador y la condición de bloqueo.

| Condición | Texto de la etiqueta | Color |
|---|---|---|
| Aún no se ha recibido estado | Waiting for oscillator status | Gris |
| La configuración es Auto, la radio ha seleccionado una fuente | Auto -> \<fuente\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración difiere del estado activo | \<configuración\> -> \<activo\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración coincide con el estado activo | \<fuente\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| External seleccionado pero no se detecta señal externa | \<texto\> (not detected) añadido | Verde (bloqueado) / Rojo (desbloqueado) |

La radio envía `ext` para la fuente externa en algunas respuestas de firmware. AetherSDR normaliza esto a `external` antes de mostrar, por lo que la etiqueta siempre muestra **External 10 MHz** en lugar de **Ext**.

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, aumento, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de radio

| Control | Comportamiento |
|---|---|
| **Line Out:** | Control deslizante de ganancia de salida de línea. |
| **Mute (Line Out)** | Silencia la salida de línea. |
| **Headphone:** | Control deslizante de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Predeterminado | Comportamiento |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Auto | Selecciona el códec de audio para SmartLink/LAN. Se almacena en la configuración `AudioCompression`. |

### Gestión de energía

| Control | Predeterminado | Comportamiento |
|---|---|---|
| **Prevent system sleep while connected** | False | Mantiene el SO activo mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena en la configuración `InhibitSleepWhileConnected`. |

### Dispositivos de audio de PC

| Control | Comportamiento |
|---|---|
| **PC Audio Devices: Input: / Output:** | Selecciona los dispositivos de entrada/salida de audio del host. |

### Aumento y búfer de audio

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Audio Boost:** | Off | - | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en la configuración `AudioBoost`. |
| **Audio Buffer:** | 200 | 50-1000 ms | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Se almacena en la configuración `AudioBufferMs`. |

### Grabación

| Control | Predeterminado | Comportamiento |
|---|---|---|
| **Recording: Radio Side / Client Side** | Radio Side | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena en la configuración `RecordingMode`. |
| **Save to:** | Documents/AetherSDR/Recordings | Carpeta para las grabaciones guardadas (solo lado del cliente). Se almacena en la configuración `QsoRecordingDir`. |
| **...** | - | Examina para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | False | Graba automáticamente mientras transmite. Se almacena en la configuración `QsoRecordingAutoRecord`. |
| **Idle timeout:** | 120 | 10-3600 seg | Segundos de silencio antes de que se detenga la grabación. Se almacena en la configuración `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

| Control | Comportamiento |
|---|---|
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. El punto de estado indica Running/Stopped/Unknown. |

## Pestaña Filters

La pestaña **Filters** proporciona opciones de filtro de baja latencia / nítido por ancho de banda.

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Voice / CW / Digital filter sharpness sliders** | - | 0-3 | Establece la nitidez del filtro (0=mínima latencia a 3=máxima nitidez) por modo; el control deslizante está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Off | - | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **Use Low Latency Filters for Digital Modes** | Off | - | Fuerza filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR
