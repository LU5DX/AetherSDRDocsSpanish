# Diálogo de Configuración de Radio de AetherSDR

El diálogo **Configuración de Radio** es la ventana maestra de configuración para los ajustes específicos de cada radio. Contiene pestañas para información de la radio, red, GPS, transmisión, fonía/CW, recepción, audio, filtros, transvertidores, cables USB, periféricos y, opcionalmente, puertos serie.

## Abrir el diálogo Configuración de Radio

1. Haga clic en `Settings > Radio Setup...`.

## Diseño del diálogo

El diálogo **Configuración de Radio** ahora utiliza un diseño de ventana sin bordes con una barra de título personalizada. La barra de título muestra "Radio Setup" y proporciona los controles de ventana estándar (minimizar, maximizar, cerrar).

El diálogo recuerda su tamaño y posición entre sesiones. La geometría se guarda en `RadioSetupDialogGeometry` en la configuración de la aplicación.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio y los controles de gestión de firmware.

### Información de la radio (solo lectura)

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región normativa (p. ej., USA) |
| **HW Version** | Cadena de versión del hardware |
| **Model** | Modelo de radio (p. ej., FLEX-8600) |
| **Options** | Opciones licenciadas de la radio |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de vencimiento, ID de radio y versión licenciada |

### Campos configurables por el usuario

| Control | Qué hace |
|---|---|
| **Nickname** | Ingrese un nombre descriptivo para la radio |
| **Callsign** | Ingrese el indicativo de la estación |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se establece por defecto al nombre de host del SO si está vacío. Se almacena en `StationName`. |

### Encendido remoto

Haga clic en **Remote On** para habilitar la capacidad de activación remota/encendido remoto de la radio.

### Actualización de firmware

El flujo de trabajo de actualización de firmware utiliza el botón **Select Installer...** (etiquetado **Browse .ssdr...** antes de la v0.9.3).

1. Haga clic en **Check for Update** para consultar a la radio las versiones de firmware disponibles.
2. Si hay una actualización disponible, la etiqueta de estado muestra la versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
3. Descargue el instalador de SmartSDR (.msi para v4.2+, .exe para versiones anteriores).
4. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo .ssdr preextraído en el selector de archivos.
5. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

El preparador detecta automáticamente el formato a partir de los primeros 8 bytes (marca OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas.

## Pestaña Red

La pestaña **Network** muestra la información de red de la radio y permite la configuración.

### Información de red (solo lectura)

| Control | Qué muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red actuales |

### Configuración

| Control | Qué hace | Rango válido |
|---|---|---|
| **Enforce Private IP Connections:** | Alternar para rechazar pares que no sean RFC1918 | On / Off |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en `NetworkMtu`. | 576–9000 bytes |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática | DHCP / Static |

Cuando se selecciona **Static**, ingrese la **IP Address:**, **Mask:** y **Gateway:** en los campos de texto, luego haga clic en **Apply** para enviar la configuración a la radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS e información en vivo cuando un módulo GPS está instalado y activo.

### Información GPS (solo lectura)

| Indicador | Qué muestra |
|---|---|
| Estado GPS | Latitud, longitud, altitud, hora UTC y número de satélites cuando el GPS está activo |

## Pestaña TX

La pestaña **TX** configura los parámetros de transmisión.

### Configuración de banda TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

Use los cuadros giratorios de **Timings** para ajustar los tiempos de retención y retardo de TX en milisegundos.

### Interbloqueos

Active **TX REQ: RCA** y **Accessory** para habilitar las entradas de interbloqueo.

### Potencia y sintonía

| Control | Qué hace | Rango válido |
|---|---|---|
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | 0–100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — |

### Visualización

| Control | Qué hace |
|---|---|
| **Show TX in Waterfall:** | Alternar para dibujar la señal de TX en el waterfall |

### Comportamiento de seguimiento de slice

| Control | Qué hace |
|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante la operación en Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. Se almacena en `ActiveFollowsTxSlice`. |

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

La sección de calibración siempre es visible independientemente de la presencia de GPSDO. Cuando hay un GPSDO presente, la etiqueta de estado lo confirma en verde; cuando está ausente, en ámbar.

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz para usar en la calibración |
| **Start** | Inicia la secuencia de calibración de frecuencia. AetherSDR restablece el error de frecuencia a 0 ppb, luego envía `radio pll_start` a la radio. El botón muestra **Busy** mientras se ejecuta la calibración. |
| **Freq Offset (ppb):** | Muestra o establece manualmente el desplazamiento de frecuencia actual en partes por mil millones |

### Fuente de referencia de 10 MHz

| Control | Qué hace | Rango válido |
|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. | Auto / TCXO / GPSDO / External |

La etiqueta de estado de bloqueo junto al control se actualiza en vivo:

- Si la radio aún no ha informado el estado del oscilador: **Waiting for oscillator status**
- Si se selecciona **Auto** y la radio resolvió una fuente específica: **Auto -> \<fuente resuelta\>** seguido de **Locked** o **Unlocked**
- Si se selecciona una fuente específica pero una fuente diferente está activa: **\<fuente seleccionada\> -> \<fuente activa\>** seguido de **Locked** o **Unlocked**
- De lo contrario: nombre de la fuente activa seguido de **Locked** o **Unlocked**

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, la compresión, los dispositivos de PC, el refuerzo, el búfer, la grabación y NVIDIA BNR.

### Salidas de audio de la radio

| Control | Qué hace |
|---|---|
| **Line Out:** | Deslice para ajustar la ganancia de la salida de línea |
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

### Dispositivos de audio del PC

| Control | Qué hace |
|---|---|
| **PC Audio Devices: Input:** | Seleccione el dispositivo de entrada de audio del host |
| **PC Audio Devices: Output:** | Seleccione el dispositivo de salida de audio del host |

### Refuerzo de audio

Active **Audio Boost:** para habilitar ganancia adicional en la ruta de audio del cliente. Se almacena en `AudioBoost`.

### Búfer de audio

Ingrese un valor en **Audio Buffer:** para establecer el búfer de audio del lado del cliente en milisegundos. Aumente esto cuando use conexiones VPN o SmartLink con latencia inestable. Se almacena en `AudioBufferMs`.

| Rango válido | Predeterminado |
|---|---|
| 50–1000 ms | 200 ms |

### Grabación

| Control | Qué hace | Rango válido |
|---|---|---|
| **Recording: Radio Side / Client Side** | Elige la grabación del lado de la radio o del lado del cliente. Se almacena en `RecordingMode`. | Radio Side / Client Side |
| **Save to:** | Carpeta para las grabaciones guardadas (solo lado del cliente). Se establece por defecto en Documentos/AetherSDR/Recordings. Se almacena en `QsoRecordingDir`. | — |
| **...** | Haga clic para explorar la carpeta de grabación | — |
| **Auto-record on TX** | Marque para grabar automáticamente mientras transmite. Se almacena en `QsoRecordingAutoRecord`. | On / Off |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga. Se almacena en `QsoRecordingIdleTimeout`. | 10–3600 seg (predeterminado 120) |

### NVIDIA BNR

| Control | Qué hace |
|---|---|
| **Autostart Container** | Haga clic para configurar el inicio automático del contenedor |
| **Start** | Haga clic para iniciar el contenedor de eliminación de ruido NVIDIA Broadcast |
| **Stop** | Haga clic para detener el contenedor |
| **Check Status** | Haga clic para verificar el estado del contenedor |

Un punto de estado coloreado indica el estado del contenedor (Running/Stopped/Unknown).

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

### Modo automático

Active **Auto** para Voice, CW o Digital para habilitar la selección automática del nivel de filtro. Cuando está habilitado, el control deslizante de nitidez manual para ese modo está deshabilitado.

### Filtros de baja latencia

Marque **Use Low Latency Filters for Digital Modes** para forzar filtros de baja latencia en DIGU/DIGL.

## Pestaña XVTR

La pestaña **XVTR** configura los ajustes por transvertidor. Contiene pestañas anidadas, una por transvertidor configurado, más una pestaña **+** para crear nuevos transvertidores.

### Controles por transvertidor

| Control | Qué hace |
|---|---|
| **RX Only:** | Alternar para forzar solo RX en ese transvertidor |
| **Remove** | Haga clic para eliminar la definición del transvertidor |

### Crear un nuevo transvertidor

1. Haga clic en la pestaña **+** (etiquetada **Create New Transverter**).
2. Configure los parámetros del transvertidor.

## Pestaña USB Cables

La pestaña **USB Cables** asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

### Detección de cables

La **Cables list / Status** muestra los cables USB detectados por tipo con estado Plugged/Unplugged.

### Configuración por cable

Cada cable detectado proporciona los siguientes parámetros:

| Control | Qué hace |
|---|---|
| **Name:** | Identificador del cable |
| **Enabled** | Alternar habilitación del cable |
| **Speed** | Selección de velocidad en baudios |
| **Data Bits** | Selección de bits de datos |
| **Parity** | Selección de paridad |
| **Stop Bits** | Selección de bits de parada |
| **Flow** | Selección de control de flujo |
| **Source** | Selección de fuente de señal |
| **Auto Report** | Alternar informe automático |
| **BCD Type** | Selección de tipo de salida BCD |
| **Polarity** | Selección de polaridad de señal |
| **Bit Configuration (0-7)** | Configuración de bits por pin |

## Pestaña Peripherals

La pestaña **Peripherals** gestiona dispositivos externos mediante conexión TCP directa (TGXL, PGXL, Antenna Genius, ShackSwitch).

### TGXL

Haga clic en **Connect** para abrir una conexión TCP directa al TGXL en el puerto 9010. La IP y el puerto se guardan en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar.

Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en el firmware 4.2. El TGXL activa el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita keying del lado del cliente.

Si el campo IP está vacío y la radio ha descubierto el TGXL, el
