# Configuración de la radio

El diálogo de Configuración de la radio es la ventana maestra de configuración por radio. Proporciona acceso a la información de la radio, configuración de red, GPS, configuración de TX, ajustes de Phone/CW, calibración de RX, configuración de audio, nombres de antenas, opciones de filtro, definiciones de transvertidores, asignaciones de cables USB, conexiones periféricas, muestreo APD, apariencia del tema y configuración del puerto serie FlexControl.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Muchos campos se completan con datos en vivo de la radio.
- El diálogo recuerda su tamaño y posición entre sesiones. Si el diálogo aparece fuera de la pantalla, elimine la entrada `RadioSetupDialogGeometry` de su archivo de configuración.

## Abrir Configuración de la radio

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en su última posición y tamaño utilizados.

# Pestaña Radio

La pestaña Radio muestra información de identificación reportada directamente por la radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de solucionar problemas o contactar al soporte técnico.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por la radio.
   - **Region** — la región regulatoria de la radio (el valor predeterminado es `USA` si la radio no reporta una).
   - **Options** — las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis según lo reportado por la radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones de radio licenciadas. |
| Remote On | Botón pulsador | Habilita el encendido remoto / activación remota. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. |
| Model | Indicador | Modelo de la radio. |
| Nickname | Campo de texto | Apodo descriptivo de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. El valor predeterminado es el nombre del host del sistema operativo si está vacío. Se almacena en AppSettings como `StationName`. |
| License Info | Indicador | Muestra los detalles de la licencia de la radio (Suscripción / Caducidad / ID de radio / Versión licenciada). |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Browse .ssdr... | Botón pulsador | Elige un archivo de imagen de firmware. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |

Todos los campos de Información de la radio son de solo lectura. No hay claves de configuración persistentes asociadas con ellos.

# Pestaña Network

La pestaña Network muestra la información de red de la radio y opciones de red avanzadas.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador (solo lectura) | Direcciones de red de solo lectura. |
| Enforce Private IP Connections: | Botón de alternancia | Rechaza pares que no sean RFC1918. |
| Network MTU: | Spinbox | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes, valor predeterminado 1450. Se almacena en AppSettings como `NetworkMtu`. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Envía la configuración de red a la radio. |

# Pestaña GPS

La pestaña GPS muestra la presencia del GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **GPS**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| GPS | Pestaña | Presencia del GPS e información en vivo de latitud/longitud/altitud/hora/satélites. |

# Pestaña TX

La pestaña TX muestra los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall, seguimiento de slice/TX y un acceso directo a la Configuración de banda de TX.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| TX Band Settings | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms / Timeout (sec)) | Spinbox / Campo de texto | Tiempos de retención/retardo de TX. El campo **Timeout** se muestra en segundos; la radio almacena el valor en milisegundos (interno de FlexLib). |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y accesorio. |
| Max Power: | Spinbox | Establece el límite de potencia de TX a nivel de radio. Rango 0-100 %. |
| Tune Mode: | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación de división. |
| Active Slice Follows TX | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |

### Tiempos de TX

Los campos de tiempo controlan cuánto tiempo mantiene la radio los estados de clave:

| Campo | Unidad de visualización | Unidad de almacenamiento de la radio | Comportamiento |
|---|---|---|---|
| ACC TX: | ms | ms | Retardo de TX del accesorio. |
| TX Delay: | ms | ms | Retardo de activación de TX. |
| RCA TX1: | ms | ms | Retardo de RCA TX1. |
| Timeout: | segundos | ms | Tiempo de espera del enclavamiento. Se muestra en segundos enteros para legibilidad; la radio espera y almacena milisegundos. |

# Pestaña Phone/CW

La pestaña Phone/CW muestra los valores predeterminados de micrófono, keyer CW y RTTY.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel del micrófono incluso en RX. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el keyer iámbico en la radio. |
| Iambic Mode: A / B | Botón pulsador | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente excluyente. |
| Swap: | Botón de alternancia | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB | USB). |
| CWX: | Botón de alternancia | Habilita el keying de macros CWX. |
| Decode: | Botón de alternancia | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. |
| RTTY Mark Default: | Spinbox | Frecuencia de marca RTTY predeterminada. |

# Pestaña RX

La pestaña RX muestra la calibración de desviación de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | Desviación de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto a ella. |

## Calibración de frecuencia

Los controles de calibración siempre son visibles independientemente de si hay un GPSDO instalado. El banner de estado en la parte superior del grupo muestra:

- **GPSDO instalado** — "GPSDO installed. Manual frequency offset calibration available." (texto verde)
- **Sin GPSDO** — "Manual frequency offset calibration available." (texto ámbar)

Los siguientes controles están disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón pulsador | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en progreso. Antes de activar el barrido PLL, AetherSDR restablece el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Spinbox | Desviación de frecuencia manual en partes por mil millones, aplicada después de que se completa la calibración o establecida directamente para corrección manual. |

Aparece una etiqueta de estado a la derecha del botón Start y se actualiza durante la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Inactivo | *(vacío)* | — |
| Frecuencia de calibración no ingresada | "Enter cal frequency" | Ámbar |
| Secuencia iniciada | "Starting…" | Gris-azul |
| En progreso | Actualizado según el estado del PLL reportado por la radio | Gris-azul |

El botón Start se vuelve a habilitar y su etiqueta vuelve a **Start** cuando la secuencia de calibración se completa o falla.

## Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** y su etiqueta de estado de bloqueo acompañante se actualizaron para manejar una gama más amplia de estados del oscilador reportados por la radio.

**Población del cuadro combinado:** La lista de fuentes disponibles se construye dinámicamente cada vez que se abre la pestaña o cambia el estado del oscilador de la radio. Las fuentes aparecen en el cuadro combinado solo si la radio informa que el hardware relevante está presente, si la configuración actual o el estado activo usa esa fuente, o si se ha recibido el estado del oscilador (en cuyo caso TCXO y External 10 MHz siempre se incluyen como opciones).

| Valor de la fuente | Etiqueta mostrada en el cuadro combinado |
|---|---|
| `auto` | Auto |
| `tcxo` | TCXO |
| `gpsdo` | GPSDO |
| `external` / `ext` | External 10 MHz |

**Etiqueta de estado de bloqueo:** La etiqueta a la derecha del cuadro combinado muestra información de estado más detallada:

| Condición | Texto mostrado | Color |
|---|---|---|
| Aún no se ha recibido el estado del oscilador | "Waiting for oscillator status" | Gris-azul |
| Fuente bloqueada | `<source> Locked` | Verde (`#00c040`) |
| Fuente desbloqueada | `<source> Unlocked` | Rojo (`#c04040`) |
| El modo Auto ha seleccionado una fuente | `Auto -> <resolved source> Locked/Unlocked` | Verde o rojo |
| La configuración y el estado activo difieren | `<setting> -> <active> Locked/Unlocked` | Verde o rojo |
| External seleccionada pero no se detecta señal | `External 10 MHz` | Gris-azul |

# Pestaña Audio

La pestaña Audio muestra las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Line Out: | Deslizador | Ganancia de la salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone: | Deslizador | Ganancia de los auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada. Se almacena en AppSettings como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | Elige los dispositivos de audio de entrada/salida del host. |
| Audio Boost: | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en AppSettings como `AudioBoost`. |
| Audio Buffer: | Campo de texto | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Rango 50-1000 ms, valor predeterminado 200. Se almacena en AppSettings como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Botón pulsador | Elige la grabación del lado de la radio o del lado del cliente. Se almacena en AppSettings como `RecordingMode`. |
| Save to: | Campo de texto | Carpeta para las grabaciones guardadas (solo del lado del cliente). Se almacena en AppSettings como `QsoRecordingDir`. |
| ... | Botón pulsador | Examina para seleccionar la carpeta de grabación. |
| Auto-record on TX | Casilla de verificación | Graba automáticamente mientras se transmite. Se almacena en AppSettings como `QsoRecordingAutoRecord`. |
| Idle timeout: | Spinbox | Segundos de silencio antes de que se detenga la grabación. Rango 10-3600 seg, valor predeterminado 120. Se almacena en AppSettings como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Botón pulsador | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

# Pestaña Antennas

La pestaña Antennas le permite asignar nombres descriptivos a
