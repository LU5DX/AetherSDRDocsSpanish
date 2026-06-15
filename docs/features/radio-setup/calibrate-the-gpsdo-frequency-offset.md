# Configuración de la Radio

El cuadro de diálogo Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, Antenas, Audio, Filtros, XVTR, Cables USB, periféricos, APD, Temas, SmartLink y Serie (FlexControl).

## Abrir Configuración de la Radio

1. Haga clic en **Settings** en el menú principal.
2. Seleccione **Radio Setup...**.

El cuadro de diálogo recuerda su posición y tamaño entre sesiones.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware. Cada valor de solo lectura tiene un botón de copia que aparece con un icono de documento al pasar el cursor o al enfocarlo; haga clic en él para copiar el valor al portapapeles. Un breve mensaje emergente "¡Copiado!" confirma la acción.

### Información de la radio

Los siguientes campos son indicadores de solo lectura de la radio conectada:

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. |
| **Region** | Región normativa de la radio (ej., USA). |
| **HW Version** | Cadena de versión de hardware. Incluye un botón de copia al portapapeles junto al valor. |
| **Options** | Opciones de radio licenciadas. Incluye un botón de copia al portapapeles junto al valor. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo de la radio. Incluye un botón de copia al portapapeles junto al valor. |
| **License Info** | Detalles de la suscripción, fecha de vencimiento, ID de la radio y versión licenciada. Cada campo incluye un botón de copia al portapapeles junto al valor. |

### Campos de identificación de la radio

| Control | Descripción |
|---|---|
| **Nickname** | Apodo descriptivo de la radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, se utiliza el nombre del host del SO. Clave de configuración: `StationName`. |

### Control remoto y reinicio

| Control | Descripción |
|---|---|
| **Remote On** | Habilita el encendido/activación remota. |
| **Reboot Radio** | Reinicia la radio conectada. Haga clic para ver un cuadro de diálogo de confirmación. En conexiones LAN, AetherSDR se reconecta automáticamente después de que la radio termine de iniciar. En conexiones SmartLink/WAN, debe reconectarse manualmente. El botón está deshabilitado cuando la radio está desconectada. |

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Select Installer...** | Abre un cuadro de diálogo para seleccionar un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae la carga útil .ssdr y muestra el progreso. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |

1. Haga clic en **Check for Update** para consultar actualizaciones de firmware. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y seleccione el archivo descargado. AetherSDR acepta archivos `.msi`, `.exe` o un archivo `.ssdr` preextraído y prepara el firmware automáticamente.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio. Una barra de progreso y un texto de estado muestran el progreso de la carga.

## Pestaña Network

La pestaña Network muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |

### Configuración de red

| Control | Descripción |
|---|---|
| **Enforce Private IP Connections** | Activa/desactiva el rechazo de pares que no sean RFC1918. |
| **Network MTU** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango válido: 576-9000 bytes. Predeterminado: 1450. Clave de configuración: `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |

### Configuración IP

1. Cambie entre **DHCP** y **Static** usando el botón de alternancia.
2. En modo Static, introduzca la **IP Address**, **Mask** y **Gateway**.
3. Haga clic en **Apply** para enviar la configuración de red a la radio.

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS e información en vivo, incluyendo latitud, longitud, altitud, hora y conteo de satélites.

## Pestaña TX

La pestaña TX proporciona configuración de transmisión, incluyendo tiempos, enclavamientos, límites de potencia, modo de sintonía y opciones de visualización del waterfall.

### Configuración de Banda TX

Haga clic en **TX Band Settings** para abrir el cuadro de diálogo dedicado de potencia/sintonía por banda.

### Tiempos

| Control | Descripción |
|---|---|
| **Timings (in ms)** | Tiempos de colgado/retardo de TX. |

### Enclavamientos

| Control | Descripción |
|---|---|
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y de accesorio. |

### Potencia y sintonía

| Control | Descripción |
|---|---|
| **Max Power** | Establece el límite máximo de potencia de TX a nivel de radio. Rango válido: 0-100%. |
| **Tune Mode** | Selecciona cómo se comporta el botón de sintonía. |

### Seguimiento del waterfall y del slice

| Control | Descripción |
|---|---|
| **Show TX in Waterfall** | Dibuja la señal TX en el waterfall. |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante una operación en Split. Clave de configuración: `TxFollowsActiveSlice`. Predeterminado: False. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Clave de configuración: `ActiveFollowsTxSlice`. Predeterminado: False. |

## Pestaña Phone/CW

La pestaña Phone/CW configura los valores predeterminados del micrófono, el manipulador CW y RTTY.

### Micrófono

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel del micrófono incluso en RX. |

### Manipulador CW

| Control | Descripción |
|---|---|
| **Iambic** | Activa o desactiva el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. Predeterminado: A. |
| **Swap** | Intercambia dit/dah. |
| **Sideband** | Selecciona la banda lateral del tono CW. Rango válido: LSB, USB. |
| **CWX** | Activa el tecleo por macros CWX. |
| **Decode** | Activa la superposición de decodificación CW en el panadapter. Clave de configuración: `CwDecodeOverlay`. Predeterminado: True. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default** | Frecuencia predeterminada de la marca RTTY. |

## Pestaña RX

La pestaña RX proporciona calibración de desviación de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

1. En **Cal Frequency (MHz):**, introduzca la frecuencia de una señal de referencia conocida y precisa.
2. Haga clic en **Start** para iniciar el barrido de calibración. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido.
3. Cuando el barrido finalice, revise la desviación medida en **Freq Offset (ppb):**.
4. Si prefiere establecer la desviación manualmente, edite **Freq Offset (ppb):** directamente.

### Mensajes de estado de calibración

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Azul-gris | La secuencia de comandos de calibración se ha enviado a la radio. |
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
| `External 10 MHz` (not detected) | External seleccionado pero no se detecta señal |

Codificación de colores:
- Verde (`#00c040`): El oscilador está bloqueado.
- Rojo (`#c04040`): El oscilador está desbloqueado.
- Azul-gris (`#8aa8c0`): Estado del oscilador aún no recibido.

### Banner de estado GPSDO

- **Banner verde**: El GPSDO está instalado. La calibración manual de desviación de frecuencia está disponible.
- **Banner ámbar**: No hay GPSDO instalado. La calibración manual de desviación de frecuencia está disponible.

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres personalizados a cada puerto de antena de la radio.

### Pasos

1. Seleccione un puerto de antena de la lista.
2. Introduzca un nombre personalizado en el campo de texto.
3. El nombre se envía a la radio y aparece en los controles de selección de antena en todo AetherSDR.

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos del PC, realce, búfer, grabación y el contenedor NVIDIA BNR.

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
| **Audio Compression (SmartLink)** | Selecciona el códec de audio para SmartLink/LAN. Opciones: Auto, Uncompressed, Opus. Clave de configuración: `AudioCompression`. Predeterminado: Auto. |

### Gestión de energía

| Control | Descripción |
|---|---|
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada. Clave de configuración: `InhibitSleepWhileConnected`. Predeterminado: False. |

### Dispositivos de audio del PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input / Output** | Selecciona los dispositivos de audio de entrada y salida del host. |

### Realce y búfer de audio

| Control | Descripción |
|---|---|
| **Audio Boost** | Activa ganancia extra en la ruta de audio del cliente. Clave de configuración: `AudioBoost`. |
| **Audio Buffer** | Aumenta el búfer de audio en milisegundos para fluctuaciones de VPN/SmartLink. Rango válido: 50-1000 ms. Predeterminado: 200. Clave de configuración: `AudioBufferMs`. |

### Grabación

| Control | Descripción |
|---|---|
| **Recording** | Selecciona grabación del lado de la radio o del lado del cliente. Clave de configuración: `RecordingMode`. Predeterminado: Radio Side. |
| **Save to** | Carpeta para las grabaciones guardadas (solo lado del cliente). Clave de configuración: `QsoRecordingDir`. Valor predeterminado: Documents/AetherSDR/Recordings. |
| **...** | Examina para seleccionar la carpeta de grabaciones. |
| **Auto-record on TX** | Graba automáticamente mientras transmite. Clave de configuración: `QsoRecordingAutoRecord`. Predeterminado: False. |
| **Idle timeout** | Segundos de silencio antes de que se detenga la grabación. Rango válido: 10-3600 seg. Predeterminado: 120. Clave de configuración: `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **Autostart Container** | Activa el inicio automático del contenedor de eliminación de ruido NVIDIA Broadcast. |
| **Start** | Inicia el contenedor NVIDIA BNR. |
| **Stop** | Detiene el contenedor NVIDIA BNR. |
| **Check Status** | Comprueba el estado de ejecución del contenedor. |

Un punto de estado coloreado indica el estado del contenedor: verde para En ejecución, rojo para Detenido, gris para Desconocido.

## Pestaña Filters

La pestaña Filters proporciona opciones de filtro de baja latencia y nítidos por modo de ancho de banda.

### Nitidez del filtro

| Control | Descripción |
|---|---|
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro por modo (0=menor latencia a 3=más nítido). Deshabilitado cuando Auto está activado. |
| **Auto (Voice / CW / Digital)** | Activa la selección automática del nivel de filtro para ese modo. Deshabilita el deslizador de nitidez manual. |

### Filtros de modo digital

| Control | Descripción |
|---|---|
| **Use Low Latency Filters for Digital Modes** | Fuerza el uso de filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transvertidor. Contiene pestañas anidadas, una por transvertidor configurado, más una pestaña '+' para crear nuevos.

### Gestión de transvertidores

| Control | Descripción |
|---|---|
| **RX Only** | Fuerza solo RX en ese transvertidor. |
| **Remove** | Elimina la definición del transvertidor. |
| **Create New Transverter** | Añade una nueva entrada de transvertidor. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

### Configuración de cables

| Control | Descripción |
|---|---|
| **Cables list / Status** | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| **Name** | Nombre del cable. |
| **Enabled** | Activa el cable. |
| **Speed** | Velocidad en baudios. |
| **Data Bits** | Configuración de bits de datos. |
| **Parity** | Configuración
