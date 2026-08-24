# Configuración de Radio

El cuadro de diálogo Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, Phone/CW, RX, calibración, audio, antenas, filtros, XVTR, cables USB, periféricos, APD, temas, puerto serie, configuración de certificado anclado SmartLink y acceso a receptores públicos KiwiSDR.

## Apertura del cuadro de diálogo

1. Abra `Settings > Radio Setup...`.
2. El cuadro de diálogo se abre como una ventana persistente. Su tamaño y posición se guardan entre sesiones.

---

## Pestaña Radio

La pestaña Radio muestra información del radio, identificación, información de licencia y controles de actualización de firmware.

### Información del radio

| Control | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Número de serie del chasis (solo lectura). | Incluye un botón de copiar al portapapeles (ícono de bandeja) junto al valor. Nuevo en v26.5.3 (#2976). |
| Region | Indicador | Región regulatoria del radio. |
| HW Version | Cadena de versión de hardware. | Incluye un botón de copiar al portapapeles junto al valor (#2976). |
| Model | Modelo del radio. | Incluye un botón de copiar al portapapeles junto al valor (#2976). |
| Options | Muestra las opciones licenciadas del radio. | Incluye un botón de copiar al portapapeles junto al valor (#2976). |
| FlexControl | Indicador | Estado de detección del hardware FlexControl. |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. |
| Nickname | Campo de texto | Apodo amigable del radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del SO si está vacío. Se almacena en AppSettings. Se envía al radio como 'client station \<name\>'. |
| License Info | Indicador | Muestra los detalles de licencia del radio (Subscription, Expiration, Radio ID, Licensed version). |
| Select Installer... | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae el payload .ssdr y emite progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| Reboot Radio | Botón pulsador | Reinicia el radio conectado. Deshabilitado cuando el radio está desconectado. Muestra un diálogo de confirmación antes de reiniciar. En conexiones LAN, AetherSDR se reconecta automáticamente después de que el radio arranca; en SmartLink/WAN, se requiere reconexión manual. Nuevo en v26.8.4 (#4448). |
| SmartLink (pestaña) | Gestión de certificados TLS SmartLink anclados. Lista cada certificado anclado (host, huella SHA-256, fecha de anclaje) con botones Forget y Forget All por fila. Nuevo en v26.5.3 (#2951 Fase 2). | Se construye de forma diferida al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: una discrepancia de certificado anclado pausa firmemente el handshake con un diálogo modal. |
| Pinned SmartLink Certificates (sección) | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Lista cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso). | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de anclaje migró de cadenas simples a objetos {fp, pinnedAt}. |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)'). | Respaldada por WanCertCache en WanConnection.cpp. |
| Forget selected | Elimina la huella del certificado anclado del host seleccionado para que la siguiente conexión vuelva a anclar silenciosamente. | |
| Forget all | Borra todos los certificados anclados (con confirmación). La siguiente conexión a cada radio vuelve a anclar silenciosamente. | Muestra QMessageBox::question antes de borrar. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Upload Firmware | Botón pulsador | Inicia la carga de firmware con barra de progreso y estado. |
| Agent Automation (MCP): | Habilita el puente de automatización en la aplicación para que un asistente de codificación con IA (mediante el servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador lo habilita explícitamente. | Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén secreto del SO. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que la lectura del llavero esté disponible. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Afectado por AETHER_AUTOMATION_ALLOW_TX (forzado activado) y AETHER_AUTOMATION_NO_TX (fijado desactivado). Un watchdog de desactivación forzada limita la TX originada por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo mutador (set/invoke/connect/tune/capture) es rechazado. | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante con ajuste a valores preestablecidos que configura el buffer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se descarten paquetes. | Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión en net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra cuánto otorgó realmente el kernel. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de buffer que el kernel realmente otorgó (versus el valor preestablecido solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |

Cada valor de solo lectura tiene un botón de copiar al portapapeles junto a él (un pequeño ícono que aparece al pasar el cursor). Haga clic en el botón para copiar el valor.

### Remote On

Haga clic en **Remote On** para habilitar la función de encendido remoto / wake remoto.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar el radio conectado. Un diálogo de confirmación advierte:

- **Conexión LAN:** AetherSDR se desconecta y se reconecta automáticamente una vez que el radio termina de arrancar.
- **Conexión SmartLink/WAN:** AetherSDR se desconecta. Debe reconectarse manualmente después de que el radio se reinicie.

El botón está deshabilitado cuando el radio está desconectado o reconectándose. Se rehabilita automáticamente cuando el radio se reconecta.

### Actualización de firmware

**Check for Update** consulta al radio las actualizaciones de firmware disponibles. Cuando se encuentra una versión más reciente, AetherSDR muestra un mensaje informativo:

> Update available: v*X.Y.Z*
> Download the SmartSDR installer from flexradio.com,
> then click 'Select Installer...' to stage it.

**Select Installer...** (renombrado de Browse .ssdr... en v0.9.3) acepta tres tipos de archivo:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador WiX de SmartSDR | .msi | FlexRadio v4.2 y posteriores |
| Instalador autoextraíble de SmartSDR | .exe | Versiones anteriores de SmartSDR |
| Archivo de firmware extraído | .ssdr | Como en versiones anteriores de AetherSDR |

El preparador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (magic OLE/MSI frente al encabezado PE/COFF MZ) y extrae el payload .ssdr sin requerir herramientas externas.

#### Para preparar firmware desde un instalador local

1. Descargue el instalador SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo .msi, .exe o .ssdr.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el progreso y cualquier error.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware al radio.

---

## Pestaña Network

La pestaña Network muestra información de red del radio y opciones de red avanzadas.

### Información de red

| Control | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles (#2976). |

### Configuración de red

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Enforce Private IP Connections | Botón de alternancia | — | — | Rechaza pares que no sean RFC1918. |
| Network MTU | Spinbox | 1450 | 576–9000 bytes | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. |
| DHCP / Static | Botón de alternancia | — | — | Cambia entre modos DHCP e IP estática. |
| IP Address / Mask / Gateway | Campo de texto | — | — | Campos de configuración de IP estática. |
| Apply | Botón pulsador | — | — | Envía la configuración de red al radio. |

---

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y la información en vivo de latitud, longitud, altitud, hora y satélites.

---

## Pestaña TX

La pestaña TX contiene temporizaciones de TX, interbloqueos, potencia máxima, modo de sintonía, visualización en waterfall, opciones de slice/TX y un acceso directo a TX Band Settings.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

La sección de temporizaciones TX incluye campos spinbox para valores en milisegundos.

| Control | Etiqueta de visualización | Predeterminado | Comportamiento |
|---|---|---|---|
| ACC TX | ACC TX: | — | Retardo de temporización ACC en ms. |
| TX Delay | TX Delay: | — | Retardo de TX en ms. |
| RCA TX1 | RCA TX1: | — | Retardo de RCA TX1 en ms. |
| Timeout | Timeout (sec): | — | Tiempo de espera de interbloqueo mostrado en segundos. El radio almacena este valor en milisegundos. |

### Interbloqueos

Los botones de alternancia **TX REQ: RCA** y **TX REQ: Accessory** habilitan las entradas de interbloqueo RCA y de accesorios.

### Potencia y sintonía

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Max Power | Spinbox | — | 0–100% | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode | Cuadro combinado | — | — | Selecciona cómo se comporta el botón de sintonía. |

### Waterfall y seguimiento de slice

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Show TX in Waterfall | Botón de alternancia | — | — | Dibuja la señal TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | False | `TxFollowsActiveSlice` | La TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante operación Split. |
| Active Slice Follows TX | Botón pulsador | False | `ActiveFollowsTxSlice` | Cambia el slice activo cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

---

## Pestaña Phone/CW

La pestaña Phone/CW configura los valores predeterminados de micrófono, manipulador CW y RTTY.

### Micrófono

**Enable/Disable the Level Meter During Receive** alterna la visualización del medidor de nivel de micrófono incluso en RX.

### Manipulador CW

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Iambic | Botón de alternancia | — | Enabled / Disabled | Habilita o deshabilita el manipulador iambic en el radio. |
| Iambic Mode | Botón pulsador | A | A / B | Selecciona el modo iambic Curtis A o B tanto para el radio como para el manipulador local por software. Par mutuamente excluyente. |
| Swap | Botón de alternancia | — | — | Intercambia dit/dah. |
| Sideband | Cuadro combinado | — | LSB / USB | Selecciona la banda lateral de tono CW. |
| CWX | Botón de alternancia | — | — | Habilita CW
