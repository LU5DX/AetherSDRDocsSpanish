# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana de configuración maestra para los ajustes por radio, que incluyen información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, antenas, transverters, cables USB, periféricos, APD, temas y configuración del puerto serie.

## Abrir el diálogo

- Haga clic en `Settings > Radio Setup...` mientras está conectado a una radio.

## Diseño del diálogo

El diálogo contiene una interfaz de pestañas con las siguientes pestañas:

- **Radio**: Información de la radio, identificación, información de licencia y actualización de firmware
- **Network**: Información de red y opciones de red avanzadas
- **GPS**: Presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites
- **TX**: Temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía y ajustes de seguimiento de slice/TX
- **Phone/CW**: Micrófono, manipulador CW, valores predeterminados de RTTY
- **RX**: Calibración de desvío de frecuencia GPSDO y fuente de referencia de 10 MHz
- **Antennas**: Configuración de nombres de antenas
- **Filters**: Opciones de filtro de baja latencia / nítido por ancho de banda
- **XVTR**: Configuración por transverter
- **USB Cables**: Asignación de adaptadores serie USB
- **Peripherals**: Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius)
- **APD**: Selección de puerto de muestra para Predistorsión Adaptativa Externa (solo FLEX-8x00)
- **Themes**: Ajustes de apariencia de la interfaz de usuario, incluyendo anulaciones de color por slice
- **Serial**: Configuración del puerto serie FlexControl

El diálogo recuerda su tamaño y posición entre sesiones usando `RadioSetupDialogGeometry` en AppSettings.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio e información de licencia, y proporciona controles de actualización de firmware.

### Información de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). |
| **Region** | Indicador | Región regulatoria de la radio. |
| **HW Version** | Indicador | Cadena de versión del hardware. |
| **Model** | Indicador | Modelo de la radio. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de multiFLEX habilitado. |
| **License Info** | Indicador | Muestra suscripción, vencimiento, ID de radio y versión licenciada de la radio. |

### Identificación de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo descriptivo de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del SO si está vacío. Se almacena en AppSettings. Se envía a la radio como `client station <name>`. |

### Encendido remoto

| Control | Tipo | Comportamiento |
|---|---|---|
| **Remote On** | Botón pulsador | Habilita el encendido/activación remota. |

### Actualización de firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón pulsador | Consulta actualizaciones de firmware desde la radio. |
| **Select Installer...** | Botón pulsador | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware** | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| Estado del firmware | Indicador | Vacío hasta que comienza una carga de firmware; luego muestra progreso y texto de resultado. |

#### Flujo de trabajo de actualización de firmware

Cuando **Check for Update** encuentra una versión más reciente, el área de estado le indica que descargue el instalador de SmartSDR desde flexradio.com. Use **Select Installer...** para señalar a AetherSDR el archivo que descargó.

**Formatos de instalador compatibles**

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador WiX de FlexRadio (SmartSDR v4.2 y posteriores). Recomendado. |
| `.exe` | Instalador autoextraíble antiguo (versiones pre-v4.2). |
| `.ssdr` | Archivo de firmware preextraído. |

**Pasos**

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión y le indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en **Select Installer...** y ubique el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR prepara el firmware e informa el progreso en el área de estado.
6. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Pestaña Network

La pestaña Network muestra información de red de la radio y proporciona configuración de red avanzada.

### Información de red

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enforce Private IP Connections** | Botón de alternancia | Rechaza pares que no sean RFC1918. |
| **Network MTU** | Spinbox | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes. Rango 576-9000 bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | Campos de configuración de IP estática. |
| **Apply** | Botón pulsador | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información de posicionamiento en vivo.

| Control | Tipo | Comportamiento |
|---|---|---|
| Información GPS | Indicador | Información en vivo de latitud/longitud/altitud/hora/satélites. |

## Pestaña TX

La pestaña TX proporciona ajustes de temporización de transmisión, enclavamiento, potencia y seguimiento de slice/TX.

### Ajustes de banda TX

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Band Settings** | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |

### Temporizaciones

| Control | Tipo | Comportamiento |
|---|---|---|
| **ACC TX:** | Spinbox | Retardo de ACC TX en milisegundos. |
| **TX Delay:** | Spinbox | Retardo de TX en milisegundos. |
| **RCA TX1:** | Spinbox | Retardo de RCA TX1 en milisegundos. |
| **Timeout (sec):** | Spinbox | Tiempo de espera de enclavamiento en segundos (rango 0-3600). La radio almacena este valor en milisegundos internamente. |
| **TX2:** | Spinbox | Retardo de TX2 en milisegundos. |

### Enclavamientos

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX REQ: RCA** | Botón de alternancia | Habilita la entrada de enclavamiento RCA. |
| **TX REQ: Accessory** | Botón de alternancia | Habilita la entrada de enclavamiento del accesorio. |

### Potencia y sintonía

| Control | Tipo | Comportamiento |
|---|---|---|
| **Max Power:** | Spinbox | Establece el límite de potencia de TX a nivel de radio (0-100%). |
| **Tune Mode:** | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |

### Visualización en el waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| **Show TX in Waterfall:** | Botón de alternancia | Dibuja la señal de TX en el waterfall. |

### Comportamiento de seguimiento Slice/TX

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Follows Active Slice** | Botón pulsador | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante una operación de Split. Se almacena como `TxFollowsActiveSlice`. Valor predeterminado: False. |
| **Active Slice Follows TX** | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. Valor predeterminado: False. |

## Pestaña Phone/CW

La pestaña Phone/CW proporciona configuración de micrófono, manipulador CW y RTTY.

### Micrófono

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Tipo | Comportamiento |
|---|---|---|
| **Iambic:** | Botón de alternancia | Habilita/deshabilita el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Botón pulsador | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. Valor predeterminado: A. |
| **Swap:** | Botón de alternancia | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB | USB). |
| **CWX:** | Botón de alternancia | Habilita la activación de macros CWX. |
| **Decode:** | Botón de alternancia | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. Valor predeterminado: True. |

### RTTY

| Control | Tipo | Comportamiento |
|---|---|---|
| **RTTY Mark Default:** | Spinbox | Frecuencia predeterminada de la marca RTTY. |

## Pestaña RX

La pestaña RX proporciona calibración de frecuencia y selección de fuente de referencia.

### Calibración de frecuencia

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | Frecuencia utilizada para la calibración manual. |
| **Start** | Botón pulsador | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración del PLL. Se deshabilita y etiqueta como "Busy" mientras una calibración está en curso. |
| **Freq Offset (ppb):** | Spinbox | Desvío de frecuencia manual en partes por mil millones. |

### Fuente de referencia de 10 MHz

| Control | Tipo | Comportamiento |
|---|---|---|
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External 10 MHz. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb, establece la frecuencia de calibración e inicia el barrido de calibración del PLL. El campo de estado junto al botón Start se actualiza a medida que avanza la calibración.
5. Mientras la calibración está en ejecución, el botón **Start** está deshabilitado y muestra "Busy". Se vuelve a habilitar cuando la calibración se completa o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario después de que la calibración se complete.

## Pestaña Antennas

La pestaña Antennas proporciona configuración de nombres de antenas.

| Control | Tipo | Comportamiento |
|---|---|---|
| Campos de nombre de antena | Campo de texto | Configuración de nombre por antena para ANT1, ANT2, XVTA y XVTB. |

## Pestaña Audio

La pestaña Audio proporciona controles de salida de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Line Out:** | Deslizador | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón pulsador | Silencia la salida de línea. |
| **Headphone:** | Deslizador | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón pulsador | Silencia los auriculares. |
| **Front Speaker: / Mute** | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio (SmartLink)

| Control | Tipo | Comportamiento |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón pulsador | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. Valor predeterminado: Auto. |

### Prevención de suspensión del sistema

| Control | Tipo | Comportamiento |
|---|---|---|
| **Prevent system sleep while connected** | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. Valor predeterminado: False. |

### Dispositivos de audio del PC

| Control | Tipo | Comportamiento |
|---|---|---|
| **PC Audio Devices: Input:** | Cuadro combinado | Selecciona el dispositivo de entrada de audio del host. |
| **PC Audio Devices: Output:** | Cuadro combinado | Selecciona el dispositivo de salida de audio del host. |

### Refuerzo y búfer de audio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Audio Boost:** | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| **Audio Buffer:** | Campo de texto | Aumenta el búfer de audio en milisegundos para jitter de VPN/SmartLink. Rango 50-1000 ms. Se almacena como `AudioBufferMs`. Valor predeterminado: 200. |

### Grabación

| Control | Tipo | Comportamiento |
|---|---|---|
| **Recording: Radio Side / Client Side** | Botón pulsador | Selecciona grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. Valor predeterminado: Radio Side. |
| **Save to:** | Campo de texto | Carpeta para las grabaciones guardadas (solo lado del cliente). Se almacena como `QsoRecordingDir`. Valor predeterminado: Documentos/AetherSDR/Grabaciones. |
| **...** | Botón pulsador | Busca la carpeta de grabación. |
| **Auto-record on TX** | Casilla de verificación | Graba automáticamente mientras se transmite. Se almacena como `QsoRecordingAutoRecord`. Valor predeterminado: False. |
| **Idle timeout:** | Spinbox | Segundos de silencio antes de que se detenga la grabación. Rango 10-3600 seg. Se almacena como
