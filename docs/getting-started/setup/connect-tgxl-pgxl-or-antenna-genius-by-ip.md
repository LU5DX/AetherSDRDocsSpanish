# Configuración de la Radio

El cuadro de diálogo Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Telefonía/CW, RX, audio, antenas, filtros, XVTR, cables USB, periféricos, APD, temas y configuración del puerto serie.

## Abrir el cuadro de diálogo

1. Abra `Settings > Radio Setup...`.
2. El cuadro de diálogo se abre como una ventana persistente. Su tamaño y posición se guardan entre sesiones.

---

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador | Número de serie del chasis (solo lectura). |
| Region | Indicador | Región regulatoria de la radio. |
| HW Version | Indicador | Cadena de versión del hardware. |
| Model | Indicador | Modelo de la radio. |
| Options | Indicador | Muestra las opciones de radio licenciadas. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado habilitado de multiFLEX. |
| Nickname | Campo de texto | Apodo descriptivo de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto, usa el nombre del host del SO si está vacío. Se almacena en AppSettings. Se envía a la radio como 'client station \<name\>'. |
| License Info | Indicador | Muestra los detalles de la licencia de la radio (Suscripción, Vencimiento, ID de Radio, Versión licenciada). |

Cada valor de solo lectura tiene un botón para copiar al portapapeles junto a él (un icono pequeño que aparece al pasar el cursor). Haga clic en el botón para copiar el valor.

### Remote On

Haga clic en **Remote On** para habilitar la funcionalidad de encendido remoto.

### Actualización de firmware

**Check for Update** consulta a la radio si hay actualizaciones de firmware disponibles. Cuando se encuentra una versión más reciente, AetherSDR muestra un mensaje informativo:

> Update available: v*X.Y.Z*
> Download the SmartSDR installer from flexradio.com,
> then click 'Select Installer...' to stage it.

**Select Installer...** (renombrado desde Browse .ssdr... en v0.9.3) acepta tres tipos de archivo:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador WiX de SmartSDR | .msi | FlexRadio v4.2 y posteriores |
| Instalador autoextraíble de SmartSDR | .exe | Versiones antiguas de SmartSDR |
| Archivo de firmware extraído | .ssdr | Como en versiones anteriores de AetherSDR |

El preparador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (mágica OLE/MSI versus cabecera PE/COFF MZ) y extrae la carga útil .ssdr sin necesidad de herramientas externas.

#### Para preparar firmware desde un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo .msi, .exe o .ssdr.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el progreso y posibles errores.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware a la radio.

---

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

### Información de red

| Control | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Enforce Private IP Connections | Botón de alternancia | — | — | Rechaza pares que no sean RFC1918. |
| Network MTU | Spinbox | 1450 | 576–9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. |
| DHCP / Static | Botón de alternancia | — | — | Alterna entre modos DHCP e IP estática. |
| IP Address / Mask / Gateway | Campo de texto | — | — | Campos de configuración de IP estática. |
| Apply | Botón pulsador | — | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y la información en vivo de latitud, longitud, altitud, hora y satélites.

---

## Pestaña TX

La pestaña TX contiene temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, opciones de seguimiento de slice/TX y un acceso directo a TX Band Settings.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el cuadro de diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

La sección de temporizaciones de TX incluye campos spinbox para valores en milisegundos.

| Control | Etiqueta de visualización | Predeterminado | Comportamiento |
|---|---|---|---|
| ACC TX | ACC TX: | — | Retardo de temporización ACC en ms. |
| TX Delay | TX Delay: | — | Retardo de TX en ms. |
| RCA TX1 | RCA TX1: | — | Retardo RCA TX1 en ms. |
| Timeout | Timeout (sec): | — | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |

### Enclavamientos

Los botones de alternancia **TX REQ: RCA** y **TX REQ: Accessory** habilitan las entradas de enclavamiento RCA y de accesorio.

### Potencia y sintonía

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Max Power | Spinbox | — | 0–100% | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode | Cuadro combinado | — | — | Selecciona cómo se comporta el botón de sintonía. |

### Seguimiento de waterfall y slice

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Show TX in Waterfall | Botón de alternancia | — | — | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | Falso | `TxFollowsActiveSlice` | TX sigue el slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se desactiva automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón pulsador | Falso | `ActiveFollowsTxSlice` | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

---

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Micrófono

**Enable/Disable the Level Meter During Receive** alterna la visualización del medidor de nivel de micrófono incluso en RX.

### Manipulador CW

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Iambic | Botón de alternancia | — | Activado / Desactivado | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode | Botón pulsador | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| Swap | Botón de alternancia | — | — | Intercambia dit/dah. |
| Sideband | Cuadro combinado | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX | Botón de alternancia | — | — | Habilita la activación por macros CWX. |
| Decode | Botón de alternancia | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. Clave de configuración: `CwDecodeOverlay`. |

### RTTY

El spinbox **RTTY Mark Default** establece la frecuencia de marca RTTY predeterminada.

---

## Pestaña RX

La pestaña RX contiene la calibración del offset de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

| Control | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz) | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb) | Spinbox | Offset de frecuencia manual en ppb. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** lista las fuentes de oscilador disponibles dinámicamente según el hardware presente y el estado del oscilador informado por la radio.

| Etiqueta | Valor interno | Cuándo se muestra |
|---|---|---|
| Auto | auto | Siempre se muestra |
| TCXO | tcxo | Se muestra cuando hay hardware TCXO presente, se ha recibido el estado del oscilador o la configuración actual o guardada es `tcxo` |
| GPSDO | gpsdo | Se muestra cuando hay hardware GPSDO presente o la configuración actual o guardada es `gpsdo` |
| External 10 MHz | external | Se muestra cuando hay una referencia externa presente, se ha recibido el estado del oscilador o la configuración actual o guardada es `external` |

#### Visualización del estado de bloqueo

La etiqueta de estado de bloqueo junto al cuadro combinado muestra información más detallada que texto plano:

| Situación | Ejemplo de texto mostrado |
|---|---|
| Estado del oscilador aún no recibido | `Waiting for oscillator status` |
| El modo Auto ha resuelto a una fuente | `Auto -> GPSDO Locked` |
| La configuración guardada difiere del estado activo | `TCXO -> GPSDO Locked` |
| La configuración y el estado coinciden | `GPSDO Locked` |
| External seleccionado pero referencia no detectada | `External 10 MHz Unlocked (not detected)` |

El color de la etiqueta se actualiza automáticamente: verde (`#00c040`) cuando está bloqueado, rojo (`#c04040`) cuando está desbloqueado y gris (`#8aa8c0`) mientras espera el estado.

---

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| Line Out | Deslizador | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone | Deslizador | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker / Mute | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

**Audio Compression (SmartLink):** alterna entre Auto, Uncompressed y Opus. Clave de configuración: `AudioCompression`.

### Suspensión del sistema

La casilla **Prevent system sleep while connected** mantiene el SO despierto mientras la radio está conectada para evitar cortes en los flujos de audio/TCP/UDP durante la inactividad. Predeterminado: Falso. Clave de configuración: `InhibitSleepWhileConnected`.

### Dispositivos de audio del PC

Los cuadros combinados **PC Audio Devices: Input:** y **Output:** seleccionan los dispositivos de audio de entrada y salida del host.

### Realce de audio

El botón de alternancia **Audio Boost** habilita ganancia adicional en la ruta de audio del cliente. Clave de configuración: `AudioBoost`.

### Búfer de audio

El campo de texto **Audio Buffer** establece el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Predeterminado: 200. Rango: 50–1000 ms. Clave de configuración: `AudioBufferMs`.

### Grabación

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Recording | Botón pulsador | Radio Side | `RecordingMode` | Elige grabación del lado de la radio o del lado del cliente. Opciones: Radio Side / Client Side. |
| Save to | Campo de texto | — | `QsoRecordingDir` | Carpeta para grabaciones guardadas (solo lado del cliente). Por defecto, Documentos/AetherSDR/Recordings. |
| ... | Botón pulsador | — | — | Navega para seleccionar la carpeta de grabación. |
| Auto-record on TX | Casilla | Falso | `QsoRecordingAutoRecord` | Graba automáticamente mientras transmite. |
| Idle timeout | Spinbox | 120 | `QsoRecordingIdleTimeout` | Segundos de silencio antes de detener la grabación. Rango: 10–3600 seg. |

### NVIDIA BNR

Los controles de **NVIDIA BNR** (Autostart Container, Start, Stop, Check Status) gestionan el contenedor de eliminación de ruido NVIDIA Broadcast. Un punto de estado indica En ejecución (verde), Detenido (rojo) o Desconocido (gris).

---

## Pestaña Antennas

La pestaña Antennas permite nombrar los puertos de antena de la radio para mostrarlos en los paneles de panadapter y slice. Esta pestaña se construye de forma diferida la primera vez que se hace clic en ella.

---

## Pestaña Filters

La pestaña Filters proporciona opciones de filtro de baja latencia y de nitidez por ancho de banda.

### Nitidez del filtro

Los **deslizadores de nitidez de filtro Voice / CW / Digital** establecen la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está activado.

Los botones de alternancia **Auto (Voice / CW / Digital)** habilitan la selección automática del nivel de filtro para ese modo, deshabilitando el deslizador de nitidez manual.

### Filtros de modo digital

La casilla **Use Low Latency Filters for Digital Modes** fuerza el uso de filtros de baja latencia en DIGU/DIGL.

---

## Pestaña XVTR

La pestaña XVTR configura los ajustes por transvertidor. Contiene pestañas anidadas, una por transvertidor, y una pestaña '+' para crear nuevos transvertidores.

| Control | Tipo | Comportamiento |
|---|---|---|
| RX Only | Botón de alternancia | Fuerza solo RX en ese transvertidor. |
| Remove | Botón pulsador | Elimina la definición del transvertidor. |
| Create New Transverter | Botón pulsador | Añade una nueva entrada de transvertidor. |

---

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a los tipos de cable CAT, BCD, bit y PTT.

| Control | Tipo | Comportamiento |
|---|---|---|
| Cables list / Status | Indicador | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| Name / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0–7) | Cuadro combinado | Parámetros serie y comportamiento por cable. |

---

## Pestaña Peripherals

La pestaña Peripherals habilita la conexión IP manual a dispositivos externos (TGXL, PGXL, Antenna Genius o ShackSwitch) cuando la detección automática no ha encontrado el dispositivo.

### Antes de comenzar

- AetherSDR ya debe estar conectado a una radio FLEX-8600. La pestaña Peripherals solo está disponible cuando hay una conex
