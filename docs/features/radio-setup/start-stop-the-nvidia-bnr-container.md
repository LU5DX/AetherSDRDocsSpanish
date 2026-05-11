# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos y serial (FlexControl).

## Abrir el diálogo

1. Asegúrese de que AetherSDR esté conectado a la radio.
2. Haga clic en `Settings > Radio Setup...`.
3. El diálogo se abre como una ventana sin marco con una barra de título personalizada. Puede arrastrar la barra de título para mover el diálogo y usar los bordes de la ventana para redimensionarlo.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). |
| **Region** | Indicador | Región regulatoria de la radio (ej., USA). |
| **HW Version** | Indicador | Cadena de versión del hardware. |
| **Model** | Indicador | Modelo de radio. |
| **Nickname** | Campo de texto | Apodo amigable de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto es el nombre del host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como `client station <name>`. |
| **Remote On** | Botón | Habilita el encendido remoto / remote-on. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado habilitado de multiFLEX. |
| **License Info** | Indicador | Muestra los detalles de la licencia (Suscripción / Expiración / ID de Radio / Versión licenciada) desde la radio. |

### Actualización de firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón | Consulta al servidor de actualizaciones de FlexRadio en busca de actualizaciones de firmware. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware** | Botón | Inicia la carga del firmware con barra de progreso y estado. |
| Estado del firmware | Indicador | Vacío hasta que comienza una carga de firmware, luego muestra el progreso y el texto del resultado. |

#### Verificar actualizaciones

1. Haga clic en **Check for Update**. AetherSDR consulta al servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra "Update available: v*x.x.x* — Download the SmartSDR installer from flexradio.com, then click **Select Installer...** to stage it." en ámbar.

#### Preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com si aún no lo tiene localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — Instalador WiX de FlexRadio v4.2+
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El gestor detecta el formato del archivo a partir de los primeros 8 bytes y extrae la carga útil `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparing firmware from *filename*..." mientras la preparación está en curso.
4. Cuando la preparación se complete, haga clic en **Upload Firmware**. Una barra de progreso y una etiqueta de estado supervisan la carga.

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. |
| **Enforce Private IP Connections:** | Alternar | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spinbox | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576-9000, predeterminado 1450). Se almacena en AppSettings como `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static** | Alternar | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | Campos de configuración de IP estática (habilitados en modo Static). |
| **Apply** | Botón | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

| Control | Tipo | Comportamiento |
|---|---|---|
| Información GPS | Indicador | Datos GPS en vivo cuando hay un módulo GPS instalado y tiene una posición fija. |

## Pestaña TX

La pestaña TX controla los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y Configuración de Banda de TX.

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Band Settings** | Botón | Abre el diálogo dedicado de potencia/sintonía por banda. |
| **Timings (in ms)** | Spinbox | Tiempos de retención / retardo de TX. |
| **Interlocks - TX REQ: RCA / Accessory** | Alternar | Habilita las entradas de enclavamiento RCA y accessory. |
| **Max Power:** | Spinbox | Establece el límite de potencia de TX a nivel de radio (0-100%). |
| **Tune Mode:** | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** | Alternar | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | Botón | El TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando el TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña Phone/CW controla el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Alternar | Muestra el medidor de nivel de micrófono incluso en RX. |
| **Iambic:** | Alternar | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Par de botones | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Mutuamente excluyentes. |
| **Swap:** | Alternar | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB | USB). |
| **CWX:** | Alternar | Habilita el tecleo de macros CWX. |
| **Decode:** | Alternar | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX controla la calibración del desplazamiento de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | Frecuencia utilizada para la calibración manual. |
| **Start** | Botón | Inicia el barrido de calibración de frecuencia. |
| **Freq Offset (ppb):** | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto a él y se actualiza en vivo. |

### Calibración de frecuencia

Los controles de calibración de frecuencia están disponibles independientemente de si hay un GPSDO instalado.

Aparece una etiqueta de estado junto a **Start** y proporciona retroalimentación en línea:

| Texto de estado | Significado |
|---|---|
| Starting... | AetherSDR ha enviado los comandos de calibración a la radio. |
| Busy | El botón **Start** está deshabilitado; la calibración está en progreso. |
| (texto de error) | Se reportó un problema; verifique el valor en **Cal Frequency (MHz)**. |

Cuando hay hardware GPSDO presente, la etiqueta en la parte superior del grupo muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Fuente de Referencia de 10 MHz

El cuadro combinado se completa dinámicamente según lo que reporta la radio:

| Entrada | Se muestra cuando |
|---|---|
| Auto | Siempre presente. |
| TCXO | La radio reporta hardware TCXO presente, o TCXO es la configuración o el estado activo actual. |
| GPSDO | La radio reporta hardware GPSDO presente, o GPSDO es la configuración o el estado activo actual. |
| External 10 MHz | La radio reporta una referencia externa detectada, o External es la configuración o el estado activo actual, o se ha recibido el estado del oscilador. |

La etiqueta de estado de bloqueo junto al cuadro combinado muestra el estado actual del oscilador:

| Condición | Texto de la etiqueta (ejemplos) |
|---|---|
| Aún no se ha recibido estado | Waiting for oscillator status |
| Modo Auto, la radio resolvió a una fuente | Auto -> GPSDO Locked |
| La configuración difiere del estado activo | TCXO -> GPSDO Locked |
| La configuración coincide con el estado activo | GPSDO Locked |
| Fuente activa desbloqueada | GPSDO Unlocked |
| External seleccionado, sin señal detectada | External 10 MHz Unlocked (not detected) |

El color de la etiqueta es verde cuando está bloqueado, rojo cuando está desbloqueado y gris azulado apagado antes de que llegue el estado.

#### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)** (por ejemplo, una portadora de WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no puede iniciar.
5. Haga clic en **Start**. La etiqueta de estado muestra "Starting..." y luego "Busy" mientras se ejecuta el barrido de calibración.
6. Cuando se complete, el campo **Freq Offset (ppb)** se actualiza con el desplazamiento calculado.

## Pestaña Audio

La pestaña Audio controla las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Line Out:** | Deslizador | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón | Silencia la salida de línea. |
| **Headphone:** | Deslizador | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón | Silencia los auriculares. |
| **Front Speaker: / Mute** | Botón | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujo de audio/TCP/UDP durante la inactividad. Se almacena en AppSettings como `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | Elige los dispositivos de audio de entrada/salida del host. |
| **Audio Boost:** | Alternar | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en AppSettings como `AudioBoost`. |
| **Audio Buffer:** | Campo de texto | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink (50-1000 ms, predeterminado 200). Se almacena en AppSettings como `AudioBufferMs`. |
| **Recording: Radio Side / Client Side** | Botón | Elige la grabación del lado de la radio o del lado del cliente. Se almacena en AppSettings como `RecordingMode`. |
| **Save to:** | Campo de texto | Carpeta para las grabaciones guardadas (solo del lado del cliente). Por defecto es Documents/AetherSDR/Recordings. Se almacena en AppSettings como `QsoRecordingDir`. |
| **...** | Botón | Navega para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | Casilla de verificación | Graba automáticamente mientras se transmite. Se almacena en AppSettings como `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Spinbox | Segundos de silencio antes de que la grabación se detenga (10-3600 seg, predeterminado 120). Se almacena en AppSettings como `QsoRecordingIdleTimeout`. |

### NVIDIA BNR (Broadcast Noise Removal)

El contenedor NVIDIA BNR aplica supresión de ruido basada en IA al audio de su micrófono.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Cuando está activo, AetherSDR inicia el contenedor NVIDIA BNR automáticamente al iniciar. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR inmediatamente. |
| **Stop** | Botón | Detiene un contenedor NVIDIA BNR en ejecución inmediatamente. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el punto de estado. |
| Punto de estado NVIDIA BNR | Indicador | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown. |

#### Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible cuando está desconectado.
- El contenedor NVIDIA Broadcast debe estar instalado en su sistema independientemente de AetherSDR. AetherSDR lo controla pero no lo instala.

#### Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que AetherSDR se inicie, haga clic en **Autostart Container** para activarlo.
5. Para iniciar el
