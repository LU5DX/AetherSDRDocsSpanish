# Configuración del Radio

El cuadro de diálogo Configuración del Radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información del radio, red, GPS, calibración, TX, Phone/CW, RX, antenas, audio, filtros, XVTR, cables USB, periféricos, APD, temas, gestión de certificados SmartLink, (opcionalmente) serial FlexControl, receptor público KiwiSDR, y configuración de automatización/consulta QRZ.

El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

## Pestaña Radio

La pestaña Radio muestra identificación del radio, información de licencia y controles de actualización de firmware.

**Soporte de desplazamiento:** En v26.6.3 la pestaña Radio (y otras pestañas con grupos de contenido apilados) se envolvió en un QScrollArea vertical. Esto evita que el cuadro de diálogo exceda la altura de la pantalla en pantallas pequeñas o de alta densidad de píxeles (high-DPI). La barra de desplazamiento se oculta cuando el contenido ya cabe.

| Control | Comportamiento | Predeterminado |
|---------|----------------|----------------|
| Radio SN | Número de serie del chasis (solo lectura). Incluye un botón de copiar al portapapeles (ícono de bandeja) junto al valor. | — |
| Region | Región regulatoria del radio (solo lectura). | USA |
| HW Version | Cadena de versión de hardware. Incluye un botón de copiar al portapapeles junto al valor. | — |
| Remote On | Habilita el encendido remoto / remote-on. | — |
| Options | Muestra las opciones licenciadas del radio. Incluye un botón de copiar al portapapeles junto al valor. | — |
| FlexControl | Estado detectado del hardware FlexControl (solo lectura). | — |
| multiFLEX | Estado habilitado de multiFLEX (solo lectura). | — |
| Model | Modelo del radio. Incluye un botón de copiar al portapapeles junto al valor. | — |
| Nickname | Apodo amigable del radio. | — |
| Callsign | Indicativo de la estación. | — |
| Station Name | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del SO si está vacío. Se guarda en AppSettings. Se envía al radio como 'client station <nombre>'. | — |
| License Info | Muestra detalles de licencia del radio (Subscription / Expiration / Radio ID / Licensed version). Cada campo incluye un botón de copiar al portapapeles junto al valor. | — |
| Check for Update | Consulta actualizaciones de firmware. | — |
| Upload Firmware | Inicia la carga de firmware con barra de progreso y estado. | — |
| Select Installer... | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr pre-extraído. Pasa la ruta seleccionada a FirmwareStager, que extrae el contenido .ssdr y emite progreso. | — |
| Reboot Radio | Reinicia el radio conectado. Abre un diálogo de confirmación antes de enviar el comando de reinicio. Cuando se conecta vía SmartLink/WAN, no se soporta la reconexión automática después del reinicio; reconéctese manualmente cuando el radio termine de iniciar. En LAN, AetherSDR se reconecta automáticamente cuando el radio vuelve a estar en línea. El diálogo se cierra después del reinicio. Deshabilitado cuando el radio está desconectado; habilitado/deshabilitado automáticamente según el estado de conexión. | — |
| Agent Automation (MCP): | Habilita el puente de automatización en la aplicación para que un asistente de codificación con IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador lo acepta explícitamente. | Nuevo en v26.8.4 (#3646). Se guarda mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se configure AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se guarda en el almacén secreto del SO. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador de posición '(loading…)' hasta que la lectura del llavero (keychain) esté disponible. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP keyee el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; al habilitarlo por primera vez se muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado a desactivado). Un watchdog de des-keying forzado limita el TX originado por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea solo de observación: los clientes MCP pueden leer el estado, pero se rechaza todo verbo mutador (set/invoke/connect/tune/capture). | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante con ajuste a presets que establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | Nuevo en v26.8.4 (#3810). Presets de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <tamaño>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de búfer que el kernel realmente concedió (en comparación con el preset solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |

### Botones de copiar

Cada indicador de solo lectura en la pestaña Radio (Radio SN, Region, HW Version, Options, FlexControl, multiFLEX, Model, campos de License Info) incluye un pequeño botón de copiar que aparece al pasar el cursor. Haga clic en el botón para copiar el valor mostrado al portapapeles.

### Área de resumen

La pestaña Radio también muestra:
- **Firmware status** — Vacío hasta que comienza una carga de firmware; luego muestra progreso y texto de resultado.
- **License Info** — Estado de suscripción, fecha de expiración, Radio ID y versión licenciada.

## Pestaña Network

La pestaña Network muestra información de red del radio y opciones de red avanzadas.

| Control | Comportamiento | Predeterminado | Clave de ajuste |
|---|---|---|---|
| IP Address / Mask / MAC Address | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. | — | — |
| Enforce Private IP Connections: | Rechaza pares que no sean RFC1918. | — | — |
| Network MTU: | Establece el tamaño máximo de paquete UDP VITA-49 de salida en bytes. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. | 1450 | `NetworkMtu` |
| DHCP / Static | Cambia entre modos DHCP e IP estática. | — | — |
| IP Address: / Mask: / Gateway: | Campos de configuración de IP estática. | — | — |
| Apply | Envía la configuración de red al radio. | — | — |

## Pestaña GPS

La pestaña GPS muestra presencia de GPS e información en vivo de lat/lon/alt/hora/satélites.

## Pestaña Calibration

La pestaña Calibration proporciona calibración de frecuencia manual para radios que no pueden calibrar su propio oscilador (como el HL2). Esta pestaña solo se muestra cuando el backend del radio conectado informa que se soporta la calibración de frecuencia del lado del host (capacidad `hostFrequencyCalibration`).

| Control | Comportamiento | Predeterminado | Clave de ajuste |
|---|---|---|---|
| Calibration controls | Controles de calibración de frecuencia manual para radios que no pueden auto-calibrarse. | — | — |

**Nota:** Esta pestaña está oculta para dispositivos FlexRadio, que realizan su propia calibración de hardware a través de la pestaña RX. La pestaña se reevalúa en los cambios de estado de conexión, por lo que al cambiar a un radio diferente se actualizan los valores de calibración mostrados. Los datos de calibración también se releen cada vez que se muestra el diálogo, para recoger cambios realizados mientras el diálogo estaba cerrado (por ejemplo, mediante una llamada de puente `freqcal`).

## Pestaña TX

La pestaña TX configura tiempos de TX, interbloqueos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y ajustes de banda TX (TX Band Settings).

| Control | Comportamiento | Predeterminado | Clave de ajuste |
|---|---|---|---|
| TX Band Settings | Abre el diálogo dedicado de potencia/sintonía por banda. | — | — |
| Timings (in ms) | Tiempos de retención / retardo de TX. | — | — |
| Interlocks - TX REQ: RCA / Accessory | Habilita las entradas de interbloqueo RCA y de accesorio. | — | — |
| Max Power: | Establece el límite de potencia TX a nivel de radio (0-100%). | — | — |
| Tune Mode: | Selecciona cómo se comporta el botón de sintonía. | — | — |
| Show TX in Waterfall: | Dibuja la señal TX en el waterfall. | — | — |
| TX Follows Active Slice | El TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante operación en Split. | False | `TxFollowsActiveSlice` |
| Active Slice Follows TX | Cambia la slice activa cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | False | `ActiveFollowsTxSlice` |

**Nota sobre el campo de tiempo de espera:** El campo "Timeout" está etiquetado como **Timeout (sec)** y muestra el valor en segundos. Internamente el radio lo almacena en milisegundos; el ajuste se convierte automáticamente al enviarse.

## Pestaña Phone/CW

La pestaña Phone/CW configura los valores predeterminados de micrófono, teclado CW (keyer) y RTTY.

| Control | Comportamiento | Predeterminado | Clave de ajuste |
|---|---|---|---|
| Enable/Disable the Level Meter During Receive | Muestra el medidor de nivel de micrófono incluso en RX. | — | — |
| Iambic: | Habilita o deshabilita el keyer iámbico en el radio. | — | — |
| Iambic Mode: A / B | Selecciona el modo iámbico Curtis A o B tanto para el radio como para el keyer de software local. Par mutuamente excluyente. | A | — |
| Swap: | Intercambia dit/dah. | — | — |
| Sideband: | Selecciona la banda lateral del tono CW (LSB \| USB). | — | — |
| CWX: | Habilita el keying de macros CWX. | — | — |
| Decode: RX | Habilita la superposición de decodificación CW en el panadapter para CW recibido. | True | `CwDecoder` (JSON anidado, campo `rx`) |
| Decode: TX | Decodifica el propio keying CW del operador mediante el tono lateral (sidetone) del lado del cliente; útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. | False | `CwDecoder` (JSON anidado, campo `tx`) |
| RTTY Mark Default: | Frecuencia de marca RTTY predeterminada. | — | — |

**Nota:** En v0.9.1, se añadieron los botones Mode A y Mode B junto al interruptor Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el keyer iámbico de software local (IambicKeyer), que refleja el estado iámbico del radio para el tono lateral (sidetone) de menos de 5 ms.

Desde v26.5.3, el ajuste de superposición de decodificación CW se divide en dos interruptores independientes: **Decode: RX** y **Decode: TX**. Los ajustes se guardan como un blob JSON anidado bajo `CwDecoder` con los campos `rx` y `tx`. La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura.

## Pestaña RX

La pestaña RX proporciona calibración de compensación de frecuencia GPSDO y configuración de la fuente de referencia de 10 MHz.

| Control | Comportamiento | Predeterminado | Clave de ajuste |
|---|---|---|---|
| Cal Frequency (MHz): | Frecuencia utilizada para la calibración manual. | — | — |
| Start | Inicia el barrido de calibración de frecuencia. | — | — |
| Freq Offset (ppb): | Compensación de frecuencia manual en ppb. | — | — |
| 10 MHz Reference Source: | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/External). | Auto | — |

### Visualización de la fuente de referencia de 10 MHz

El cuadro combinado `10 MHz Reference Source:` en la pestaña `RX` se completa dinámicamente según el hardware presente en el radio conectado y el ajuste y estado actuales del oscilador informados por el radio. Pueden aparecer las siguientes fuentes:

| Entrada | Cuándo se muestra |
|---|---|
| Auto | Siempre se muestra. |
| TCXO | Se muestra cuando el radio informa que hay un TCXO presente, o cuando el estado actual o informado se refiere a TCXO. |
| GPSDO | Se muestra cuando el radio informa que hay un GPSDO presente, o cuando el estado actual o informado se refiere a GPSDO. |
| External 10 MHz | Se muestra cuando el radio informa que hay una referencia externa presente o activa, o cuando el estado actual o informado se refiere a externa. |

El cuadro combinado selecciona automáticamente el ajuste de oscilador guardado cuando se abre el diálogo. Si el ajuste guardado no está en la lista
