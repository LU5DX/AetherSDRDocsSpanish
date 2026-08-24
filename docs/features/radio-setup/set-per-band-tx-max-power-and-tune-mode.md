# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Organiza la identificación de la radio, red, GPS, transmisión, teléfono/CW, recepción, calibración, nombres de antenas, filtros, transverters, cables USB, periféricos, APD, temas, gestión de certificados SmartLink, configuraciones de puerto serie, clúster DX, receptores KiwiSDR y configuraciones de interfaz de usuario en múltiples pestañas.

## Abrir Configuración de la Radio

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como un diálogo persistente; su geometría se guarda y restaura automáticamente entre sesiones.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de la radio

| Control | Tipo | Notas |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). Haga clic en el icono de copiar junto al valor para copiarlo al portapapeles. Nuevo en v26.5.3 (#2976). |
| **Region** | Indicador | Región reglamentaria de la radio. |
| **HW Version** | Indicador | Cadena de versión del hardware. Haga clic en el icono de copiar para copiar el texto. Nuevo en v26.5.3 (#2976). |
| **Model** | Indicador | Modelo de la radio. Haga clic en el icono de copiar para copiar el texto. Nuevo en v26.5.3 (#2976). |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. Haga clic en el icono de copiar para copiar el texto. Nuevo en v26.5.3 (#2976). |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de habilitación de multiFLEX. |

### Identificación

| Control | Tipo | Notas |
|---|---|---|
| **Nickname** | Campo de texto | Apodo amigable de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del sistema operativo si está vacío. Se almacena en AppSettings. Se envía a la radio como 'client station <name>'. |

### Copiar valores de solo lectura

Cada campo de información de solo lectura en esta pestaña (Radio SN, Callsign, Options, HW Version, Region, Model, IP Address, Mask, MAC Address y campos de información de licencia) muestra un pequeño icono de copiar al pasar el cursor sobre el valor. Haga clic en el icono para copiar el texto al portapapeles. Un breve aviso emergente "Copied" confirma la acción.

### Información de licencia

El diálogo muestra detalles de licencia de la radio, incluidos el estado de suscripción, fecha de vencimiento, ID de radio y versión licenciada. Cada campo incluye un botón de copiar al portapapeles junto al valor.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar actualizaciones de firmware.
   - Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
2. Descargue el instalador de SmartSDR desde flexradio.com si hay uno disponible.
3. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo `.ssdr` preextraído.
   - El preparador de firmware detecta el formato del archivo automáticamente y extrae el `.ssdr` sin requerir herramientas externas.
   - Mientras el preparador prepara el firmware, se muestra la barra de progreso y la etiqueta de estado indica "Preparing firmware from \<filename\>...".
4. Una vez completada la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio. El progreso y el resultado se muestran en la etiqueta de estado.

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta actualizaciones de firmware disponibles. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. Anteriormente etiquetado como **Browse .ssdr...** (cambiado en v26.5.3). |
| **Upload Firmware** | Botón | Inicia la carga del firmware. La barra de progreso y la etiqueta de estado se actualizan durante el proceso. |

### Encendido remoto

Haga clic en **Remote On** para habilitar el despertar remoto / capacidad de encendido remoto.

### Reiniciar la radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada.

| Control | Tipo | Notas |
|---|---|---|
| **Reboot Radio** | Botón | Reinicia la radio. Se muestra un diálogo de confirmación antes de reiniciar. El botón está deshabilitado cuando la radio no está conectada. Para conexiones LAN, AetherSDR se reconecta automáticamente después de que la radio termine de iniciar. Para conexiones SmartLink/WAN, debe reconectarse manualmente. El diálogo se cierra después de iniciar el reinicio. |

1. Haga clic en **Reboot Radio**.
2. Un diálogo de confirmación explica la diferencia de comportamiento entre conexiones LAN y WAN.
3. Haga clic en **OK** para confirmar. AetherSDR envía el comando de reinicio a la radio y cierra el diálogo de configuración.

## Pestaña Network

La pestaña Network muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red

| Control | Tipo | Notas |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |

### Configuración de red

| Control | Tipo | Predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | Habilitado | — | Rechaza pares que no sean RFC1918. El botón siempre muestra "Enabled" cuando está marcado. |
| **Agent Automation (MCP):** | Botón de alternancia | Deshabilitado | — | Habilita el puente de automatización en la aplicación para que un asistente de codificación con IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador opta por activarlo. Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de esta alternativa y deshabilita el control en la interfaz de usuario. La activación de transmisión permanece bloqueada a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| **Access Token:** | Campo de texto | (ninguno) | — | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén de secretos del sistema operativo. Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que la lectura del llavero esté disponible. |
| **Copy (Access Token)** | Botón | — | — | Copia el token de acceso al portapapeles. Nuevo en v26.8.4. |
| **Rotate (Access Token)** | Botón | — | — | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. Nuevo en v26.8.4. |
| **Allow TX via MCP: Enable transmit control** | Casilla de verificación | Falso | — | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador. Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado en desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| **Observe only: Read-only (block all driving)** | Casilla de verificación | Falso | — | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero cada verbo de mutación (set/invoke/connect/tune/capture) es rechazado. Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones sin interfaz/CI. |
| **VITA-49 RX buffer:** | Control deslizante | 4 MB | 0.25–4 MB (preajustes) | Control deslizante de ajuste a preajustes que establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas del panadapter/waterfall para que no se pierdan paquetes. Nuevo en v26.8.4 (#3810). Preajustes de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| **granted: (VITA-49 RX buffer)** | Indicador | — | — | Muestra el tamaño de búfer que el kernel realmente concedió (frente al preajuste solicitado). Muestra '(applies on connect)' cuando no hay una conexión activa. Nuevo en v26.8.4. |
| **Network MTU:** | Cuadro de giro | 1450 | 576–9000 bytes | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | — | Alterna entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | — | — | Campos de configuración de IP estática. |

### Aplicar configuración de red

Haga clic en **Apply** para enviar la configuración de red a la radio.

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y latitud, longitud, altitud, hora e información de satélites en vivo.

## Pestaña TX

Use esta página para configurar los ajustes de transmisión, incluidos tiempos, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall y comportamiento de seguimiento de slice/TX.

### Configuración de banda TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y sintonía por banda.

### Controles TX

| Control | Tipo | Predeterminado | Notas |
|---|---|---|---|
| **Max Power:** | Cuadro de giro | — | Establece el límite de potencia TX a nivel de radio. |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón de sintonía. |
| **Timings** | Cuadro de giro | — | Tiempos de retención/retardo TX. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y de accesorio. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en el waterfall. |
| **TX Follows Active Slice** | Botón | Falso | TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Falso | Cambia la slice activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

### Campos de tiempo TX

| Campo | Etiqueta de visualización | Unidad informada | Sufijo de comando |
|---|---|---|---|
| ACC TX | ACC TX | ms | `acc_tx_delay` |
| TX Delay | TX Delay | ms | `tx_delay` |
| RCA TX1 | RCA TX1 | ms | `tx1_delay` |
| Timeout (sec) | Timeout (sec) | segundos | `interlock_timeout` (valor multiplicado por 1000 antes de enviarse a la radio) |

El campo de tiempo de espera de enclavamiento se muestra en segundos completos para legibilidad. La radio almacena y espera el valor en milisegundos; AetherSDR multiplica por 1000 antes de enviar el comando a la radio.

## Pestaña Phone/CW

La pestaña Phone/CW configura los valores predeterminados de micrófono, manipulador CW y RTTY.

### Configuración del manipulador CW

| Control | Tipo | Predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Iambic:** | Botón de alternancia | — | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Botón | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| **Swap:** | Botón de alternancia | — | — | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado | — | LSB / USB | Selecciona la banda lateral de tono CW. |
| **CWX:** | Botón de alternancia | — | — | Habilita el teclado de macros CWX. |
| **Decode: RX** | Botón de alternancia | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Nuevo en v26.5.3: separado de un solo alternador CwDecodeOverlay en alternadores RX/TX independientes. Se persiste como blob JSON anidado bajo `CwDecoder` con campos rx y tx. La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura. |
| **Decode: TX** | Botón de alternancia | Falso | — | Decodifica el propio tecleo CW del operador mediante tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paleta/bug. Nuevo en v26.5.3 (#2417). |

### Otros ajustes de audio

| Control | Tipo | Notas |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| **RTTY Mark Default:** | Cuadro de giro | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX contiene controles para calibración manual de compensación de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración siempre se muestran independientemente de si hay un GPSDO instalado.

### Cómo ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia de precisión conocida en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra el texto de progreso ("Starting…" y luego el estado en vivo).
   - Antes de comenzar, Aether
