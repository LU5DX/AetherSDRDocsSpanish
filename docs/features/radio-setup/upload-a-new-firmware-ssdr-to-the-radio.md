# Cargar un Nuevo Archivo de Firmware en la Radio

Esta página explica cómo cargar una imagen de firmware en su FLEX-8600 utilizando el diálogo de Configuración de Radio. Esto se hace para actualizar la radio a una versión de firmware específica sin usar la comprobación automática de actualizaciones.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La pestaña Radio no se completará correctamente sin una conexión activa.
- Descargue el instalador de SmartSDR desde flexradio.com y anote dónde se guarda en su computadora. AetherSDR acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Select Installer...** para abrir un selector de archivos.
4. Navegue hasta el instalador o archivo de firmware en su computadora, selecciónelo y confirme. AetherSDR detecta automáticamente el formato desde el encabezado del archivo y extrae el `.ssdr` si es necesario. Aparece un mensaje de estado mientras se prepara el firmware.
5. Cuando el estado indique que el firmware está listo, haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga está completa antes de hacer cualquier otra cosa.
7. Reinicie la radio según lo indicado en las notas de la versión del firmware para aplicar el nuevo firmware.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). Muestra el número de serie del chasis si está disponible; de lo contrario, muestra el número de serie de la radio. Muestra una raya (`—`) si no se reporta ningún valor. Aparece un pequeño botón de copia junto al valor al pasar el cursor o al enfocarlo; haga clic en él para copiar el número de serie al portapapeles. |
| **Region** | Indicador | Región regulatoria de la radio. |
| **HW Version** | Indicador | Cadena de la versión de hardware. Muestra una raya (`—`) si está vacía, con el prefijo `v` si no tiene una `v` inicial. Hay un botón de copia disponible. |
| **Model** | Indicador | Modelo de la radio. Hay un botón de copia disponible. |
| **Nickname** | Campo de texto | Apodo descriptivo de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica a este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto, usa el nombre del host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como `client station <name>`. |
| **Remote On** | Botón | Habilita el encendido/activación remota. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. Muestra la cadena de opciones reportada por la radio o, si está vacía, inserta valores predeterminados sensatos (ej. `GPS, PGXL` si la radio tiene un amplificador, de lo contrario `GPS`). Hay un botón de copia disponible. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de multiFLEX habilitado. |
| **License Info** | Indicador | Muestra los detalles de la licencia (Suscripción / Vencimiento / ID de Radio / Versión licenciada) desde la radio. |
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Si se encuentra una actualización, el área de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo. |
| **Select Installer...** | Botón | Abre un diálogo de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Se muestra un mensaje de estado mientras se prepara el archivo. Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Botón | Inicia la carga usando el archivo preparado por **Select Installer...**. Aparecen una barra de progreso y un texto de estado debajo que se actualizan a medida que avanza la transferencia. |
| TX Follows Active Slice | Botón | TX sigue la porción activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| Active Slice Follows TX | Botón | Cambia la porción activa cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |
| APD (pestaña) | Pestaña | Selección del puerto de muestra de Predistorsión Adaptativa Externa por antena TX (ANT1, ANT2, XVTA, XVTB). La pestaña está oculta a menos que la radio reporte apd configurable=1 (FLEX-8x00 con SmartSDR 4.2.18+). Nuevo en v26.5.1 (#2186). Se construye de forma perezosa solo cuando se hace clic en la pestaña por primera vez. |
| External Sampler (por ANT TX) | Encabezado de sección dentro de la pestaña APD que muestra una cuadrícula de 2x2 de cuadros combinados de puertos de muestra ANT1/ANT2/XVTA/XVTB. |
| ANT1: / ANT2: / XVTA: / XVTB: | Cuadro combinado | Elige el puerto de muestra (INTERNAL, RX_A, RX_B, XVTA, XVTB) que la radio usa para la realimentación APD en esa antena TX. INTERNAL muestrea dentro de la radio; los puertos externos requieren una señal de realimentación acoplada desde la salida del amplificador lineal. Al cambiar, se envía setApdSamplerPort() a la radio. |
| Equalizer Reset: | Etiqueta de fila de sección para el botón de reinicio del ecualizador APD. |
| Reset (APD Equalizer) | Botón | Limpia todos los datos de entrenamiento APD por antena en la radio. Envía resetApdEqualizer() al TransmitModel de la radio. |
| Themes (pestaña) | Pestaña | Ajustes de apariencia de la interfaz de usuario, incluyendo anulaciones de color por porción. La etiqueta de la pestaña en el código es 'Themes'. Se construye de forma perezosa al hacer clic por primera vez. |
| Slice Colors | Encabezado de grupo para los controles de color de porción. |
| Use Aether defaults | Botón de opción | Usa la paleta de colores de porción incorporada (cian/magenta/verde/amarillo/naranja/verde azulado/coral/lavanda). Al seleccionar esto, se deshabilitan los botones de color personalizados. |
| Custom colors | Botón de opción | Habilita selectores de color por porción (A-H). Al seleccionar esto, se habilitan los ocho botones de color debajo. |
| Botones de color A/B/C/D/E/F/G/H | Botón | Haga clic para abrir un selector de color para esa letra de porción (A-H). El fondo del botón refleja el color actualmente asignado. 8 botones dispuestos en una cuadrícula horizontal. Se almacena a través de SliceColorManager que persiste en AppSettings. |
| Reset All to Defaults | Botón | Restablece cada color personalizado por porción a su valor predeterminado incorporado. |
| SmartLink (pestaña) | Pestaña | Gestión de certificados TLS de SmartLink anclados. Lista cada certificado anclado (host, huella SHA-256, fecha de anclaje) con botones Forget y Forget All por fila. Nuevo en v26.5.3 (#2951 Fase 2). Se construye de forma perezosa al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: la discrepancia de anclaje de certificado ahora pausa firmemente el protocolo de enlace con un diálogo modal. |
| Pinned SmartLink Certificates (sección) | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Lista cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso). Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de anclaje migró de cadenas simples a objetos {fp, pinnedAt}. |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)'). Respaldado por WanCertCache en WanConnection.cpp. |
| Forget selected | Botón | Elimina la huella del certificado anclado del host seleccionado para que la próxima conexión lo vuelva a anclar silenciosamente. |
| Forget all | Botón | Limpia todos los certificados anclados (con confirmación). La próxima conexión a cada radio los vuelve a anclar silenciosamente. Muestra QMessageBox::question antes de borrar. |

## Pestaña Network

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. |
| **Enforce Private IP Connections:** | Alternar | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spinbox | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes (576-9000). El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Alternar | Cambia entre modos de IP DHCP y Estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | Campos de configuración de IP estática. |
| **Apply** | Botón | Envía la configuración de red a la radio. |

## Pestaña GPS

| Control | Tipo | Comportamiento |
|---|---|---|
| GPS info | Indicador | Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites. |

## Pestaña TX

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Band Settings** | Botón | Abre el diálogo dedicado de potencia/sintonía por banda. |
| **ACC TX:** | Campo de texto | Retardo de transmisión ACC en milisegundos. Rango 0-5000 ms. |
| **TX Delay:** | Campo de texto | Retardo de TX en milisegundos. Rango 0-5000 ms. |
| **RCA TX1:** | Campo de texto | Retardo de RCA TX1 en milisegundos. Rango 0-5000 ms. |
| **Timeout (sec):** | Campo de texto | Tiempo de espera de interbloqueo en segundos. La radio almacena este valor en milisegundos internamente. Rango 0-3600 segundos. |
| **TX2:** | Campo de texto | Retardo de TX2 en milisegundos. Rango 0-5000 ms. |
| **Interlocks - TX REQ: RCA / Accessory** | Alternar | Habilita las entradas de interbloqueo RCA y Accessory. |
| **Max Power:** | Spinbox | Establece el límite de potencia de TX a nivel de radio (0-100%). |
| **Tune Mode:** | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** | Alternar | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | Botón | TX sigue la porción activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón | Cambia la porción activa cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Alternar | Muestra el medidor de nivel de micrófono incluso en RX. |
| **Iambic:** | Alternar | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Botón | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. El valor predeterminado es A. |
| **Swap:** | Alternar | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB / USB). |
| **CWX:** | Alternar | Habilita el teclado de macros CWX. |
| **Decode:** | Alternar | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Campo | Ingrese la frecuencia de referencia conocida en MHz (seis decimales). |
| **Start** | Botón | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y etiqueta como **Busy** mientras se ejecuta un barrido. |
| **Freq Offset (ppb)** | Spinbox | Desplazamiento de frecuencia manual en partes por billón. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (Auto / TCXO / GPSDO / External). |
| Etiqueta de estado del oscilador | Indicador | Muestra la fuente resuelta, el estado de bloqueo (Locked / Unlocked) y (para External) si se detecta una señal. Se actualiza en vivo. |

## Pestaña Audio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Line Out:** | Control deslizante | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón | Silencia la salida de línea. |
| **Headphone:** | Control deslizante | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón | Silencia los auriculares. |
| **Front Speaker: / Mute** | Botón | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena en AppSettings como `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | Elige los dispositivos de audio de entrada/salida del host. |
| **Audio Boost:** | Alternar | Habilita ganancia adicional en el |
