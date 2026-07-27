# Configuración de la radio

El diálogo de Configuración de la radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, antenas, audio, filtros, XVTR, cables USB, periféricos, APD, temas, gestión de certificados SmartLink, (opcionalmente) serie FlexControl, receptor público KiwiSDR, y configuración de automatización/consulta QRZ.

El diálogo recuerda su tamaño y posición entre sesiones.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

**Soporte de desplazamiento:** En v26.6.3, la pestaña Radio (y otras pestañas con grupos de contenido apilados) se envolvió en un QScrollArea vertical. Esto evita que el diálogo supere la altura de la pantalla en pantallas pequeñas o de alta densidad. La barra de desplazamiento está oculta cuando el contenido ya cabe.

| Control | Comportamiento | Por defecto |
|---|---|---|
| Radio SN | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. | — |
| Region | Región regulatoria de la radio (solo lectura). | USA |
| HW Version | Cadena de versión del hardware. Incluye un botón de copia al portapapeles junto al valor. | — |
| Remote On | Habilita el encendido remoto / activación remota. | — |
| Options | Muestra las opciones de radio licenciadas. Incluye un botón de copia al portapapeles junto al valor. | — |
| FlexControl | Estado detectado del hardware FlexControl (solo lectura). | — |
| multiFLEX | Estado habilitado de multiFLEX (solo lectura). | — |
| Model | Modelo de la radio. Incluye un botón de copia al portapapeles junto al valor. | — |
| Nickname | Apodo amigable de la radio. | — |
| Callsign | Indicativo de la estación. | — |
| Station Name | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Usa el nombre de host del SO si está vacío. Se almacena en AppSettings. Se envía a la radio como 'client station <nombre>'. | — |
| License Info | Muestra los detalles de la licencia de la radio (Suscripción / Vencimiento / ID de radio / Versión licenciada). Cada campo incluye un botón de copia al portapapeles junto al valor. | — |
| Check for Update | Consulta actualizaciones de firmware. | — |
| Upload Firmware | Inicia la carga de firmware con barra de progreso y estado. | — |
| Select Installer... | Abre un diálogo de archivo para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr previamente extraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite el progreso. | — |
| Reboot Radio | Reinicia la radio conectada. Abre un diálogo de confirmación antes de enviar el comando de reinicio. Cuando está conectado a través de SmartLink/WAN, la reconexión automática no es compatible después del reinicio; reconéctese manualmente después de que la radio termine de iniciar. En LAN, AetherSDR se reconecta automáticamente una vez que la radio vuelve a estar en línea. El diálogo se cierra después del reinicio. Deshabilitado cuando la radio está desconectada; se habilita/deshabilita automáticamente según el estado de la conexión. | — |

### Botones de copia

Cada indicador de solo lectura en la pestaña Radio (Radio SN, Region, HW Version, Options, FlexControl, multiFLEX, Model, campos de License Info) incluye un pequeño botón de copia que aparece al pasar el cursor. Haga clic en el botón para copiar el valor mostrado al portapapeles.

### Área de resumen

La pestaña Radio también muestra:
- **Firmware status** — Vacío hasta que comience una carga de firmware, luego muestra el progreso y el texto del resultado.
- **License Info** — Estado de la suscripción, fecha de vencimiento, ID de radio y versión licenciada.

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones avanzadas de red.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| IP Address / Mask / MAC Address | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. | — | — |
| Enforce Private IP Connections: | Rechaza pares que no sean RFC1918. | — | — |
| Network MTU: | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. | 1450 | `NetworkMtu` |
| DHCP / Static | Cambia entre los modos DHCP e IP estática. | — | — |
| IP Address: / Mask: / Gateway: | Campos de configuración de IP estática. | — | — |
| Apply | Envía la configuración de red a la radio. | — | — |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS y la información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña TX configura los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall, seguimiento de slice/TX y configuración de bandas de TX.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| TX Band Settings | Abre el diálogo dedicado de potencia/sintonía por banda. | — | — |
| Timings (in ms) | Tiempos de retención/retardo de TX. | — | — |
| Interlocks - TX REQ: RCA / Accessory | Habilita las entradas de enclavamiento RCA y Accessory. | — | — |
| Max Power: | Establece el límite de potencia de TX a nivel de radio (0-100%). | — | — |
| Tune Mode: | Selecciona cómo se comporta el botón de sintonía. | — | — |
| Show TX in Waterfall: | Dibuja la señal de TX en el waterfall. | — | — |
| TX Follows Active Slice | TX sigue el slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación de división. | False | `TxFollowsActiveSlice` |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | False | `ActiveFollowsTxSlice` |

**Nota sobre el campo de tiempo de espera:** El campo "Timeout" está etiquetado como **Timeout (sec)** y muestra el valor en segundos. Internamente la radio lo almacena en milisegundos; la configuración se convierte automáticamente al enviarse.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| Enable/Disable the Level Meter During Receive | Muestra el medidor de nivel de micrófono incluso en RX. | — | — |
| Iambic: | Habilita o deshabilita el manipulador iámbico en la radio. | — | — |
| Iambic Mode: A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A | — |
| Swap: | Intercambia dit/dah. | — | — |
| Sideband: | Selecciona la banda lateral del tono CW (LSB \| USB). | — | — |
| CWX: | Habilita la activación de macros CWX. | — | — |
| Decode: | Habilita la superposición de decodificación CW en el panadapter. | True | `CwDecodeOverlay` |
| RTTY Mark Default: | Frecuencia de marca RTTY predeterminada. | — | — |

**Nota:** En v0.9.1, se agregaron los botones Mode A y Mode B junto al conmutador Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el manipulador iámbico de software local (IambicKeyer) que refleja el estado iámbico de la radio para un tono lateral de menos de 5 ms.

## Pestaña RX

La pestaña RX proporciona calibración de desviación de frecuencia del GPSDO y configuración de la fuente de referencia de 10 MHz.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| Cal Frequency (MHz): | Frecuencia utilizada para la calibración manual. | — | — |
| Start | Inicia el barrido de calibración de frecuencia. | — | — |
| Freq Offset (ppb): | Desviación de frecuencia manual en ppb. | — | — |
| 10 MHz Reference Source: | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/External). | Auto | — |

### Visualización de la fuente de referencia de 10 MHz

El cuadro combinado `10 MHz Reference Source:` en la pestaña `RX` se completa dinámicamente según el hardware presente en la radio conectada y la configuración y el estado actual del oscilador informados por la radio. Pueden aparecer las siguientes fuentes:

| Entrada | Cuándo se muestra |
|---|---|
| Auto | Siempre se muestra. |
| TCXO | Se muestra cuando la radio informa que hay un TCXO presente, o cuando el estado actual o informado se refiere a TCXO. |
| GPSDO | Se muestra cuando la radio informa que hay un GPSDO presente, o cuando el estado actual o informado se refiere a GPSDO. |
| External 10 MHz | Se muestra cuando la radio informa que hay una referencia externa presente o activa, o cuando el estado actual o informado se refiere a externa. |

El cuadro combinado selecciona la configuración del oscilador guardada automáticamente cuando se abre el diálogo. Si la configuración guardada no está en la lista, se intenta con el estado actual informado; si este también está ausente, se selecciona Auto.

#### Etiqueta de estado de bloqueo

La etiqueta de estado junto al cuadro combinado muestra información más detallada:
- Cuando se selecciona Auto y la radio ha cambiado a una fuente específica, la etiqueta muestra **Auto -> \<fuente\>** seguido de **Locked** o **Unlocked**.
- Cuando la fuente solicitada difiere de la fuente activa, la etiqueta muestra **\<solicitada\> -> \<activa\>** seguido de **Locked** o **Unlocked**.
- Cuando la fuente solicitada y la activa coinciden, la etiqueta muestra **\<fuente\> Locked** o **\<fuente\> Unlocked**.
- Cuando se selecciona External 10 MHz pero no se detecta ninguna referencia externa, la etiqueta agrega **(not detected)**.
- Mientras espera que la radio informe el estado del oscilador, la etiqueta muestra **Waiting for oscillator status**.

El color de la etiqueta es verde cuando está bloqueado y rojo cuando está desbloqueado. Antes de que la radio informe cualquier estado del oscilador, la etiqueta se muestra en un gris neutro.

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres amigables a cada puerto de antena en la radio.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| ANT1 / ANT2 / XVTA / XVTB | Campos de texto para establecer nombres amigables para cada puerto de antena. | — | — |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos del PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| Line Out: | Deslizador de ganancia de salida de línea. | — | — |
| Mute (Line Out) | Silencia la salida de línea. | — | — |
| Headphone: | Deslizador de ganancia de auriculares. | — | — |
| Mute (Headphone) | Silencia los auriculares. | — | — |
| Front Speaker: / Mute | Silencia el altavoz frontal (específico del modelo). | — | — |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. | Auto | `AudioCompression` |
| Prevent system sleep while connected | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. | False | `InhibitSleepWhileConnected` |
| PC Audio Devices: Input: / Output: | Selecciona los dispositivos de audio de entrada/salida del host. | — | — |
| Audio Boost: | Habilita ganancia adicional en la ruta de audio del cliente. | — | `AudioBoost` |
| Audio Buffer: | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Se aplica a AudioEngine::setRxBufferCapMs(). | 200 | `AudioBufferMs` |
| Recording: Radio Side / Client Side | Selecciona la grabación del lado de la radio o del lado del cliente. | Radio Side | `RecordingMode` |
| Save to: | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto, Documents/AetherSDR/Recordings. | — | `QsoRecordingDir` |
| ... | Navega para buscar la carpeta de grabación. | — | — |
| Auto-record on TX | Graba automáticamente mientras se transmite. | False | `QsoRecordingAutoRecord` |
| Idle timeout: | Segundos de silencio antes de que se detenga la grabación. | 120 | `QsoRecordingIdleTimeout` |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. | — | — |

## Pestaña Filters

La pestaña Filters proporciona opciones de filtro de baja latencia / nítido por ancho de banda.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| Voice / CW / Digital filter sharpness sliders | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está habilitado. Los comandos se envían como 'radio filter_sharpness <modo> level=<N>'. | — | — |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Los comandos se envían como 'radio filter_sharpness <modo> auto_level=1'. | — | — |
| Use Low Latency Filters for Digital Modes | Fuerza filtros de baja latencia en DIGU/DIGL. | — | — |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transverter — RX Only, válido, eliminar, además de Crear nuevo transverter. Contiene pestañas anidadas, una por transverter, y una pestaña '+'.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| RX Only: | Fuerza solo RX en ese transverter. | — | — |
| Remove (xvtr) | Elimina la definición del transverter. | — | — |
| Create New Transverter | Agrega una nueva entrada de transverter. | — | — |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Comportamiento | Por defecto | Clave de configuración |
|---|---|---|---|
| Cables list / Status | Cables USB detectados por tipo con estado Conectado/Desconectado. | — | — |
| Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Parámetros y comportamiento serie por
