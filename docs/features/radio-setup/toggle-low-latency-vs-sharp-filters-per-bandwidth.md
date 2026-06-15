# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración para ajustes por radio, incluyendo información de radio, red, GPS, TX, Phone/CW, RX, audio, filtros, antenas, transverters, cables USB, periféricos, APD, temas, puerto serie y gestión de certificados anclados de SmartLink.

## Abrir el diálogo

- Haga clic en `Settings > Radio Setup...` mientras está conectado a una radio.

## Diseño del diálogo

El diálogo contiene una interfaz con pestañas:

- **Radio** - Información de radio, identificación, info de licencia, actualización de firmware y reinicio de radio
- **Network** - Información de red y opciones de red avanzadas
- **GPS** - Presencia GPS e información en vivo de lat/lon/alt/hora/satélites
- **TX** - Temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía y ajustes de seguimiento slice/TX
- **Phone/CW** - Micrófono, manipulador CW, valores predeterminados RTTY
- **RX** - Calibración de desplazamiento de frecuencia GPSDO y fuente de referencia de 10 MHz
- **Antennas** - Configuración de nombre de antena
- **Filters** - Opciones de filtro de baja latencia / Sharp por ancho de banda
- **XVTR** - Configuración por transverter
- **USB Cables** - Asignación de adaptador serie USB
- **Peripherals** - Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius)
- **APD** - Selección de puerto de muestra de Predistorsión Adaptativa Externa (solo FLEX-8x00)
- **Themes** - Ajustes de apariencia de la interfaz, incluyendo anulaciones de color por slice
- **SmartLink** - Gestión de certificados TLS anclados
- **Serial** - Configuración del puerto serie FlexControl

El diálogo recuerda su tamaño y posición entre sesiones usando `RadioSetupDialogGeometry` en AppSettings.

Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Radio, Themes, Audio, Filters, Peripherals en pantallas pequeñas o de alta densidad) están envueltas en un área de desplazamiento para que el diálogo no crezca más allá del borde de la pantalla. La barra de desplazamiento aparece solo cuando es necesario; en pantallas anchas no hay cambio visual.

## Pestaña Radio

La pestaña Radio muestra información de identificación y licencia de la radio, proporciona controles de actualización de firmware e incluye un botón Reboot Radio. Cada valor de solo lectura tiene un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar: haga clic para copiar el valor.

### Información de radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). Si el serial del chasis está vacío, recurre al número de serie de la radio. Muestra "—" si no está disponible. |
| **Region** | Indicador | Región regulatoria de la radio. Predeterminado: USA. |
| **HW Version** | Indicador | Cadena de versión de hardware. Prefijada con "v" si no está presente. Muestra "—" si no está disponible. |
| **Model** | Indicador | Modelo de radio. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. Si está vacío, muestra una estimación basada en la presencia del amplificador ("GPS, PGXL" o "GPS"). Muestra "—" si no está disponible. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de habilitación de multiFLEX. |
| **License Info** | Indicador | Muestra suscripción, vencimiento, ID de radio y versión licenciada desde la radio. |

### Identificación de radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo de radio fácil de usar. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del sistema operativo si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como `client station <nombre>`. |

### Remote On

| Control | Tipo | Comportamiento |
|---|---|---|
| **Remote On** | Botón pulsador | Habilita el encendido remoto / remote-on. |

### Reboot Radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Reboot Radio** | Botón pulsador | Reinicia la radio conectada. Aparece un diálogo de confirmación antes de reiniciar. En conexiones LAN, AetherSDR se reconecta automáticamente una vez que la radio termina de iniciar. En conexiones SmartLink/WAN, debe reconectarse manualmente después de que la radio inicie. El diálogo se cierra después del reinicio. El botón está deshabilitado cuando la radio está desconectada. |

### Actualización de firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón pulsador | Consulta actualizaciones de firmware desde la radio. |
| **Select Installer...** | Botón pulsador | Abre un selector de archivos que acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware** | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| Estado del firmware | Indicador | Vacío hasta que comienza una carga de firmware, luego muestra progreso y texto de resultado. |

#### Flujo de trabajo de actualización de firmware

Cuando **Check for Update** encuentra una versión más reciente, el área de estado le indica que descargue el instalador de SmartSDR desde flexradio.com. Use **Select Installer...** para indicarle a AetherSDR el archivo que descargó.

**Formatos de instalador compatibles**

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador FlexRadio WiX (SmartSDR v4.2 y posteriores). Recomendado. |
| `.exe` | Instalador autoextraíble antiguo (versiones pre-v4.2). |
| `.ssdr` | Archivo de firmware preextraído. |

**Pasos**

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión y le indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en **Select Installer...** y localice el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR prepara el firmware e informa el progreso en el área de estado.
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
| **Enforce Private IP Connections:** | Botón de alternancia | Rechaza pares no RFC1918. Siempre muestra el texto "Enabled". |
| **Network MTU:** | Spinbox | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | Campos de configuración de IP estática. |
| **Apply** | Botón pulsador | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra presencia GPS e información de posicionamiento en vivo.

| Control | Tipo | Comportamiento |
|---|---|---|
| Información GPS | Indicador | Información en vivo de lat/lon/alt/hora/satélites. |

## Pestaña TX

La pestaña TX proporciona ajustes de temporización de transmisión, enclavamientos, potencia y seguimiento slice/TX.

### TX Band Settings

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Band Settings** | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |

### Temporizaciones

| Control | Tipo | Comportamiento |
|---|---|---|
| **ACC TX:** | Spinbox | Retardo ACC TX en milisegundos. |
| **TX Delay:** | Spinbox | Retardo TX en milisegundos. |
| **RCA TX1:** | Spinbox | Retardo RCA TX1 en milisegundos. |
| **Timeout (sec):** | Spinbox | Tiempo de espera de enclavamiento en segundos (rango 0-3600). La radio almacena este valor en milisegundos internamente. |
| **TX2:** | Spinbox | Retardo TX2 en milisegundos. |

### Enclavamientos

| Control | Tipo | Comportamiento |
|---|---|---|
| **Interlocks - TX REQ: RCA** | Botón de alternancia | Habilita la entrada de enclavamiento RCA. |
| **Interlocks - TX REQ: Accessory** | Botón de alternancia | Habilita la entrada de enclavamiento del accesorio. |

### Potencia y sintonía

| Control | Tipo | Comportamiento |
|---|---|---|
| **Max Power:** | Spinbox | Establece el límite de potencia TX a nivel de radio (0-100%). |
| **Tune Mode:** | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |

### Visualización en waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| **Show TX in Waterfall:** | Botón de alternancia | Dibuja la señal TX en el waterfall. |

### Comportamiento de seguimiento Slice/TX

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Follows Active Slice** | Botón pulsador | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante operación en Split. Se almacena como `TxFollowsActiveSlice`. Predeterminado: False. |
| **Active Slice Follows TX** | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. Predeterminado: False. |

## Pestaña Phone/CW

La pestaña Phone/CW proporciona configuración de micrófono, manipulador CW y RTTY.

### Micrófono

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Tipo | Comportamiento |
|---|---|---|
| **Iambic:** | Botón de alternancia | Habilita/deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Botón pulsador | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Swap:** | Botón de alternancia | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB | USB). |
| **CWX:** | Botón de alternancia | Habilita la activación por macro CWX. |
| **Decode:** | Botón de alternancia | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. Predeterminado: True. |

### RTTY

| Control | Tipo | Comportamiento |
|---|---|---|
| **RTTY Mark Default:** | Spinbox | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona calibración de frecuencia y selección de fuente de referencia.

### Calibración de frecuencia

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | Frecuencia utilizada para calibración manual. |
| **Start** | Botón pulsador | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración PLL. Deshabilitado y etiquetado como "Busy" mientras una calibración está en curso. |
| **Freq Offset (ppb):** | Spinbox | Desplazamiento de frecuencia manual en partes por billón. |

### Fuente de referencia de 10 MHz

| Control | Tipo | Comportamiento |
|---|---|---|
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External 10 MHz. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb, establece la frecuencia de calibración e inicia el barrido de calibración PLL. El campo de estado junto al botón Start se actualiza a medida que la calibración progresa.
5. Mientras la calibración está en ejecución, el botón **Start** está deshabilitado y muestra "Busy". Se vuelve a habilitar cuando la calibración se completa o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario después de que la calibración se complete.

## Pestaña Antennas

La pestaña Antennas proporciona configuración de nombre de antena.

| Control | Tipo | Comportamiento |
|---|---|---|
| Campos de nombre de antena | Campo de texto | Configuración de nombre por antena para ANT1, ANT2, XVTA y XVTB. |

## Pestaña Audio

La pestaña Audio proporciona controles de salida de audio de radio, compresión, dispositivos PC, refuerzo, búfer, grabación y contenedor NVIDIA BNR.

### Salidas de audio de radio

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
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón pulsador | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. Predeterminado: Auto. |

### Prevención de suspensión del sistema

| Control | Tipo | Comportamiento |
|---|---|---|
| **Prevent system sleep while connected** | Casilla de verificación | Mantiene
