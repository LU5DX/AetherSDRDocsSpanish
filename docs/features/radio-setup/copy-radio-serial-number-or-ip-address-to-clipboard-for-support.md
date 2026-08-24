# Configuración del Radio

Esta página cubre el diálogo **Radio Setup**, la ventana maestra de configuración por radio. Incluye información del radio, configuración de red, GPS, TX, Phone/CW, RX, audio, filtros, transverters, cables USB, conexiones periféricas y gestión de certificados SmartLink fijados. Muchos valores de solo lectura incluyen un botón de copiado al portapapeles para compartirlos fácilmente con soporte técnico.

## Antes de comenzar

- Su radio debe estar conectado a AetherSDR, salvo que se indique lo contrario.

## Abrir Configuración del Radio

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre con una lista de navegación de pestañas a la izquierda y un panel de configuración a la derecha.

## Copiar valores al portapapeles

Varios valores de solo lectura (número de serie, versión de hardware, modelo, opciones, dirección IP, dirección MAC, campos de licencia) incluyen un botón de copiado al portapapeles (icono de bandeja) inmediatamente a la derecha del valor. Haga clic en él para copiar el valor al portapapeles de su sistema y pegarlo en un ticket de soporte o correo electrónico.

### Copiar el número de serie del radio

1. Abra `Settings > Radio Setup...`.
2. En la pestaña **Radio**, localice la etiqueta de solo lectura **Radio SN**.
3. Haga clic en el botón de copiado al portapapeles (icono de bandeja) inmediatamente a la derecha del valor del número de serie.

### Copiar la dirección IP o dirección MAC del radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice la etiqueta de solo lectura **IP Address** o **MAC Address**.
4. Haga clic en el botón de copiado al portapapeles (icono de bandeja) inmediatamente a la derecha del valor.

### Copiar la versión de firmware o información de licencia

1. Abra `Settings > Radio Setup...`.
2. En la pestaña **Radio**, desplácese a la sección **License Info**.
3. Haga clic en el botón de copiado al portapapeles junto a cualquier campo: **Subscription**, **Expiration**, **Radio ID** o **Licensed version**.

También puede copiar **HW Version**, **Model** u **Options** desde la pestaña **Radio** de la misma manera.

## Pestañas

### Radio

La pestaña **Radio** muestra identificación del radio, información de licencia y controles de actualización de firmware.

| Control | Comportamiento | Notas |
|---------|----------|-------|
| Radio SN | Número de serie del chasis (solo lectura). | Incluye un botón de copiado al portapapeles (icono de bandeja) junto al valor. |
| Region | Región regulatoria del radio. | |
| HW Version | Cadena de versión de hardware. | Incluye un botón de copiado al portapapeles junto al valor. |
| Remote On | Habilita el encendido remoto / remote-on. | |
| Options | Muestra las opciones licenciadas del radio. | Incluye un botón de copiado al portapapeles junto al valor. |
| FlexControl | Estado detectado del hardware FlexControl. | |
| multiFLEX | Estado habilitado de multiFLEX. | |
| Reboot Radio | Reinicia el radio conectado con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente una vez que el arranque finaliza. | Solo habilitado cuando está conectado y el backend admite un reinicio del cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente después del reinicio. |
| Model | Modelo del radio. | Incluye un botón de copiado al portapapeles junto al valor. |
| Nickname | Apodo amigable del radio. | |
| Callsign | Indicativo de la estación. | |
| Station Name | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se establece por defecto al nombre de host del SO si está vacío. | Se almacena en AppSettings. Se envía al radio como 'client station `<name>`'. |
| License Info (Subscription / Expiration / Radio ID / Licensed version) | Muestra los detalles de licencia del radio. | Cada campo incluye un botón de copiado al portapapeles junto al valor. |
| Check for Update | Consulta actualizaciones de firmware. | |
| Select Installer... | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae el payload .ssdr y emite progreso. | La etiqueta cambió desde 'Browse .ssdr...' en una versión anterior. |
| Upload Firmware | Inicia la carga del firmware con barra de progreso y estado. | |

### Network

La pestaña **Network** muestra información de red del radio y opciones avanzadas de red.

| Control | Comportamiento | Notas |
|---------|----------|-------|
| IP Address / Mask / MAC Address | Direcciones de red de solo lectura. | Cada una incluye un botón de copiado al portapapeles. |
| Enforce Private IP Connections: | Rechaza pares no RFC1918. | |
| Agent Automation (MCP): | Habilita el puente de automatización integrado para que un asistente de codificación con IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador debe aceptarlo explícitamente. | Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento `AETHER_AUTOMATION` fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se establezca `AETHER_AUTOMATION_ALLOW_TX`. |
| Access Token: | Muestra de solo lectura del token de acceso MCP; péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se almacena en el almacén de secretos del SO. | Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador de posición '(loading…)' hasta que se lea la lectura del llavero. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP keyee el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. | Se aplica en el puente; ningún cliente puede cambiarlo. Es anulado por `AETHER_AUTOMATION_ALLOW_TX` (forzado a activado) y `AETHER_AUTOMATION_NO_TX` (fijado a desactivado). Un watchdog de deskeying forzado limita la TX originada por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo mutador (set/invoke/connect/tune/capture) es rechazado. | Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento `AETHER_AUTOMATION_READONLY` lo fija a activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante con ajuste a valores preestablecidos que configura el buffer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un tamaño mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a `net.core.rmem_max`; una etiqueta en vivo 'granted: \<size\>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de buffer que el kernel realmente concedió (frente al valor preestablecido solicitado). | Muestra '(applies on connect)' cuando no hay una conexión activa. |
| Network MTU: | Establece el tamaño máximo de paquete UDP de salida VITA-49 en bytes. Valor predeterminado 1450. Rango 576-9000 bytes. | Se almacena en AppSettings. |
| DHCP / Static | Cambia entre modos DHCP e IP estática. | |
| IP Address: / Mask: / Gateway: | Campos de configuración de IP estática. | |
| Apply | Envía la configuración de red al radio. | |

### GPS

La pestaña **GPS** muestra presencia de GPS e información en vivo de lat/lon/alt/hora/satélites.

### TX

La pestaña **TX** configura temporizaciones de TX, interbloqueos, potencia máxima, modo de sintonización, visualización en waterfall, seguimiento de slice/TX y proporciona un acceso directo a TX Band Settings.

| Control | Comportamiento | Notas |
|---------|----------|-------|
| TX Band Settings | Abre el diálogo dedicado de potencia/sintonización por banda. | |
| Timings (in ms) | Temporizaciones de retención / retardo de TX. | |
| Interlocks - TX REQ: RCA / Accessory | Habilita las entradas de interbloqueo RCA y accesorio. | |
| Max Power: | Establece el límite de potencia TX a nivel de radio. Rango 0-100 %. | |
| Tune Mode: | Selecciona cómo se comporta el botón de sintonización. | |
| Show TX in Waterfall: | Dibuja la señal TX en el waterfall. | |
| TX Follows Active Slice | La TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Valor predeterminado False. | Se deshabilita automáticamente durante la operación en Split. |
| Active Slice Follows TX | Cambia la slice activa cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. Valor predeterminado False. | |

### Phone/CW

La pestaña **Phone/CW** configura el micrófono, keyer CW y valores predeterminados de RTTY.

| Control | Comportamiento | Notas |
|---------|----------|-------|
| Enable/Disable the Level Meter During Receive | Muestra el medidor de nivel de micrófono incluso en RX. | |
| Iambic: | Habilita o deshabilita el keyer iambic en el radio. | Se agregaron botones Mode A y Mode B junto al interruptor Enabled. |
| Iambic Mode: A / B | Selecciona el modo iambic Curtis A o B tanto para el radio como para el keyer de software local. Valor predeterminado A. | Par mutuamente excluyente. |
| Swap: | Intercambia dit/dah. | |
| Sideband: | Selecciona la banda lateral del tono CW. Opciones: LSB, USB. | |
| CWX: | Habilita el keying de macros CWX. | |
| Decode: RX | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Valor predeterminado True. | Se persiste como un blob JSON anidado bajo `CwDecoder` con campos `rx` y `tx`. La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura. |
| Decode: TX | Decodifica el propio keying CW del operador mediante el tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Valor predeterminado False. | |
| RTTY Mark Default: | Frecuencia de marca RTTY predeterminada. | |

### RX

La pestaña **RX** maneja la calibración de offset de frecuencia GPSDO y la fuente de referencia de 10 MHz.

| Control | Comportamiento | Notas |
|---------|----------|-------|
| Cal Frequency (MHz): | Frecuencia utilizada para la calibración manual. | |
| Start | Inicia el barrido de calibración de frecuencia. | |
| Freq Offset (ppb): | Offset de frecuencia manual en ppb. | |
| 10 MHz Reference Source: | Selecciona la fuente de referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. Valor predeterminado Auto. | El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. |

### Calibration

La pestaña **Calibration** está disponible solo en radios cuyo backend requiere calibración de frecuencia del lado del host (actualmente solo HL2 y backends similares de solo RX). En radios FLEX, esta pestaña está oculta porque el radio realiza su propia calibración de hardware en la pestaña **RX**.

Cuando está conectado a un radio compatible, la pestaña proporciona:

| Control | Comportamiento | Notas |
|---------|----------|-------|
| (Controles de calibración de frecuencia del host) | Corrige manualmente la frecuencia del oscilador local del radio en ppb/ppm. | La pestaña está oculta a menos que el backend conectado informe la capacidad `hostFrequencyCalibration`. Escribir "calibration" en el cuadro de búsqueda del diálogo no mostrará la pestaña en un radio FLEX. |

### Antennas

La pestaña **Antennas** le permite asignar nombres de visualización personalizados a cada puerto de antena (ANT1, ANT2, XVTA, XVTB, etc.). Estos nombres aparecen en los indicadores de antena RX/TX del panadapter en lugar de los tokens de puerto sin procesar.

| Control | Comportamiento | Notas |
|---------|----------|-------|
| Port / Custom name / Preview / Clear (columnas de tabla) | Cuadrícula de filas de puertos de antena. Cada fila tiene una etiqueta de puerto de solo lectura (p. ej., ANT1), un campo de texto editable (máx. 16 caracteres), una vista previa del nombre de visualización final y un botón Clear para restablecer el nombre personalizado. | Las filas se actualizan automáticamente cuando cambian las asignaciones de antena de las slices. Cuando el nombre personalizado de un puerto está vacío, se usa el token de puerto sin procesar como nombre de visualización. |

### Audio

La pestaña **Audio** configura las salidas de audio del radio, compresión, dispositivos de PC, boost, buffer, grabación y el contenedor NVIDIA BNR.

| Control | Comportamiento | Notas |
|---------|----------|-------|
| Line Out: | Ganancia de salida de línea. | |
| Mute (Line Out) | Silencia la salida de línea. | |
| Headphone: | Ganancia de auriculares. | |
| Mute (Headphone) | Silencia los auriculares. | |
| Front Speaker: / Mute | Silencia el altavoz frontal (específico del modelo). | |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. Valor predeterminado Auto. | |
| Prevent system sleep while connected | Mantiene el SO despierto mientras el radio está conectado para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Valor predeterminado False. | |
| PC Audio Devices: Input: / Output: | Selecciona los dispositivos de audio de entrada/salida del host. | |
| Audio Boost: | Habilita ganancia adicional en la ruta de audio del cliente. | |
| Audio Buffer: | Aumenta el buffer de audio en milisegundos para la fluctuación de VPN/SmartLink. Valor predeterminado 200. Rango 50-1000 ms. | Se almacena como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Selecciona la grabación del lado del radio o del lado del cliente. Valor predeterminado Radio Side. | |
| Save to: | Carpeta para grabaciones guardadas (solo lado del cliente). Valor predeterminado Documents/AetherSDR/Recordings. | |
| ... | Busca la carpeta de grabaciones. | |
| Auto-record on TX | Graba automáticamente mientras transmite. Valor predeterminado False. | |
| Idle timeout: |
