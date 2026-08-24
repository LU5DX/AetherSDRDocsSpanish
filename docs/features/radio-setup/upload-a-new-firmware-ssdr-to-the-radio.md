# Diálogo de Configuración de Radio

Esta página documenta el diálogo de Configuración de Radio, la ventana maestra de configuración por radio en AetherSDR. Cubre información del radio, configuración de red, GPS, transmisión, Phone/CW, recepción, audio, filtros, transverters, cables USB, conexiones periféricas, gestión de certificados SmartLink, y más.

## Abriendo el diálogo de Configuración de Radio

1. Abra AetherSDR y conéctese a su radio.
2. Haga clic en **Settings > Radio Setup...**.

El diálogo se abre como una ventana persistente. Muchos valores de solo lectura (número de serie, versión de hardware, opciones, modelo, suscripción, IP, MAC, versión de firmware) incluyen un botón de copiar al portapapeles junto a la etiqueta para facilitar su compartición con soporte técnico.

## Búsqueda

El diálogo incluye un cuadro de búsqueda en la parte superior. Mientras escribe, las páginas y controles coincidentes se resaltan y las filas no coincidentes se ocultan. La búsqueda no distingue entre mayúsculas y minúsculas y coincide con palabras clave que describen cada control.

## Pestaña Radio

La pestaña Radio contiene información del radio, identificación, información de licencia y controles de actualización de firmware.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). Muestra el número de serie del chasis si está disponible; de lo contrario, el número de serie del radio. Muestra una raya (`—`) si no se reporta ningún valor. Aparece un pequeño botón de copiar junto al valor al pasar el cursor o enfocar; haga clic en él para copiar el número de serie al portapapeles. |
| **Region** | Indicador | Región regulatoria del radio (predeterminado: USA). |
| **HW Version** | Indicador | Cadena de versión de hardware. Muestra una raya (`—`) si está vacía, con prefijo `v` si no tiene `v` inicial. Hay un botón de copiar disponible. |
| **Model** | Indicador | Modelo del radio. Hay un botón de copiar disponible. |
| **Nickname** | Campo de texto | Apodo amigable del radio para el usuario. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Se predetermina al nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía al radio como `client station <name>`. |
| **Remote On** | Botón | Habilita el encendido remoto / remote-on. |
| **Options** | Indicador | Muestra las opciones licenciadas del radio. Muestra la cadena de opciones reportada por el radio o, si está vacía, inserta valores predeterminados sensatos (p. ej., `GPS, PGXL` si el radio tiene un amplificador; de lo contrario, `GPS`). Hay un botón de copiar disponible. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado habilitado de multiFLEX. |
| **License Info** | Indicador | Muestra los detalles de licencia (Subscription / Expiration / Radio ID / Licensed version) del radio. Cada campo incluye un botón de copiar al portapapeles. |
| **Check for Update** | Botón | Consulta actualizaciones de firmware disponibles. Si se encuentra una actualización, el área de estado muestra la versión disponible e instruye a descargar el instalador de SmartSDR desde flexradio.com, luego usar **Select Installer...** para prepararlo. |
| **Select Installer...** | Botón | Abre un diálogo de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Se muestra un mensaje de estado mientras se prepara el archivo. Renombrado de **Browse .ssdr...** en v26.5.3. |
| **Upload Firmware** | Botón | Inicia la carga usando el archivo preparado por **Select Installer...**. Aparecen una barra de progreso y texto de estado debajo, que se actualizan a medida que avanza la transferencia. |
| **Reboot Radio** | Botón | Reinicia el radio conectado con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente cuando el arranque finaliza. En conexiones SmartLink/WAN, debe reconectarse manualmente. El botón solo está habilitado cuando está conectado y el backend admite un reinicio del cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). Nuevo en v26.8.4 (#4448). |

### Estado del firmware

Debajo del botón **Upload Firmware**, aparece un área de estado cuando comienza una carga de firmware. Muestra el progreso y el texto de resultado a medida que avanza la transferencia.

## Pestaña Network

La pestaña Network contiene información de red del radio y opciones de red avanzadas.

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |
| **Enforce Private IP Connections:** | Alternador | Rechaza pares no RFC1918. Predeterminado: habilitado. |
| **Agent Automation (MCP):** | Alternador | Habilita el puente de automatización en la aplicación para que un asistente de codificación por IA (a través del servidor MCP) pueda inspeccionar y manejar la aplicación en ejecución. Desactivado por defecto; el operador decide activarlo. Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento `AETHER_AUTOMATION` fuerza la habilitación del puente independientemente de este alternador y deshabilita el control en la interfaz. La activación de transmisión permanece bloqueada a menos que se establezca `AETHER_AUTOMATION_ALLOW_TX`. |
| **Access Token:** | Campo de texto | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se almacena en el almacén secreto del SO. Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador de posición `(loading…)` hasta que se lea el llavero. |
| **Copy (Access Token)** | Botón | Copia el token de acceso al portapapeles. Nuevo en v26.8.4. |
| **Rotate (Access Token)** | Botón | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. Nuevo en v26.8.4. |
| **Allow TX via MCP: Enable transmit control** | Casilla de verificación | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador. Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por `AETHER_AUTOMATION_ALLOW_TX` (fuerza activación) y `AETHER_AUTOMATION_NO_TX` (fija desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| **Observe only: Read-only (block all driving)** | Casilla de verificación | Hace que el puente sea solo de observación: los clientes MCP pueden leer el estado, pero cada verbo mutador (set/invoke/connect/tune/capture) es rechazado. Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede eludirlo. La variable de lanzamiento `AETHER_AUTOMATION_READONLY` lo fija activado para ejecuciones headless/CI. |
| **VITA-49 RX buffer:** | Control deslizante | Control deslizante con ajuste a valores predefinidos que establece el buffer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. Nuevo en v26.8.4 (#3810). Predefinidos de 256 KB a 4 MB. El sistema limita la concesión en `net.core.rmem_max`; una etiqueta en vivo **granted:** muestra lo que el kernel realmente concedió. |
| **granted: (VITA-49 RX buffer)** | Indicador | Muestra el tamaño de buffer que el kernel realmente concedió (vs. el predefinido solicitado). Nuevo en v26.8.4. Muestra `(applies on connect)` cuando no hay conexión activa. |
| **Network MTU:** | Cuadro de giro | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576-9000). El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Alternador | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | Campos de configuración de IP estática. |
| **Apply** | Botón | Envía la configuración de red al radio. |

## Pestaña Calibration

La pestaña Calibration proporciona calibración de frecuencia manual para radios que no pueden calibrar su propio oscilador (como HL2). Está oculta a menos que el backend del radio conectado reporte que admite calibración de frecuencia del lado del host.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de giro | Frecuencia utilizada para la calibración manual. |
| **Start** | Botón | Inicia el barrido de calibración de frecuencia. |
| **Freq Offset (ppb):** | Cuadro de giro | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (Auto, TCXO, GPSDO, External). El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro y se actualiza en vivo. |

Los valores de calibración se releen cada vez que se muestra el diálogo o cambia el estado de la conexión, de modo que una pulsación de Trim nunca puede confirmar un número de calibración de un radio diferente.

## Pestaña GPS

| Control | Tipo | Comportamiento |
|---|---|---|
| GPS info | Indicador | Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites. |

## Pestaña TX

La pestaña TX contiene tiempos de transmisión, interbloqueos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y un acceso directo a la Configuración de Banda TX.

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Band Settings** | Botón | Abre el diálogo dedicado de potencia/sintonía por banda. |
| **Timings (in ms)** | Cuadro de giro | Tiempos de retención/retardo de TX. |
| **ACC TX:** | Campo de texto | Retardo de transmisión ACC en milisegundos. Rango 0-5000 ms. |
| **TX Delay:** | Campo de texto | Retardo de TX en milisegundos. Rango 0-5000 ms. |
| **RCA TX1:** | Campo de texto | Retardo RCA TX1 en milisegundos. Rango 0-5000 ms. |
| **Timeout (sec):** | Campo de texto | Tiempo de espera de interbloqueo en segundos. El radio almacena este valor en milisegundos internamente. Rango 0-3600 segundos. |
| **TX2:** | Campo de texto | Retardo TX2 en milisegundos. Rango 0-5000 ms. |
| **Interlocks - TX REQ: RCA / Accessory** | Alternador | Habilita las entradas de interbloqueo RCA y de accesorio. |
| **Max Power:** | Cuadro de giro | Establece el límite de potencia TX a nivel de radio (0-100%). |
| **Tune Mode:** | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** | Alternador | Dibuja la señal TX en el waterfall. |
| **TX Follows Active Slice** | Botón | La TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |

## Pestaña Phone/CW

La pestaña Phone/CW contiene valores predeterminados de micrófono, manipulador CW y RTTY.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Alternador | Muestra el medidor de nivel de micrófono incluso en RX. |
| **Iambic:** | Alternador | Habilita o deshabilita el manipulador iambic en el radio. |
| **Iambic Mode: A / B** | Botón | Selecciona el modo iambic Curtis A o B tanto para el radio como para el manipulador de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Swap:** | Alternador | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB | USB). |
| **CWX:** | Alternador | Habilita la activación por macros CWX. |
| **Decode: RX** | Alternador | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Predeterminado: True. Se almacena en AppSettings como JSON anidado bajo `CwDecoder` (campo rx). Nuevo en v26.5.3: dividido del alternador único CwDecodeOverlay en alternadores RX/TX independientes. La clave legacy `CwDecodeOverlay` se migra automáticamente en la primera lectura. |
| **Decode: TX** | Alternador | Decodifica la propia activación CW del operador mediante tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Predeterminado: False. Se almacena en AppSettings como JSON anidado bajo `CwDecoder` (campo tx). Nuevo en v26.5.3 (#2417). |
| **RTTY Mark Default:** | Cuadro de giro | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX contiene calibración de desplazamiento de frecuencia GPSDO y configuración de la fuente de referencia de 10 MHz.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de giro | Frecuencia utilizada para la calibración manual. |
| **Start** | Botón | Inicia el barrido de calibración de frecuencia. |
| **Freq Offset (ppb):** | Cuadro de giro | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (Auto, TCXO, GPSDO, External). El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro y se actualiza en vivo. |

## Pestaña Antennas

La pestaña Antennas proporciona edición de nombres de visualización por puerto de antena para el radio. Permite asignar nombres personalizados a cada puerto
