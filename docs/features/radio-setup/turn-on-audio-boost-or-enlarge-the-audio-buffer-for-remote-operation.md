# Diálogo de Configuración de Radio de AetherSDR

El diálogo **Configuración de Radio** es la ventana maestra de configuración para los ajustes específicos de cada radio. Contiene pestañas para información de la radio, red, GPS, transmisión, teléfono/CW, recepción, antenas, audio, filtros, transvertidores, cables USB, periféricos, APD, Temas, SmartLink y, opcionalmente, puertos serie.

## Abrir el diálogo Configuración de Radio

1. Haga clic en `Settings > Radio Setup...`.

## Disposición del diálogo

El diálogo **Configuración de Radio** es un diálogo persistente que recuerda su tamaño y posición entre sesiones. La geometría se guarda en `RadioSetupDialogGeometry` en la configuración de la aplicación.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio y los controles de gestión del firmware.

### Información de la radio (solo lectura)

| Control | Lo que muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región reguladora (p. ej., USA) |
| **HW Version** | Cadena de la versión del hardware |
| **Model** | Modelo de la radio (p. ej., FLEX-8600) |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado de habilitación de multiFLEX |
| **License Info** | Estado de la suscripción, fecha de vencimiento, ID de radio y versión licenciada |

Cada campo de solo lectura tiene un botón de copia a su derecha que copia el valor mostrado al portapapeles. Cuando el valor está vacío o no disponible, el botón de copia está atenuado.

### Campos configurables por el usuario

| Control | Lo que hace |
|---|---|
| **Nickname** | Ingrese un nombre descriptivo para la radio |
| **Callsign** | Ingrese el indicativo de la estación |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre del host del SO si está vacío. Se almacena en `StationName`. |

### Encendido remoto

Haga clic en **Remote On** para habilitar la capacidad de activación/encendido remoto de la radio.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar las versiones de firmware disponibles en la radio.
2. Si hay una actualización disponible, la etiqueta de estado muestra la versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
3. Descargue el instalador de SmartSDR (.msi para v4.2+, .exe para versiones anteriores).
4. Haga clic en **Browse .ssdr...** y seleccione el instalador descargado o un archivo .ssdr previamente extraído en el selector de archivos.
5. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Pestaña Red

La pestaña **Network** muestra información de red de la radio y permite su configuración.

### Información de red (solo lectura)

| Control | Lo que muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red actuales |

### Configuración

| Control | Lo que hace | Rango válido |
|---|---|---|
| **Enforce Private IP Connections:** | Active para rechazar pares que no sean RFC1918 | On / Off |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en `NetworkMtu`. | 576–9000 bytes |
| **DHCP / Static** | Cambia entre los modos DHCP e IP estática | DHCP / Static |

Cuando se selecciona **Static**, ingrese la **IP Address:**, **Mask:** y **Gateway:** en los campos de texto, luego haga clic en **Apply** para enviar la configuración a la radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS e información en vivo cuando hay un módulo GPS instalado y activo.

### Información del GPS (solo lectura)

| Indicador | Lo que muestra |
|---|---|
| Estado del GPS | Latitud, longitud, altitud, hora UTC y número de satélites cuando el GPS está activo |

## Pestaña TX

La pestaña **TX** configura los parámetros de transmisión.

### Ajustes de banda TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonización por banda.

### Temporizaciones

Use los controles giratorios **Timings** para establecer los tiempos de espera y retardo de TX en milisegundos. El campo **Timeout (sec)** muestra el tiempo de espera del interbloqueo en segundos para facilitar la lectura; la radio almacena este valor internamente en milisegundos.

### Interbloqueos

Active **TX REQ: RCA** y **Accessory** para habilitar las entradas de interbloqueo.

### Potencia y sintonización

| Control | Lo que hace | Rango válido |
|---|---|---|
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | 0–100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonización | — |

### Visualización

| Control | Lo que hace |
|---|---|
| **Show TX in Waterfall:** | Active para dibujar la señal de TX en el waterfall |

### Comportamiento de seguimiento de slice

| Control | Lo que hace |
|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Es mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante una operación Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con TX Follows Active Slice. Se almacena en `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura los valores predeterminados del micrófono, el manipulador CW y RTTY.

### Medidor de nivel

Active **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel del micrófono incluso durante la recepción.

### Manipulador CW

| Control | Lo que hace | Rango válido |
|---|---|---|
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio | Enabled / Disabled |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A / B |
| **Swap:** | Intercambia dit/dah | On / Off |
| **Sideband:** | Selecciona la banda lateral del tono CW | LSB / USB |
| **CWX:** | Habilita el keying de macros CWX | On / Off |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Se almacena en `CwDecodeOverlay`. | On / Off |

### RTTY

| Control | Lo que hace |
|---|---|
| **RTTY Mark Default:** | Establece la frecuencia de marca RTTY predeterminada |

## Pestaña RX

La pestaña **RX** proporciona la calibración de frecuencia y la selección de la fuente de referencia.

### Calibración de frecuencia

| Control | Lo que hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz para usar en la calibración |
| **Start** | Inicia el barrido de calibración de frecuencia |
| **Freq Offset (ppb):** | Muestra o permite ajustar manualmente el desplazamiento de frecuencia actual en partes por mil millones |

### Fuente de referencia de 10 MHz

| Control | Lo que hace | Rango válido |
|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. | Auto / TCXO / GPSDO / External |

La etiqueta de estado de bloqueo junto al control se actualiza en vivo.

## Pestaña Antenas

La pestaña **Antennas** configura los nombres de las antenas para cada puerto de antena de la radio. Esta pestaña se construye de forma diferida al hacer clic por primera vez.

| Control | Lo que hace |
|---|---|
| **ANT1:** | Ingrese un nombre personalizado para el puerto de antena 1 |
| **ANT2:** | Ingrese un nombre personalizado para el puerto de antena 2 |
| **XVTA:** | Ingrese un nombre personalizado para el puerto de transvertidor A |
| **XVTB:** | Ingrese un nombre personalizado para el puerto de transvertidor B |

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y NVIDIA BNR.

### Salidas de audio de la radio

| Control | Lo que hace |
|---|---|
| **Line Out:** | Deslice para ajustar la ganancia de la salida de línea |
| **Mute (Line Out)** | Haga clic para silenciar la salida de línea |
| **Headphone:** | Deslice para ajustar la ganancia de los auriculares |
| **Mute (Headphone)** | Haga clic para silenciar los auriculares |
| **Front Speaker:** / **Mute** | Haga clic para silenciar el altavoz frontal (específico del modelo) |

### Compresión de audio

| Control | Lo que hace | Rango válido |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink/LAN. Se almacena en `AudioCompression`. | Auto / Uncompressed / Opus |

### Prevención de suspensión del sistema

Marque **Prevent system sleep while connected** para mantener el SO activo mientras la radio está conectada. Se almacena en `InhibitSleepWhileConnected`.

### Dispositivos de audio del PC

| Control | Lo que hace |
|---|---|
| **PC Audio Devices: Input:** | Seleccione el dispositivo de entrada de audio del host |
| **PC Audio Devices: Output:** | Seleccione el dispositivo de salida de audio del host |

### Refuerzo de audio

Active **Audio Boost:** para habilitar ganancia adicional en la ruta de audio del cliente. Se almacena en `AudioBoost`.

### Búfer de audio

Ingrese un valor en **Audio Buffer:** para establecer el búfer de audio del lado del cliente en milisegundos. Aumente este valor cuando use conexiones VPN o SmartLink con latencia inestable. Se almacena en `AudioBufferMs`.

| Rango válido | Predeterminado |
|---|---|
| 50–1000 ms | 200 ms |

### Grabación

| Control | Lo que hace | Rango válido |
|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena en `RecordingMode`. | Radio Side / Client Side |
| **Save to:** | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. Se almacena en `QsoRecordingDir`. | — |
| **...** | Haga clic para buscar la carpeta de grabación | — |
| **Auto-record on TX** | Marque para grabar automáticamente mientras transmite. Se almacena en `QsoRecordingAutoRecord`. | On / Off |
| **Idle timeout:** | Segundos de silencio antes de que se detenga la grabación. Se almacena en `QsoRecordingIdleTimeout`. | 10–3600 seg (predeterminado 120) |

### NVIDIA BNR

| Control | Lo que hace |
|---|---|
| **Autostart Container** | Haga clic para configurar el inicio automático del contenedor |
| **Start** | Haga clic para iniciar el contenedor de eliminación de ruido NVIDIA Broadcast |
| **Stop** | Haga clic para detener el contenedor |
| **Check Status** | Haga clic para verificar el estado del contenedor |

Un punto de estado de color indica el estado del contenedor (En ejecución/Detenido/Desconocido).

## Pestaña Filtros

La pestaña **Filters** configura la nitidez del filtro por modo.

### Nitidez del filtro

Use los deslizadores para **Voice**, **CW** y **Digital** para establecer la nitidez del filtro:

| Valor | Significado |
|---|---|
| 0 | Latencia más baja |
| 1 | — |
| 2 | — |
| 3 | Más nítido |

Los deslizadores están deshabilitados cuando **Auto** está activado para ese modo.

### Modo automático

Active **Auto** para Voice, CW o Digital para habilitar la selección automática del nivel de filtro. Cuando está activado, el deslizador de nitidez manual para ese modo se deshabilita.

### Filtros de baja latencia

Marque **Use Low Latency Filters for Digital Modes** para forzar filtros de baja latencia en DIGU/DIGL.

## Pestaña XVTR

La pestaña **XVTR** configura los ajustes por transvertidor. Contiene pestañas anidadas, una por cada transvertidor configurado, más una pestaña **+** para crear nuevos transvertidores.

### Controles por transvertidor

| Control | Lo que hace |
|---|---|
| **RX Only:** | Active para forzar solo RX en ese transvertidor |
| **Remove** | Haga clic para eliminar la definición del transvertidor |

### Crear un nuevo transvertidor

1. Haga clic en la pestaña **+** (etiquetada **Create New Transverter**).
2. Configure los parámetros del transvertidor.

### Política XVTR

La sección **XVTR Policy** permite configurar cómo se manejan los transvertidores con respecto a los bordes de banda y límites de frecuencia. Esto se gestiona a través del modelo `XvtrPolicy`.

| Control | Lo que hace |
|---|---|
| Selección de política | Elija cómo se aplican los bordes de banda y los límites de frecuencia del transvertidor |

## Pestaña Cables USB

La pestaña **USB Cables** asigna adaptadores serie USB a los tipos de cable CAT, BCD, bit y PTT.

### Detección de cables

La **Cables list / Status** muestra los cables USB detectados por tipo con el estado Conectado/Desconectado.

### Configuración por cable

Cada cable detectado proporciona los siguientes parámetros:

| Control | Lo que hace |
|---|---|
| **Name:** | Identificador del cable |
| **Enabled** | Active para habilitar el cable |
| **Speed** | Selección de velocidad en baudios |
| **Data Bits** | Selección de bits de datos |
| **Parity** | Selección de paridad |
| **Stop Bits** | Selección de bits de parada |
| **Flow** | Selección de control de flujo |
| **Source** | Selección de la fuente de señal |
| **Auto Report** | Active el informe automático |
| **BCD Type** | Selección del tipo de salida BCD |
| **Polarity** | Selección de la polaridad de la señal |
| **Bit Configuration (0-7)** | Configuración de bits por pin |

## Pestaña Periféricos

La pestaña **Peripherals** gestiona dispositivos externos a través de una conexión TCP directa (TGXL, PGXL, Antenna Genius).

### TGXL

Haga clic en **Connect** para abrir una conexión TCP directa al TGXL en el puerto 9010. La IP y el puerto se guardan en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, por lo que AetherSDR se reconecta automáticamente al inicio.

Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está defectuosa en el firmware 4.2. El TGXL maneja el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita keying del lado del cliente.

Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente.

### PGXL

Haga clic en **Connect** para abrir una conexión TCP directa al Power Genius XL (puerto predeterminado 900
