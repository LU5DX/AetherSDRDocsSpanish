# Configurar la configuración de la radio

El diálogo **Radio Setup** (`Settings > Radio Setup...`) proporciona la configuración maestra por radio, con secciones de pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, calibración, antenas, transverters, cables USB, periféricos, pre-distorsión adaptativa, temas, certificados fijados de SmartLink, configuración del puerto serie, navegación de receptores públicos KiwiSDR, parámetros de búsqueda de indicativos, configuración del amplificador (Acom) y parámetros del puente de automatización.

## Antes de comenzar

- La radio debe estar conectada antes de que la mayoría de las pestañas muestren información en vivo.
- Algunas pestañas (APD, Themes, SmartLink, Serial, KiwiSDR, Callsign Lookup, Acom, Automation Bridge) se construyen de forma diferida y solo aparecen al hacer clic por primera vez.
- AetherSDR utiliza una clase base `PersistentDialog` que guarda y restaura la geometría de la ventana automáticamente.

## Pasos para abrir

1. Haga clic en **Settings > Radio Setup...** en el menú principal.
2. El diálogo se abre mostrando la pestaña **Radio** de forma predeterminada.
3. Haga clic en cualquier pestaña para acceder a su configuración.

---

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, la información de licencia y los controles de actualización de firmware.

### Lectura de la información de la radio

- **Radio SN** — Número de serie del chasis (solo lectura). Muestra el número de serie del chasis si está disponible; de lo contrario, el número de serie de la radio. Incluye un botón de copiar al portapapeles junto al valor.
- **Region** — Región regulatoria de la radio (solo lectura).
- **HW Version** — Versión de hardware (solo lectura). Incluye un botón de copiar al portapapeles junto al valor.
- **Model** — Modelo de la radio (solo lectura). Incluye un botón de copiar al portapapeles junto al valor.
- **Options** — Opciones de radio con licencia (solo lectura). Muestra la lista de opciones de la radio, o un valor predeterminado como "GPS, PGXL" si se detecta un amplificador. Incluye un botón de copiar al portapapeles junto al valor.
- **FlexControl** — Estado detectado del hardware FlexControl (solo lectura).
- **multiFLEX** — Estado de habilitación de multiFLEX (solo lectura).
- **License Info** — Muestra suscripción, vencimiento, ID de la radio y versión con licencia (solo lectura). Cada campo incluye un botón de copiar al portapapeles junto al valor.

### Copiar información de la radio

Cada valor de solo lectura tiene un pequeño botón de copiar junto a él. Haga clic en el botón de copiar para copiar el valor al portapapeles. Aparece una breve ventana emergente "Copied!" cerca del botón. El botón de copiar está deshabilitado cuando el valor está vacío o muestra "—".

### Configuración de identificación

| Control | Qué hace | Notas |
|---|---|---|
| **Nickname** | Apodo de la radio fácil de usar (editable). | — |
| **Callsign** | Indicativo de la estación (editable). | — |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Se almacena en AppSettings. | Si está vacío, se usa el nombre de host del sistema operativo. Se envía a la radio como 'client station <name>'. |
| Select Installer... | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr pre-extraído. Pasa la ruta seleccionada a FirmwareStager, que extrae el contenido .ssdr y emite el progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| SmartLink (tab) | Gestión de certificados TLS fijados de SmartLink. Enumera cada certificado fijado (host, huella SHA-256, fecha de fijado) con los botones Forget y Forget All por fila. Nuevo en v26.5.3 (#2951 Fase 2). | Se construye de forma diferida al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: una discrepancia en la fijación del certificado ahora pausa el handshake con un diálogo modal. |
| Pinned SmartLink Certificates (section) | Encabezado de sección para la tabla de certificados fijados dentro de la pestaña SmartLink. Enumera todos los hosts que este cliente ha fijado en la primera conexión (trust-on-first-use). | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de fijación se migró de cadenas simples a objetos {fp, pinnedAt}. |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)'). | Respaldado por WanCertCache en WanConnection.cpp. |
| Forget selected | Elimina la huella del certificado fijado del host seleccionado para que la próxima conexión se vuelva a fijar silenciosamente. | — |
| Forget all | Borra todos los certificados fijados (con confirmación). La próxima conexión a cada radio se vuelve a fijar silenciosamente. | Muestra QMessageBox::question antes de borrar. |
| Reboot Radio | Reinicia la radio conectada con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente cuando el arranque finaliza. | Nuevo en v26.8.4 (#4448). Solo se habilita cuando está conectado y el backend admite el reinicio del cliente (por ejemplo, HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN, el operador debe reconectarse manualmente después del reinicio. |
| Agent Automation (MCP): | Habilita el puente de automatización dentro de la aplicación para que un asistente de codificación con IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador debe optar por habilitarlo. | Nuevo en v26.8.4 (#3646). Se conserva mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de esta opción y deshabilita el control en la interfaz. La activación de transmisión permanece bloqueada a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén de secretos del sistema operativo. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que se complete la lectura del llavero. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. AETER_AUTOMATION_ALLOW_TX (fuerza activación) y AETHER_AUTOMATION_NO_TX (bloqueo fijo) lo anulan. Un vigilante de desactivación forzada limita la transmisión originada por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) se rechaza. | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante de ajuste a valores preestablecidos que configura el búfer de recepción del núcleo (SO_RCVBUF) para el socket de transmisión VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el núcleo realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño del búfer que el núcleo realmente concedió (en comparación con el valor preestablecido solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay una conexión activa. |

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar las actualizaciones de firmware disponibles. El resultado aparece en la etiqueta de estado. Si hay una actualización disponible, la etiqueta le indica que descargue el instalador SmartSDR de flexradio.com.
2. Haga clic en **Select Installer...** para abrir un selector de archivos. Seleccione uno de:
   - `.msi` — Instalador SmartSDR basado en WiX para firmware 4.2+.
   - `.exe` — Instalador SmartSDR autocontenido más antiguo.
   - `.ssdr` — Archivo de firmware pre-extraído.
3. El preparador de firmware detecta el formato del archivo automáticamente y extrae el contenido `.ssdr`. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción.
4. Una vez que la extracción se completa, haga clic en **Upload Firmware** para iniciar la carga. Una barra de progreso y una etiqueta de estado muestran el progreso de la carga.

| Control | Qué hace | Notas |
|---|---|---|
| **Check for Update** | Consulta las actualizaciones de firmware disponibles. | Cuando se encuentra una actualización, la etiqueta le indica que descargue el instalador de flexradio.com. |
| **Select Installer...** | Abre un selector de archivos para archivos `.msi`, `.exe` o `.ssdr`. | Renombrado de **Browse .ssdr...** en v26.5.3. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. | Solo se habilita después de que la extracción se completa. |

### Remote On

Haga clic en **Remote On** para habilitar la funcionalidad de activación remota / encendido remoto en la radio.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación:
- **Conexión LAN**: AetherSDR se desconecta y se reconecta automáticamente cuando la radio termina de arrancar.
- **Conexión SmartLink/WAN**: AetherSDR se desconecta y no se reconecta automáticamente. Debe reconectarse manualmente cuando la radio termina de arrancar.

El botón está deshabilitado cuando la radio está desconectada. Se vuelve a habilitar automáticamente cuando la radio se reconecta.

---

## Pestaña Network

La pestaña **Network** muestra la información de red de la radio y las opciones avanzadas de red.

### Lectura de la información de red

- **IP Address / Mask / MAC Address** — Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles.

### Configuración de red

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Enforce Private IP Connections:** | Conmutador para rechazar pares que no sean RFC1918. | Habilitado | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. | 1450 | Rango de 576–9000 bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. |
| **DHCP / Static** | Conmutación entre modos DHCP e IP estática. | — | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — | Habilitados cuando se selecciona el modo Static. |
| **Apply** | Envía la configuración de red a la radio. | — | — |

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS y la información en vivo de posición/satélites cuando un receptor GPS está activo.

- Latitud, longitud, altitud, hora y número de satélites (solo lectura).
- Indicador de estado de bloqueo GPS.

---

## Pestaña TX

La pestaña **TX** configura los tiempos de transmisión, los interbloqueos, la potencia máxima, el modo de sintonía, la visualización en el waterfall, el seguimiento slice/TX y la configuración de banda TX.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Timings

Use los cuadros de giro en la sección **Timings (in ms)** para configurar los tiempos de retención y retardo de TX.

### Interlocks

Active **TX REQ: RCA** y **TX REQ: Accessory** para habilitar las entradas de interbloqueo RCA y de accesorio.

### Max Power

Establezca el límite de potencia de transmisión a nivel de radio usando el cuadro de giro **Max Power:** (0–100%).

### Tune Mode

Seleccione el comportamiento del botón de sintonía en el cuadro combinado **Tune Mode:**.

### Waterfall

Active **Show TX in Waterfall:** para dibujar la señal de TX en el waterfall.

### Seguimiento Slice/TX

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. | False | Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). | False | Mutuamente excluyente con **TX Follows Active Slice**. |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura los valores predeterminados del micrófono, el manipulador CW y RTTY.

### Level Meter

Active **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel del micrófono incluso durante la recepción.

### CW Keyer

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Iambic:** | Habilita o deshabilita el manipulador iambic en la radio. | — | En v0.9.1, se agregaron los botones Mode A y Mode B junto al conmutador Enabled. Mode A = Curtis A; Mode B = Curtis B. |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. | A | Par mutuamente excluyente agregado en v0.9.1. |
| **Swap:** | Intercambia dit/dah. | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW. | — | Opciones: LSB / USB. |
