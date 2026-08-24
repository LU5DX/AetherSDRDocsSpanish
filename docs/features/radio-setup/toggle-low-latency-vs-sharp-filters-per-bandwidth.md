# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración para ajustes específicos de cada radio, incluyendo información del radio, red, GPS, TX, Phone/CW, RX, calibración, audio, filtros, antenas, transverters, cables USB, periféricos, APD, temas, puerto serie, gestión de certificados fijados de SmartLink e integración de receptores KiwiSDR.

## Apertura del diálogo

- Haga clic en `Settings > Radio Setup...` mientras está conectado a un radio.

## Diseño del diálogo

El diálogo contiene una interfaz con pestañas que incluye las siguientes pestañas:

- **Radio** - Información del radio, identificación, información de licencia, actualización de firmware y reinicio del radio
- **Network** - Información de red y opciones avanzadas de red
- **GPS** - Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites
- **TX** - Temporizaciones de TX, interbloqueos, potencia máxima, modo de sintonía y ajustes de slice/seguimiento de TX
- **Phone/CW** - Micrófono, manipulador CW, valores predeterminados de RTTY
- **RX** - Calibración de desviación de frecuencia del GPSDO y fuente de referencia de 10 MHz
- **Calibration** - Calibración manual de frecuencia para radios que no pueden calibrarse solos (solo HL2)
- **Antennas** - Configuración de nombres de antenas
- **Filters** - Opciones de filtro de baja latencia / nítido por ancho de banda
- **XVTR** - Configuración por transverter
- **USB Cables** - Asignación de adaptadores serie USB
- **Peripherals** - Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius)
- **APD** - Selección del puerto de muestra para Predistorsión Adaptativa Externa (solo FLEX-8x00)
- **Themes** - Ajustes de apariencia de la interfaz, incluyendo anulaciones de color por slice
- **SmartLink** - Gestión de certificados TLS fijados
- **Serial** - Configuración del puerto serie de FlexControl
- **KiwiSDR** - Configuración y conexión de receptores públicos KiwiSDR

El diálogo recuerda su tamaño y posición entre sesiones usando `RadioSetupDialogGeometry` en AppSettings.

Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Radio, Themes, Audio, Filters, Peripherals en pantallas pequeñas o de alta densidad de píxeles) están envueltas en un área de desplazamiento para que el diálogo no crezca más allá del borde de la pantalla. La barra de desplazamiento aparece solo cuando es necesario; en pantallas anchas no hay cambio visual.

El diálogo es un singleton persistente: se construye una vez y se muestra/eleva bajo demanda. Las páginas se construyen de forma diferida cuando se seleccionan por primera vez, y cualquier valor de calibración almacenado se vuelve a leer cada vez que se muestra el diálogo o cambia el estado de conexión.

## Pestaña Radio

La pestaña Radio muestra información de identificación y licencia del radio, proporciona controles de actualización de firmware e incluye un botón Reiniciar Radio. Cada valor de solo lectura tiene un botón de copiar (icono de portapapeles) que aparece al pasar el cursor o al enfocar — haga clic para copiar el valor.

### Información del radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). Si el serial del chasis está vacío, se usa el número de serie del radio. Muestra "—" si no está disponible. Incluye un botón de copiar al portapapeles (icono de bandeja) junto al valor. |
| **Region** | Indicador | Región regulatoria del radio. Predeterminado: USA. |
| **HW Version** | Indicador | Cadena de versión del hardware. Se prefija con "v" si no está presente. Muestra "—" si no está disponible. Incluye un botón de copiar al portapapeles junto al valor. |
| **Model** | Indicador | Modelo del radio. Incluye un botón de copiar al portapapeles junto al valor. |
| **Options** | Indicador | Muestra las opciones licenciadas del radio. Si está vacío, muestra una suposición basada en la presencia de amplificador ("GPS, PGXL" o "GPS"). Muestra "—" si no está disponible. Incluye un botón de copiar al portapapeles junto al valor. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de habilitación de multiFLEX. |
| **License Info** | Indicador | Muestra suscripción, expiración, ID del radio y versión licenciada del radio. Cada campo incluye un botón de copiar al portapapeles junto al valor. |
| Reboot Radio | Reinicia el radio conectado con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente una vez que el arranque finaliza. | Nuevo en v26.8.4 (#4448). Solo habilitado cuando está conectado y el backend soporta un reinicio del cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente después del reinicio. |
| Agent Automation (MCP): | Habilita el puente de automatización integrado para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por predeterminado; el operador opta por habilitarlo. | Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se configure AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén secreto del sistema operativo. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador de posición '(loading…)' hasta que se lea el llavero. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por predeterminado; al habilitarlo por primera vez se muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado a desactivado). Un vigilante de desactivación forzada limita el TX originado por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) es rechazado. | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede evadirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante con ajuste a preajustes que configura el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un tamaño mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | Nuevo en v26.8.4 (#3810). Preajustes de 256 KB a 4 MB. El sistema limita la concesión en net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de búfer que el kernel realmente concedió (frente al preajuste solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |

### Identificación del radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo amigable del radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se usa el nombre de host del sistema operativo si está vacío. Se almacena en AppSettings como `StationName`. Se envía al radio como `client station <name>`. |

### Remote On

| Control | Tipo | Comportamiento |
|---|---|---|
| **Remote On** | Botón pulsador | Habilita el encendido remoto / remote-on. |

### Reiniciar Radio

| Control | Tipo | Comportamiento |
|---|---|---|
| **Reboot Radio** | Botón pulsador | Reinicia el radio conectado. Aparece un diálogo de confirmación antes de reiniciar. En conexiones LAN, AetherSDR se reconecta automáticamente una vez que el radio termina de arrancar. En conexiones SmartLink/WAN, debe reconectarse manualmente después de que el radio arranque. El diálogo se cierra después del reinicio. El botón está deshabilitado cuando el radio está desconectado. |

### Actualización de firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón pulsador | Consulta actualizaciones de firmware al radio. |
| **Select Installer...** | Botón pulsador | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware** | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| Estado del firmware | Indicador | Vacío hasta que comienza una carga de firmware, luego texto de progreso y resultado. |

#### Flujo de trabajo de actualización de firmware

Cuando **Check for Update** encuentra una versión más reciente, el área de estado le indica que descargue el instalador de SmartSDR desde flexradio.com usted mismo. Use **Select Installer...** para señalar a AetherSDR el archivo que descargó.

**Formatos de instalador soportados**

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador WiX de FlexRadio (SmartSDR v4.2 y posterior). Recomendado. |
| `.exe` | Instalador autoextraíble más antiguo (versiones previas a v4.2). |
| `.ssdr` | Archivo de firmware preextraído. |

**Pasos**

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión y le indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en **Select Installer...** y localice el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR prepara el firmware e informa el progreso en el área de estado.
6. Cuando la preparación finalice, haga clic en **Upload Firmware** para transferir el firmware al radio.

## Pestaña Network

La pestaña Network muestra información de red del radio y proporciona configuración avanzada de red.

### Información de red

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |

### Configuración de red

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | Rechaza pares que no son RFC1918. Siempre muestra el texto "Enabled". |
| **Network MTU:** | Spinbox | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | Cambia entre modos DHCP y IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | Campos de configuración de IP estática. |
| **Apply** | Botón pulsador | Envía la configuración de red al radio. |

## Pestaña GPS

La pestaña GPS muestra presencia de GPS e información de posicionamiento en vivo.

| Control | Tipo | Comportamiento |
|---|---|---|
| Información GPS | Indicador | Información en vivo de lat/lon/alt/hora/satélites. |

## Pestaña TX

La pestaña TX proporciona temporizaciones de transmisión, interbloqueos, potencia y ajustes de slice/seguimiento de TX.

### Configuración de banda TX

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Band Settings** | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |

### Temporizaciones

| Control | Tipo | Comportamiento |
|---|---|---|
| **ACC TX:** | Spinbox | Retardo de ACC TX en milisegundos. |
| **TX Delay:** | Spinbox | Retardo de TX en milisegundos. |
| **RCA TX1:** | Spinbox | Retardo de RCA TX1 en milisegundos. |
| **Timeout (sec):** | Spinbox | Tiempo de espera de interbloqueo en segundos (rango 0-3600). El radio almacena este valor en milisegundos internamente. |
| **TX2:** | Spinbox | Retardo de TX2 en milisegundos. |

### Interbloqueos

| Control | Tipo | Comportamiento |
|---|---|---|
| **Interlocks - TX REQ: RCA** | Botón de alternancia | Habilita la entrada de interbloqueo RCA. |
| **Interlocks - TX REQ: Accessory** | Botón de alternancia | Habilita la entrada de interbloqueo de accesorios. |

### Potencia y sintonía

| Control | Tipo | Comportamiento |
|---|---|---|
| **Max Power:** | Spinbox | Establece el límite de potencia TX a nivel de radio (0-100%). |
| **Tune Mode:** | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |

### Visualización en waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| **Show TX in Waterfall:** | Botón de alternancia | Dibuja la señal TX en el waterfall. |

### Comportamiento de slice/seguimiento de TX

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Follows Active Slice** | Botón pulsador | El TX sigue al slice activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena como `TxFollowsActiveSlice`. Predeterminado: False. |
| **Active Slice Follows TX** | Botón pulsador | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o
