# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona controles para información del radio, red, GPS, TX, antenas, Phone/CW, RX, calibración, audio, filtros, XVTR, cables USB, periféricos, serial (FlexControl), APD, temas y gestión de certificados fijados de SmartLink. Muchos valores de solo lectura incluyen un botón de copiar al portapapeles junto a la etiqueta para facilitar su intercambio con soporte técnico.

## Abrir el diálogo

1. Seleccione `Settings > Radio Setup...` desde el menú principal.
2. El diálogo se abre como una ventana persistente que recuerda su posición y tamaño entre sesiones. Puede arrastrarla por la barra de título.
3. Cierre el diálogo haciendo clic en el botón **X** de la barra de título o presionando `Escape`.

## Pestaña Radio

La pestaña **Radio** muestra la identificación del radio, información de licencia y controles de actualización de firmware. El contenido de la pestaña está envuelto en un área desplazable para que todos los controles permanezcan accesibles en pantallas pequeñas o de alto DPI.

### Información del radio (solo lectura)

Cada campo de solo lectura incluye un botón de copiar (icono de portapapeles) que aparece al pasar el cursor o al enfocar. Haga clic en el botón para copiar el valor del campo al portapapeles del sistema. Una breve ventana emergente "¡Copiado!" confirma la acción.

| Control | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis. Haga clic en el botón de copiar para copiarlo. |
| **Region** | Región regulatoria del radio. |
| **HW Version** | Cadena de versión de hardware. Haga clic en el botón de copiar para copiarla. |
| **Model** | Modelo del radio. |
| **Options** | Muestra las opciones licenciadas del radio. Haga clic en el botón de copiar para copiarlas. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **License Info** | Muestra la suscripción, expiración, Radio ID (haga clic en el botón de copiar para copiarlo) y detalles de la versión licenciada. |

### Campos de identificación

| Control | Comportamiento |
|---|---|
| **Nickname** | Apodo amigable del radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del sistema operativo si está vacío. Se almacena en la configuración `StationName`. Se envía al radio como "cliente estación <nombre>". |

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de encendido remoto / activación remota.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar el radio conectado. Aparece un diálogo de confirmación antes de que proceda el reinicio.

- **En una conexión LAN**: AetherSDR se desconecta y se reconecta automáticamente una vez que el radio termina de iniciar.
- **En una conexión SmartLink/WAN**: AetherSDR se desconecta. Deberá reconectarse manualmente después de que el radio termine de iniciar.

El botón está deshabilitado cuando el radio está desconectado o cuando el backend conectado no admite reinicio por cliente (por ejemplo, un radio solo de recepción como el HL2). Se habilita automáticamente cuando el radio se reconecta, sin necesidad de reabrir el diálogo.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar al servidor de actualizaciones de FlexRadio las versiones de firmware disponibles.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` previamente extraído. El preparador detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. Aparece un indicador de progreso mientras se completa la preparación.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado al radio.

## Pestaña Network

La pestaña **Network** muestra la información de red del radio y proporciona opciones de red avanzadas.

### Información de red (solo lectura)

| Control | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada campo incluye un botón de copiar (icono de portapapeles) que aparece al pasar el cursor o al enfocar. Haga clic en el botón para copiar el valor al portapapeles del sistema. |

### Agent Automation (MCP)

La pestaña Network incluye la sección Agent Automation (MCP) para el puente de automatización dentro de la aplicación.

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Agent Automation (MCP):** | Deshabilitado | - | Habilita el puente de automatización dentro de la aplicación para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador decide activarlo. Se conserva mediante AutomationBridgeSettings. La variable de entorno de lanzamiento `AETHER_AUTOMATION` fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. El control de transmisión permanece bloqueado a menos que se configure `AETHER_AUTOMATION_ALLOW_TX`. |
| **Access Token:** | (ninguno) | - | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se almacena en el almacén secreto del sistema operativo. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador de posición '(cargando…)' hasta que se complete la lectura del llavero. |
| **Copy (Access Token)** | - | - | Copia el token de acceso al portapapeles. |
| **Rotate (Access Token)** | - | - | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. |
| **Allow TX via MCP: Enable transmit control** | Falso | - | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. Se aplica en el puente; ningún cliente puede cambiarlo. Es anulado por `AETHER_AUTOMATION_ALLOW_TX` (forzado a activado) y `AETHER_AUTOMATION_NO_TX` (fijado a desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| **Observe only: Read-only (block all driving)** | Falso | - | Hace que el puente sea solo de observación: los clientes MCP pueden leer el estado, pero cada verbo mutador (set/invoke/connect/tune/capture) es rechazado. Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento `AETHER_AUTOMATION_READONLY` lo fija a activado para ejecuciones sin interfaz/CI. |

### Configuración de red

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Desactivado | - | Rechaza pares que no sean RFC1918. |
| **VITA-49 RX buffer:** | 4 MB | 0,25-4 MB (preajustes) | Control deslizante de ajuste a preajuste que establece el búfer de recepción del núcleo (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. Preajustes de 256 KB a 4 MB. El sistema limita la concesión a `net.core.rmem_max`. |
| **granted: (VITA-49 RX buffer)** | - | - | Muestra el tamaño de búfer que el núcleo realmente concedió (en comparación con el preajuste solicitado). Muestra '(se aplica al conectar)' cuando no hay una conexión activa. |
| **Network MTU:** | 1450 | 576-9000 bytes | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en la configuración `NetworkMtu`. |
| **DHCP / Static** | DHCP | - | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | - | - | Campos de configuración de IP estática (se muestran cuando está seleccionado el modo Static). |
| **Apply** | - | - | Envía la configuración de red al radio. |

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS y la información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña **TX** controla los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y proporciona un acceso directo a la Configuración de Bandas de TX.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Tiempos de TX

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | - | - | Tiempos de retención/retardo de TX. |

### Otros controles de TX

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Interlocks - TX REQ: RCA / Accessory** | Desactivado | - | Habilita las entradas de enclavamiento RCA y de accesorio. |
| **Max Power:** | - | 0-100 % | Establece el límite de potencia de TX a nivel del radio. |
| **Tune Mode:** | - | - | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** | Desactivado | - | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | Falso | - | TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación en Split. Se almacena en la configuración `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Falso | - | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. Se almacena en la configuración `ActiveFollowsTxSlice`. |

## Pestaña Antennas

La pestaña **Antennas** le permite asignar nombres personalizados a cada puerto de antena del radio. Esta pestaña se construye de forma diferida cuando se hace clic por primera vez. Cuando el nombre personalizado de un puerto está vacío, se usa el token de puerto original como nombre de visualización.

### Campos de nombre de antena

| Control | Comportamiento |
|---|---|
| **Port / Custom name / Preview / Clear (columnas de tabla)** | Cuadrícula de filas de puertos de antena. Cada fila tiene una etiqueta de puerto de solo lectura (p. ej., ANT1), un campo de texto editable (máx. 16 caracteres), una vista previa del nombre de visualización final y un botón Clear para restablecer el nombre personalizado. Las filas se actualizan automáticamente cuando cambian las asignaciones de antena de las slices. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura los valores predeterminados del micrófono, manipulador CW y RTTY.

### Medidor de audio

| Control | Comportamiento |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Iambic:** | Deshabilitado | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en el radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para el radio como para el manipulador local de software. Par mutuamente excluyente. |
| **Swap:** | Desactivado | - | Intercambia punto/raya. |
| **Sideband:** | - | LSB / USB | Selecciona la banda lateral del tono de CW. |
| **CWX:** | Desactivado | - | Habilita el manipulación por macros CWX. |
| **Decode: RX** | Verdadero | - | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Se almacena en la configuración `CwDecoder` (JSON anidado, campo rx). |
| **Decode: TX** | Falso | - | Decodifica el propio manipulación CW del operador mediante el tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paleta/bug. Se almacena en la configuración `CwDecoder` (JSON anidado, campo tx). |

### RTTY

| Control | Comportamiento |
|---|---|
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña **RX** proporciona calibración de desviación de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo indica:
- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y se etiqueta **Busy** mientras un barrido está en progreso. |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de calibración: Starting, texto de progreso o error. Se actualiza en vivo durante el barrido. |

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** selecciona qué oscilador utiliza el radio como referencia de frecuencia.

#### Población del cuadro combinado

El cuadro combinado se puebla dinámicamente según lo que informa el radio. Los elementos aparecen de acuerdo con las siguientes reglas:

| Etiqueta del elemento | Cuándo se muestra |
|---|---|
| Auto | Siempre presente. |
| TCXO | Presente cuando el radio ha informado cualquier estado de oscilador, cuando el radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Presente cuando el radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Presente cuando el radio ha informado cualquier estado de oscilador, cuando el radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

El cuadro combinado selecciona el elemento que coincide con el `oscSetting` actual del radio. Si ese valor no está en la lista, el cuadro combinado recurre
