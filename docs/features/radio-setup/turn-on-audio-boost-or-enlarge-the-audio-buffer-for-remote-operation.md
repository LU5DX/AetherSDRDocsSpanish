# Diálogo de Configuración de Radio de AetherSDR

El diálogo **Configuración de Radio** es la ventana de configuración maestra para los ajustes específicos de cada radio. Contiene pestañas para información de la radio, red, GPS, transmisión, teléfono/CW, recepción, antenas, audio, filtros, transverters, cables USB, periféricos, APD, Temas, SmartLink, KiwiSDR y, opcionalmente, puertos serie.

## Abrir el diálogo de Configuración de Radio

1. Haga clic en `Settings > Radio Setup...`.

## Disposición del diálogo

El diálogo **Configuración de Radio** es un diálogo persistente que recuerda su tamaño y posición entre sesiones. La geometría se guarda en `RadioSetupDialogGeometry` en la configuración de la aplicación.

Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Temas, Audio, Filtros, Periféricos, KiwiSDR) están envueltas en un área de desplazamiento vertical. La barra de desplazamiento aparece solo cuando el contenido se desborda; en pantallas anchas no hay ningún cambio visual.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio y los controles de gestión del firmware.

### Información de la radio (solo lectura)

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región reguladora (ej. USA) |
| **HW Version** | Cadena de versión del hardware |
| **Model** | Modelo de radio (ej. FLEX-8600) |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado de habilitación de multiFLEX |
| **License Info** | Estado de suscripción, fecha de vencimiento, ID de radio y versión licenciada |

Cada campo de solo lectura tiene un botón de copia a su derecha que copia el valor mostrado al portapapeles. Cuando el valor está vacío o no está disponible, el botón de copia se atenúa.

### Campos configurables por el usuario

| Control | Qué hace |
|---|---|
| **Nickname** | Ingrese un nombre descriptivo para la radio |
| **Callsign** | Ingrese el indicativo de la estación |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si está vacío. Se almacena en `StationName`. |

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de activación remota / encendido remoto de la radio.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación antes del reinicio.

- En una conexión LAN: AetherSDR se desconecta y se reconecta automáticamente una vez que la radio termina de iniciarse.
- En una conexión SmartLink/WAN: AetherSDR se desconecta. Debe reconectarse manualmente después de que la radio termine de iniciarse.

El botón está deshabilitado cuando la radio está desconectada o reconectándose.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar a la radio las versiones de firmware disponibles.
2. Si hay una actualización disponible, la etiqueta de estado muestra la versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
3. Descargue el instalador de SmartSDR (.msi para v4.2+, .exe para versiones anteriores).
4. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo .ssdr previamente extraído en el selector de archivos.
5. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción. Cuando la preparación finalice, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Pestaña Network

La pestaña **Network** muestra información de la red de la radio y permite la configuración.

### Información de red (solo lectura)

| Control | Qué muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red actuales |

### Configuración

| Control | Qué hace | Rango válido |
|---|---|---|
| **Enforce Private IP Connections:** | Alterna para rechazar pares que no sean RFC1918 | On / Off |
| **Network MTU:** | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes. El valor predeterminado de 1450 es seguro para la mayoría de las túneles VPN/SD-WAN. Se almacena en `NetworkMtu`. | 576–9000 bytes |
| **DHCP / Static** | Cambia entre modos DHCP y IP estática | DHCP / Static |

Cuando se selecciona **Static**, ingrese la **IP Address:**, **Mask:** y **Gateway:** en los campos de texto, luego haga clic en **Apply** para enviar la configuración a la radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS e información en vivo cuando hay un módulo GPS instalado y activo.

### Información GPS (solo lectura)

| Indicador | Qué muestra |
|---|---|
| Estado GPS | Latitud, longitud, altitud, hora UTC y número de satélites cuando el GPS está activo |

## Pestaña TX

La pestaña **TX** configura los parámetros de transmisión.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Timings

Use los controles de selección numérica **Timings** para establecer los tiempos de retención y retardo de TX en milisegundos. El campo **Timeout (sec)** muestra el tiempo de espera de interlock en segundos para facilitar la lectura; la radio almacena este valor internamente en milisegundos.

### Interlocks

Active o desactive **TX REQ: RCA** y **Accessory** para habilitar las entradas de interlock.

### Power y Tune

| Control | Qué hace | Rango válido |
|---|---|---|
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | 0–100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — |

### Display

| Control | Qué hace |
|---|---|
| **Show TX in Waterfall:** | Alterna para dibujar la señal de TX en el waterfall |

### Comportamiento de seguimiento de slice

| Control | Qué hace |
|---|---|
| **TX Follows Active Slice** | TX sigue la slice activa. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante una operación en Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Cambia la slice activa cuando el TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. Se almacena en `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de nivel

Active o desactive **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel del micrófono incluso durante la recepción.

### Manipulador CW

| Control | Qué hace | Rango válido |
|---|---|---|
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio | Enabled / Disabled |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. | A / B |
| **Swap:** | Intercambia dit/dah | On / Off |
| **Sideband:** | Selecciona la banda lateral del tono CW | LSB / USB |
| **CWX:** | Habilita la activación de macros CWX | On / Off |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Se almacena en `CwDecodeOverlay`. | On / Off |

### RTTY

| Control | Qué hace |
|---|---|
| **RTTY Mark Default:** | Establece la frecuencia de marca RTTY predeterminada |

## Pestaña RX

La pestaña **RX** proporciona calibración de frecuencia y selección de la fuente de referencia.

### Calibración de frecuencia

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz para usar en la calibración |
| **Start** | Inicia el barrido de calibración de frecuencia |
| **Freq Offset (ppb):** | Muestra o establece manualmente el desplazamiento de frecuencia actual en partes por mil millones |

### Fuente de referencia de 10 MHz

| Control | Qué hace | Rango válido |
|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. | Auto / TCXO / GPSDO / External |

La etiqueta de estado de bloqueo junto al control se actualiza en vivo.

## Pestaña Antennas

La pestaña **Antennas** configura los nombres de las antenas para cada puerto de antena de la radio. Esta pestaña se construye de forma diferida al hacer clic por primera vez.

| Control | Qué hace |
|---|---|
| **ANT1:** | Ingrese un nombre personalizado para el puerto de antena 1 |
| **ANT2:** | Ingrese un nombre personalizado para el puerto de antena 2 |
| **XVTA:** | Ingrese un nombre personalizado para el puerto del transverter A |
| **XVTB:** | Ingrese un nombre personalizado para el puerto del transverter B |

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, la compresión, los dispositivos del PC, la ganancia adicional, el búfer, la grabación y NVIDIA BNR.

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

### Dispositivos de audio del PC

| Control | Qué hace |
|---|---|
| **PC Audio Devices: Input:** | Seleccione el dispositivo de entrada de audio del host |
| **PC Audio Devices: Output:** | Seleccione el dispositivo de salida de audio del host |

### Audio Boost

Active **Audio Boost:** para habilitar ganancia adicional en la ruta de audio del cliente. Se almacena en `AudioBoost`.

### Audio Buffer

Ingrese un valor en **Audio Buffer:** para establecer el búfer de audio del lado del cliente en milisegundos. Aumente este valor cuando use conexiones VPN o SmartLink con latencia inestable. Se almacena en `AudioBufferMs`.

| Rango válido | Valor predeterminado |
|---|---|
| 50–1000 ms | 200 ms |

### Recording

| Control | Qué hace | Rango válido |
|---|---|---|
| **Recording: Radio Side / Client Side** | Elige la grabación del lado de la radio o del lado del cliente. Se almacena en `RecordingMode`. | Radio Side / Client Side |
| **Save to:** | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto es Documents/AetherSDR/Recordings. Se almacena en `QsoRecordingDir`. | — |
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

Un punto de estado de color indica el estado del contenedor (En ejecución/Detenido/Desconocido).

## Pestaña Filters

La pestaña **Filters** configura la nitidez del filtro por modo.

### Nitidez del filtro

Use los deslizadores para **Voice**, **CW** y **Digital** para establecer la nitidez del filtro:

| Valor | Significado |
|---|---|
| 0 | Latencia más baja |
| 1 | — |
| 2 | — |
| 3 | Más nítido |

Los deslizadores están deshabilitados cuando **Auto** está habilitado para ese modo.

### Modo automático

Active o desactive **Auto** para Voice, CW o Digital para habilitar la selección automática del nivel del filtro. Cuando está habilitado, el deslizador de nitidez manual para ese modo se deshabilita.

### Low Latency Filters

Marque **Use Low Latency Filters for Digital Modes** para forzar el uso de filtros de baja latencia en DIGU/DIGL.

## Pestaña XVTR

La pestaña **XVTR** configura los ajustes por transverter. Contiene pestañas anidadas, una por transverter configurado, más una pestaña **+** para crear nuevos transverters.

### Controles por transverter

| Control | Qué hace |
|---|---|
| **RX Only:** | Alterna para forzar solo recepción en ese transverter |
| **Remove** | Haga clic para eliminar la definición del transverter |
| **Create New Transverter** | Haga clic en la pestaña **+** para añadir una nueva entrada de transverter |

### Crear un nuevo transverter

1. Haga clic en la pestaña **+** (etiquetada **Create New Transverter**).
2. Configure los parámetros del transverter.

### XVTR Policy

La sección **XVTR Policy** permite configurar cómo se manejan los transverters con respecto a los bordes de banda y los límites de frecuencia. Esto se gestiona a través del modelo `XvtrPolicy`.

| Control | Qué hace |
|---|---|
| Selección de política | Elija cómo se aplican los bordes de banda y los límites de frecuencia del transverter |

## Pestaña USB Cables

La pestaña **USB Cables** asigna adaptadores serie USB a los tipos de cable CAT, BCD, de bit y PTT.

### Detección de cables

La **Cables list / Status** muestra los cables USB detectados por tipo con el estado Conectado/Desconectado.

### Configuración por cable

Cada cable detectado proporciona los siguientes parámetros:

| Control | Qué hace |
|---|---|
| **Name:** | Identificador del cable |
| **Enabled** | Alterna la habilitación del cable |
| **Speed** | Selección de velocidad en baudios |
| **Data Bits** | Selección de bits de datos |
| **Parity** | Selección de paridad |
| **Stop Bits** | Selección de bits de parada |
| **Flow** | Selección de control de flujo |
| **Source** | Selección de fuente de señal |
| **Auto Report** | Alterna el informe automático |
| **BCD Type** | Selección de tipo de salida BCD |
| **Polarity** | Selección de polaridad de la señal |
| **Bit Configuration (0-7)** | Configuración de bits por pin |

## Pestaña Peripherals

La pestaña **Peripherals** gestiona dispositivos externos a través de una conexión TCP directa (TGXL, PGXL, Antenna Genius).

### TG
