# Diálogo de Configuración de Radio de AetherSDR

El diálogo **Configuración de Radio** es la ventana de configuración maestra para los ajustes por radio. Contiene pestañas para información de radio, red, GPS, transmisión, teléfono/CW, recepción, antenas, audio, filtros, transvertidores, cables USB, periféricos, APD, Temas, SmartLink y, opcionalmente, puertos serie.

## Abrir el diálogo Configuración de Radio

1. Haga clic en `Settings > Radio Setup...`.

## Diseño del diálogo

El diálogo **Configuración de Radio** utiliza un diálogo persistente que recuerda su tamaño y posición entre sesiones. La geometría se guarda en `RadioSetupDialogGeometry` en la configuración de la aplicación.

Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Temas, Audio, Filtros, Periféricos) están envueltas en un área de desplazamiento vertical. La barra de desplazamiento aparece solo cuando el contenido se desborda; en pantallas anchas no hay cambio visual.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio y los controles de gestión de firmware.

### Información de radio (solo lectura)

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región regulatoria (ej. USA) |
| **HW Version** | Cadena de versión de hardware |
| **Model** | Modelo de radio (ej. FLEX-8600) |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de expiración, ID de radio y versión licenciada |

Cada campo de solo lectura tiene un botón de copia a su derecha que copia el valor mostrado al portapapeles. Cuando el valor está vacío o no disponible, el botón de copia está atenuado.

### Campos configurables por el usuario

| Control | Qué hace |
|---|---|
| **Nickname** | Ingrese un nombre descriptivo para la radio |
| **Callsign** | Ingrese el indicativo de la estación |
| **Station Name** | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Si está vacío, se usa el nombre del host del SO. Se almacena en `StationName`. |

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de encendido remoto/activación remota de la radio.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación antes del reinicio.

- En una conexión LAN: AetherSDR se desconecta y se reconecta automáticamente una vez que la radio termina de iniciar.
- En una conexión SmartLink/WAN: AetherSDR se desconecta. Debe reconectarse manualmente después de que la radio termine de iniciar.

El botón está deshabilitado cuando la radio está desconectada o reconectándose.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar a la radio las versiones de firmware disponibles.
2. Si hay una actualización disponible, la etiqueta de estado muestra la versión y le indica que descargue el instalador de SmartSDR desde flexradio.com.
3. Descargue el instalador de SmartSDR (.msi para v4.2+, .exe para versiones anteriores).
4. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo .ssdr preextraído en el selector de archivos.
5. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Pestaña Network

La pestaña **Network** muestra la información de red de la radio y permite la configuración.

### Información de red (solo lectura)

| Control | Qué muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red actuales |

### Configuración

| Control | Qué hace | Rango válido |
|---|---|---|
| **Enforce Private IP Connections:** | Active para rechazar pares no RFC1918 | On / Off |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 de salida en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en `NetworkMtu`. | 576–9000 bytes |
| **DHCP / Static** | Cambia entre los modos DHCP e IP estática | DHCP / Static |

Cuando se selecciona **Static**, ingrese la **IP Address:**, **Mask:** y **Gateway:** en los campos de texto, luego haga clic en **Apply** para enviar la configuración a la radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS e información en vivo cuando un módulo GPS está instalado y activo.

### Información GPS (solo lectura)

| Indicador | Qué muestra |
|---|---|
| Estado GPS | Latitud, longitud, altitud, hora UTC y número de satélites cuando el GPS está activo |

## Pestaña TX

La pestaña **TX** configura los parámetros de transmisión.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonización por banda.

### Timings

Use los cuadros de giro **Timings** para establecer los tiempos de espera y retardo de TX en milisegundos. El campo **Timeout (sec)** muestra el tiempo de espera de interbloqueo en segundos para facilitar la lectura; la radio almacena este valor internamente en milisegundos.

### Interlocks

Active **TX REQ: RCA** y **Accessory** para habilitar las entradas de interbloqueo.

### Power and Tune

| Control | Qué hace | Rango válido |
|---|---|---|
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | 0–100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonización | — |

### Display

| Control | Qué hace |
|---|---|
| **Show TX in Waterfall:** | Active para dibujar la señal de TX en el waterfall |

### Comportamiento de seguimiento de slice

| Control | Qué hace |
|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Se excluye mutuamente con Active Slice Follows TX. Se desactiva automáticamente durante la operación Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Se excluye mutuamente con TX Follows Active Slice. Se almacena en `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de nivel

Active **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel del micrófono incluso durante la recepción.

### Manipulador CW

| Control | Qué hace | Rango válido |
|---|---|---|
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio | Enabled / Disabled |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A / B |
| **Swap:** | Intercambia dit/dah | On / Off |
| **Sideband:** | Selecciona la banda lateral del tono CW | LSB / USB |
| **CWX:** | Habilita el keying de macros CWX | On / Off |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Se almacena en `CwDecodeOverlay`. | On / Off |

### RTTY

| Control | Qué hace |
|---|---|
| **RTTY Mark Default:** | Establece la frecuencia de marca RTTY predeterminada |

## Pestaña RX

La pestaña **RX** proporciona calibración de frecuencia y selección de fuente de referencia.

### Calibración de frecuencia

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz para usar en la calibración |
| **Start** | Inicia el barrido de calibración de frecuencia |
| **Freq Offset (ppb):** | Muestra o permite ajustar manualmente el desplazamiento de frecuencia actual en partes por mil millones |

### Fuente de referencia de 10 MHz

| Control | Qué hace | Rango válido |
|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. | Auto / TCXO / GPSDO / External |

La etiqueta de estado de bloqueo junto al control se actualiza en vivo.

## Pestaña Antennas

La pestaña **Antennas** configura los nombres de las antenas para cada puerto de antena en la radio. Esta pestaña se construye de forma diferida cuando se hace clic por primera vez.

| Control | Qué hace |
|---|---|
| **ANT1:** | Ingrese un nombre personalizado para el puerto de antena 1 |
| **ANT2:** | Ingrese un nombre personalizado para el puerto de antena 2 |
| **XVTA:** | Ingrese un nombre personalizado para el puerto de transvertidor A |
| **XVTB:** | Ingrese un nombre personalizado para el puerto de transvertidor B |

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, la compresión, los dispositivos de PC, el refuerzo, el búfer, la grabación y NVIDIA BNR.

### Salidas de audio de la radio

| Control | Qué hace |
|---|---|
| **Line Out:** | Deslice para ajustar la ganancia de salida de línea |
| **Mute (Line Out)** | Haga clic para silenciar la salida de línea |
| **Headphone:** | Deslice para ajustar la ganancia de los auriculares |
| **Mute (Headphone)** | Haga clic para silenciar los auriculares |
| **Front Speaker:** / **Mute** | Haga clic para silenciar el altavoz frontal (específico del modelo) |

### Compresión de audio

| Control | Qué hace | Rango válido |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink/LAN. Se almacena en `AudioCompression`. | Auto / Uncompressed / Opus |

### Prevención de suspensión del sistema

Marque **Prevent system sleep while connected** para mantener el SO despierto mientras la radio está conectada. Se almacena en `InhibitSleepWhileConnected`.

### PC Audio Devices

| Control | Qué hace |
|---|---|
| **PC Audio Devices: Input:** | Seleccione el dispositivo de entrada de audio del host |
| **PC Audio Devices: Output:** | Seleccione el dispositivo de salida de audio del host |

### Audio Boost

Active **Audio Boost:** para habilitar ganancia adicional en la ruta de audio del cliente. Se almacena en `AudioBoost`.

### Audio Buffer

Ingrese un valor en **Audio Buffer:** para establecer el búfer de audio del lado del cliente en milisegundos. Aumente este valor cuando use conexiones VPN o SmartLink con latencia inestable. Se almacena en `AudioBufferMs`.

| Rango válido | Predeterminado |
|---|---|
| 50–1000 ms | 200 ms |

### Recording

| Control | Qué hace | Rango válido |
|---|---|---|
| **Recording: Radio Side / Client Side** | Elige la grabación del lado de la radio o del lado del cliente. Se almacena en `RecordingMode`. | Radio Side / Client Side |
| **Save to:** | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto en Documents/AetherSDR/Recordings. Se almacena en `QsoRecordingDir`. | — |
| **...** | Haga clic para buscar la carpeta de grabación | — |
| **Auto-record on TX** | Marque para grabar automáticamente mientras transmite. Se almacena en `QsoRecordingAutoRecord`. | On / Off |
| **Idle timeout:** | Segundos de silencio antes de que se detenga la grabación. Se almacena en `QsoRecordingIdleTimeout`. | 10–3600 seg (predeterminado 120) |

### NVIDIA BNR

| Control | Qué hace |
|---|---|
| **Autostart Container** | Haga clic para configurar el inicio automático del contenedor |
| **Start** | Haga clic para iniciar el contenedor de eliminación de ruido NVIDIA Broadcast |
| **Stop** | Haga clic para detener el contenedor |
| **Check Status** | Haga clic para verificar el estado del contenedor |

Un punto de estado de color indica el estado del contenedor (Running/Stopped/Unknown).

## Pestaña Filters

La pestaña **Filters** configura la nitidez del filtro por modo.

### Nitidez del filtro

Use los controles deslizantes para **Voice**, **CW** y **Digital** para establecer la nitidez del filtro:

| Valor | Significado |
|---|---|
| 0 | Latencia más baja |
| 1 | — |
| 2 | — |
| 3 | Más nítido |

Los controles deslizantes están deshabilitados cuando **Auto** está habilitado para ese modo.

### Modo Auto

Active **Auto** para Voice, CW o Digital para habilitar la selección automática del nivel de filtro. Cuando está habilitado, el control deslizante de nitidez manual para ese modo se deshabilita.

### Low Latency Filters

Marque **Use Low Latency Filters for Digital Modes** para forzar filtros de baja latencia en DIGU/DIGL.

## Pestaña XVTR

La pestaña **XVTR** configura los ajustes por transvertidor. Contiene pestañas anidadas, una por transvertidor configurado, más una pestaña **+** para crear nuevos transvertidores.

### Controles por transvertidor

| Control | Qué hace |
|---|---|
| **RX Only:** | Active para forzar solo RX en ese transvertidor |
| **Remove** | Haga clic para eliminar la definición del transvertidor |

### Crear un nuevo transvertidor

1. Haga clic en la pestaña **+** (etiquetada **Create New Transverter**).
2. Configure los parámetros del transvertidor.

### XVTR Policy

La sección **XVTR Policy** permite configurar cómo se manejan los transvertidores con respecto a los bordes de banda y los límites de frecuencia. Esto se gestiona a través del modelo `XvtrPolicy`.

| Control | Qué hace |
|---|---|
| Policy selection | Elija cómo se aplican los bordes de banda y los límites de frecuencia del transvertidor |

## Pestaña USB Cables

La pestaña **USB Cables** asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

### Detección de cables

La lista **Cables list / Status** muestra los cables USB detectados por tipo con estado Plugged/Unplugged.

### Configuración por cable

Cada cable detectado proporciona los siguientes parámetros:

| Control | Qué hace |
|---|---|
| **Name:** | Identificador del cable |
| **Enabled** | Activar/desactivar cable |
| **Speed** | Selección de baudios |
| **Data Bits** | Selección de bits de datos |
| **Parity** | Selección de paridad |
| **Stop Bits** | Selección de bits de parada |
| **Flow** | Selección de control de flujo |
| **Source** | Selección de fuente de señal |
| **Auto Report** | Activar/desactivar informe automático |
| **BCD Type** | Selección de tipo de salida BCD |
| **Polarity** | Selección de polaridad de señal |
| **Bit Configuration (0-7)** | Configuración de bits por pin |

## Pestaña Peripherals

La pestaña **Peripherals** gestiona dispositivos externos a través de conexión TCP directa (TGXL, PGXL, Antenna Genius).

### TGXL

Haga clic en **Connect** para abrir una conexión TCP directa al TGXL en el puerto 9010. La IP y el puerto se guardan en `TGXL
