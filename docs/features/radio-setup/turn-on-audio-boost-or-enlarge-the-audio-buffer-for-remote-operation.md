# Diálogo de Configuración de Radio de AetherSDR

El diálogo **Radio Setup** es la ventana de configuración maestra para los ajustes específicos de cada radio. Contiene pestañas para información del radio, red, GPS, transmisión, teléfono/CW, recepción, antenas, audio, filtros, transverters, cables USB, periféricos, APD, Themes, SmartLink, KiwiSDR y, opcionalmente, puertos serie.

## Abrir el diálogo Radio Setup

1. Haga clic en `Settings > Radio Setup...`.

## Disposición del diálogo

El diálogo **Radio Setup** es un diálogo persistente que recuerda su tamaño y posición entre sesiones. La geometría se guarda en `RadioSetupDialogGeometry` en la configuración de la aplicación.

Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Themes, Audio, Filters, Peripherals, KiwiSDR) están envueltas en un área de desplazamiento vertical. La barra de desplazamiento aparece solo cuando el contenido se desborda; en pantallas anchas no hay cambio visual.

## Pestaña Radio

La pestaña **Radio** muestra la identificación del radio y los controles de gestión de firmware.

### Información del radio (solo lectura)

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región regulatoria (p. ej., USA) |
| **HW Version** | Cadena de versión de hardware |
| **Model** | Modelo del radio (p. ej., FLEX-8600) |
| **Options** | Opciones licenciadas del radio |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de expiración, ID de radio y versión licenciada |

Cada campo de solo lectura tiene un botón de copiar a su derecha que copia el valor mostrado al portapapeles. Cuando el valor está vacío o no disponible, el botón de copiar aparece atenuado.

### Campos configurables por el usuario

| Control | Qué hace |
|---|---|
| **Nickname** | Ingrese un nombre amigable para el radio |
| **Callsign** | Ingrese el indicativo de la estación |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa el nombre de host del sistema operativo. Se guarda en `StationName`. |

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de despertado remoto / encendido remoto del radio.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar el radio conectado. Aparece un diálogo de confirmación antes del reinicio.

- En una conexión LAN: AetherSDR se desconecta y se reconecta automáticamente una vez que el radio termina de arrancar.
- En una conexión SmartLink/WAN: AetherSDR se desconecta. Debe reconectarse manualmente después de que el radio termine de arrancar.

El botón está deshabilitado cuando el radio está desconectado o reconectándose.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar al radio las versiones de firmware disponibles.
2. Si hay una actualización disponible, la etiqueta de estado muestra la versión y le indica que descargue el instalador de SmartSDR desde flexradio.com.
3. Descargue el instalador de SmartSDR (.msi para v4.2+, .exe para versiones anteriores).
4. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo .ssdr previamente extraído en el selector de archivos.
5. Una barra de progreso y una etiqueta de estado muestran el progreso de extracción. Cuando la preparación se completa, haga clic en **Upload Firmware** para transferir el firmware al radio.

## Pestaña Network

La pestaña **Network** muestra la información de red del radio y permite su configuración.

### Información de red (solo lectura)

| Control | Qué muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red actuales |

### Configuración

| Control | Qué hace | Rango válido |
|---|---|---|
| **Enforce Private IP Connections:** | Alternar para rechazar pares no-RFC1918 | On / Off |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 de salida en bytes. El valor predeterminado de 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se guarda en `NetworkMtu`. | 576–9000 bytes |
| **DHCP / Static** | Cambia entre los modos DHCP e IP estática | DHCP / Static |
| **Agent Automation (MCP):** | Alternar para habilitar el puente de automatización en la aplicación para que un asistente de codificación de IA (mediante el servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador lo activa. | Enabled / Disabled |
| **Access Token:** | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se guarda en el almacén de secretos del sistema operativo. | — |
| **Copy (Access Token)** | Haga clic para copiar el token de acceso al portapapeles | — |
| **Rotate (Access Token)** | Haga clic para generar un nuevo token y aplicarlo inmediatamente, bloqueando a cualquier cliente que aún use el anterior | — |
| **Allow TX via MCP: Enable transmit control** | Marque para permitir que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; al habilitarlo por primera vez se muestra una confirmación de responsabilidad del operador. | On / Off |
| **Observe only: Read-only (block all driving)** | Marque para que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) es rechazado. | On / Off |
| **VITA-49 RX buffer:** | Control deslizante de ajuste a valores preestablecidos que configura el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | 0.25–4 MB (valores preestablecidos) |
| **granted: (VITA-49 RX buffer)** | Muestra el tamaño de búfer que el kernel realmente otorgó (frente al valor preestablecido solicitado). | — |

Cuando se selecciona **Static**, ingrese la **IP Address:**, **Mask:** y **Gateway:** en los campos de texto y luego haga clic en **Apply** para enviar la configuración al radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS e información en vivo cuando hay un módulo GPS instalado y activo.

### Información del GPS (solo lectura)

| Indicador | Qué muestra |
|---|---|
| Estado GPS | Latitud, longitud, altitud, hora UTC y número de satélites cuando el GPS está activo |

## Pestaña TX

La pestaña **TX** configura los parámetros de transmisión.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonización por banda.

### Timings

Use las cajas de giro **Timings** para establecer los tiempos de retención y retardo de TX en milisegundos. El campo **Timeout (sec)** muestra el tiempo de espera de interbloqueo en segundos para facilitar la lectura; el radio almacena este valor internamente en milisegundos.

### Interlocks

Active **TX REQ: RCA** y **Accessory** para habilitar las entradas de interbloqueo.

### Power and Tune

| Control | Qué hace | Rango válido |
|---|---|---|
| **Max Power:** | Establece el límite máximo de potencia de TX a nivel del radio | 0–100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — |

### Display

| Control | Qué hace |
|---|---|
| **Show TX in Waterfall:** | Alternar para dibujar la señal de TX en el waterfall |

### Comportamiento de seguimiento de slice

| Control | Qué hace |
|---|---|
| **TX Follows Active Slice** | El TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante una operación Split. Se guarda en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. Se guarda en `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura los valores predeterminados de micrófono, manipulación CW y RTTY.

### Medidor de nivel

Active **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel de micrófono incluso durante la recepción.

### Manipulación CW

| Control | Qué hace | Rango válido |
|---|---|---|
| **Iambic:** | Habilita o deshabilita la manipulación iámbica en el radio | Enabled / Disabled |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para el radio como para el manipulador de software local. Par mutuamente excluyente. | A / B |
| **Swap:** | Intercambia punto/raya | On / Off |
| **Sideband:** | Selecciona la banda lateral del tono CW | LSB / USB |
| **CWX:** | Habilita la manipulación por macros CWX | On / Off |
| **Decode: RX** | Habilita la superposición de decodificación CW en el panadapter para el CW recibido. Se guarda en `CwDecoder` (JSON anidado, campo `rx`). | On / Off |
| **Decode: TX** | Decodifica la propia manipulación CW del operador mediante el tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Se guarda en `CwDecoder` (JSON anidado, campo `tx`). | On / Off |

### RTTY

| Control | Qué hace |
|---|---|
| **RTTY Mark Default:** | Establece la frecuencia predeterminada de marca RTTY |

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

## Pestaña Calibration

La pestaña **Calibration** proporciona calibración manual de frecuencia para radios que no pueden calibrarse a sí mismos (p. ej., HL2). Esta pestaña está oculta a menos que el radio conectado admita la calibración de frecuencia del lado del host.

### Calibración manual de frecuencia

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz para usar en la calibración |
| **Start** | Inicia el barrido de calibración de frecuencia |
| **Freq Offset (ppb):** | Muestra o establece manualmente el desplazamiento de frecuencia actual en partes por mil millones |

El estado de calibración se vuelve a leer cada vez que se muestra el diálogo o se conecta un radio diferente, de modo que una pulsación de Trim no pueda confirmar el valor de calibración del radio anterior.

## Pestaña Antennas

La pestaña **Antennas** configura los nombres de antena para cada puerto de antena del radio. Esta pestaña se construye de forma perezosa al hacer clic en ella por primera vez.

| Control | Qué hace |
|---|---|
| **ANT1:** | Ingrese un nombre personalizado para el puerto de antena 1 |
| **ANT2:** | Ingrese un nombre personalizado para el puerto de antena 2 |
| **XVTA:** | Ingrese un nombre personalizado para el puerto A del transverter |
| **XVTB:** | Ingrese un nombre personalizado para el puerto B del transverter |

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio del radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y NVIDIA BNR.

### Salidas de audio del radio

| Control | Qué hace |
|---|---|
| **Line Out:** | Deslice para ajustar la ganancia de salida de línea |
| **Mute (Line Out)** | Haga clic para silenciar la salida de línea |
| **Headphone:** | Deslice para ajustar la ganancia de auriculares |
| **Mute (Headphone)** | Haga clic para silenciar los auriculares |
| **Front Speaker:** / **Mute** | Haga clic para silenciar el altavoz frontal (específico del modelo) |

### Compresión de audio

| Control | Qué hace | Rango válido |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio usado sobre SmartLink/LAN. Se guarda en `AudioCompression`. | Auto / Uncompressed / Opus |

### Prevención de suspensión del sistema

Marque **Prevent system sleep while connected** para mantener el sistema operativo despierto mientras el radio está conectado. Se guarda en `InhibitSleepWhileConnected`.

### Dispositivos de audio del PC

| Control | Qué hace |
|---|---|
| **PC Audio Devices: Input:** | Seleccione el dispositivo de entrada de audio del host |
| **PC Audio Devices: Output:** | Seleccione el dispositivo de salida de audio del host |

### Refuerzo de audio

Active **Audio Boost:** para habilitar ganancia adicional en la ruta de audio del cliente. Se guarda en `AudioBoost`.

### Búfer de audio

Ingrese un valor en **Audio Buffer:** para establecer el búfer de audio del lado del cliente en milisegundos. Auméntelo cuando use conexiones VPN o SmartLink con latencia inestable. Se guarda en `AudioBufferMs`.

| Rango válido | Predeterminado |
|---|---|
| 50–1000 ms | 200 ms |

### Grabación

| Control | Qué hace | Rango válido |
|---|---|---|
| **Recording: Radio Side / Client Side** | Elige la grabación del lado del radio o del lado del cliente. Se guarda en `RecordingMode`. | Radio Side / Client Side |
| **Save to:** | Carpeta para grabaciones guardadas (solo del lado del cliente). El valor predeterminado es Documents/AetherSDR/Recordings. Se guarda en `QsoRecordingDir`. | — |
| **...** | Haga clic para explorar la carpeta de grabaciones | — |
| **Auto-record on TX** | Marque para grabar automáticamente mientras transmite. Se guarda en `QsoRecordingAutoRecord`. | On / Off |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga. Se guarda en `QsoRecordingIdleTimeout`. | 10–3600 seg (predeterminado 120) |

### NVIDIA BNR

| Control | Qué hace |
|---|---|
| **Autostart Container** | Haga clic para configurar el inicio automático del contenedor |
| **Start** | Haga clic para iniciar el contenedor de eliminación de ruido NVIDIA Broadcast |
| **Stop** | Haga clic para detener el contenedor |
| **Check Status** | Haga clic para verificar el estado del contenedor |

Un punto de estado de color indica el estado del contenedor (Running/Stopped/Unknown).

## Pestaña Filters

La pestaña **Filters** configura la nitidez de los filtros por modo.

### Nitidez de filtro

Use los controles deslizantes para **Voice**, **
