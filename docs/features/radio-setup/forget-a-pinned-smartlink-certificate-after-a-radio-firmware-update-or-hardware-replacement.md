# Referencia del diálogo de configuración de radio

El diálogo **Radio Setup** es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, configuración de red, GPS, TX, Phone/CW, RX, calibración, audio, filtros, transverters, cables USB, periféricos, APD, temas, gestión de certificados SmartLink y configuración de puertos serie.

## Abrir el diálogo

1. Haga clic en **Settings > Radio Setup...** en el menú principal.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

Muchos valores de solo lectura (número de serie, versión de hardware, opciones, modelo, detalles de suscripción, dirección IP, dirección MAC, versión de firmware) incluyen un botón de copiar al portapapeles junto a la etiqueta. Haga clic en este botón para copiar el valor a su portapapeles y compartirlo con el soporte técnico.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Radio SN | Indicador | Número de serie del chasis (solo lectura). Incluye botón de copiar al portapapeles. |
| Region | Indicador | Región regulatoria de la radio. Valor predeterminado: USA. |
| HW Version | Indicador | Cadena de versión de hardware. Incluye botón de copiar al portapapeles. |
| Remote On | Botón pulsador | Habilita el encendido remoto / remote-on. |
| Options | Indicador | Opciones de radio licenciadas. Incluye botón de copiar al portapapeles. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. |
| Model | Indicador | Modelo de la radio. Incluye botón de copiar al portapapeles. |
| Nickname | Campo de texto | Apodo de la radio fácil de usar. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa el nombre de host del sistema operativo. Se guarda en AppSettings como `StationName`. Se envía a la radio como 'client station <nombre>'. |
| License Info | Indicador | Muestra los detalles de la licencia, incluidos Subscription, Expiration, Radio ID y Licensed version. Cada campo incluye un botón de copiar al portapapeles. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Select Installer... | Botón pulsador | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae el contenido .ssdr y emite el progreso. Etiqueta cambiada desde 'Browse .ssdr...' en v26.5.3. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| Reboot Radio | Botón pulsador | Reinicia la radio conectada con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente una vez que el reinicio finaliza. Nuevo en v26.8.4 (#4448). Solo se habilita cuando está conectado y el backend admite un reinicio del cliente (por ejemplo, HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN, el operador debe reconectarse manualmente después del reinicio. |
| Agent Automation (MCP): | Botón de alternancia | Habilita el puente de automatización integrado en la aplicación para que un asistente de codificación con IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador debe aceptar. Nuevo en v26.8.4 (#3646). Se guarda mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la activación del puente independientemente de esta opción y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Campo de texto | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén secreto del sistema operativo. Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(cargando…)' hasta que se complete la lectura del llavero. |
| Copy (Access Token) | Botón pulsador | Copia el token de acceso al portapapeles. Nuevo en v26.8.4. |
| Rotate (Access Token) | Botón pulsador | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Casilla de verificación | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; el primer encendido muestra una confirmación de responsabilidad del operador. Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado en desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| Observe only: Read-only (block all driving) | Casilla de verificación | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero se rechaza todo verbo de mutación (set/invoke/connect/tune/capture). Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante | Control deslizante con ajuste a valores preestablecidos que configura el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un tamaño mayor absorbe ráfagas de panadapter/waterfall para que no se descarten paquetes. Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión en net.core.rmem_max; una etiqueta en vivo 'granted: <tamaño>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Indicador | Muestra el tamaño de búfer que el kernel realmente concedió (frente al valor preestablecido solicitado). Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay ninguna conexión activa. |

## Pestaña Network

La pestaña **Network** muestra información de red de la radio y opciones de red avanzadas.

| Control | Tipo | Descripción |
|---------|------|-------------|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |
| Enforce Private IP Connections: | Botón de alternancia | Rechaza pares que no sean RFC1918. |
| Network MTU: | Spinbox | Establece el tamaño máximo de paquete UDP VITA-49 de salida en bytes. Valor predeterminado: 1450. Rango válido: 576-9000 bytes. Se guarda en AppSettings como `NetworkMtu`. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de lat/lon/alt/hora/satélites.

## Pestaña TX

La pestaña **TX** configura los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y proporciona un acceso directo a la configuración de banda de TX.

| Control | Tipo | Descripción |
|---------|------|-------------|
| TX Band Settings | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms) | Spinbox | Tiempos de retención/retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y de accesorio. |
| Max Power: | Spinbox | Establece el límite de potencia de TX a nivel de radio. Rango válido: 0-100%. |
| Tune Mode: | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | Valor predeterminado: False. La TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante una operación de Split. Se guarda como `TxFollowsActiveSlice`. |
| Active Slice Follows TX | Botón pulsador | Valor predeterminado: False. Cambia la slice activa cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. Se guarda como `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el manipulador iambic en la radio. En v0.9.1, se agregaron los botones Mode A y Mode B junto a la opción Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el nuevo manipulador iambic de software local (IambicKeyer), que refleja el estado iambic de la radio para un tono lateral inferior a 5 ms. |
| Iambic Mode: A / B | Botón pulsador | Valor predeterminado: A. Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente agregado en v0.9.1. |
| Swap: | Botón de alternancia | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | Selecciona la banda lateral del tono CW. Opciones: LSB, USB. |
| CWX: | Botón de alternancia | Habilita el keying de macros CWX. |
| Decode: RX | Botón de alternancia | Valor predeterminado: True. Habilita la superposición de decodificación CW en el panadapter para CW recibido. Se guarda como JSON anidado bajo `CwDecoder` (campo rx). Nuevo en v26.5.3: se dividió del único conmutador CwDecodeOverlay en conmutadores RX/TX independientes. La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura. |
| Decode: TX | Botón de alternancia | Valor predeterminado: False. Decodifica el propio keying CW del operador mediante el tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Se guarda como JSON anidado bajo `CwDecoder` (campo tx). Nuevo en v26.5.3 (#2417). |
| RTTY Mark Default: | Spinbox | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña **RX** configura la calibración de compensación de frecuencia GPSDO y la fuente de referencia de 10 MHz.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | Compensación de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Valor predeterminado: Auto. Las opciones dependen del hardware instalado: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Pestaña Calibration

La pestaña **Calibration** proporciona calibración de frecuencia manual en el lado del host para radios que no pueden calibrar su propio oscilador (p. ej., HL2). Esta pestaña está oculta para radios que admiten calibración por hardware (como las radios Flex, que calibran en la pestaña RX). Nuevo en v26.8.4.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Calibration controls | Varios | Calibración de frecuencia manual en ppb/ppm para radios sin capacidad de autocalibración. La pestaña está limitada por capacidad: solo aparece cuando la radio conectada informa soporte de `hostFrequencyCalibration`. |

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo (boost), búfer, grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Descripción |
|---------|------|-------------|
| Line Out: | Control deslizante | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone: | Control deslizante | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | Silencia el altavoz frontal (según el modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Valor predeterminado: Auto. Selecciona el códec de audio para SmartLink/LAN. Se guarda como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | Valor predeterminado: False. Mantiene el sistema operativo despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se guarda como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | Selecciona los dispositivos de entrada/salida de audio del host. |
| Audio Boost: | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. Se guarda como `AudioBoost`. |
| Audio Buffer: | Campo de texto | Valor predeterminado: 200. Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Rango válido: 50-1000 ms. Se guarda como `AudioBufferMs`. Se aplica a AudioEngine::setRxBufferCapMs(). |
| Recording: Radio Side / Client Side | Botón pulsador | Valor predeterminado: Radio Side. Selecciona la grabación del lado de la radio o del lado del cliente. Se guarda como `RecordingMode`. |
| Save to: | Campo de texto
