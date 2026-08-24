# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información del radio, configuración de red, GPS, configuración de transmisión, ajustes de Phone/CW, calibración de recepción, nombres de antenas, filtros, transverters, cables USB, periféricos, Pre-Distorsión Adaptativa (APD), temas, gestión de certificados SmartLink y configuración del puerto serie para FlexControl.

## Antes de comenzar

- AetherSDR debe estar conectado al radio para acceder a las pestañas que se comunican con el radio.
- Algunas pestañas (APD, Themes, Calibration, SmartLink, Serial) se construyen de forma diferida al hacer clic por primera vez.
- La pestaña APD solo es visible en radios de la serie FLEX-8x00 con firmware SmartSDR 4.2.18 o posterior.
- La pestaña Calibration solo es visible cuando el radio conectado no puede calibrar su propio oscilador (p. ej. HL2). Los radios Flex gestionan la calibración en la pestaña RX.

## Apertura del diálogo

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo de Configuración de Radio.

## Comportamiento general del diálogo

- El diálogo recuerda su tamaño y posición entre sesiones.
- Orden de pestañas de izquierda a derecha: Radio, Network, GPS, TX, Phone/CW, RX, Calibration, Antennas, Audio, Filters, XVTR, USB Cables, Peripherals, APD, Themes, SmartLink, Serial.
- Las pestañas cuyo contenido puede exceder la altura del diálogo (Themes, Audio, Filters, Peripherals en pantallas pequeñas o de alta densidad de píxeles) están envueltas en un área de desplazamiento para que el diálogo nunca crezca más allá del borde de la pantalla.
- Haga clic en **Close** para cerrar el diálogo.

## Pestaña Radio

Muestra la identificación del radio, información de licencia y controles de actualización de firmware. Incluye un botón **Reboot Radio**.

### Pasos

1. Haga clic en la pestaña **Radio**.
2. Consulte los indicadores de solo lectura para **Radio SN**, **Region**, **HW Version**, **Model**, **Options**, **FlexControl**, **multiFLEX** y **License Info** (Subscription, Expiration, Radio ID, Licensed version). Cada indicador de solo lectura incluye un botón de copia al portapapeles junto a la etiqueta: haga clic para copiar el valor al portapapeles.
3. Opcionalmente, establezca un **Nickname**, **Callsign** o **Station Name** en los campos de texto. El **Station Name** identifica a este cliente AetherSDR ante otras estaciones multiFLEX; si está vacío, se utiliza el nombre de host del sistema operativo por defecto. Se almacena en AppSettings como `StationName`.
4. Haga clic en **Remote On** para habilitar el encendido remoto/remote-on.
5. Para reiniciar el radio:
   - Haga clic en **Reboot Radio**. Aparece un diálogo de confirmación.
   - En conexiones LAN, AetherSDR se reconecta automáticamente cuando el radio termina de arrancar.
   - En conexiones SmartLink/WAN, debe reconectarse manualmente después de que el radio arranque.
   - El botón está deshabilitado cuando el radio está desconectado o cuando el backend no admite un reinicio del cliente (p. ej. HL2 es solo RX, por lo que el botón está deshabilitado). Se vuelve a habilitar automáticamente cuando el radio se reconecta.
6. Para actualizar el firmware:
   - Haga clic en **Check for Update** para consultar el servidor de actualizaciones de FlexRadio.
   - Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
   - Haga clic en **Select Installer...** para abrir un selector de archivos. Seleccione el instalador o un archivo `.ssdr` preextraído.
   - Cuando el preparado esté completo, haga clic en **Upload Firmware** para transferir el firmware al radio.

### Notas sobre la actualización de firmware

- La etiqueta del botón **Select Installer...** cambió desde **Browse .ssdr...** en v26.5.3.
- El botón acepta archivos `.msi`, `.exe` y `.ssdr`.
- El preparador detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas.
- Una barra de progreso y una etiqueta de estado rastrean la carga.

## Pestaña Network

Configure cómo el radio obtiene su dirección de red y opciones avanzadas de red.

### Pasos

1. Haga clic en la pestaña **Network**.
2. Tenga en cuenta los indicadores de solo lectura **IP Address**, **Mask** y **MAC Address**. Cada uno incluye un botón de copia al portapapeles.
3. Alterne **Enforce Private IP Connections:** para rechazar pares no RFC1918.
4. Configure el puente de Automatización de Agente (MCP):
   - Alterne **Agent Automation (MCP):** para habilitar el puente de automatización integrado, de modo que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador se adhiere voluntariamente. Se conserva mediante AutomationBridgeSettings.
   - El campo **Access Token:** muestra el token de acceso MCP (solo lectura). Péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se almacena en el almacén de secretos del sistema operativo.
   - Haga clic en **Copy** para copiar el token de acceso al portapapeles.
   - Haga clic en **Rotate** para generar un nuevo token y aplicarlo inmediatamente, bloqueando a cualquier cliente que aún use el anterior.
   - Marque **Allow TX via MCP: Enable transmit control** para permitir que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador.
   - Marque **Observe only: Read-only (block all driving)** para que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) se rechaza. Se aplica en la aplicación, por lo que un cliente no puede omitirlo.
5. Configure **VITA-49 RX buffer:** como un control deslizante de ajuste a ajuste preestablecido (256 KB a 4 MB, predeterminado 4 MB). Esto establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; los valores más grandes absorben ráfagas del panadapter/waterfall para que no se pierdan paquetes. El sistema limita la concesión a `net.core.rmem_max`.
   - La etiqueta **granted:** muestra el tamaño de búfer que el kernel realmente concedió (frente al preestablecido solicitado). Muestra "(applies on connect)" cuando no hay conexión activa.
6. Configure **Network MTU:** como un valor de cuadro de giro (576-9000 bytes, predeterminado 1450). Esto establece el tamaño máximo de paquete UDP VITA-49 saliente. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`.
7. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo.
8. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:**.
9. Haga clic en **Apply** para enviar la configuración de red al radio.
10. Reconéctese al radio en su nueva dirección usando `Settings > Connect to Radio...`.

### Notas sobre la Automatización de Agente (MCP)

- La variable de entorno de lanzamiento `AETHER_AUTOMATION` fuerza la habilitación del puente independientemente del alternador y deshabilita el control en la interfaz.
- La activación de transmisión permanece bloqueada a menos que se establezca `AETHER_AUTOMATION_ALLOW_TX`.
- `AETHER_AUTOMATION_ALLOW_TX` fuerza la habilitación de TX; `AETHER_AUTOMATION_NO_TX` lo fija en desactivado.
- `AETHER_AUTOMATION_READONLY` fija el modo de solo observación para ejecuciones headless/CI.
- Un vigilante de desactivación forzada limita la TX originada por el puente.
- El campo Access Token genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. El marcador de posición muestra "(loading…)" hasta que se lee el llavero.

## Pestaña GPS

Muestra la información GPS del radio.

- Muestra el estado de presencia del GPS.
- Muestra latitud, longitud, altitud, hora y número de satélites en vivo.
- Indicadores de solo lectura.

## Pestaña TX

Configure la temporización de transmisión, interbloqueos, límites de potencia y comportamiento.

### Pasos

1. Haga clic en la pestaña **TX**.
2. Ajuste los cuadros de giro **Timings** para ACC TX, TX Delay, RCA TX1, Timeout y TX2 en milisegundos.
   - **Timeout (sec):** Se muestra en segundos enteros; el radio lo almacena en milisegundos internamente.
3. Alterne **Interlocks - TX REQ: RCA / Accessory** para habilitar las entradas de interbloqueo.
4. Establezca **Max Power:** como porcentaje (0-100%).
5. Seleccione **Tune Mode:** en el cuadro combinado.
6. Alterne **Show TX in Waterfall:** para mostrar la señal de TX en el waterfall.
7. Configure el seguimiento de slice:
   - **TX Follows Active Slice:** Botón pulsador (predeterminado False). Se almacena como `TxFollowsActiveSlice`. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split.
   - **Active Slice Follows TX:** Botón pulsador (predeterminado False). Se almacena como `ActiveFollowsTxSlice`. Cambia el slice activo cuando la TX se mueve externamente (p. ej. WSJT-X o CAT).
8. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

## Pestaña Phone/CW

Configure el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Pasos

1. Haga clic en la pestaña **Phone/CW**.
2. Alterne **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel de micrófono incluso en RX.
3. Configure los ajustes de CW:
   - **Iambic:** Alterne para habilitar o deshabilitar el manipulador iambic en el radio. Mutuamente excluyente con el manipulador iambic del lado del radio; también controla el manipulador iambic de software local para tono lateral inferior a 5 ms.
   - **Iambic Mode: A / B:** Seleccione el modo iambic Curtis A o B. Se aplica tanto al radio como al manipulador de software local.
   - **Swap:** Alterne para intercambiar punto/raya.
   - **Sideband:** Seleccione LSB o USB para el tono CW.
   - **CWX:** Alterne para habilitar el tecleo por macros CWX.
   - **Decode: RX:** Alterne (predeterminado True) para habilitar la superposición de decodificación CW en el panadapter para CW recibido. Se almacena como un blob JSON anidado bajo `CwDecoder` con un campo `rx`.
   - **Decode: TX:** Alterne (predeterminado False) para decodificar el propio tecleo CW del operador mediante tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la temporización de paleta/manipulador. Se almacena como un blob JSON anidado bajo `CwDecoder` con un campo `tx`.
4. Establezca **RTTY Mark Default:** cuadro de giro para la frecuencia de marca RTTY predeterminada.

### Notas sobre la decodificación CW

- Los alternadores de decodificación RX y TX se separaron de un único alternador `CwDecodeOverlay` en v26.5.3.
- La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura.

## Pestaña RX

Configure la calibración de compensación de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

### Pasos

1. Haga clic en la pestaña **RX**.
2. Establezca **Cal Frequency (MHz):** para la calibración manual.
3. Haga clic en **Start** para comenzar el barrido de calibración de frecuencia.
4. Ajuste **Freq Offset (ppb):** manualmente.
5. Seleccione **10 MHz Reference Source:** en el cuadro combinado (Auto, TCXO, GPSDO, External). Las opciones dependen del hardware instalado. El estado de bloqueo (Locked/Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo.

## Pestaña Calibration

Configure la calibración de frecuencia del lado del host para radios que no pueden calibrar su propio oscilador (p. ej. HL2). Esta pestaña está oculta para radios Flex, que gestionan la calibración en la pestaña RX.

### Pasos

1. Haga clic en la pestaña **Calibration** (solo visible cuando el radio conectado requiere calibración de frecuencia del lado del host).
2. Configure los ajustes de calibración de frecuencia según corresponda para el radio conectado.
3. Haga clic en **Trim** o la acción equivalente para aplicar la calibración al radio.

### Notas sobre calibración

- La pestaña está condicionada por la capacidad `hostFrequencyCalibration`, no por el nombre de la familia.
- El valor de calibración se vuelve a leer cada vez que se muestra el diálogo o cambia el estado de la conexión, por lo que una pulsación de Trim no puede confirmar el número de un radio anterior.

## Pestaña Antennas

Configure los nombres de visualización de los puertos de antena.

### Pasos

1. Haga clic en la pestaña **Antennas**.
2. Para cada fila de puerto de antena (p. ej. **ANT1**, **ANT2**, **XVTA**, **XVTB**):
   - Consulte la etiqueta de puerto de solo lectura.
   - Ingrese un nombre personalizado (máximo 16 caracteres) en el campo de texto editable.
   - Previsualice el nombre de visualización final en la columna Preview.
   - Haga clic en **Clear** para restablecer el nombre personalizado a vacío.
3. Cuando el nombre personalizado de un puerto está vacío, se usa el token de puerto original como nombre de visualización.
4. Las filas se actualizan automáticamente cuando cambian las asignaciones de antena de los slices.

## Pestaña Audio

Configure las salidas de audio del radio, los dispositivos de audio del PC, la grabación y el contenedor NVIDIA BNR.

### Pasos

1. Haga clic en la pestaña **Audio**.
2. Ajuste los controles deslizantes **Line Out:** y **Headphone:**. Haga clic en los botones **Mute** correspondientes para silenciar.
3. Haga clic en **Front Speaker: / Mute** para silenciar el altavoz frontal (según el modelo).
4. Seleccione **Audio Compression (SmartLink):** como **Auto**, **Uncompressed** u **Opus**. Se almacena como `AudioCompression`.
5. Alterne **Prevent system sleep while connected** para mantener el sistema operativo despierto. Se almacena como `InhibitSleepWhileConnected`.
6. Seleccione **PC Audio Devices: Input:** y **Output:** en los cuadros combinados.
7. Alterne **Audio Boost:** para ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`.
8. Establezca **Audio Buffer:** (50-1000 ms, predeterminado 200) para la fluctuación VPN/SmartLink. Se almacena como `Audio
