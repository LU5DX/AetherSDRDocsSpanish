# Configuración de la Radio

El diálogo de Configuración de la Radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, antenas, audio, filtros, XVTR, cables USB, periféricos, APD, temas y (opcionalmente) FlexControl serial.

El diálogo recuerda su tamaño y posición entre sesiones.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

| Control                       | Comportamiento                                                                                                                                                                             | Valor predeterminado                                                                                                                                                   |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Radio SN                      | Número de serie del chasis (solo lectura).                                                                                                                                                 | —                                                                                                                                                                      |
| Region                        | Región regulatoria de la radio (solo lectura).                                                                                                                                             | USA                                                                                                                                                                    |
| HW Version                    | Cadena de versión del hardware (solo lectura).                                                                                                                                             | —                                                                                                                                                                      |
| Remote On                     | Activa el encendido remoto / encendido remoto.                                                                                                                                             | —                                                                                                                                                                      |
| Options                       | Muestra las opciones de radio licenciadas (solo lectura).                                                                                                                                  | —                                                                                                                                                                      |
| FlexControl                   | Estado detectado del hardware FlexControl (solo lectura).                                                                                                                                  | —                                                                                                                                                                      |
| multiFLEX                     | Estado habilitado de multiFLEX (solo lectura).                                                                                                                                             | —                                                                                                                                                                      |
| Model                         | Modelo de la radio (solo lectura).                                                                                                                                                         | —                                                                                                                                                                      |
| Nickname                      | Apodo amigable de la radio.                                                                                                                                                                | —                                                                                                                                                                      |
| Callsign                      | Indicativo de la estación.                                                                                                                                                                 | —                                                                                                                                                                      |
| Station Name                  | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se establece por defecto al nombre de host del SO si está vacío.                                                         | —                                                                                                                                                                      |
| License Info                  | Muestra los detalles de la licencia desde la radio (Suscripción / Expiración / ID de Radio / Versión licenciada).                                                                          | —                                                                                                                                                                      |
| Check for Update              | Consulta actualizaciones de firmware.                                                                                                                                                      | —                                                                                                                                                                      |
| Browse .ssdr...               | Elige un archivo de imagen de firmware.                                                                                                                                                    | —                                                                                                                                                                      |
| Upload Firmware               | Inicia la carga de firmware con barra de progreso y estado.                                                                                                                                | —                                                                                                                                                                      |

### Área de resumen

La pestaña Radio también muestra:
- **Firmware status** — Vacío hasta que comience una carga de firmware, luego muestra el progreso y el texto de resultado.
- **License Info** — Estado de suscripción, fecha de expiración, ID de Radio y versión licenciada.

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| IP Address / Mask / MAC Address | Direcciones de red de solo lectura. | — | — |
| Enforce Private IP Connections: | Rechaza pares no RFC1918. | — | — |
| Network MTU: | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. | 1450 | `NetworkMtu` |
| DHCP / Static | Cambia entre modos DHCP e IP estática. | — | — |
| IP Address: / Mask: / Gateway: | Campos de configuración de IP estática. | — | — |
| Apply | Envía la configuración de red a la radio. | — | — |

**Nota:** La MTU predeterminada de 1450 es segura para la mayoría de los túneles VPN/SD-WAN.

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de lat/lon/alt/hora/satélites.

## Pestaña TX

La pestaña TX configura temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y Configuración de Banda TX.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| TX Band Settings | Abre el diálogo dedicado de potencia/sintonía por banda. | — | — |
| Timings | Temporizaciones de retención/retardo de TX en milisegundos; el tiempo de espera se muestra en segundos. | — | — |
| Interlocks - TX REQ: RCA / Accessory | Habilita las entradas de enclavamiento RCA y Accessory. | — | — |
| Max Power: | Establece el límite de potencia TX a nivel de radio (0-100%). | — | — |
| Tune Mode: | Selecciona cómo se comporta el botón de sintonía. | — | — |
| Show TX in Waterfall: | Dibuja la señal TX en el waterfall. | — | — |
| TX Follows Active Slice | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se desactiva automáticamente durante operación Split. | False | `TxFollowsActiveSlice` |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | False | `ActiveFollowsTxSlice` |

**Nota sobre el campo de tiempo de espera:** El campo "Timeout" ahora está etiquetado como **Timeout (sec)** y muestra el valor en segundos. Internamente la radio lo almacena en milisegundos; la configuración se convierte automáticamente al enviarse.

## Pestaña Phone/CW

La pestaña Phone/CW configura los valores predeterminados de micrófono, manipulador CW y RTTY.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Enable/Disable the Level Meter During Receive | Muestra el medidor de nivel de micrófono incluso en RX. | — | — |
| Iambic: | Habilita o deshabilita el manipulador iámbico en la radio. | — | — |
| Iambic Mode: A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. | A | — |
| Swap: | Intercambia dit/dah. | — | — |
| Sideband: | Selecciona la banda lateral del tono CW (LSB | USB). | — | — |
| CWX: | Habilita la activación de macros CWX. | — | — |
| Decode: | Habilita la superposición de decodificación CW en el panadapter. | True | `CwDecodeOverlay` |
| RTTY Mark Default: | Frecuencia de marca RTTY predeterminada. | — | — |

**Nota:** En v0.9.1, se añadieron los botones Mode A y Mode B junto al conmutador Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el nuevo manipulador iámbico de software local (IambicKeyer) que refleja el estado iámbico de la radio para un tono de monitorización de menos de 5 ms.

## Pestaña RX

La pestaña RX proporciona calibración de compensación de frecuencia GPSDO y configuración de la fuente de referencia de 10 MHz.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Cal Frequency (MHz): | Frecuencia utilizada para la calibración manual. | — | — |
| Start | Inicia el barrido de calibración de frecuencia. | — | — |
| Freq Offset (ppb): | Compensación de frecuencia manual en ppb. | — | — |
| 10 MHz Reference Source: | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/Externo). | Auto | — |

### Visualización de la fuente de referencia de 10 MHz (v0.9.7)

El cuadro combinado `10 MHz Reference Source:` en la pestaña `RX` se actualizó en v0.9.7. La lista de fuentes disponibles y la etiqueta de estado de bloqueo junto a ella ahora se comportan de manera diferente a versiones anteriores.

#### Cuadro combinado de fuente

El cuadro combinado ahora se completa dinámicamente según el hardware presente en la radio conectada y la configuración y el estado actual del oscilador informados por la radio. Pueden aparecer las siguientes fuentes:

| Entrada | Cuándo se muestra |
|---|---|
| Auto | Siempre se muestra. |
| TCXO | Se muestra cuando la radio informa que hay un TCXO presente, o cuando el estado actual o informado se refiere a TCXO. |
| GPSDO | Se muestra cuando la radio informa que hay un GPSDO presente, o cuando el estado actual o informado se refiere a GPSDO. |
| External 10 MHz | Se muestra cuando la radio informa que hay una referencia externa presente o activa, o cuando el estado actual o informado se refiere a externa. Nota: la etiqueta cambió de "External" a "External 10 MHz" en v0.9.7. |

El cuadro combinado selecciona la configuración de oscilador guardada automáticamente cuando se abre el diálogo. Si la configuración guardada no está en la lista, se intenta con el estado informado actual; si ese también está ausente, se selecciona Auto.

#### Etiqueta de estado de bloqueo

La etiqueta de estado junto al cuadro combinado se actualizó para mostrar información más completa:

- Cuando se selecciona Auto y la radio ha cambiado a una fuente específica, la etiqueta muestra **Auto -> \<fuente\>** seguido de **Locked** o **Unlocked**.
- Cuando la fuente solicitada difiere de la fuente activa, la etiqueta muestra **\<solicitada\> -> \<activa\>** seguido de **Locked** o **Unlocked**.
- Cuando la fuente solicitada y la activa coinciden, la etiqueta muestra **\<fuente\> Locked** o **\<fuente\> Unlocked**.
- Cuando se selecciona External 10 MHz pero no se detecta ninguna referencia externa, la etiqueta agrega **(not detected)**.
- Mientras se espera que la radio informe el estado del oscilador, la etiqueta muestra **Waiting for oscillator status**.

El color de la etiqueta es verde cuando está bloqueada y rojo cuando está desbloqueada. Antes de que la radio informe cualquier estado del oscilador, la etiqueta se muestra en un gris neutro.

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres amigables a cada puerto de antena en la radio.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| ANT1 / ANT2 / XVTA / XVTB | Campos de texto para establecer nombres amigables para cada puerto de antena. | — | — |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Line Out: | Deslizador de ganancia de salida de línea. | — | — |
| Mute (Line Out) | Silencia la salida de línea. | — | — |
| Headphone: | Deslizador de ganancia de auriculares. | — | — |
| Mute (Headphone) | Silencia los auriculares. | — | — |
| Front Speaker: / Mute | Silencia el altavoz frontal (específico del modelo). | — | — |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. | Auto | `AudioCompression` |
| Prevent system sleep while connected | Mantiene el SO activo mientras la radio está conectada para evitar caídas de flujo de audio/TCP/UDP durante la inactividad. | False | `InhibitSleepWhileConnected` |
| PC Audio Devices: Input: / Output: | Elige los dispositivos de audio de entrada/salida del host. | — | — |
| Audio Boost: | Habilita ganancia adicional en la ruta de audio del cliente. | — | `AudioBoost` |
| Audio Buffer: | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. | 200 | `AudioBufferMs` |
| Recording: Radio Side / Client Side | Elige la grabación del lado de la radio o del lado del cliente. | Radio Side | `RecordingMode` |
| Save to: | Carpeta para grabaciones guardadas (solo lado del cliente). Valor predeterminado: Documentos/AetherSDR/Grabaciones. | — | `QsoRecordingDir` |
| ... | Navega para seleccionar la carpeta de grabación. | — | — |
| Auto-record on TX | Graba automáticamente mientras se transmite. | False | `QsoRecordingAutoRecord` |
| Idle timeout: | Segundos de silencio antes de que se detenga la grabación. | 120 | `QsoRecordingIdleTimeout` |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. | — | — |

### Punto de estado NVIDIA BNR

Un punto de color junto a los controles NVIDIA BNR indica el estado del contenedor (Running/Stopped/Unknown).

## Pestaña Filters

La pestaña Filters configura opciones de filtro de baja latencia / nítido por ancho de banda.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Deslizadores de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está habilitado. | — | — |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. | — | — |
| Use Low Latency Filters for Digital Modes | Fuerza filtros de baja latencia en DIGU/DIGL. | — | — |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transvertidor. Contiene pestañas anidadas, una por xvtr, y una pestaña '+'.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| RX Only: | Fuerza solo RX en ese transvertidor. | — | — |
| Remove (xvtr) | Elimina la definición del transvertidor. | — | — |
| Create New Transverter | Agrega una nueva entrada de transvertidor. | — | — |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores seriales USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Cables list / Status | Cables USB detectados por tipo con estado Plugged/Unplugged. | — | — |
| Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Parámetros seriales y comportamiento por cable. | — | — |

## Pestaña Peripherals

La pestaña Peripherals permite la conexión a dispositivos externos por IP (TGXL, PGXL, Antenna Genius).

### Conexión directa TGXL

Consulte la sección dedicada a continuación para obtener instrucciones de configuración detalladas.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Connect / Disconnect (TGXL) | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar. | Connect | — |
| Connect / Disconnect (PGXL) | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect | — |
| Connect / Disconnect (Antenna Genius) | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto |
