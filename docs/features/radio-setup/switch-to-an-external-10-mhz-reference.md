# Diálogo de Configuración de Radio

## Descripción General

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona acceso a información de la radio, ajustes de red, GPS, configuración de transmisión, ajustes de teléfono/CW, calibración de recepción, audio, filtros, transverters, cables USB, periféricos, puertos serie, gestión de certificados fijos de SmartLink, configuración del receptor KiwiSDR y ajustes de APD.

Para abrir el diálogo, haga clic en `Settings > Radio Setup...`. El diálogo requiere una conexión de radio activa.

## Pestaña Radio

La pestaña Radio muestra información de identificación de la radio, detalles de licencia y controles de actualización de firmware.

### Campos de Información

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Radio SN | Indicador | Número de serie del chasis (solo lectura). Incluye un botón de copiar al portapapeles junto al valor. |
| Region | Indicador | Región regulatoria de la radio. |
| HW Version | Indicador | Cadena de versión del hardware. Incluye un botón de copiar al portapapeles. |
| Options | Indicador | Muestra las opciones licenciadas de la radio. Incluye un botón de copiar al portapapeles. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. |
| Model | Indicador | Modelo de la radio. Incluye un botón de copiar al portapapeles. |
| Nickname | Campo de texto | Apodo amigable de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa el nombre de host del SO por defecto. Se almacena como `StationName` en AppSettings. Se envía a la radio como 'client station <name>'. |
| License Info (Subscription / Expiration / Radio ID / Licensed version) | Indicador | Muestra los detalles de licencia de la radio. Cada campo incluye un botón de copiar al portapapeles. |

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Remote On | Botón pulsador | Habilita el encendido remoto / remote-on. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Select Installer... | Botón pulsador | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae el contenido .ssdr y emite progreso. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| Reboot Radio | Botón pulsador | Reinicia la radio conectada con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente cuando el arranque termina. Nuevo en v26.8.4 (#4448). Solo se habilita cuando hay conexión y el backend soporta reinicio de cliente (p. ej. HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente tras el reinicio. |
| Agent Automation (MCP): | Botón de alternancia | Habilita el puente de automatización dentro de la aplicación para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador debe aceptarlo explícitamente. Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de esta alternancia y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Campo de texto | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén de secretos del SO. Nuevo en v26.8.4. Genera automáticamente un token hex de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que se complete la lectura del llavero. |
| Copy (Access Token) | Botón pulsador | Copia el token de acceso al portapapeles. Nuevo en v26.8.4. |
| Rotate (Access Token) | Botón pulsador | Genera un token nuevo y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Casilla de verificación | Permite que un cliente MCP keyee el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; el primer uso muestra una confirmación de responsabilidad del operador. Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado en desactivado). Un watchdog de deskeying forzado limita las TX originadas por el puente. |
| Observe only: Read-only (block all driving) | Casilla de verificación | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero todo verbo de mutación (set/invoke/connect/tune/capture) es rechazado. Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Deslizador | Deslizador con ajuste a valores preestablecidos que configura el buffer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión en net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Indicador | Muestra el tamaño de buffer que el kernel realmente concedió (en comparación con el valor preestablecido solicitado). Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones avanzadas de red.

### Campos de Información

| Control | Tipo | Comportamiento |
|---------|------|----------|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Enforce Private IP Connections: | Botón de alternancia | Habilitado | - | Rechaza pares no RFC1918. |
| Network MTU: | Spinbox | 1450 | 576-9000 bytes | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena como `NetworkMtu` en AppSettings. |
| DHCP / Static | Botón de alternancia | - | - | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | - | - | Campos de configuración de IP estática. |
| Apply | Botón pulsador | - | - | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información de posición en vivo, incluyendo latitud, longitud, altitud, hora y número de satélites.

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, interbloqueos, potencia máxima, modo de sintonía, visualización del waterfall y comportamiento de seguimiento slice/TX.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| TX Band Settings | Botón pulsador | - | - | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms) | Spinbox | - | - | Tiempos de retención/retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | - | - | Habilita las entradas de interbloqueo RCA y de accesorios. |
| Max Power: | Spinbox | - | 0-100 % | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode: | Cuadro combinado | - | - | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | - | - | Dibuja la señal TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | False | - | La TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante operación Split. |
| Active Slice Follows TX | Botón pulsador | False | - | Cambia la slice activa cuando la TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el keyer CW y los valores predeterminados de RTTY.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | - | - | Muestra el medidor de nivel de micrófono también en RX. |
| Iambic: | Botón de alternancia | - | Habilitado / Deshabilitado | Habilita o deshabilita el keyer iambic en la radio. |
| Iambic Mode: A / B | Botón pulsador | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente excluyente. |
| Swap: | Botón de alternancia | - | - | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | - | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX: | Botón de alternancia | - | - | Habilita el keying de macros CWX. |
| Decode: RX | Botón de alternancia | True | - | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Se almacena como JSON anidado bajo `CwDecoder` (campo rx). |
| Decode: TX | Botón de alternancia | False | - | Decodifica el propio keying CW del operador mediante el sidetone del cliente, útil como herramienta de autoentrenamiento para sincronización de paddle/bug. Se almacena como JSON anidado bajo `CwDecoder` (campo tx). |
| RTTY Mark Default: | Spinbox | - | - | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX proporciona calibración de desviación de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Cal Frequency (MHz): | Spinbox | - | - | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | - | - | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | - | - | Desviación de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Auto | Auto / TCXO / GPSDO / External | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Pestaña Calibration

La pestaña Calibration proporciona calibración de frecuencia manual para radios que no pueden calibrar su propio oscilador (p. ej. HL2). Esta pestaña está oculta a menos que el backend de la radio conectada soporte la calibración de frecuencia del host; está limitada por capacidad, no por familia, por lo que nunca aparece en una Flex donde la calibración de hardware de la pestaña RX maneja la tarea.

La pestaña vuelve a leer la calibración almacenada cada vez que se muestra el diálogo, de modo que una llamada al puente `freqcal` o la configuración de otra radio realizada mientras el diálogo estaba cerrado se recogen antes de que una pulsación de Trim pueda confirmar un valor incorrecto.

### Controles

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Calibration controls | Varios | Entradas de calibración de frecuencia y control Trim para la radio conectada. Se resiembran desde el modelo de radio en vivo cada vez que se abre el diálogo o cambia la conexión. |

## Pestaña Audio

La pestaña Audio gestiona las salidas de audio de la radio, compresión, dispositivos de PC, aumento, buffer, grabación y el contenedor NVIDIA BNR.

### Controles

| Control | Tipo | Predeterminado | Rango Válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Line Out: | Deslizador | - | - | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | - | - | Silencia la salida de línea. |
| Headphone: | Deslizador | - | - | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | - | - | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | - | - | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Auto | - | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | False | - | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | - | - | Selecciona los dispositivos de audio de entrada/salida del host. |
| Audio Boost: | Botón de alternancia | - | - | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| Audio Buffer: | Campo de texto | 200 | 50-1000 ms | Aumenta el buffer de audio en milisegundos para jitter de VPN/SmartLink. Se almacena como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Botón pulsador | Radio Side | Radio Side / Client Side | Selecciona grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. |
| Save to: | Campo de texto | - | - | Carpeta para grabaciones guardadas (solo lado del cliente). Predeterminado: Documents/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`. |
| ... | Botón pulsador | - | - | Navega para seleccionar la carpeta de grabaciones. |
| Auto-record on TX | Casilla de verificación | False | - | Graba automáticamente mientras se transmite. Se almacena como `QsoRecordingAutoRecord`. |
| Idle timeout: | Spinbox | 120 | 10-3600 seg | Segundos de silencio antes de que la grabación se detenga. Se almacena como `QsoRecordingIdleTimeout`. |
| NVIDIA
