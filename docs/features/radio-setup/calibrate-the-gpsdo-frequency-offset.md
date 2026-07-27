# Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, Phone/CW, RX, Antenas, Audio, Filtros, XVTR, cables USB, periféricos, APD, Temas, SmartLink y Serial (FlexControl).

## Abrir Configuración de Radio

1. Haga clic en **Settings** en el menú principal.
2. Seleccione **Radio Setup...**.

El diálogo recuerda su posición y tamaño entre sesiones.

## Radio (pestaña)

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware. Cada valor de solo lectura tiene un botón de copia que aparece con un icono de documento al pasar el ratón o enfocar; haga clic en él para copiar el valor al portapapeles. Un breve mensaje emergente "¡Copiado!" confirma la acción.

### Información de la radio

Los siguientes campos son indicadores de solo lectura de la radio conectada:

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. |
| **Region** | Región regulatoria de la radio (ej., USA). |
| **HW Version** | Cadena de versión de hardware. Incluye un botón de copia al portapapeles junto al valor. |
| **Options** | Opciones de radio licenciadas. Incluye un botón de copia al portapapeles junto al valor. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo de la radio. Incluye un botón de copia al portapapeles junto al valor. |
| **License Info** | Detalles de suscripción, fecha de vencimiento, ID de radio y versión licenciada. Cada campo incluye un botón de copia al portapapeles junto al valor. |

### Campos de identificación de la radio

| Control | Descripción |
|---|---|
| **Nickname** | Apodo amigable de la radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Por defecto es el nombre de host del SO si está vacío. Clave de configuración: `StationName`. |

### Control remoto y reinicio

| Control | Descripción |
|---|---|
| **Remote On** | Habilita el despertado remoto/encendido remoto. |
| **Reboot Radio** | Reinicia la radio conectada. Haga clic para ver un diálogo de confirmación. En conexiones LAN, AetherSDR se reconecta automáticamente después de que la radio termine de iniciar. En conexiones SmartLink/WAN, debe reconectarse manualmente. El botón está deshabilitado cuando la radio está desconectada. |

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Select Installer...** | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae la carga útil .ssdr y emite el progreso. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |

1. Haga clic en **Check for Update** para consultar actualizaciones de firmware. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que debe descargar el instalador.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y seleccione el archivo descargado. AetherSDR acepta archivos `.msi`, `.exe` o un archivo `.ssdr` preextraído y prepara el firmware automáticamente.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio. Una barra de progreso y texto de estado muestran el progreso de la carga.

## SmartLink (pestaña)

La pestaña SmartLink gestiona los certificados TLS de SmartLink anclados. Enumera cada certificado anclado (host, huella SHA-256, fecha de anclado) con botones por fila para Olvidar y Olvidar todo. La pestaña se construye de forma diferida al hacer clic por primera vez. Si ocurre una discrepancia de anclaje de certificado, el handshake se pausa con un diálogo modal.

| Control | Descripción |
|---|---|
| **Pinned SmartLink Certificates (sección)** | Encabezado de sección para la tabla de certificados anclados. Enumera cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso). |
| **Host / SHA-256 fingerprint / Pinned (columnas de tabla)** | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)'). |
| **Forget selected** | Elimina la huella del certificado anclado del host seleccionado para que la siguiente conexión lo vuelva a anclar de forma silenciosa. |
| **Forget all** | Limpia todos los certificados anclados (con confirmación). La siguiente conexión a cada radio lo vuelve a anclar de forma silenciosa. Muestra un diálogo de confirmación antes de borrar. |

## Network (pestaña)

La pestaña Network muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |

### Configuración de red

| Control | Descripción |
|---|---|
| **Enforce Private IP Connections** | Alternar para rechazar pares que no sean RFC1918. |
| **Network MTU** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango válido: 576-9000 bytes. Predeterminado: 1450. Clave de configuración: `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. |

### Configuración IP

1. Cambie entre **DHCP** y **Static** usando el botón de alternancia.
2. En modo Static, ingrese la **IP Address**, **Mask** y **Gateway**.
3. Haga clic en **Apply** para enviar la configuración de red a la radio.

## GPS (pestaña)

La pestaña GPS muestra la presencia de GPS e información en vivo, incluyendo latitud, longitud, altitud, hora y conteo de satélites.

## TX (pestaña)

La pestaña TX proporciona configuración de transmisión, incluyendo temporizaciones, enclavamientos, límites de potencia, modo de sintonía y opciones de visualización del waterfall.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

| Control | Descripción |
|---|---|
| **Timings (in ms)** | Temporizaciones de retención/retardo de TX. |

### Enclavamientos

| Control | Descripción |
|---|---|
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y accessory. |

### Potencia y sintonía

| Control | Descripción |
|---|---|
| **Max Power** | Establece el límite de potencia de TX a nivel de radio. Rango válido: 0-100%. |
| **Tune Mode** | Selecciona cómo se comporta el botón de sintonía. |

### Waterfall y seguimiento de slice

| Control | Descripción |
|---|---|
| **Show TX in Waterfall** | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. Clave de configuración: `TxFollowsActiveSlice`. Predeterminado: False. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Clave de configuración: `ActiveFollowsTxSlice`. Predeterminado: False. |

## Phone/CW (pestaña)

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Micrófono

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Descripción |
|---|---|
| **Iambic** | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Swap** | Intercambia dit/dah. |
| **Sideband** | Selecciona la banda lateral del tono CW. Rango válido: LSB, USB. |
| **CWX** | Habilita el keying de macros CWX. |
| **Decode** | Habilita la superposición de decodificación CW en el panadapter. Clave de configuración: `CwDecodeOverlay`. Predeterminado: True. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default** | Frecuencia de marca RTTY predeterminada. |

## RX (pestaña)

La pestaña RX proporciona calibración de offset de frecuencia del GPSDO y selección de fuente de referencia de 10 MHz.

### Calibración de frecuencia

1. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia conocida y precisa.
2. Haga clic en **Start** para comenzar el barrido de calibración. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido.
3. Cuando el barrido termine, revise el offset medido en **Freq Offset (ppb):**.
4. Si prefiere establecer el offset manualmente, edite **Freq Offset (ppb):** directamente.

### Mensajes de estado de calibración

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Azul-gris | La secuencia de comandos de calibración se ha enviado a la radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. |
| Busy | — | Se muestra en el propio botón **Start** mientras un barrido está en progreso. |

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

Codificación de color:
- Verde (`#00c040`): Oscilador bloqueado.
- Rojo (`#c04040`): Oscilador desbloqueado.
- Azul-gris (`#8aa8c0`): Estado del oscilador aún no recibido.

### Banner de estado GPSDO

- **Banner verde**: GPSDO instalado. La calibración manual de offset de frecuencia está disponible.
- **Banner ámbar**: No hay GPSDO instalado. La calibración manual de offset de frecuencia está disponible.

## Antennas (pestaña)

La pestaña Antennas le permite asignar nombres personalizados a cada puerto de antena en la radio.

### Pasos

1. Seleccione un puerto de antena de la lista.
2. Ingrese un nombre personalizado en el campo de texto.
3. El nombre se envía a la radio y aparece en los controles de selección de antena en todo AetherSDR.

## Audio (pestaña)

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

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
| **Audio Compression (SmartLink)** | Selecciona el códec de audio para SmartLink/LAN. Opciones: Auto, Uncompressed, Opus. Clave de configuración: `AudioCompression`. Predeterminado: Auto. |

### Gestión de energía

| Control | Descripción |
|---|---|
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Clave de configuración: `InhibitSleepWhileConnected`. Predeterminado: False. |

### Dispositivos de audio del PC

| Control | Descripción |
|---|---|
| **PC Audio Devices: Input / Output** | Selecciona los dispositivos de audio de entrada y salida del host. |

### Refuerzo y búfer de audio

| Control | Descripción |
|---|---|
| **Audio Boost** | Habilita ganancia adicional en la ruta de audio del cliente. Clave de configuración: `AudioBoost`. |
| **Audio Buffer** | Aumenta el búfer de audio en milisegundos para jitter en VPN/SmartLink. Rango válido: 50-1000 ms. Predeterminado: 200. Clave de configuración: `AudioBufferMs`. |

### Grabación

| Control | Descripción |
|---|---|
| **Recording** | Selecciona grabación del lado de la radio o del lado del cliente. Clave de configuración: `RecordingMode`. Predeterminado: Radio Side. |
| **Save to** | Carpeta para grabaciones guardadas (solo lado del cliente). Clave de configuración: `QsoRecordingDir`. Por defecto en Documents/AetherSDR/Recordings. |
| **...** | Navega para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | Graba automáticamente mientras transmite. Clave de configuración: `QsoRecordingAutoRecord`. Predeterminado: False. |
| **Idle timeout** | Segundos de silencio antes de detener la grabación. Rango válido: 10-3600 seg. Predeterminado: 120. Clave de configuración: `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

| Control | Descripción |
|---|---|
| **Autostart Container** | Habilita el inicio automático del contenedor de eliminación de ruido NVIDIA Broadcast. |
| **Start** | Inicia el contenedor NVIDIA BNR. |
| **Stop** | Detiene el contenedor NVIDIA BNR. |
| **Check Status** | Verifica el estado de ejecución del contenedor. |

Un punto de estado de color indica el estado del contenedor: verde para Running, rojo para Stopped, gris para Unknown.

## Filters (pestaña)

La pestaña Filters proporciona opciones de filtro de baja latencia y nítidos por modo de ancho de banda.

### Nitidez de filtro

| Control | Descripción |
|---|---|
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro por modo (0=latencia más baja a 3=más nítido). Deshabilitado cuando Auto está habilitado. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo. Deshabilita el control deslizante de nitidez manual
