# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona acceso a todos los ajustes a nivel de radio, incluyendo identificación de la radio, configuración de red, GPS, parámetros de transmisión, ajustes de teléfono/CW, calibración de recepción, configuración de audio, filtros, transverters, cables USB, periféricos, muestreo APD, temas, gestión de certificados SmartLink, configuración de puertos serie, receptores públicos KiwiSDR y configuración de puertos serie.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La mayoría de los controles no están disponibles sin una conexión activa.

## Abrir el diálogo

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como una ventana persistente. Su posición y tamaño se guardan automáticamente al cerrarlo y se restauran la próxima vez que lo abra. La geometría se almacena en AppSettings bajo la clave `RadioSetupDialogGeometry`.

### Áreas de desplazamiento de pestañas

Algunas pestañas (Themes, Audio, Filters, Peripherals, KiwiSDR) contienen más controles de los que caben verticalmente en pantallas pequeñas o de alta densidad de píxeles. Estas pestañas se envuelven automáticamente en un área de desplazamiento vertical para que pueda desplazarse hacia abajo y alcanzar todos los controles sin redimensionar el diálogo más allá del borde de la pantalla. La barra de desplazamiento aparece solo cuando el contenido excede el área visible.

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, información de licencia, remote on, actualización de firmware y controles de reinicio.

### Información de la Radio

La sección de información de la radio muestra indicadores de solo lectura para:

| Control | Descripción | Notas |
|---|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). | Incluye un botón de copiar al portapapeles (ícono de bandeja) junto al valor. |
| **Region** | Región regulatoria de la radio (p. ej., USA). | |
| **HW Version** | Cadena de versión de hardware. | Incluye un botón de copiar al portapapeles junto al valor. |
| **Model** | Modelo de la radio. | Incluye un botón de copiar al portapapeles junto al valor. |
| **Options** | Muestra las opciones de radio licenciadas. | Incluye un botón de copiar al portapapeles junto al valor. |
| **FlexControl** | Estado detectado del hardware FlexControl. | |
| **multiFLEX** | Estado de habilitación de multiFLEX. | |
| **License Info** (Subscription / Expiration / Radio ID / Licensed version) | Muestra los detalles de la licencia de la radio. | Cada campo incluye un botón de copiar al portapapeles junto al valor. |
| **Select Installer...** | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr pre-extraído. Pasa la ruta seleccionada a FirmwareStager que extrae el contenido .ssdr y emite el progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| **SmartLink (tab)** | Gestión de certificados TLS SmartLink fijados. Lista cada certificado fijado (host, huella SHA-256, fecha de fijación) con botones Forget por fila y Forget All. Nuevo en v26.5.3 (#2951 Phase 2). | Se construye de forma diferida al hacer clic por primera vez. Phase 2 de GHSA-wfx7-w6p8-4jr2: la discrepancia de certificado fijado ahora pausa firmemente el handshake con un diálogo modal. |
| **Pinned SmartLink Certificates (section)** | Encabezado de sección para la tabla de certificados fijados dentro de la pestaña SmartLink. Lista cada host que este cliente ha fijado en la primera conexión (confianza en el primer uso). | Phase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de fijación se migró de cadenas simples a objetos {fp, pinnedAt}. |
| **Host / SHA-256 fingerprint / Pinned (columnas de tabla)** | Tabla de solo lectura de 3 columnas: Host (nombre de host), huella SHA-256 (monoespaciada), Pinned (AAAA-MM-DD o '(pre-phase 2)'). | Respaldada por WanCertCache en WanConnection.cpp. |
| **Forget selected** | Elimina la huella del certificado fijado del host seleccionado para que la próxima conexión se vuelva a fijar silenciosamente. | |
| **Forget all** | Borra todos los certificados fijados (con confirmación). La próxima conexión a cada radio se vuelve a fijar silenciosamente. | Muestra QMessageBox::question antes de borrar. |
| Reboot Radio | Reinicia la radio conectada con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente una vez que el arranque finaliza. | Nuevo en v26.8.4 (#4448). Solo se habilita cuando está conectado y el backend admite un reinicio del cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente después del reinicio. |
| Agent Automation (MCP): | Habilita el puente de automatización en la aplicación para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador lo acepta voluntariamente. | Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz de usuario. El keying de transmisión permanece bloqueado a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén secreto del sistema operativo. | Nuevo en v26.8.4. Genera automáticamente un token hex de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que llegue la lectura del llavero. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP keyee el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Aplicado en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado activado) y AETHER_AUTOMATION_NO_TX (fijado desactivado). Un watchdog de fuerza de deskey limita la TX originada por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero cada verbo mutador (set/invoke/connect/tune/capture) es rechazado. | Nuevo en v26.8.4 (#4188). Aplicado en la aplicación, por lo que un cliente no puede evitarlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante de ajuste a preajustes que establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; uno más grande absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | Nuevo en v26.8.4 (#3810). Preajustes de 256 KB a 4 MB. El sistema limita la concesión en net.core.rmem_max; una etiqueta en vivo 'granted: <tamaño>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de búfer que el kernel realmente concedió (frente al preajuste solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |

### Identificación de la Radio

Establezca un apodo legible, su indicativo y un nombre de estación en la FLEX-8600 conectada. Estos valores identifican la radio y este cliente ante otras estaciones multiFLEX en la red.

| Control | Descripción | Predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como nombre de la radio. | Nombre informado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(en blanco)_ |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se almacena en AppSettings. Se envía a la radio como 'client station <nombre>'. | Nombre de host del SO |

### Pasos para establecer la identificación de la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el campo **Nickname**, escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio inmediatamente.
5. En el campo **Callsign**, escriba su indicativo de estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en el botón de cerrar de la ventana o presione Escape para descartar el diálogo.

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de activación remota / remote-on.

### Reiniciar la Radio

El botón **Reboot Radio** reinicia la radio conectada. Esto es útil después de actualizaciones de firmware o cambios de configuración que requieren un reinicio.

- El botón se habilita solo cuando la radio está conectada. Se deshabilita automáticamente al desconectarse o reconectarse.
- Aparece un diálogo de confirmación antes de reiniciar.
- El texto de advertencia difiere según el tipo de conexión:
  - **SmartLink/WAN**: "Reboot the connected radio now? AetherSDR will disconnect. SmartLink/WAN sessions do not auto-reconnect today — you will need to reconnect manually once the radio finishes booting."
  - **Direct/LAN**: "Reboot the connected radio now? AetherSDR will disconnect and automatically reconnect once the radio finishes booting."
- Haga clic en **OK** para confirmar. El diálogo se cierra y AetherSDR se desconecta.
- El botón tiene una apariencia deshabilitada estilizada para que permanezca visible pero claramente atenuado cuando la radio no está conectada.

### Pasos para reiniciar la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Reboot Radio**.
4. Lea el diálogo de confirmación que aparece.
5. Haga clic en **OK** para confirmar. AetherSDR se desconecta y el diálogo se cierra.
6. Espere a que la radio termine de arrancar. En conexiones directas/LAN, AetherSDR se reconecta automáticamente.

### Actualización de Firmware

Use los controles de actualización de firmware para buscar y aplicar actualizaciones de firmware a la radio.

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr pre-extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de 'Browse .ssdr...' en v26.5.3. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |

#### Para buscar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com y luego use **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

#### Para preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr pre-extraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Open.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<nombre de archivo\>..." y aparece la barra de progreso.
   - El preparador de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magia OLE/MSI para .msi, PE/COFF MZ para .exe, o CTRL+Z para .ssdr) y extrae el .ssdr sin herramientas externas.
3. Espere a que la preparación se complete. La etiqueta de estado muestra "Ready to upload \<nombre de archivo\>".
4. Haga clic en **Upload Firmware**.
   - Aparece un diálogo de confirmación: "This will restart the radio. Are you sure you want to upload \<nombre de archivo\>?"
5. Haga clic en **Yes** para confirmar.
   - La carga comienza. La etiqueta de estado muestra "Uploading... (X%)" y la barra de progreso se actualiza.
   - La radio se reinicia después de que la carga se completa. La etiqueta de estado muestra "Upload and reboot successful."
6. Haga clic en el botón de cerrar de la ventana o presione Escape para descartar el diálogo.

## Pestaña Network

La pestaña **Network** muestra información de red de la radio y proporciona opciones de red avanzadas.

| Control | Descripción | Predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. | — |
| **Enforce Private IP Connections:** | Rechaza pares no-RFC1918. El botón de alternancia muestra "Enabled" |
