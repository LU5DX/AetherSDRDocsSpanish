# Configuración de la Radio

El cuadro de diálogo Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, Antenas, Audio, Filtros, XVTR, Cables USB, periféricos, APD, Temas y Serial (FlexControl).

## Abrir la Configuración de la Radio

1. Haga clic en **Settings** en el menú principal.
2. Seleccione **Radio Setup...**.

El cuadro de diálogo recuerda su posición y tamaño entre sesiones.

## Radio (pestaña)

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Información de la radio

Los siguientes campos son indicadores de solo lectura de la radio conectada:

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis. |
| **Region** | Región regulatoria de la radio (ej., USA). |
| **HW Version** | Cadena de versión de hardware. |
| **Options** | Opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo de la radio. |
| **License Info** | Detalles de suscripción, fecha de vencimiento, ID de radio y versión licenciada. |

### Campos de identificación de la radio

| Control | Descripción |
|---|---|
| **Nickname** | Apodo amigable de la radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre del host del sistema operativo si está vacío. Clave de configuración: `StationName`. |

### Control remoto

| Control | Descripción |
|---|---|
| **Remote On** | Habilita el encendido remoto. |

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar actualizaciones de firmware. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y seleccione el archivo descargado. AetherSDR acepta archivos `.msi`, `.exe` o un archivo `.ssdr` preextraído y prepara el firmware automáticamente.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio. Una barra de progreso y texto de estado muestran el progreso de la carga.

## Network (pestaña)

La pestaña Network muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Descripción |
|---|---|
| **Enforce Private IP Connections** | Activa/desactiva el rechazo de pares que no sean RFC1918. |
| **Network MTU** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango válido: 576-9000 bytes. Valor predeterminado: 1450. Clave de configuración: `NetworkMtu`. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |

### Configuración IP

1. Cambie entre **DHCP** y **Static** usando el botón de alternancia.
2. En modo Static, ingrese la **IP Address**, **Mask** y **Gateway**.
3. Haga clic en **Apply** para enviar la configuración de red a la radio.

## GPS (pestaña)

La pestaña GPS muestra la presencia de GPS e información en vivo que incluye latitud, longitud, altitud, hora y cantidad de satélites.

## TX (pestaña)

La pestaña TX proporciona configuración de transmisión que incluye temporizaciones, enclavamientos, límites de potencia, modo de sintonía y opciones de visualización del waterfall.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el cuadro de diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

| Control | Descripción |
|---|---|
| **ACC TX** | Retardo de ACC TX en milisegundos. |
| **TX Delay** | Retardo de TX en milisegundos. |
| **RCA TX1** | Retardo de RCA TX1 en milisegundos. |
| **Timeout (sec)** | Tiempo de espera de enclavamiento en segundos (se muestra en segundos, se almacena en milisegundos en la radio). |
| **TX2** | Retardo de TX2 en milisegundos. |

### Enclavamientos

| Control | Descripción |
|---|---|
| **TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y del accesorio. |

### Potencia y sintonía

| Control | Descripción |
|---|---|
| **Max Power** | Establece el límite máximo de potencia de transmisión a nivel de radio. Rango válido: 0-100%. |
| **Tune Mode** | Selecciona cómo se comporta el botón de sintonía. |

### Seguimiento del waterfall y del slice

| Control | Descripción |
|---|---|
| **Show TX in Waterfall** | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | TX sigue al slice activo. Es mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante una operación en Split. Clave de configuración: `TxFollowsActiveSlice`. Valor predeterminado: False. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. Clave de configuración: `ActiveFollowsTxSlice`. Valor predeterminado: False. |

## Phone/CW (pestaña)

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Micrófono

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Descripción |
|---|---|
| **Iambic** | Activa o desactiva el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. Valor predeterminado: A. |
| **Swap** | Intercambia dit/dah. |
| **Sideband** | Selecciona la banda lateral del tono CW. Rango válido: LSB, USB. |
| **CWX** | Habilita el keying de macros CWX. |
| **Decode** | Activa la superposición de decodificación CW en el panadapter. Clave de configuración: `CwDecodeOverlay`. Valor predeterminado: True. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default** | Frecuencia de marca RTTY predeterminada. |

## RX (pestaña)

La pestaña RX proporciona la calibración de compensación de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

1. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia conocida y precisa.
2. Haga clic en **Start** para iniciar el barrido de calibración. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido.
3. Cuando el barrido se complete, revise la compensación medida en **Freq Offset (ppb):**.
4. Si prefiere establecer la compensación manualmente, edite **Freq Offset (ppb):** directamente.

### Mensajes de estado de calibración

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Azul grisáceo | La secuencia de comandos de calibración se ha enviado a la radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. |
| Busy | — | Se muestra en el propio botón **Start** mientras un barrido está en curso. |

### Fuente de referencia de 10 MHz

| Control | Descripción |
|---|---|
| **10 MHz Reference Source** | Selecciona la fuente de referencia del oscilador. Valores válidos: Auto, TCXO, GPSDO, External 10 MHz. Las opciones mostradas dependen del hardware instalado. |

La etiqueta de estado de bloqueo junto al cuadro combinado muestra el estado actual del oscilador:

| Visualización | Significado |
|---|---|
| `Auto -> GPSDO` (locked) | Auto seleccionado, la radio eligió GPSDO, bloqueado |
| `GPSDO` (locked) | Fuente coincidente y bloqueada |
| `External 10 MHz` (not detected) | Externa seleccionada pero no se detecta señal |

Codificación de colores:
- Verde (`#00c040`): El oscilador está bloqueado.
- Rojo (`#c04040`): El oscilador está desbloqueado.
- Azul grisáceo (`#8aa8c0`): Estado del oscilador aún no recibido.

### Banner de estado del GPSDO

- **Banner verde**: GPSDO instalado. La calibración manual de compensación de frecuencia está disponible.
- **Banner ámbar**: No hay GPSDO instalado. La calibración manual de compensación de frecuencia está disponible.

## Antennas (pestaña)

La pestaña Antennas permite asignar nombres personalizados a cada puerto de antena en la radio.

### Pasos

1. Seleccione un puerto de antena de la lista.
2. Ingrese un nombre personalizado en el campo de texto.
3. El nombre se envía a la radio y aparece en los controles de selección de antena en todo AetherSDR.

## Audio (pestaña)

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Descripción |
|---|---|
| **Line Out** | Control deslizante de ganancia de salida de línea. |
| **Mute (Line Out)** | Silencia la salida de línea. |
| **Headphone** | Control deslizante de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker / Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Descripción |
|---|---|
| **Audio Compression (SmartLink)** | Selecciona el códec de audio para SmartLink/LAN. Opciones: Auto, Uncompressed, Opus. Clave de configuración: `AudioCompression`. Valor predeterminado: Auto. |

### Gestión de energía

| Control | Descripción |
|---|---|
| **Prevent system sleep while connected** | Mantiene el sistema operativo despierto mientras la radio está conectada. Clave de configuración: `InhibitSleepWhileConnected`. Valor predeterminado: False. |

### Dispositivos de audio de PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input / Output** | Selecciona los dispositivos de entrada y salida de audio del host. |

### Realce y búfer de audio

| Control | Descripción |
|---|---|
| **Audio Boost** | Habilita ganancia adicional en la ruta de audio del cliente. Clave de configuración: `AudioBoost`. |
| **Audio Buffer** | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Rango válido: 50-1000 ms. Valor predeterminado: 200. Clave de configuración: `AudioBufferMs`. |

### Grabación

| Control | Descripción |
|---|---|
| **Recording** | Selecciona la grabación del lado de la radio o del lado del cliente. Clave de configuración: `RecordingMode`. Valor predeterminado: Radio Side. |
| **Save to** | Carpeta para grabaciones guardadas (solo del lado del cliente). Clave de configuración: `QsoRecordingDir`. Valor predeterminado: Documentos/AetherSDR/Recordings. |
| **...** | Busca la carpeta de grabación. |
| **Auto-record on TX** | Graba automáticamente mientras transmite. Clave de configuración: `QsoRecordingAutoRecord`. Valor predeterminado: False. |
| **Idle timeout** | Segundos de silencio antes de que se detenga la grabación. Rango válido: 10-3600 seg. Valor predeterminado: 120. Clave de configuración: `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **Autostart Container** | Habilita el inicio automático del contenedor de eliminación de ruido NVIDIA Broadcast. |
| **Start** | Inicia el contenedor NVIDIA BNR. |
| **Stop** | Detiene el contenedor NVIDIA BNR. |
| **Check Status** | Verifica el estado de ejecución del contenedor. |

Un punto de estado de color indica el estado del contenedor: verde para En ejecución, rojo para Detenido, gris para Desconocido.

## Filters (pestaña)

La pestaña Filters proporciona opciones de filtro de baja latencia y nítidos por modo de ancho de banda.

### Nitidez del filtro

| Control | Descripción |
|---|---|
| **Voice filter sharpness slider** | Establece la nitidez del filtro para modos de voz (0=menor latencia a 3=más nítido). |
| **CW filter sharpness slider** | Establece la nitidez del filtro para modo CW. |
| **Digital filter sharpness slider** | Establece la nitidez del filtro para modos digitales. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo. Desactiva el control deslizante de nitidez manual. |

### Filtros de modo digital

| Control | Descripción |
|---|---|
| **Use Low Latency Filters for Digital Modes** | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## XVTR (pestaña)

La pestaña XVTR proporciona configuración por transvertidor.

### Gestión de transvertidores

| Control | Descripción |
|---|---|
| **RX Only** | Fuerza solo RX en ese transvertidor. |
| **Remove** | Elimina la definición del transvertidor. |
| **Create New Transverter** | Agrega una nueva entrada de transvertidor. |

La pestaña contiene pestañas anidadas, una por transvertidor configurado, más una pestaña '+' para crear nuevos.

## USB Cables (pestaña)

La pestaña USB Cables asigna adaptadores seriales USB a tipos de cable CAT, BCD, bit y PTT.

### Configuración de cable

| Control | Descripción |
|---|---|
| **Cables list / Status** | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| **Name** | Nombre del cable. |
| **Enabled** | Habilita el cable. |
| **Speed** | Velocidad en baudios. |
| **Data Bits** | Configuración de bits de datos. |
| **Parity** | Configuración de paridad. |
| **Stop Bits** | Configuración de bits de parada. |
| **Flow** | Control de flujo. |
| **Source** | Fuente del cable. |
| **Auto Report** | Habilita el reporte automático. |
| **BCD Type** | Tipo BCD para cables BCD. |
| **Polarity** | Polaridad de la señal. |
| **Bit Configuration (0-7)** | Configuración de bits para cables de bits. |

## Peripherals (pestaña)

La pestaña Peripherals proporciona gestión de conexión IP manual para dispositivos externos (TGXL, PGXL, Antenna Genius, ShackSwitch).

### TGXL

| Control | Descripción |
|---|---|
| **Connect / Disconnect (TGXL)** | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar. Necesario para recuperar TUNE en firmware 4.2+. |

### PGXL

| Control | Descripción |
|---|---|
|
