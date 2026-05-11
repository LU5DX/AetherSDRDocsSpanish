# Cargar un Nuevo Archivo de Firmware en la Radio

Esta página explica cómo cargar una imagen de firmware en su FLEX-8600 utilizando el diálogo de Configuración de Radio. Realizaría esto para actualizar la radio a una versión de firmware específica sin usar la verificación automática de actualizaciones.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Radio no se completará correctamente sin una conexión activa.
- Descargue el instalador de SmartSDR desde flexradio.com y anote dónde se guarda en su computadora. AetherSDR acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` pre-extraído.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Select Installer...** para abrir un selector de archivos.
4. Navegue hasta el instalador o archivo de firmware en su computadora, selecciónelo y confirme. AetherSDR detecta automáticamente el formato desde la cabecera del archivo y extrae el `.ssdr` si es necesario. Aparece un mensaje de estado mientras se prepara el firmware.
5. Cuando el estado indique que el firmware está listo, haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga está completa antes de hacer cualquier otra cosa.
7. Reinicie la radio según lo indicado en las notas de la versión del firmware para aplicar el nuevo firmware.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). |
| **Region** | Indicador | Región regulatoria de la radio. |
| **HW Version** | Indicador | Cadena de versión de hardware. |
| **Model** | Indicador | Modelo de la radio. |
| **Nickname** | Campo de texto | Apodo descriptivo de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre del host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como `client station <name>`. |
| **Remote On** | Botón | Activa el encendido remoto / remote-on. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de habilitación de multiFLEX. |
| **License Info** | Indicador | Muestra los detalles de la licencia (Suscripción / Vencimiento / ID de Radio / Versión licenciada) desde la radio. |
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Si se encuentra una actualización, el área de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo. |
| **Select Installer...** | Botón | Abre un diálogo de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo `.ssdr` pre-extraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Se muestra un mensaje de estado mientras se prepara el archivo. Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Botón | Inicia la carga usando el archivo preparado por **Select Installer...**. Aparecen una barra de progreso y texto de estado debajo que se actualizan a medida que avanza la transferencia. |
| TX Follows Active Slice | Botón | TX sigue la porción activa. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. |
| Active Slice Follows TX | Botón | Cambia la porción activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |

## Pestaña Network

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. |
| **Enforce Private IP Connections:** | Interruptor | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spinbox | Establece el tamaño máximo del paquete UDP VITA-49 de salida en bytes (576-9000). El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Interruptor | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | Campos de configuración de IP estática. |
| **Apply** | Botón | Envía la configuración de red a la radio. |

## Pestaña GPS

| Control | Tipo | Comportamiento |
|---|---|---|
| Información GPS | Indicador | Presencia de GPS e información de lat/lon/alt/hora/satélites en vivo. |

## Pestaña TX

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Band Settings** | Botón | Abre el diálogo dedicado de potencia/tono por banda. |
| **Timings (in ms)** | Spinbox | Temporizaciones de retención/retardo de TX. |
| **Interlocks - TX REQ: RCA / Accessory** | Interruptor | Activa las entradas de enclavamiento RCA y de accesorio. |
| **Max Power:** | Spinbox | Establece el límite de potencia de TX a nivel de radio (0-100%). |
| **Tune Mode:** | Combo box | Selecciona cómo se comporta el botón de tono. |
| **Show TX in Waterfall:** | Interruptor | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | Botón | TX sigue la porción activa. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. |
| **Active Slice Follows TX** | Botón | Cambia la porción activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |

## Pestaña Phone/CW

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Interruptor | Muestra el medidor de nivel de micrófono incluso en RX. |
| **Iambic:** | Interruptor | Activa o desactiva el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Botón | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. |
| **Swap:** | Interruptor | Intercambia dit/dah. |
| **Sideband:** | Combo box | Selecciona la banda lateral del tono CW (LSB / USB). |
| **CWX:** | Interruptor | Activa el keying de macros CWX. |
| **Decode:** | Interruptor | Activa la superposición de decodificación CW en el panadapter. |
| **RTTY Mark Default:** | Spinbox | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Campo | Ingrese la frecuencia de referencia conocida en MHz (seis decimales). |
| **Start** | Botón | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Deshabilitado y etiquetado como **Busy** mientras se ejecuta un barrido. |
| **Freq Offset (ppb)** | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Combo box | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado y el estado en vivo de la radio. |
| Etiqueta de estado del oscilador | Indicador | Muestra la fuente resuelta, el estado de bloqueo y (para Externo) si se detecta una señal. Se actualiza en vivo. |

## Pestaña Audio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Line Out:** | Deslizador | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón | Silencia la salida de línea. |
| **Headphone:** | Deslizador | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón | Silencia los auriculares. |
| **Front Speaker: / Mute** | Botón | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón | Selecciona el códec de audio para SmartLink/LAN. |
| **Prevent system sleep while connected** | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada. |
| **PC Audio Devices: Input: / Output:** | Combo box | Elige los dispositivos de audio de entrada/salida del host. |
| **Audio Boost:** | Interruptor | Activa ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | Campo de texto | Aumenta el búfer de audio en milisegundos (50-1000 ms) para la fluctuación de VPN/SmartLink. |
| **Recording: Radio Side / Client Side** | Botón | Elige la grabación del lado de la radio o del lado del cliente. |
| **Save to:** | Campo de texto | Carpeta para grabaciones guardadas (solo del lado del cliente). |
| **...** | Botón | Navega para buscar la carpeta de grabación. |
| **Auto-record on TX** | Casilla de verificación | Graba automáticamente mientras transmite. |
| **Idle timeout:** | Spinbox | Segundos de silencio antes de que se detenga la grabación (10-3600 seg). |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Botón | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Pestaña Filters

| Control | Tipo | Comportamiento |
|---|---|---|
| **Voice / CW / Digital filter sharpness sliders** | Deslizador | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. |
| **Auto (Voice / CW / Digital)** | Interruptor | Activa la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Fuerza filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

| Control | Tipo | Comportamiento |
|---|---|---|
| **RX Only:** | Interruptor | Fuerza solo RX en ese transvertidor. |
| **Remove (xvtr)** | Botón | Elimina la definición del transvertidor. |
| **Create New Transverter** | Botón | Añade una nueva entrada de transvertidor. |

## Pestaña USB Cables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cables list / Status** | Indicador | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| **Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7)** | Combo box | Parámetros seriales y comportamiento por cable. |

## Pestaña Peripherals

| Control | Tipo | Comportamiento |
|---|---|---|
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio `tgxl autotune handle=<H>` que está rota en firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de enclavamiento de hardware; no se necesita keying del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se completa automáticamente. Si el usuario borra el campo IP y cierra el diálogo sin hacer clic en Connect/Disconnect, la IP/puerto manual guardada se elimina y el dispositivo se desconecta automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. Mismo comportamiento que TGXL para campo IP vacío al cerrar. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado Connected solo cuando el dispositivo conectado es un Antenna Genius genuino (no un ShackSwitch). Mismo comportamiento que TGXL para campo IP vacío al cerrar. |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo UDP/TCP de AG en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo 'ShackSwitch' en el beacon de difusión de AG. El descubrimiento automático a través de UDP también funciona sin esta fila. Fila oculta del estado Connected si Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del beacon si es mayor a 1024, de lo contrario usa `SS_WebPort` o el puerto 5000. |

## Pestaña Serial

| Control | Tipo | Comportamiento |
|---|---|---|
| **Port / Refresh / Path** | Combo box | Selecciona/edita el dispositivo serial. |
| **Baud / Data / Parity / Stop** | Combo box | Parámetros de la línea serial. |
| **DTR / RTS: Function / Polarity** | Combo box | Asigna función de señal y polaridad. |
| **Paddle Swap (swap dit/dah)** | Casilla de verificación | Intercambia dit/dah para la paleta. |
| **Auto-open serial port on startup** | Casilla de verificación | Vuelve a abrir el puerto al iniciar la aplicación. |
| **FlexControl Tuning Knob: Detect / Close** | Botón | Detecta o cierra una perilla FlexControl. |
| **Auto-detect on startup**
