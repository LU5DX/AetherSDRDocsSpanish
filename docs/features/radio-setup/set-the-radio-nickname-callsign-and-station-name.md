# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona acceso a todos los ajustes a nivel de radio, incluyendo identificación de la radio, configuración de red, GPS, parámetros de transmisión, configuración de teléfono/CW, calibración de recepción, configuración de audio, filtros, transvertidores, cables USB, periféricos, muestreo APD, temas, gestión de certificados SmartLink, configuración de puertos serie, receptores públicos KiwiSDR y configuración de puertos serie.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La mayoría de los controles no están disponibles sin una conexión activa.

## Abriendo el diálogo

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como una ventana persistente. Su posición y tamaño se guardan automáticamente al cerrarlo y se restauran la próxima vez que lo abra. La geometría se almacena en AppSettings bajo la clave `RadioSetupDialogGeometry`.

### Áreas de desplazamiento en pestañas

Algunas pestañas (Themes, Audio, Filters, Peripherals, KiwiSDR) contienen más controles de los que caben verticalmente en pantallas pequeñas o de alta densidad de píxeles (DPI). Estas pestañas se envuelven automáticamente en un área de desplazamiento vertical para que pueda desplazarse hacia abajo y acceder a todos los controles sin redimensionar el diálogo más allá del borde de la pantalla. La barra de desplazamiento aparece solo cuando el contenido supera el área visible.

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
| **Select Installer...** | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae la carga útil .ssdr y emite el progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| **SmartLink (tab)** | Gestión de certificados TLS de SmartLink fijados. Lista cada certificado fijado (host, huella SHA-256, fecha de fijación) con opciones Forget y Forget All por fila. Nuevo en v26.5.3 (#2951 Phase 2). | Se construye de forma diferida al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: la discrepancia de certificado fijado ahora pausa firmemente el protocolo de enlace con un diálogo modal. |
| **Pinned SmartLink Certificates (section)** | Encabezado de sección para la tabla de certificados fijados dentro de la pestaña SmartLink. Lista todos los hosts que este cliente ha fijado en la primera conexión (confianza en el primer uso). | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de fijación migró de cadenas simples a objetos {fp, pinnedAt}. |
| **Host / SHA-256 fingerprint / Pinned (table columns)** | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)'). | Respaldado por WanCertCache en WanConnection.cpp. |
| **Forget selected** | Elimina la huella del certificado fijado del host seleccionado para que la próxima conexión lo vuelva a fijar silenciosamente. | |
| **Forget all** | Limpia todos los certificados fijados (con confirmación). La próxima conexión a cada radio los volverá a fijar silenciosamente. | Muestra QMessageBox::question antes de borrar. |

### Identificación de la Radio

Establezca un apodo legible, su indicativo y un nombre de estación en el FLEX-8600 conectado. Estos valores identifican la radio y este cliente para otras estaciones multiFLEX en la red.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta fácil de usar para la radio. Se envía a la radio como el nombre de la radio. | Nombre informado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(en blanco)_ |
| **Station Name** | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Se almacena en AppSettings. Se envía a la radio como 'client station <nombre>'. | Nombre de host del sistema operativo |

### Pasos para configurar la identificación de la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el campo **Nickname**, escriba el apodo que desee asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio inmediatamente.
5. En el campo **Callsign**, escriba su indicativo de estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica a este cliente para otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en el botón de cierre de la ventana o presione Escape para cerrar el diálogo.

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de activación/encendido remoto.

### Reboot Radio

El botón **Reboot Radio** reinicia la radio conectada. Esto es útil después de actualizaciones de firmware o cambios de configuración que requieran un reinicio.

- El botón está habilitado solo cuando la radio está conectada. Se deshabilita automáticamente al desconectarse o reconectarse.
- Aparece un diálogo de confirmación antes de reiniciar.
- El texto de advertencia difiere según el tipo de conexión:
  - **SmartLink/WAN**: "¿Reiniciar la radio conectada ahora? AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente una vez que la radio termine de iniciarse."
  - **Direct/LAN**: "¿Reiniciar la radio conectada ahora? AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciarse."
- Haga clic en **OK** para confirmar. El diálogo se cierra y AetherSDR se desconecta.
- El botón tiene una apariencia deshabilitada con estilo, por lo que permanece visible pero claramente atenuado cuando la radio no está conectada.

### Pasos para reiniciar la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Reboot Radio**.
4. Lea el diálogo de confirmación que aparece.
5. Haga clic en **OK** para confirmar. AetherSDR se desconecta y el diálogo se cierra.
6. Espere a que la radio termine de iniciarse. En conexiones directas/LAN, AetherSDR se reconecta automáticamente.

### Actualización de Firmware

Use los controles de actualización de firmware para buscar y aplicar actualizaciones de firmware a la radio.

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta si hay actualizaciones de firmware. |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de 'Browse .ssdr...' en v26.5.3. |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. |

#### Para buscar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com, y luego use **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

#### Para preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr preextraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Open.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from <nombre_de_archivo>..." y aparece la barra de progreso.
   - El gestor de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magia OLE/MSI para .msi, PE/COFF MZ para .exe, o CTRL+Z para .ssdr) y extrae el .ssdr sin herramientas externas.
3. Espere a que la preparación se complete. La etiqueta de estado muestra "Ready to upload <nombre_de_archivo>".
4. Haga clic en **Upload Firmware**.
   - Aparece un diálogo de confirmación: "Esto reiniciará la radio. ¿Está seguro de que desea cargar <nombre_de_archivo>?"
5. Haga clic en **Yes** para confirmar.
   - La carga comienza. La etiqueta de estado muestra "Uploading... (X%)" y la barra de progreso se actualiza.
   - La radio se reinicia después de que la carga se completa. La etiqueta de estado muestra "Upload and reboot successful."
6. Haga clic en el botón de cierre de la ventana o presione Escape para cerrar el diálogo.

## Pestaña Network

La pestaña **Network** muestra la información de red de la radio y proporciona opciones de red avanzadas.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918. El botón de alternancia muestra "Enabled" / "Disabled". | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red a la radio. | — |

### Para configurar IP estática

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Haga clic en **DHCP / Static** para cambiar al modo Static.
4. Introduzca los valores de **IP Address**, **Mask** y **Gateway**.
5. Haga clic en **Apply** para enviar la configuración a la radio.

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de latitud, longitud, altitud, hora y satélites.

## Pestaña TX

La pestaña **TX** proporciona controles de temporización de transmisión, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, comportamiento de seguimiento slice/TX y un acceso directo a la Configuración de Banda de TX.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Timings

Los controles de temporización incluyen campos para retrasos de enclavamiento y tiempo de espera. El campo de tiempo de espera se muestra en segundos para facilitar la lectura, pero se almacena y transmite a la radio en milisegundos.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **ACC TX:** | Retraso de transmisión ACC en milisegundos. | — |
| **TX Delay:** | Retraso de transmisión en milisegundos. | — |
| **RCA TX1:** | Retraso de RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos internamente. | — |

### Interlocks

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de enclavamiento RCA. |
| **TX REQ: Accessory** | Habilita la entrada de enclavamiento del accesorio. |

### Power and Tune

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0-100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |

### Slice/TX Follow Behavior

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Excluyente mutuamente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Excluyente mutuamente con 'TX Follows Active Slice'. | False |

## Pestaña Phone/CW

La pestaña **Phone/CW** proporciona configuración predeterminada de micrófono, manipulador CW y RTTY.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par excluyente mutuamente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW (LS
