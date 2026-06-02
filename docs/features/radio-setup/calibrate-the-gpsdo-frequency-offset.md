# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Fono/CW, RX, Antenas, Audio, Filtros, XVTR, Cables USB, periféricos, APD, Temas, SmartLink y Serial (FlexControl).

## Abrir Configuración de la Radio

1. Haga clic en **Settings** en el menú principal.
2. Seleccione **Radio Setup...**.

El diálogo recuerda su posición y tamaño entre sesiones.

## Radio (pestaña)

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware. Cada valor de solo lectura tiene un botón de copiar que aparece con un icono de documento al pasar el mouse o al enfocarse; haga clic en él para copiar el valor al portapapeles. Un breve mensaje emergente "Copied!" confirma la acción.

### Información de la radio

Los siguientes campos son indicadores de solo lectura de la radio conectada:

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Region** | Región regulatoria de la radio (ej., USA). |
| **HW Version** | Cadena de versión del hardware. |
| **Options** | Opciones de radio licenciadas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo de la radio. |
| **License Info** | Detalles de la suscripción, fecha de vencimiento, ID de la radio y versión licenciada. |

### Campos de identificación de la radio

| Control | Descripción |
|---|---|
| **Nickname** | Apodo amigable de la radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se establece por defecto al nombre del host del SO si está vacío. Clave de ajuste: `StationName`. |

### Control remoto

| Control | Descripción |
|---|---|
| **Remote On** | Habilita el encendido/activación remota. |

### Actualización de firmware

1. Haga clic en **Check for Update** para buscar actualizaciones de firmware. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Browse .ssdr...** y seleccione el archivo descargado. AetherSDR acepta archivos `.msi`, `.exe` o un archivo `.ssdr` pre-extraído y prepara el firmware automáticamente.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio. Una barra de progreso y texto de estado muestran el progreso de la carga.

## Red (pestaña)

La pestaña Red muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. |

### Ajustes de red

| Control | Descripción |
|---|---|
| **Enforce Private IP Connections** | Alternar para rechazar pares no RFC1918. |
| **Network MTU** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango válido: 576-9000 bytes. Predeterminado: 1450. Clave de ajuste: `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |

### Configuración IP

1. Cambie entre **DHCP** y **Static** usando el botón de alternancia.
2. En modo Static, ingrese la **IP Address**, **Mask** y **Gateway**.
3. Haga clic en **Apply** para enviar la configuración de red a la radio.

## GPS (pestaña)

La pestaña GPS muestra la presencia del GPS e información en vivo incluyendo latitud, longitud, altitud, hora y número de satélites.

## TX (pestaña)

La pestaña TX proporciona configuración de transmisión incluyendo temporizaciones, enclavamientos, límites de potencia, modo de sintonía y opciones de visualización del waterfall.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

| Control | Descripción |
|---|---|
| **Timings (in ms)** | Temporizaciones de retención/demora de TX. |

### Enclavamientos

| Control | Descripción |
|---|---|
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y del accesorio. |

### Potencia y sintonía

| Control | Descripción |
|---|---|
| **Max Power** | Establece el límite máximo de potencia de TX a nivel de radio. Rango válido: 0-100%. |
| **Tune Mode** | Selecciona cómo se comporta el botón de sintonía. |

### Waterfall y seguimiento de slice

| Control | Descripción |
|---|---|
| **Show TX in Waterfall** | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. Clave de ajuste: `TxFollowsActiveSlice`. Predeterminado: False. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Clave de ajuste: `ActiveFollowsTxSlice`. Predeterminado: False. |

## Fono/CW (pestaña)

La pestaña Fono/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Micrófono

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel del micrófono incluso en RX. |

### Manipulador CW

| Control | Descripción |
|---|---|
| **Iambic** | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Swap** | Intercambia dit/dah. |
| **Sideband** | Selecciona la banda lateral del tono CW. Rango válido: LSB, USB. |
| **CWX** | Habilita el keying por macros CWX. |
| **Decode** | Habilita la superposición de decodificación CW en el panadapter. Clave de ajuste: `CwDecodeOverlay`. Predeterminado: True. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default** | Frecuencia de marca RTTY predeterminada. |

## RX (pestaña)

La pestaña RX proporciona calibración de desviación de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

1. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia conocida y precisa.
2. Haga clic en **Start** para iniciar el barrido de calibración. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido.
3. Cuando el barrido se complete, revise la desviación medida en **Freq Offset (ppb):**.
4. Si prefiere establecer la desviación manualmente, edite **Freq Offset (ppb):** directamente.

### Mensajes de estado de calibración

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Azul-gris | La secuencia de comandos de calibración se ha enviado a la radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. |
| Busy | — | Se muestra en el botón **Start** mientras un barrido está en progreso. |

### Fuente de referencia de 10 MHz

| Control | Descripción |
|---|---|
| **10 MHz Reference Source** | Selecciona la fuente de referencia del oscilador. Valores válidos: Auto, TCXO, GPSDO, External 10 MHz. Las opciones mostradas dependen del hardware instalado. |

La etiqueta de estado de bloqueo junto al cuadro combinado muestra el estado actual del oscilador:

| Visualización | Significado |
|---|---|
| `Auto -> GPSDO` (locked) | Auto seleccionado, la radio eligió GPSDO, bloqueado |
| `GPSDO` (locked) | Fuente coincidente y bloqueada |
| `External 10 MHz` (not detected) | External seleccionado pero no se detecta señal |

Codificación de colores:
- Verde (`#00c040`): El oscilador está bloqueado.
- Rojo (`#c04040`): El oscilador está desbloqueado.
- Azul-gris (`#8aa8c0`): Estado del oscilador aún no recibido.

### Banner de estado del GPSDO

- **Banner verde**: GPSDO instalado. La calibración manual de desviación de frecuencia está disponible.
- **Banner ámbar**: No hay GPSDO instalado. La calibración manual de desviación de frecuencia está disponible.

## Antenas (pestaña)

La pestaña Antenas le permite asignar nombres personalizados a cada puerto de antena de la radio.

### Pasos

1. Seleccione un puerto de antena de la lista.
2. Ingrese un nombre personalizado en el campo de texto.
3. El nombre se envía a la radio y aparece en los controles de selección de antena en todo AetherSDR.

## Audio (pestaña)

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Descripción |
|---|---|
| **Line Out** | Deslizador de ganancia de salida de línea. |
| **Mute (Line Out)** | Silencia la salida de línea. |
| **Headphone** | Deslizador de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker / Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Descripción |
|---|---|
| **Audio Compression (SmartLink)** | Selecciona el códec de audio para SmartLink/LAN. Opciones: Auto, Uncompressed, Opus. Clave de ajuste: `AudioCompression`. Predeterminado: Auto. |

### Gestión de energía

| Control | Descripción |
|---|---|
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada. Clave de ajuste: `InhibitSleepWhileConnected`. Predeterminado: False. |

### Dispositivos de audio del PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input / Output** | Selecciona los dispositivos de entrada y salida de audio del host. |

### Refuerzo y búfer de audio

| Control | Descripción |
|---|---|
| **Audio Boost** | Habilita ganancia adicional en la ruta de audio del cliente. Clave de ajuste: `AudioBoost`. |
| **Audio Buffer** | Aumenta el búfer de audio en milisegundos para jitter en VPN/SmartLink. Rango válido: 50-1000 ms. Predeterminado: 200. Clave de ajuste: `AudioBufferMs`. |

### Grabación

| Control | Descripción |
|---|---|
| **Recording** | Selecciona la grabación del lado de la radio o del lado del cliente. Clave de ajuste: `RecordingMode`. Predeterminado: Radio Side. |
| **Save to** | Carpeta para las grabaciones guardadas (solo lado del cliente). Clave de ajuste: `QsoRecordingDir`. Se establece por defecto en Documents/AetherSDR/Recordings. |
| **...** | Busca la carpeta de grabación. |
| **Auto-record on TX** | Graba automáticamente mientras transmite. Clave de ajuste: `QsoRecordingAutoRecord`. Predeterminado: False. |
| **Idle timeout** | Segundos de silencio antes de que la grabación se detenga. Rango válido: 10-3600 seg. Predeterminado: 120. Clave de ajuste: `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **Autostart Container** | Habilita el inicio automático del contenedor de eliminación de ruido NVIDIA Broadcast. |
| **Start** | Inicia el contenedor NVIDIA BNR. |
| **Stop** | Detiene el contenedor NVIDIA BNR. |
| **Check Status** | Verifica el estado de ejecución del contenedor. |

Un punto de estado de color indica el estado del contenedor: verde para Running, rojo para Stopped, gris para Unknown.

## Filtros (pestaña)

La pestaña Filtros proporciona opciones de filtro de baja latencia y nítidos por modo de ancho de banda.

### Nitidez del filtro

| Control | Descripción |
|---|---|
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro por modo (0=menor latencia a 3=más nítido). Deshabilitado cuando Auto está habilitado. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo. Deshabilita el deslizador de nitidez manual. |

### Filtros de modo digital

| Control | Descripción |
|---|---|
| **Use Low Latency Filters for Digital Modes** | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## XVTR (pestaña)

La pestaña XVTR proporciona configuración por transverter. Contiene pestañas anidadas, una por cada transverter configurado, más una pestaña '+' para crear nuevos.

### Gestión de transverters

| Control | Descripción |
|---|---|
| **RX Only** | Fuerza solo RX en ese transverter. |
| **Remove** | Elimina la definición del transverter. |
| **Create New Transverter** | Añade una nueva entrada de transverter. |

## Cables USB (pestaña)

La pestaña Cables USB asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

### Configuración de cable

| Control | Descripción |
|---|---|
| **Cables list / Status** | Cables USB detectados por tipo con estado Plugged/Unplugged. |
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

## Periféricos (pestaña)

La pestaña Periféricos proporciona gestión de conexión IP manual para dispositivos externos (TGXL, PGXL, Antenna Genius).

### TGXL

| Control | Descripción |
|---|---|
| **Connect / Disconnect (TGXL)** | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar. Requerido para recuperar TUNE en firmware 4.2+. |

### PGXL

| Control | Descripción |
|---|---|
| **Connect / Disconnect (PGXL)** | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |

### Antenna Genius
