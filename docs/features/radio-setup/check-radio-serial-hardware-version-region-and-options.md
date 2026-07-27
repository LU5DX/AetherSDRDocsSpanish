# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana de configuración maestra por radio. Proporciona acceso a la información de la radio, configuración de red, GPS, configuración de TX, ajustes de Phone/CW, calibración de RX, configuración de audio, nombres de antenas, opciones de filtros, definiciones de transvertidores, asignaciones de cables USB, conexiones periféricas, muestreo APD, apariencia del tema, integración con KiwiSDR, búsqueda de indicativos y configuración del puerto serie FlexControl.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Muchos campos se completan con datos en vivo de la radio.
- El diálogo recuerda su tamaño y posición entre sesiones. Si el diálogo aparece fuera de la pantalla, elimine la entrada `RadioSetupDialogGeometry` de su archivo de configuración.

## Abriendo la Configuración de la Radio

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en su última posición y tamaño.

# Pestaña Radio

La pestaña Radio muestra información de identificación reportada directamente por la radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de solucionar problemas o contactar al soporte.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por la radio.
   - **Region** — la región regulatoria de la radio (por defecto `USA` si la radio no reporta una).
   - **Options** — las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis. Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware. Incluye un botón de copia al portapapeles junto al valor. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones de radio licenciadas. Incluye un botón de copia al portapapeles junto al valor. |
| Remote On | Botón pulsador | Habilita el encendido/activación remota. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado habilitado de multiFLEX. |
| Model | Indicador (solo lectura) | Modelo de radio. Incluye un botón de copia al portapapeles junto al valor. |
| Nickname | Campo de texto | Apodo de radio fácil de usar. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Por defecto es el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. |
| License Info | Indicador | Muestra los detalles de la licencia de la radio (Suscripción, Expiración, ID de Radio, Versión licenciada). Cada campo incluye un botón de copia al portapapeles. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Select Installer... | Botón pulsador | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite el progreso. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| Reboot Radio | Botón pulsador | Reinicia la radio conectada. Deshabilitado cuando la radio está desconectada. Muestra un diálogo de confirmación antes de reiniciar. Las sesiones LAN se reconectan automáticamente; las sesiones WAN/SmartLink requieren reconexión manual. |

Todos los campos de Información de la Radio son de solo lectura. No hay claves de configuración persistente asociadas a ellos.

## Reiniciando la radio

El botón **Reboot Radio** se encuentra en el grupo de Información de la Radio. Solo está habilitado mientras AetherSDR está conectado a la radio.

1. Haga clic en **Reboot Radio**.
2. Aparece un diálogo de confirmación:
   - En conexiones LAN: "AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciar."
   - En conexiones WAN/SmartLink: "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente una vez que la radio termine de iniciar."
3. Haga clic en **OK** para confirmar. El diálogo se cierra automáticamente después de confirmar.
4. La radio se reinicia. AetherSDR se desconecta y reconecta automáticamente en LAN, o espera la reconexión manual en WAN.

## Copiando información de la radio

Cada valor en el grupo de Información de la Radio tiene un pequeño botón de copia a su derecha. Haga clic en el botón de copia para copiar el valor al portapapeles.

| Destino de copia | Qué se copia |
|---|---|
| Radio SN | La cadena del número de serie del chasis. |
| HW Version | La cadena de versión de hardware (con prefijo `v`). |
| Region | La cadena de región regulatoria. |
| Options | La cadena de opciones licenciadas. |
| Remote On | El texto de la etiqueta "Remote On". |
| FlexControl | La cadena de estado de FlexControl. |
| multiFLEX | La cadena de estado de multiFLEX. |
| Model | La cadena del modelo de radio. |
| Nickname | El texto del apodo. |
| Callsign | El texto del indicativo. |
| Station Name | El texto del nombre de la estación. |
| License Info | La cadena completa de detalles de la licencia. |
| Check for Update | El texto de la etiqueta "Check for Update". |
| Select Installer... | El texto de la ruta del archivo después de navegar. |
| Upload Firmware | El texto de la etiqueta "Upload Firmware". |

El botón de copia aparece como un pequeño icono de documento. Solo se puede hacer clic cuando el valor asociado no está vacío y no es un marcador de posición de guión. Al hacer clic, el valor se copia al portapapeles del sistema y aparece un breve mensaje emergente "¡Copiado!" cerca del botón.

# Pestaña Network

La pestaña Network muestra la información de red de la radio y opciones de red avanzadas.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador (solo lectura) | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |
| Enforce Private IP Connections: | Botón de alternancia | Rechaza pares no RFC1918. |
| Network MTU: | Control numérico | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes, valor predeterminado 1450. Se almacena en AppSettings como `NetworkMtu`. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Envía la configuración de red a la radio. |

# Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **GPS**.

No hay claves de configuración adicionales ni controles más allá de lo que se muestra en la pestaña.

# Pestaña TX

La pestaña TX muestra los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall, seguimiento de slice/TX y un acceso directo a la Configuración de Banda de TX.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| TX Band Settings | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms) | Control numérico | Tiempos de retención/retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y Accessory. |
| Max Power: | Control numérico | Establece el límite máximo de potencia de TX a nivel de radio. Rango 0-100 %. |
| Tune Mode: | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | TX sigue la slice activa. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| Active Slice Follows TX | Botón pulsador | Cambia la slice activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |

### Tiempos de TX

| Campo | Unidad de visualización | Unidad de almacenamiento en la radio | Comportamiento |
|---|---|---|---|
| ACC TX: | ms | ms | Retardo de TX del Accessory. |
| TX Delay: | ms | ms | Retardo de activación de TX. |
| RCA TX1: | ms | ms | Retardo de RCA TX1. |
| Timeout: | segundos | ms | Tiempo de espera de enclavamiento. Se muestra en segundos enteros para facilitar la lectura; la radio espera y almacena milisegundos. |

# Pestaña Phone/CW

La pestaña Phone/CW muestra el micrófono, el keyer de CW y los valores predeterminados de RTTY.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el keyer iámbico en la radio. |
| Iambic Mode: A / B | Botón pulsador | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente excluyente. |
| Swap: | Botón de alternancia | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | Selecciona la banda lateral del tono de CW (LSB \| USB). |
| CWX: | Botón de alternancia | Habilita la activación de macros CWX. |
| Decode: | Botón de alternancia | Habilita la superposición de decodificación de CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. |
| RTTY Mark Default: | Control numérico | Frecuencia de marca RTTY predeterminada. |

# Pestaña RX

La pestaña RX muestra la calibración del offset de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Control numérico | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Control numérico | Offset de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto a la selección. |

## Calibración de frecuencia

Los controles de calibración siempre están visibles independientemente de si hay un GPSDO instalado. El banner de estado en la parte superior del grupo dice:

- **GPSDO instalado** — "GPSDO instalado. Calibración manual de offset de frecuencia disponible." (texto verde)
- **Sin GPSDO** — "Calibración manual de offset de frecuencia disponible." (texto ámbar)

Los siguientes controles están disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Control numérico | Frecuencia utilizada para la calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón pulsador | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en curso. Antes de activar el barrido del PLL, AetherSDR restablece el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Control numérico | Offset de frecuencia manual en partes por mil millones, aplicado después de que se complete la calibración o establecido directamente para una corrección manual. |

# Pestaña Audio

La pestaña Audio muestra las salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y el contenedor NVIDIA BNR.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Line Out: | Control deslizante | Ganancia de la salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone: | Control deslizante | Ganancia de los auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en las transmisiones de audio/TCP/UDP durante la inactividad. Se almacena en AppSettings como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | Elige los dispositivos de audio de entrada/salida del host. |
| Audio Boost: | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en AppSettings como `AudioBoost`. |
| Audio Buffer: | Campo de texto | Aumenta el búfer de audio en milisegundos para compensar la fluctuación en VPN/SmartLink. Rango 50-1000 ms, valor predeterminado 200. Se almacena en AppSettings como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Botón pulsador | Elige la grabación del lado de
