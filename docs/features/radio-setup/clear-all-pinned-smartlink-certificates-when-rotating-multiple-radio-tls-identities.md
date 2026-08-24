# Diálogo de Configuración de Radio

El diálogo **Configuración de Radio** es la ventana maestra de configuración por radio. Contiene información del radio, configuración de red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, puerto serie de periféricos, gestión de certificados fijos de SmartLink y configuración de receptores públicos KiwiSDR.

## Abrir el diálogo

1. Haga clic en **Settings > Radio Setup...** en el menú principal.

## Radio (pestaña)

La pestaña Radio muestra la identificación del radio, información de licencia y proporciona controles de actualización de firmware.

### Indicadores de solo lectura con botones de copiar

Todos los campos de solo lectura incluyen un botón de copiar al portapapeles (icono de bandeja) junto a la etiqueta para facilitar su uso compartido con soporte técnico.

| Control | Comportamiento |
|---------|----------|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copiar al portapapeles. |
| **Region** | Región regulatoria del radio (solo lectura). Incluye un botón de copiar al portapapeles. |
| **HW Version** | Cadena de versión de hardware (solo lectura). Incluye un botón de copiar al portapapeles. |
| **Options** | Muestra las opciones licenciadas del radio (solo lectura). Incluye un botón de copiar al portapapeles. |
| **Model** | Modelo del radio (solo lectura). Incluye un botón de copiar al portapapeles. |
| **Campos de License Info** | Muestra Suscripción, Expiración, ID de Radio y Versión licenciada. Cada uno incluye un botón de copiar al portapapeles. |

### Otros controles en la pestaña Radio

| Control | Comportamiento | Clave de configuración |
|---------|----------|-------------|
| **FlexControl** | Estado detectado del hardware FlexControl. | (ninguna) |
| **multiFLEX** | Estado de habilitación de multiFLEX. | (ninguna) |
| **Nickname** | Apodo amigable del radio. | (ninguna) |
| **Callsign** | Indicativo de la estación. | (ninguna) |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa el nombre de host del sistema operativo. | `StationName` |
| **Remote On** | Habilita activación remota / encendido remoto. | (ninguna) |
| **Check for Update** | Consulta actualizaciones de firmware. | (ninguna) |
| **Select Installer...** | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. | (ninguna) |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. | (ninguna) |
| Reboot Radio | Reinicia el radio conectado con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente cuando el arranque finaliza. | Nuevo en v26.8.4 (#4448). Solo se habilita cuando está conectado y el backend admite reinicio por cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente después del reinicio. |
| Agent Automation (MCP): | Habilita el puente de automatización dentro de la aplicación para que un asistente de codificación de IA (mediante el servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador debe optar por activarlo. | Nuevo en v26.8.4 (#3646). Se conserva mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. La activación de transmisión permanece bloqueada a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén de secretos del sistema operativo. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. El marcador '(loading…)' aparece hasta que se completa la lectura del llavero. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Es anulado por AETHER_AUTOMATION_ALLOW_TX (forzado activado) y AETHER_AUTOMATION_NO_TX (fijado desactivado). Un vigilante de desactivación forzada limita la transmisión originada por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea solo de observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) es rechazado. | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante de ajuste predefinido que establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de transmisión VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | Nuevo en v26.8.4 (#3810). Valores predefinidos de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de búfer que el kernel realmente concedió (en comparación con el valor predefinido solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay una conexión activa. |

## Calibration (pestaña)

Nuevo en v26.8.4. Calibración manual de frecuencia para radios que no pueden calibrarse a sí mismos (HL2 y cualquier otro backend cuya capacidad `hostFrequencyCalibration` sea falsa). La pestaña está oculta para radios que manejan su propia calibración del oscilador (p. ej., Flex, que usa la calibración de hardware de la pestaña Receive).

La pestaña se habilita según la capacidad del radio, no según el nombre de la familia: si el radio corrige su propio oscilador, la página permanece oculta. El título de la página se puede buscar con palabras clave como "frequency calibration ppb ppm oscillator crystal clock error wwv gpsdo zero beat."

El valor de calibración almacenado se vuelve a leer cada vez que se abre el diálogo (de modo que una llamada al puente `freqcal` realizada mientras el diálogo estaba cerrado se refleje) y cada vez que se conecta un radio diferente, de modo que una pulsación posterior de **Trim** no pueda confirmar el número del radio anterior.

| Control | Comportamiento |
|---------|----------|
| **Página Calibration** | Calibración manual de desviación de frecuencia del oscilador para radios sin calibración integrada. Se muestra solo cuando el backend conectado informa `hostFrequencyCalibration`. |

## Network (pestaña)

Configuración avanzada de red para el radio.

| Control | Comportamiento | Clave de configuración |
|---------|----------|-------------|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. | (ninguna) |
| **Enforce Private IP Connections:** | Rechaza pares no RFC1918. El botón de alternancia muestra "Enabled" cuando está marcado. | (ninguna) |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576-9000). Valor predeterminado 1450. | `NetworkMtu` |
| **DHCP / Static** | Alterna entre modos DHCP e IP estática. | (ninguna) |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática (se muestran cuando está seleccionado el modo Static). | (ninguna) |
| **Apply** | Envía la configuración de red al radio. | (ninguna) |
| **Reboot Radio** | Abre un diálogo de confirmación antes de reiniciar el radio. AetherSDR se desconecta y, para conexiones LAN, se reconecta automáticamente después de que el radio arranca. SmartLink/WAN requiere reconexión manual. El botón está deshabilitado cuando el radio está desconectado. | (ninguna) |

## GPS (pestaña)

Muestra la presencia de GPS e información en vivo de ubicación/hora/satélites.

## TX (pestaña)

Configuración de transmisión que incluye temporizaciones, enclavamientos, límites de potencia y comportamiento de seguimiento de slice.

| Control | Comportamiento | Clave de configuración |
|---------|----------|-------------|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | (ninguna) |
| **Timings (in ms)** | Temporizaciones de retención/retardo de TX. | (ninguna) |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y de accesorio. | (ninguna) |
| **Max Power:** | Establece el límite máximo de potencia de TX a nivel de radio (0-100%). | (ninguna) |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | (ninguna) |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | (ninguna) |
| **TX Follows Active Slice** | TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante operación Split. | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | `ActiveFollowsTxSlice` |

## Phone/CW (pestaña)

Valores predeterminados de micrófono, manipulador CW y RTTY.

| Control | Comportamiento | Clave de configuración |
|---------|----------|-------------|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | (ninguna) |
| **Iambic:** | Habilita o deshabilita el manipulador iambic en el radio. | (ninguna) |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para el radio como para el manipulador de software local. Par mutuamente excluyente. | (ninguna) |
| **Swap:** | Intercambia dit/dah. | (ninguna) |
| **Sideband:** | Selecciona la banda lateral del tono CW (LSB/USB). | (ninguna) |
| **CWX:** | Habilita la activación por macros CWX. | (ninguna) |
| **Decode: RX** | Habilita la superposición de decodificación CW en el panadapter para CW recibido. | `CwDecoder` (JSON anidado, campo `rx`) |
| **Decode: TX** | Decodifica la propia manipulación CW del operador mediante tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. | `CwDecoder` (JSON anidado, campo `tx`) |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. | (ninguna) |

## RX (pestaña)

Calibración de desviación de frecuencia GPSDO y fuente de referencia de 10 MHz.

| Control | Comportamiento |
|---------|----------|
| **Cal Frequency (MHz):** | Frecuencia utilizada para calibración manual. |
| **Start** | Inicia el barrido de calibración de frecuencia. |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en ppb. |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador (Auto/TCXO/GPSDO/External). El estado de bloqueo se muestra al lado. |

## Antennas (pestaña)

Editor de nombre de visualización de antenas por puerto para el radio. Permite al operador asignar nombres personalizados a cada puerto de antena (ANT1, ANT2, XVTA, XVTB, etc.) que se muestran en los indicadores de antena RX/TX del panadapter en lugar de los tokens de puerto sin procesar.

| Control | Comportamiento |
|---------|----------|
| **Port / Custom name / Preview / Clear** (columnas de tabla) | Cuadrícula de filas de puertos de antena. Cada fila tiene una etiqueta de puerto de solo lectura (p. ej., ANT1), un campo de texto editable (máx. 16 caracteres), una vista previa del nombre de visualización final y un botón Clear para restablecer el nombre personalizado. |

## Audio (pestaña)

Salidas de audio del radio, compresión, dispositivos de PC, realce, búfer, grabación y contenedor NVIDIA BNR.

| Control | Comportamiento | Clave de configuración |
|---------|----------|-------------|
| **Line Out:** | Control deslizante de ganancia de salida de línea. | (ninguna) |
| **Mute (Line Out)** | Silencia la salida de línea. | (ninguna) |
| **Headphone:** | Control deslizante de ganancia de auriculares. | (ninguna) |
| **Mute (Headphone)** | Silencia los auriculares. | (ninguna) |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | (ninguna) |
| **Audio Compression (SmartLink):** | Selecciona el códec de audio para SmartLink/LAN (Auto/Uncompressed/Opus). | `AudioCompression` |
| **Prevent system sleep while connected** | Mantiene el sistema operativo despierto mientras el radio está conectado. | `InhibitSleepWhileConnected` |
| **PC Audio Devices: Input: / Output:** | Selecciona los dispositivos de audio de entrada/salida del host. | (ninguna) |
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para el jitter de VPN/SmartLink (50-1000 ms). Valor predeterminado 200. | `AudioBufferMs` |
| **Recording: Radio Side / Client Side** | Selecciona grabación del lado del radio o del lado del cliente. | `RecordingMode` |
| **Save to:** | Carpeta para grabaciones guardadas (solo lado del cliente). Valor predeterminado Documents/AetherSDR/Recordings. | `QsoRecordingDir` |
| **...** | Explora en busca de la carpeta de grabación. | (ninguna) |
| **Auto-record on** | (continuación de la tabla anterior) |
