# Verificar Número de Serie, Versión de Hardware, Región y Opciones de la Radio

La pestaña Radio en Configuración de Radio muestra información identificativa reportada directamente por la radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar el hardware y las opciones de su radio antes de solucionar problemas o contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los campos de la pestaña Radio se completan con datos en vivo de la radio.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por la radio.
   - **Region** — la región regulatoria de la radio (muestra `USA` si la radio no reporta ninguna).
   - **Options** — las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis según lo reportado por la radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con el prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones licenciadas de la radio. |
| Remote On | Botón pulsador | Habilita el encendido/activación remota. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. |
| Model | Indicador | Modelo de la radio. |
| Nickname | Campo de texto | Apodo descriptivo de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del sistema operativo si está vacío. Se almacena en AppSettings como `StationName`. |
| License Info | Indicador | Muestra los detalles de la licencia de la radio (Suscripción / Vencimiento / ID de Radio / Versión licenciada). |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Browse .ssdr... | Botón pulsador | Selecciona un archivo de imagen de firmware. |
| Upload Firmware | Botón pulsador | Inicia la carga de firmware con barra de progreso y estado. |

Todos los campos de Información de Radio son de solo lectura. No tienen claves de configuración persistente asociadas.

# Pestaña Network

La pestaña Network en Configuración de Radio muestra información de red de la radio y opciones avanzadas de red.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador (solo lectura) | Direcciones de red de solo lectura. |
| Enforce Private IP Connections: | Botón de alternancia | Rechaza pares que no cumplan con RFC1918. |
| Network MTU: | Spinbox | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes, valor predeterminado 1450. Se almacena en AppSettings como `NetworkMtu`. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Envía la configuración de red a la radio. |

# Pestaña GPS

La pestaña GPS en Configuración de Radio muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **GPS**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| GPS | Pestaña | Presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites. |

# Pestaña TX

La pestaña TX en Configuración de Radio muestra temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y acceso directo a Configuración de Banda TX.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| TX Band Settings | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms) | Spinbox | Temporizaciones de retención/retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y de accesorio. |
| Max Power: | Spinbox | Establece el límite de potencia de TX a nivel de radio. Rango 0-100 %. |
| Tune Mode: | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante una operación Split. |
| Active Slice Follows TX | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, desde WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |

# Pestaña Phone/CW

La pestaña Phone/CW en Configuración de Radio muestra valores predeterminados de micrófono, manipulador CW y RTTY.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en recepción. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode: A / B | Botón pulsador | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local de software. Par mutuamente excluyente. |
| Swap: | Botón de alternancia | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB | USB). |
| CWX: | Botón de alternancia | Habilita la activación por macros CWX. |
| Decode: | Botón de alternancia | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. |
| RTTY Mark Default: | Spinbox | Frecuencia predeterminada de la marca RTTY. |

# Pestaña RX

La pestaña RX en Configuración de Radio muestra la calibración de compensación de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | Compensación de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto a la selección. |

## Calibración de frecuencia

En la versión v0.9.2.1, los controles de calibración en la pestaña **RX** siempre están visibles, independientemente de si hay un GPSDO instalado. Anteriormente, los campos Cal Frequency, Start y Freq Offset estaban ocultos cuando se detectaba un GPSDO. El banner de estado en la parte superior del grupo ahora muestra:

- **GPSDO instalado** — "GPSDO instalado. Calibración manual de compensación de frecuencia disponible." (texto verde)
- **Sin GPSDO** — "Calibración manual de compensación de frecuencia disponible." (texto ámbar)

Los siguientes controles ahora están disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón pulsador | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en curso. Antes de activar el barrido del PLL, AetherSDR restablece el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego ejecuta `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Spinbox | Compensación de frecuencia manual en partes por billón, aplicada después de que la calibración se complete o establecida directamente para una corrección manual. |

Aparece una etiqueta de estado a la derecha del botón Start que se actualiza durante la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Inactivo | *(vacío)* | — |
| Frecuencia de calibración no ingresada | "Ingrese la frecuencia de calibración" | Ámbar |
| Secuencia iniciada | "Iniciando…" | Gris-azul |
| En progreso | Se actualiza según el estado del PLL reportado por la radio | Gris-azul |

El botón Start se rehabilita y su etiqueta vuelve a **Start** cuando la secuencia de calibración se completa o falla.

## Fuente de referencia de 10 MHz (v0.9.7)

En la versión v0.9.7, el cuadro combinado **10 MHz Reference Source:** y su etiqueta de estado de bloqueo se actualizaron para manejar una gama más amplia de estados del oscilador reportados por la radio.

**Población del cuadro combinado:** La lista de fuentes disponibles ahora se construye dinámicamente cada vez que se abre la pestaña o cambia el estado del oscilador de la radio. Las fuentes aparecen en el combinado solo si la radio reporta el hardware relevante como presente, si la configuración actual o el estado activo usa esa fuente, o si se ha recibido el estado del oscilador (en cuyo caso TCXO y External 10 MHz siempre se incluyen como opciones). Ya no se utilizan las opciones fijas de versiones anteriores, que podían mostrar fuentes que la radio no poseía.

| Valor de fuente | Etiqueta mostrada en el combinado |
|---|---|
| `auto` | Auto |
| `tcxo` | TCXO |
| `gpsdo` | GPSDO |
| `external` / `ext` | External 10 MHz |

**Etiqueta de estado de bloqueo:** La etiqueta a la derecha del combinado ahora muestra información de estado más completa:

| Condición | Texto mostrado | Color |
|---|---|---|
| Aún no se ha recibido el estado del oscilador | "Esperando el estado del oscilador" | Gris-azul |
| Fuente bloqueada | `<fuente> Locked` | Verde (`#00c040`) |
| Fuente desbloqueada | `<fuente> Unlocked` | Rojo (`#c04040`) |
| El modo Auto ha seleccionado una fuente | `Auto -> <fuente resuelta> Locked/Unlocked` | Verde o rojo |
| La configuración y el estado activo difieren | `<configuración> -> <activo> Locked/Unlocked` | Verde o rojo |
| External seleccionado pero sin señal detectada | `External 10 MHz` | Gris-azul |

# Pestaña Audio

La pestaña Audio en Configuración de Radio muestra las salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y el contenedor NVIDIA BNR.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Line Out: | Deslizador | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone: | Deslizador | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker: / Mute | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Botón pulsador | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`. |
| Prevent system sleep while connected | Casilla de verificación | Mantiene el sistema operativo activo mientras la radio está conectada. Se almacena en AppSettings como `InhibitSleepWhileConnected`. |
| PC Audio Devices: Input: / Output: | Cuadro combinado | Selecciona los dispositivos de audio de entrada/salida del host. |
| Audio Boost: | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en AppSettings como `AudioBoost`. |
| Audio Buffer: | Campo de texto | Aumenta el búfer de audio en milisegundos para compensar la fluctuación en VPN/SmartLink. Rango 50-1000 ms, valor predeterminado 200. Se almacena en AppSettings como `AudioBufferMs`. |
| Recording: Radio Side / Client Side | Botón pulsador | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena en AppSettings como `RecordingMode`. |
| Save to: | Campo de texto | Carpeta para las grabaciones guardadas (solo del lado del cliente). Se almacena en AppSettings como `QsoRecordingDir`. |
| ... | Botón pulsador | Navega para seleccionar la carpeta de grabación. |
| Auto-record on TX | Casilla de verificación | Graba automáticamente mientras se transmite. Se almacena en AppSettings como `QsoRecordingAutoRecord`. |
| Idle timeout: | Spinbox | Segundos de silencio antes de que se detenga la grabación. Rango 10-3600 seg, valor predeterminado 120. Se almacena en AppSettings como `QsoRecordingIdleTimeout`. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Botón pulsador | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

# Pestaña Filters

La pestaña Filters en Configuración de Radio muestra opciones de filtro de baja latencia/agudeza por ancho de banda.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Deslizadores de agudeza de filtro Voice / CW / Digital | Deslizador | Establece la agudeza del filtro (0=menor latencia a 3=más agudo) por modo; el deslizador se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de agudeza. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| Use Low Latency Filters
