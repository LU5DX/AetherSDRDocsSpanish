# Diálogo de configuración de radio

Esta página describe cada control en el diálogo **Radio Setup** (`Settings > Radio Setup...`). El diálogo tiene una barra de pestañas en la parte superior; cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copiar al portapapeles (icono de bandeja) junto al valor. |
| **Model** | Modelo de la radio (solo lectura). Incluye un botón de copiar al portapapeles junto al valor. |
| **HW Version** | Cadena de versión de hardware (solo lectura). Incluye un botón de copiar al portapapeles junto al valor. |
| **Region** | Región regulatoria; predeterminada EE. UU. (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). Incluye un botón de copiar al portapapeles junto al valor. |
| **License Info** | Muestra la suscripción, expiración, ID de radio y versión licenciada de la radio (solo lectura). Cada campo incluye un botón de copiar al portapapeles junto al valor. |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo de radio fácil de usar. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se almacena en `StationName`. Si se deja vacío, usa el nombre de host del sistema operativo. Se envía a la radio como `client station <name>`. |

### Botones de copiar

Cada indicador de solo lectura en la pestaña Radio tiene ahora un pequeño **botón de copiar al portapapeles** (icono de documentos superpuestos) a su derecha. Haga clic en el botón para copiar el valor del indicador al portapapeles del sistema. Aparece una breve etiqueta emergente ("Copied!") cerca del botón después de una copia exitosa. El botón se atenúa visualmente cuando el valor está vacío o es un guion de marcador de posición.

| Indicador con botón de copiar | Valor copiado |
|---|---|
| **Radio SN** | El número de serie del chasis, o el número de serie de la radio si el del chasis está vacío. |
| **Model** | La cadena del modelo de la radio. |
| **HW Version** | La cadena de versión de hardware, con el prefijo "v" si no está presente. |
| **Region** | La cadena de la región regulatoria. |
| **FlexControl** | La cadena del estado de detección de FlexControl. |
| **multiFLEX** | La cadena del estado habilitado de multiFLEX. |
| **Options** | La cadena de opciones licenciadas; si está vacía, muestra "GPS" o "GPS, PGXL" según la presencia del amplificador. |
| **License Info** | La cadena completa de detalles de licencia tal como se muestra. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita el encendido remoto / activación remota. |
| **Check for Update** | Consulta actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado dice: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta dice: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador SmartSDR `.msi` (formato WiX de FlexRadio v4.2+), un instalador autoejecutable `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI frente al encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` sin herramientas externas. Anteriormente etiquetado **Browse .ssdr...** (cambiado en v26.5.3). |
| **Upload Firmware** | Inicia la carga del firmware. Una barra de progreso y una etiqueta de estado siguen el avance. Solo se habilita después de que **Select Installer...** haya preparado un archivo válido. |
| **Reboot Radio** | Solicita confirmación: *Reboot the connected radio now?* El texto de advertencia difiere para conexiones WAN (SmartLink) frente a LAN. En LAN, AetherSDR se reconectará automáticamente después de que la radio arranque. En WAN, debe reconectarse manualmente. Al hacer clic en OK se envía el comando de reinicio y se cierra el diálogo. Deshabilitado cuando la radio no está conectada. Con fondo rojizo para indicar la naturaleza destructiva de la acción. |

### Preparación de una actualización de firmware

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from \<filename\>...* mientras el preparador extrae la carga útil.
4. Cuando la preparación se complete, la etiqueta de estado confirma que está listo y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

---

## Pestaña Network

Muestra las direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura reportadas por la radio. Cada una incluye un botón de copiar al portapapeles. |

### Controles

| Control | Tipo | Predeterminado |
|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | Habilitado |
| **Agent Automation (MCP):** | Botón de alternancia | Deshabilitado. Habilita el puente de automatización en la aplicación para que un asistente de codificación de IA (mediante el servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador decide activarlo. Nuevo en v26.8.4 (#3646). Se conserva mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de esta alternancia y deshabilita el control en la interfaz. El control de transmisión permanece bloqueado a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| **Access Token:** | Campo de texto (solo lectura) | (ninguno). Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén secreto del sistema operativo. Marcador de posición '(loading…)' hasta que se lea el llavero. Nuevo en v26.8.4. |
| **Copy (Access Token)** | Botón pulsador | Copia el token de acceso al portapapeles. Nuevo en v26.8.4. |
| **Rotate (Access Token)** | Botón pulsador | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. Nuevo en v26.8.4. |
| **Allow TX via MCP: Enable transmit control** | Casilla de verificación | Falso. Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; el primer cambio a habilitado muestra una confirmación de responsabilidad del operador. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado en desactivado). Un vigilante de desactivación forzada limita la transmisión originada por el puente. Nuevo en v26.8.4. |
| **Observe only: Read-only (block all driving)** | Casilla de verificación | Falso. Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) se rechaza. Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones sin interfaz/CI. Nuevo en v26.8.4 (#4188). |
| **VITA-49 RX buffer:** | Control deslizante (ajuste a valores preestablecidos) | 4 MB. Establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. Nuevo en v26.8.4 (#3810). |
| **granted: (VITA-49 RX buffer)** | Indicador | Muestra el tamaño de búfer que el kernel realmente concedió (frente al valor preestablecido solicitado). Muestra '(applies on connect)' cuando no hay conexión activa. Nuevo en v26.8.4. |
| **Network MTU:** | Control numérico | 1450. Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576–9000). El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — |
| **Apply** | Botón pulsador | Envía la configuración de red a la radio. |

---

## Pestaña Calibration

Proporciona calibración manual de compensación de frecuencia para radios que no pueden calibrar su propio oscilador. Esta pestaña está oculta por defecto y solo aparece para backends que reportan la capacidad `hostFrequencyCalibration` (como HL2).

> **Nota:** A diferencia de la pestaña Flex RX (que ofrece los mismos controles de calibración para radios con hardware GPSDO), esta pestaña Calibration se usa cuando la radio no puede corregir su oscilador y la corrección debe realizarse en el cliente host. La pestaña está restringida por capacidad: permanece oculta en una FLEX-8600 incluso si escribe "calibration" en el cuadro de filtro.

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Control numérico | — | Frecuencia utilizada para la calibración manual. |
| **Freq Offset (ppb):** | Control numérico | — | Compensación de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| **Trim** | Botón pulsador | — | Confirma la compensación de frecuencia mostrada en la calibración de la radio conectada. El valor se vuelve a leer de la radio cada vez que se abre el diálogo o cambia la conexión, por lo que no se puede confirmar accidentalmente un valor obsoleto de una radio previamente conectada. |

### Uso de la pestaña Calibration

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Calibration**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Ajuste **Freq Offset (ppb):** para corregir el error de frecuencia mostrado.
5. Haga clic en **Trim** para confirmar la compensación en la radio.

Los valores de calibración se vuelven a leer cada vez que se muestra el diálogo o se conecta una radio diferente, lo que garantiza que la compensación mostrada siempre refleje la radio actualmente conectada.

---

## Pestaña GPS

Muestra la presencia de GPS y datos de posición en vivo cuando hay un receptor GPS conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y cantidad de satélites. Se actualiza en tiempo real. |

---

## Pestaña TX

Controla temporizaciones de TX, límites de potencia, modo de sintonía y comportamiento de seguimiento de slice.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Campos de control numérico | — | Temporizaciones de retención y retardo de TX. Campos: ACC TX (ms), TX Delay (ms), RCA TX1 (ms). |
| **Timeout (sec):** | Control numérico | — | Tiempo de espera de interbloqueo en segundos. El valor se envía a la radio en milisegundos (multiplicado por 1000). |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de interbloqueo RCA y de accesorio. |
| **Max Power:** | Control numérico | — | Límite de potencia de TX a nivel de radio (0–100 %). |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal de TX en la visualización de waterfall. |
| **TX Follows Active Slice** | Botón pulsador | Falso | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón pulsador | Falso | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón pulsador | — | Abre el diálogo dedicado de potencia por banda y sintonía. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Manipulador iambic

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** muestra **Enabled**. Si muestra **Disabled**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iambic Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel del micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iambic en la radio. Siempre muestra "Enabled" cuando está activado. |
| **Iambic Mode: A / B** | Botón pulsador (par mutuamente excluyente) | A | Selecciona el modo iambic Curtis A o B para el manipulador de hardware de la radio y el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. |
