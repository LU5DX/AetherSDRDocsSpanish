# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona acceso a todos los ajustes a nivel de radio, incluyendo identificación de la radio, configuración de red, GPS, parámetros de transmisión, ajustes de telefonía/CW, calibración de recepción, configuración de audio, filtros, transvertidores, cables USB, periféricos, muestreo APD, temas, gestión de certificados SmartLink y configuración de puertos serie.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La mayoría de los controles no están disponibles sin una conexión activa.

## Abriendo el diálogo

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como una ventana persistente. Su posición y tamaño se guardan automáticamente al cerrarlo y se restauran la próxima vez que lo abra. La geometría se almacena en AppSettings bajo la clave `RadioSetupDialogGeometry`.

### Áreas de desplazamiento en pestañas

Algunas pestañas (Themes, Audio, Filters, Peripherals) contienen más controles de los que caben verticalmente en pantallas pequeñas o de alta densidad. Estas pestañas se envuelven automáticamente en un área de desplazamiento vertical para que pueda desplazarse hacia abajo y llegar a todos los controles sin redimensionar el diálogo más allá del borde de la pantalla. La barra de desplazamiento aparece solo cuando el contenido excede el área visible.

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, detalles de licencia, encendido remoto, actualización de firmware y controles de reinicio.

### Información de la Radio

La sección de información de la radio muestra indicadores de solo lectura para:

| Control | Descripción | Notas |
|---|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). | Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. |
| **Region** | Región regulatoria de la radio (ej., USA). | |
| **HW Version** | Cadena de versión del hardware. | Incluye un botón de copia al portapapeles junto al valor. |
| **Model** | Modelo de la radio. | Incluye un botón de copia al portapapeles junto al valor. |
| **Options** | Muestra las opciones de radio licenciadas. | Incluye un botón de copia al portapapeles junto al valor. |
| **FlexControl** | Estado detectado del hardware FlexControl. | |
| **multiFLEX** | Estado habilitado de multiFLEX. | |
| **License Info** (Subscription / Expiration / Radio ID / Licensed version) | Muestra los detalles de la licencia desde la radio. | Cada campo incluye un botón de copia al portapapeles junto al valor. |

### Identificación de la Radio

Establezca un apodo legible, su indicativo y un nombre de estación en la FLEX-8600 conectada. Estos valores identifican la radio y este cliente para otras estaciones multiFLEX en la red.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como el nombre de la radio. | Nombre reportado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(en blanco)_ |
| **Station Name** | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Se almacena en AppSettings. Se envía a la radio como 'client station <nombre>'. | Nombre de host del SO |

### Pasos para establecer la identificación de la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el campo **Nickname**, escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio inmediatamente.
5. En el campo **Callsign**, escriba su indicativo de estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica a este cliente para otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en el botón de cerrar de la ventana o presione Escape para cerrar el diálogo.

### Encendido Remoto

Haga clic en **Remote On** para habilitar la capacidad de activación/encendido remoto.

### Reiniciar la Radio

El botón **Reboot Radio** reinicia la radio conectada. Es útil después de actualizaciones de firmware o cambios de configuración que requieren un reinicio.

- El botón solo está habilitado cuando la radio está conectada. Se deshabilita automáticamente al desconectarse o reconectarse.
- Aparece un diálogo de confirmación antes de reiniciar.
- El texto de advertencia difiere según el tipo de conexión:
  - **SmartLink/WAN**: "¿Reiniciar la radio conectada ahora? AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy — deberá reconectarse manualmente una vez que la radio termine de iniciar."
  - **Direct/LAN**: "¿Reiniciar la radio conectada ahora? AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciar."
- Haga clic en **OK** para confirmar. El diálogo se cierra y AetherSDR se desconecta.
- El botón tiene una apariencia deshabilitada con estilo (#3334 seguimiento) para que permanezca visible pero claramente atenuado cuando la radio no está conectada.

### Pasos para reiniciar la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Reboot Radio**.
4. Lea el diálogo de confirmación que aparece.
5. Haga clic en **OK** para confirmar. AetherSDR se desconecta y el diálogo se cierra.
6. Espere a que la radio termine de iniciar. En conexiones directas/LAN, AetherSDR se reconecta automáticamente.

### Actualización de Firmware

Use los controles de actualización de firmware para buscar y aplicar actualizaciones de firmware a la radio.

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de 'Browse .ssdr...' en v26.5.3. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |

#### Para buscar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

#### Para preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr preextraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Open.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<nombre_archivo\>..." y aparece la barra de progreso.
   - El preparador de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magia OLE/MSI para .msi, PE/COFF MZ para .exe, o CTRL+Z para .ssdr) y extrae el .ssdr sin herramientas externas.
3. Espere a que la preparación se complete. La etiqueta de estado muestra "Ready to upload \<nombre_archivo\>".
4. Haga clic en **Upload Firmware**.
   - Aparece un diálogo de confirmación: "This will restart the radio. Are you sure you want to upload \<nombre_archivo\>?"
5. Haga clic en **Yes** para confirmar.
   - La carga comienza. La etiqueta de estado muestra "Uploading... (X%)" y la barra de progreso se actualiza.
   - La radio se reinicia después de que la carga se completa. La etiqueta de estado muestra "Upload and reboot successful."
6. Haga clic en el botón de cerrar de la ventana o presione Escape para cerrar el diálogo.

## Pestaña Network

La pestaña **Network** muestra información de red de la radio y proporciona opciones de red avanzadas.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. | — |
| **Enforce Private IP Connections:** | Rechaza pares no RFC1918. El botón de alternancia muestra "Enabled" / "Disabled". | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Almacenado en AppSettings. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red a la radio. | — |

### Para configurar IP estática

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Haga clic en **DHCP / Static** para cambiar al modo Static.
4. Ingrese los valores de **IP Address**, **Mask** y **Gateway**.
5. Haga clic en **Apply** para enviar la configuración a la radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS e información en vivo de latitud, longitud, altitud, hora y satélites.

## Pestaña TX

La pestaña **TX** proporciona controles de temporización de transmisión, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, comportamiento de seguimiento slice/TX y un acceso directo a TX Band Settings.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

Los controles de temporización incluyen campos para retrasos de enclavamiento y tiempo de espera. El campo de tiempo de espera se muestra en segundos para facilitar la lectura, pero se almacena y transmite a la radio en milisegundos.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **ACC TX:** | Retraso de transmisión ACC en milisegundos. | — |
| **TX Delay:** | Retraso de transmisión en milisegundos. | — |
| **RCA TX1:** | Retraso RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos internamente. | — |

### Enclavamientos

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de enclavamiento RCA. |
| **TX REQ: Accessory** | Habilita la entrada de enclavamiento del accesorio. |

### Potencia y Sintonía

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0-100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |

### Comportamiento de Seguimiento Slice/TX

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | False |

## Pestaña Phone/CW

La pestaña **Phone/CW** proporciona configuraciones predeterminadas para micrófono, manipulador CW y RTTY.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW (LSB o USB). | — |
| **CWX:** | Habilita el accionamiento de macros CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. | True |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. | — |

## Pestaña RX

La pestaña **RX** proporciona calibración de desviación de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. | — |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en ppb. | — |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado (TCXO/GPSDO/External). El estado de bloqueo (Locked/Unlocked) se muestra junto al combo y se actualiza en vivo. | Auto |

## Pestaña Audio

La pestaña **Audio** proporciona controles de salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y controles del contenedor NVIDIA BNR.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea. | — |
| **Mute (Line Out)** | Silencia la salida de línea. | — |
| **Headphone:** | Deslizador de ganancia de auriculares. | — |
| **Mute (Headphone)** | Silencia los auriculares. | — |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | — |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN. Almacenado en AppSettings. | Auto |
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. | False |
| **PC Audio Devices: Input: / Output:** | Selecciona dispositivos de
