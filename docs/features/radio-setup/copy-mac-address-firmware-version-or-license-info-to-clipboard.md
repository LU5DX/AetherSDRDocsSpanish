# Configuración de la radio

El cuadro de diálogo **Radio Setup** es la ventana principal de configuración por radio. Proporciona acceso a la información de la radio, configuración de red, GPS, configuración de TX/Teléfono/CW/RX, audio, filtros, transvertidores, cables USB, periféricos y gestión de certificados fijos de SmartLink.

Ábralo desde el menú: `Settings > Radio Setup...`.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Para modificar configuraciones a nivel de radio, conéctese primero a la radio.
- El cuadro de diálogo es un singleton persistente: cerrarlo conserva sus cambios; volver a abrirlo muestra el estado actual.

## Qué hace cada sección/pestaña

### Radio (pestaña)

Información de la radio, identificación, información de licencia y actualización de firmware.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **Radio SN** | — | Número de serie del chasis (solo lectura). | Incluye un botón de copiar al portapapeles junto al valor. |
| **Region** | USA | Región regulatoria de la radio. | Solo lectura. |
| **HW Version** | — | Cadena de versión de hardware. | Incluye un botón de copiar al portapapeles junto al valor. |
| **Remote On** | — | Habilita el encendido remoto / remote-on. | Botón pulsador. |
| **Options** | — | Muestra las opciones de radio licenciadas. | Incluye un botón de copiar al portapapeles junto al valor. |
| **FlexControl** | — | Estado detectado del hardware FlexControl. | Indicador. |
| **multiFLEX** | — | Estado de habilitación de multiFLEX. | Indicador. |
| **Reboot Radio** | — | Reinicia la radio conectada con un cuadro de diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente una vez que finaliza el arranque. | Nuevo en v26.8.4 (#4448). Solo habilitado cuando está conectado y el backend admite un reinicio del cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente después del reinicio. |
| **Model** | — | Modelo de la radio. | Incluye un botón de copiar al portapapeles junto al valor. |
| **Nickname** | — | Apodo amigable de la radio. | Campo de texto. |
| **Callsign** | — | Indicativo de la estación. | Campo de texto. |
| **Station Name** | — | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa el nombre de host del sistema operativo por defecto. | Se almacena en AppSettings (`StationName`). Se envía a la radio como 'client station <name>'. |
| **License Info** (Subscription / Expiration / Radio ID / Licensed version) | — | Muestra los detalles de licencia de la radio. | Cada campo (Subscription, Expiration, Radio ID, Licensed version) incluye un botón de copiar al portapapeles junto al valor. |
| **Check for Update** | — | Consulta actualizaciones de firmware. | Botón pulsador. |
| **Select Installer...** | — | Abre un cuadro de diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae la carga útil .ssdr y emite el progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| **Upload Firmware** | — | Inicia la carga del firmware con barra de progreso y estado. | Botón pulsador. |

### Network (pestaña)

Información de red de la radio y opciones de red avanzadas.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **IP Address / Mask / MAC Address** | — | Direcciones de red de solo lectura. | Cada una incluye un botón de copiar al portapapeles. |
| **Enforce Private IP Connections:** | — | Rechaza pares que no sean RFC1918. | Botón de alternancia. |
| **Agent Automation (MCP):** | Disabled | Habilita el puente de automatización dentro de la aplicación para que un asistente de codificación con IA (mediante el servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador opta por habilitarlo. | Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento `AETHER_AUTOMATION` fuerza la habilitación del puente independientemente de esta alternancia y deshabilita el control en la interfaz. La activación de transmisión permanece bloqueada a menos que se establezca `AETHER_AUTOMATION_ALLOW_TX`. |
| **Access Token:** | (ninguno) | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se almacena en el almacén de secretos del sistema operativo. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que se lea el llavero. |
| **Copy (Access Token)** | — | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| **Rotate (Access Token)** | — | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| **Allow TX via MCP: Enable transmit control** | False | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Es anulado por `AETHER_AUTOMATION_ALLOW_TX` (forzado a activado) y `AETHER_AUTOMATION_NO_TX` (fijado en desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| **Observe only: Read-only (block all driving)** | False | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) es rechazado. | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento `AETHER_AUTOMATION_READONLY` lo fija en activado para ejecuciones headless/CI. |
| **VITA-49 RX buffer:** | 4 MB | Control deslizante con ajuste a valores preestablecidos que define el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas del panadapter/waterfall para que no se pierdan paquetes. | Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a `net.core.rmem_max`; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| **granted: (VITA-49 RX buffer)** | — | Muestra el tamaño de búfer que el kernel realmente concedió (frente al valor preestablecido solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |
| **Network MTU:** | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576-9000). | El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings (`NetworkMtu`). |
| **DHCP / Static** | — | Cambia entre los modos DHCP e IP estática. | Botón de alternancia. |
| **IP Address: / Mask: / Gateway:** | — | Campos de configuración de IP estática. | Campos de texto. |
| **Apply** | — | Envía la configuración de red a la radio. | Botón pulsador. |

### GPS (pestaña)

Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites.

### TX (pestaña)

Tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y acceso directo a TX Band Settings.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **TX Band Settings** | — | Abre el cuadro de diálogo dedicado de potencia/sintonía por banda. | Botón pulsador. |
| **Timings (in ms)** | — | Tiempos de retención/demora de TX. | Spinbox. |
| **Interlocks - TX REQ: RCA / Accessory** | — | Habilita las entradas de enclavamiento RCA y de accesorio. | Botón de alternancia. |
| **Max Power:** | — | Establece el límite de potencia de TX a nivel de radio (0-100 %). | Spinbox. |
| **Tune Mode:** | — | Selecciona cómo se comporta el botón de sintonía. | Cuadro combinado. |
| **Show TX in Waterfall:** | — | Dibuja la señal de TX en el waterfall. | Botón de alternancia. |
| **TX Follows Active Slice** | False | TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. | Se deshabilita automáticamente durante la operación Split. Se almacena en AppSettings (`TxFollowsActiveSlice`). |
| **Active Slice Follows TX** | False | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | Se almacena en AppSettings (`ActiveFollowsTxSlice`). |

### Phone/CW (pestaña)

Micrófono, manipulador CW, valores predeterminados de RTTY.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | — | Muestra el medidor de nivel de micrófono incluso en RX. | Botón de alternancia. |
| **Iambic:** | Enabled | Habilita o deshabilita el manipulador iambic en la radio. | Botón de alternancia. En v0.9.1, se agregaron los botones Mode A y Mode B junto a la alternancia Enabled. Mode A = Curtis A; Mode B = Curtis B. También controlan el manipulador iambic de software local (IambicKeyer), que refleja el estado iambic de la radio para un tono lateral de menos de 5 ms. |
| **Iambic Mode: A / B** | A | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. | Par mutuamente excluyente agregado en v0.9.1. Botones pulsadores. |
| **Swap:** | — | Intercambia dit/dah. | Botón de alternancia. |
| **Sideband:** | LSB/USB | Selecciona la banda lateral del tono CW. | Cuadro combinado. |
| **CWX:** | — | Habilita el keying de macros CWX. | Botón de alternancia. |
| **Decode: RX** | True | Habilita la superposición de decodificación CW en el panadapter para CW recibido. | Nuevo en v26.5.3: separado de la alternancia única CwDecodeOverlay en alternancias independientes RX/TX. Se persiste como blob JSON anidado bajo `CwDecoder` con campos `rx` y `tx`. La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura. |
| **Decode: TX** | False | Decodifica el keying CW del propio operador mediante tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. | Nuevo en v26.5.3 (#2417). |
| **RTTY Mark Default:** | — | Frecuencia de marca RTTY predeterminada. | Spinbox. |

### RX (pestaña)

Calibración de desviación de frecuencia GPSDO y fuente de referencia de 10 MHz.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **Cal Frequency (MHz):** | — | Frecuencia utilizada para la calibración manual. | Spinbox. |
| **Start** | — | Inicia el barrido de calibración de frecuencia. | Botón pulsador. |
| **Freq Offset (ppb):** | — | Desviación de frecuencia manual en ppb. | Spinbox. |
| **10 MHz Reference Source:** | Auto | Selecciona la fuente de referencia del oscilador (Auto / TCXO / GPSDO / External). Las opciones mostradas dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto y se actualiza en vivo. |

### Calibration (pestaña)

Calibración de frecuencia para radios que no pueden autocalibrarse (p. ej., HL2). Solo se muestra cuando el backend conectado admite calibración de frecuencia del lado del host.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **Calibration (tab)** | — | Calibración de frecuencia manual con barrido de medición. | Nuevo en v26.8.4. Oculto a menos que el backend anuncie la capacidad `hostFrequencyCalibration` (una radio Flex usa su propia calibración de hardware en la página RX). Vuelve a leer la calibración almacenada cada vez que se abre el cuadro de diálogo o cambia la radio conectada, para que un comando de ajuste posterior no pueda confirmar el número de una radio anterior. |

### Antennas (pestaña)

Editor de nombres de visualización por puerto de antena para la radio. Permite al operador asignar nombres personalizados a cada puerto de antena (ANT1, ANT2, XVTA, XVTB, etc.) que se muestran en los indicadores de antena RX/TX del panadapter en lugar de los tokens de puerto originales.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **Port / Custom name / Preview / Clear** | — | Cuadrícula de filas de puertos de antena. Cada fila tiene una etiqueta de puerto de solo lectura (p. ej., ANT1), un campo de texto editable (máx. 16 caracteres), una vista previa del nombre de visualización final y un botón Clear para restablecer el nombre personalizado. | Las filas se actualizan automáticamente cuando cambian las asignaciones de antena de la slice. Los puertos se obtienen de RadioModel::knownAntennaTokens(). Se construyen de forma diferida al primer clic. Cuando el nombre personalizado de un puerto está vacío, se usa el token de puerto original como nombre de visualización. |

### Audio (pestaña)

Salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y contenedor NVIDIA BNR.

| Control | Predeterminado | Comportamiento | Notas |
|---|---|---|---|
| **Line Out:** | — | Ganancia de salida de línea. | Control deslizante. |
| **Mute (Line Out)** | — | Silencia la salida de línea. | Botón pulsador. |
| **Headphone:** | — | Ganancia de auriculares. | Control deslizante. |
| **Mute (Headphone)** | — | Silencia los auriculares. | Botón pulsador. |
| **Front Speaker: / Mute** | — | Silencia el altavoz frontal (según el modelo). | Botón pulsador. |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Auto | Selecciona el códec de audio para SmartLink/LAN. | Se almacena en AppSettings (`AudioCompression`). |
| **Prevent system sleep while connected
